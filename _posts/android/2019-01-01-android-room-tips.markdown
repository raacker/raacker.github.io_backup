---
layout: post
title: "Android: Room tiny tips"
date: "2019-01-01 23:28:13 +0900"
location: "Seoul, South Korea"
commentIssueId: 49
category: Android
tags: [android, java, database, SQLite, room]
---

<h3>Some of tiny tips that cause you a-day-debugging</h3>

1) Would face problem if there are more than two tables starting with same string.

This one was very tricky bug for me and quite a bit silly :(

I was trying to make join query with two tables called **TB_HELLO** and **TB_HELLOWORLD**.

But room always regarded TB_HELLOWORLD table as [TB_HELLO]WORLD because there's TB_HELLO table already.

This might be a bug but just keep in mind. Name your tables with different prefixes and <span style="color: red">never</span> make included naming like <span style=" font:bold; color:red;">TB_HELLO, TB_HELLOWORLD</span> .

<br/>
2) Join Query

If you're trying to handle more than two or three tables, you might have to make join query to get result at one call. Most of commands are good to use as same way as MySQL but to get a result, you should define result data object for Room.

```java
static class DataADataB {
  public int dataAStatus;
  public int dataBStatus;
}

// I really prefer this way to organize query with indentation.
// Concise and looks prettier :)
@Query(" SELECT " +
       "    dataAStatus, " +
       "    dataBStatus " +
       " FROM A AS tableA " +
       " INNER JOIN B AS tableB ON tableB.a_id = tableA.id")
List<DataADataB> findAllStatus();
```

[Query Multiple Tables](https://developer.android.com/training/data-storage/room/accessing-data#query-multiple-tables)

<br/>
3) SUMIF

For IF statement, there's CASE statement for substitute.

```sql
SUM(CASE WHEN data.status IS NOT 0 THEN 1 ELSE 0 END)
```
