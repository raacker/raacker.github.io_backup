---
layout: post
title: "Android: Using Room as Database with Dagger2"
date: "2018-11-30 20:46:13 +0900"
location: "Seoul, Korea"
commentIssueId: 46
category: Android
tags: [android, java, database, SQLite, test]
---

<h3>Very nice library to test your SQLite database!</h3>

I'm still building up the tables and architecture of my project yet. And I need to look inside of SQLite, how the data went correctly, where's my row, etc...

This library is awesome for any purpose with Android SQLite.

[Android Debug Database](https://github.com/amitshekhariitbhu/Android-Debug-Database)

It's very easy to use and it has comprehensive features for every needs.

Add library into build.gradle with 'debugImplementation' tag to avoid using this library in released app
```
debugImplementation 'com.amitshekhar.android:debug-db:1.0.4'
```

And that's pretty all!

If you're using simulator, do
```
$ adb forward tcp:8080 tcp:8080

or

$ adb -s simulator_name tcp:8080 tcp:8080

if you have multiple devices connected to computer
```

and go to localhost:8080.

If you're using actual device, follow the ip address that logcat is showing.

Works like a charm, doesn't it?
