---
layout: post
title: "Android: Using Room as Database with Dagger2"
date: "2018-11-29 18:52:13 +0900"
location: "Seoul, South Korea"
commentIssueId: 45
category: Android
tags: [android, java, dagger2, database, room]
---

<h3><i>A short post about my experience of using Room as SQLite library with Dagger2</i></h3>

This article will show you a brief overview of how to use Room as your SQLite library and also use Dagger2 to inject its dependencies.

Well I had really hard time with these structures and to get used to with them. This post will be a part of summary for myself :)
I used MVP architecture for this example.

<h4>1. Add dependencies to build.gradle</h4>

Put these code into your app layer build.gradle

```
    def room_version = "1.1.1"
    implementation "android.arch.persistence.room:runtime:$room_version"
    annotationProcessor "android.arch.persistence.room:compiler:$room_version"
    testImplementation "android.arch.persistence.room:testing:$room_version"

    // dagger2
    implementation 'com.google.dagger:dagger:2.15'
    annotationProcessor "com.google.dagger:dagger-compiler:2.15"
    implementation 'com.google.dagger:dagger-android:2.15'
    annotationProcessor 'com.google.dagger:dagger-android-processor:2.15'
    implementation 'com.google.dagger:dagger-android-support:2.15'
    compileOnly 'javax.annotation:jsr250-api:1.0'
    implementation 'javax.inject:javax.inject:1'

    ...
```

<h4>2. Project hierarchy</h4>

If you are new to Android or Dagger2, there are various form of project hierarchy. Just search other forms and pick one you'd like to implement

```
--data
------db
----------dao
--------------BaseDao (interface)
--------------ProjectDao (interface)
--------------PersonDao (interface)
----------entity
--------------Project (class)
--------------Person (class)
----------AppDatabase (abstract class)
----------Executor (class)
--di
------component
----------ApplicationComponent (interface)
------module
----------ApplicationModule (class)
----------DatabaseModule (class)
------ApplicationContext (annotation)
------DatabaseInfo (annotation)
--presenter
--view
------MainActivity (class)
TestApplication (class)
```

* data - will provide all data and business logic (Model)
* di - will provide dependency injection with dagger 2 library
* presenter - (will not cover in this article) presenter classes connecting between views and Models
* view - will contain every UI and view contents


<h4>3. Make Entity</h4>

Entity will be your database model which represents table you want to make.

```
@Entity(tableName = "TB_PERSON")
public class Person {
    @PrimaryKey(autoGenerate = true)
    @ColumnInfo(name = "person_id")
    public int person_id;

    @ColumnInfo(name = "name")
    public String name;

    @ColumnInfo(name = "email")
    public String email;
}
```

* Make sure all attributes of Entity must be public to be used in Dao
* You can add 'PrimaryKey' annotation to make primary key

```
@Entity(
        tableName = "TB_PROJECT",
        indices = {@Index(name = "person_idx", value = {"person_id"})},
        foreignKeys = {@ForeignKey(entity = Person.class,
                parentColumns = {"person_id"},
                childColumns = {"person_id"},
                onDelete = ForeignKey.CASCADE)
        }
)
public class Project {
    @PrimaryKey(autoGenerate = true)
    @ColumnInfo(name = "project_id")
    public int project_id;

    @ColumnInfo(name = "person_id")
    public int person_id;

    @ColumnInfo(name = "project_name")
    public String project_name;
}
```

* As you can find in Entity annotation, you can declare Foreign key to make relation among Entities.


<h4>4. Make Dao of Entities</h4>

Dao (Data Access Object) interfaces will be a access manager of each of entities.

```
@Dao
public interface BaseDao<T>  {
    @Insert(onConflict = OnConflictStrategy.REPLACE)
    long insert(T t);

    @Update
    void update(T t);

    @Delete
    void delete(T t);
}
```

Add @Dao above the interface name. Then you can use other annotations either.

* Making BaseDao will help you to add insert, update, delete queries easily


