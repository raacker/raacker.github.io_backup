---
layout: post
title: "Android: Add createDate into Room Entity"
date: "2019-01-01 23:19:13 +0900"
location: "Seoul, Korea"
commentIssueId: 48
category: Android
tags: [android, java, database, SQLite, room]
---

<h3>Room doesn't have default data for creation (yet maybe)</h3>

And also you cannot use 'Date' type directly.

To use Date, regard Date as String is the best.

```java
public class Converter {
    // Set timezone value as GMT 존맛탱... to make time as reasonable
    static DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss'Z'", Locale.getDefault());
    static {
        df.setTimeZone(TimeZone.getTimeZone("GMT"));
    }

    @TypeConverter
    public static Date timeToDate(String value) {
        if (value != null) {
            try {
                return df.parse(value);
            } catch (ParseException e) {
                Log.e(TAG, e.getMessage());
            }
            return null;
        } else {
            return null;
        }
    }

    @TypeConverter
    public static String dateToTime(Date value) {
        if (value != null) {
            return df.format(value);
        } else {
            return null;
        }
    }
}
```
Make TypeConverter to convert date to string vice versa.

Then, add createDate to Entity.

```java
@Entity(tableName = "TB_ENTITY")
public class MyEntity {
  @ColumnInfo(name = "createDate")
  @TypeConverters(Converter.class)
  public Date createDate;
}
```

All you need to do is when you're going to insert Entity, set createDate to new Date().

```java
MyEntity entity = new MyEntity();
entity.createDate = new Date();
Executor.IOThread(() -> entityDao.insert(entity));
```

You can query date value either if you make it as String.

```java
@Query("SELECT * FROM TB_ENTITY WHERE date(createDate) > date(:fromDate) AND date(createDate) < date(:toDate) ")
List<MyEntity> findEntitiesInDate(String fromDate, String toDate);
```

Happy hacking!
