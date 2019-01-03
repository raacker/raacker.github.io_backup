---
layout: post
title: "Access SQLite3 of your application through ADB"
date: "2019-01-03 22:30:57 +0900"
location: "Seoul, South Korea"
commentIssueId: 50
category: Android
tags: [android, java, database, SQLite]
---

<h3>Access SQLite3 .db file of your app via ADB shell</h3>

I introduced sqlite debugger library before. [android sqlite debugger library](https://raacker.github.io/android/2018/11/30/android-awesome-sqlite-debugger-library/)

But as far as I run complex queries(actually, even simple select query with custom columns), I always failed to get result on webpage. I'm sure it will be fixed soon...? or maybe someone can PR to the repo!

![](/images/access-sqlite3-of-your-application-through-adb.png)
Failed... even querying primary key only.

But anyhow, you might want to access to SQLite of your app manually. Here's how you can do.

1) Run adb shell

```bash
$ adb shell

or

$ adb -s [device_name] shell
# If you have multiple devices connected to computer,
# do adb devices and get the name of your device (ex. emulator-5554)
```

2) Go to /data/data

```bash
$ cd data/data
```

3) Run run-as command with your package name.
run-as is some similar command as 'su'

```bash
/data/data$ run-as com.itshaven.example.testapp
```

4) Go to databases and find .db file

```bash
/data/data/com.itshaven.example.testapp$ cd databases
/data/data/com.itshaven.example.testapp/databases$ ls
test_sqlite.db test_sqlite.db-shm test_sqlite.db-wal
```

5) Run sqlite3

```bash
/data/data/com.itshaven.example.testapp/databases$ sqlite3 test_sqlite.db
SQLite version 3.22.0 2018-01-22 18:45:57
Enter ".help" for usage hints
sqlite>
```

Done! Happy hacking!