```
@Dao
public interface PersonDao extends BaseDao<Person> {
    @Query("SELECT * FROM TB_PERSON")
    List<Person> getAll();

    @Query("SELECT * FROM TB_PERSON WHERE name LIKE :name")
    List<Person> findPersonsByName(String name);
}
```

```
@Dao
public interface ProjectDao extends BaseDao<Project> {
    @Query("SELECT * FROM TB_PROJECT")
    List<Project> getAll();

    @Query("SELECT * FROM TB_PROJECT WHERE person_id LIKE :person_id")
    List<Project> findProjectsByName(int person_id);
}
```

I will just keep them simple. One thing you can notice about these Dao interfaces is that you can pass parameter to query using semicolon.

And really great feature of Room is compile time syntax checking. Query is string but it will allow you to only use declared attributes including table name.


<h4>5. Make 'AppDatabase' which extends RoomDatabase </h4>

Finally, you should make class that extending RoomDatabase

```
@Database(entities = {Person.class, Project.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract PersonDao personDao();
    public abstract ProjectDao projectDao();
}
```

This class will provide entities' dao to manipulate data.


<h4>6. Executor </h4>

When you are trying to use Dao methods, you have to make sure you are calling those in separate thread. Because MainThread is used by UI and all the core classes, if your call takes too much time, it will block the thread and will conclusively stop the app.

Thus, you have to make new Thread to run them.

```
new Thread(new Runnable() {
  @Override
  public void run() {
    method();
  }
});
```

But it's too many lines of code to use everywhere.

The better option would be to use Wrapper class that generate Executor and run over it.

```
/*
 *  Use Executor as following way.
 *  Executor.IOThread(() -> personDao.insert(new Person()));
 */
public class Executor {
    public static void IOThread(Runnable t) {
        ExecutorService IO_EXECUTOR = Executors.newSingleThreadExecutor();
        IO_EXECUTOR.execute(t);
    }
}
```

You can use this executor to call dao methods

```
Executor.IOThread(() -> personDao.getAll());
```

Caution! I used Lambda expression on here. Since it's Java 8 feature, if you're Android Studio is yelling 'It's not possible in your version', you have to set JDK version to use Java 8.

Go to File -> Project Structures -> app in Modules -> Change Source & Target Compatibility to 1.8


<h4>7. TestApplication </h4>

We will make TestApplication class which extends Application class. Application class is used to support global functionalities.
We will add DI code later.

```
public class TestApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
    }
}
```

<h4>8. Qualifier </h4>

In Dagger2, there are 2 main components to provide dependency, Component and Module.

Module is the actual class that provides Object, and Component is the builder to inject Module class into where Module is needed.

It's not easy to understand the concept but I will not cover it in here. Please look up other articles which describes much better.

