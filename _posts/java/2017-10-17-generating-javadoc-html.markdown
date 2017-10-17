---
layout: post
title: "Generating javadoc html"
date: "2017-10-17 12:00:00 -0700"
location: "San Diego, CA"
commentIssueId: 20
category: Java
tags: [java, documentation, API]
---

When you look up the java api document page [Java SE8 api](https://docs.oracle.com/javase/8/docs/api/), you can see tons of methods, classes and all about java stuff. That's what document stands for. We can search it and find the usage and explains.

When we are using programs, including java, we need to know how to use it right? then that means when we write a program, keep maintaining documents and providing is important for users and even for you, the author.

By writing some styled comments above the classes and methods, we can generate totally same looking documents via javadoc, provided in JDK you installed.

It is simple to do, just add these comments.
{% highlight java %}
/**
 *  This is sample method
 *
 *  @author Haven Kim
 *  @param data : parameter passed by caller
 *  @return void
 */

 public void sampleMethod(String data) {
   System.out.println("We received " + data);
 }
{% endhighlight %}

By using a little bit different comments, starting with two asterisk at the first, we can create javadoc reference of this method. You can use this for class either.
And also adding @ and some keywords will allow you to add specific informations, [How to Write Doc Comments for the Javadoc Tool](http://www.oracle.com/technetwork/articles/java/index-137868.html).

then you are ready to generate your own javadoc pages.

**On the Command line**
{% highlight bash %}
javadoc -sourcepath [sourcepath] -d [output directory] -subpackages .

for example

javadoc -sourcepath ~/java_example -d ~/javadoc_test -subpackages .
{% endhighlight %}

subpackages option is used for recursivly loading whole packages. That means you can create package specific javadoc page also.

You will get bunch of html files for each of packages and detailed sub directory files.

**On the Eclipse**

Generating javadoc in eclipse is way easier.

Go 'Project' tab and click 'Generate Javadoc'. Then you can select the project you want to use and find many useful options.

![](/images/Generating javadoc html1.PNG)

then just generate it and get your documents.


python has various API generation tools [wiki.python.org](https://wiki.python.org/moin/DocumentationTools) including [PyDoc](https://docs.python.org/3/library/pydoc.html), [Doxygen](http://www.stack.nl/~dimitri/doxygen/), etc. They have pros and cons so you might want to try them and find your taste.