[Dependency Injection with Dagger2](https://github.com/codepath/android_guides/wiki/Dependency-Injection-with-Dagger-2)


@Qualifier is Dagger annotation which helps you to make custom annotation to distinguish method's return type and to understand what they actually are.

```
@Qualifier
@Retention(RetentionPolicy.RUNTIME)
public @interface ApplicationContext { }

@Qualifier
@Retention(RetentionPolicy.RUNTIME)
public @interface DatabaseInfo { }
```

By making those interfaces, we can let Dagger know what String you want to get, what object you want to get specifically.

<h4>9. DatabaseModule </h4>

Now, let's make DatabaseModule which will provide actual AppDatabase object.

```
@Module
public class DatabaseModule {
    @ApplicationContext
    private final Context mContext;

    @DatabaseInfo
    private final String mDBName = "test_database.db";

    public DatabaseModule (@ApplicationContext Context context) {
        mContext = context;
    }

    @Singleton
    @Provides
    AppDatabase provideDatabase () {
        return Room.databaseBuilder(
                mContext,
                AppDatabase.class,
                mDBName
        ).fallbackToDestructiveMigration().build();
    }

    @Provides
    @DatabaseInfo
    String provideDatabaseName() { return mDBName; }

    @Singleton
    @Provides
    PersonDao providePersonDao(AppDatabase db) { return db.personDao(); }

    @Singleton
    @Provides
    ProjectDao provideProjectDao(AppDatabase db) { return db.projectDao(); }
}
```

* @Singleton annotation will help you to keep the method produce object in Singleton way.

* Dagger will look up @Provides annotation methods to find a proper method to provide data. So if you are requesting String data with @DatabaseInfo annotation, Dagger will call provideDatabaseName() to provide what you want. Also, you can use @Named annotation which is also a qualifier.

```
@Provides @Named("name")
String provideDatabaseName();

@Provides @Named("table_name")
String provideDatabaseTableName();
```

<h4>10. ApplicationModule </h4>

```
@Module
public class ApplicationModule {
    private final Application mApplication;

    public ApplicationModule(Application app) {
        mApplication = app;
    }

    @Singleton
    @Provides
    @ApplicationContext
    Context provideContext() {
        return mApplication;
    }

    @Singleton
    @Provides
    Application provideApplication() {
        return mApplication;
    }
}
```

Application Module will hold the TestApplication object over the application life time.


<h4>11. ApplicationComponent </h4>

Now, we are going to make ApplicationComponent which will <b>inject objects from Module to where you need</b>.

```
@Singleton
@Component(modules = {
        ApplicationModule.class,
        DatabaseModule.class,
})
public interface ApplicationComponent {
    void inject (TestApplication testApplication);
    void inject (MainActivity mainActivity);

    @ApplicationContext
    Context getContext();

    Application getApplication();

    @DatabaseInfo
    String getDatabaseName();
}
```

Notice that it has inject methods which takes TestApplication and MainActivity. When you build a Component, inject method will be called to specify <b>where you need the objects from Module</b>.


<h4>12. Build ApplicationComponent </h4>

We are ready to inject our dependencies!

First, clean your project and rebuild it. Dagger will automatically generate DaggerApplicationComponent class that has all implementations to inject objects.


```
public class TestApplication extends Application {
    protected ApplicationComponent mApplicationComponent;

    @Override
    public void onCreate() {
        super.onCreate();
        mApplicationComponent = DaggerApplicationComponent
                .builder()
                .applicationModule(new ApplicationModule(this))
                .databaseModule(new DatabaseModule(this))
                .build();
        mApplicationComponent.inject(this);
    }

    public ApplicationComponent getComponent() {
        return mApplicationComponent;
    }
}
```

You can attach Modules to Component and at last, inject TestApplication object to be alive in Dagger's hand.

```
mApplicationComponent.inject(this);
```

<h4>13. Let's call Dao method  </h4>

That's all! Let's simply test it in MainActivity.

```
public class MainActivity extends AppCompatActivity {

    @Inject
    AppDatabase mAppDatabase;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ((TestApplication)getApplication()).getComponent().inject(this);
        final PersonDao personDao = mAppDatabase.personDao();
        Executor.IOThread(() -> personDao.insert(new Person()));
    }
}
```



Well it was just a quick summary to setup Room and Dagger2 to support database dependency injection so there might be some missing stuffs. If you figure out, let me know! Glad to get feedback.

Here's the github link that contains all code of this project. (I didn't do any works on MainActivity, thus won't show anything on your device :)

[https://github.com/raacker/test_room](https://github.com/raacker/test_room)

If it helped you, very pleasure.

Happy hacking



<h4>References</h4>

- Thanks for IO_EXECUTOR idea. I love it

[https://gist.github.com/florina-muntenescu/697e543652b03d3d2a06703f5d6b44b5](https://gist.github.com/florina-muntenescu/697e543652b03d3d2a06703f5d6b44b5)

- I was able to get basic idea of room with this post

[https://android.jlelse.eu/setting-android-room-in-real-project-58a77469737c](https://android.jlelse.eu/setting-android-room-in-real-project-58a77469737c)

- Good 7 tips for further readings
[https://medium.com/androiddevelopers/7-pro-tips-for-room-fbadea4bfbd1](https://medium.com/androiddevelopers/7-pro-tips-for-room-fbadea4bfbd1)

- A Good example of Dagger 2 and room
[https://github.com/laminr/aeroknow](https://medium.com/androiddevelopers/7-pro-tips-for-room-fbadea4bfbd1)
