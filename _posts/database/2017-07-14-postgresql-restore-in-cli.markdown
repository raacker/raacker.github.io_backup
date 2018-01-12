---
layout: post
title: "postgresql restore in CLI"
date: "2017-07-14 17:00:47 +0900"
location: "Daejeon, South Korea"
commentIssueId: 16
category: Database
tags: [postgresql, pgAdmin, database]
---

At my company, we use flask and postgresql combination. And if you have ever used postgresql, you might already know 'pgadmin', open source database management tool for postgresql.  

There are two ways to restore your database from backup file.

**CLI**
{% highlight text %}
$ pg_restore

$ pg_restore --no-acl --no-owner -h localhost -d [database_name] --jobs=1 [database_backup path]
{% endhighlight %}

There are several options. I'm using above command for test only local server, any owner or host address.  Check the options via pg_restore --help

**pgAdmin4**
Well actually it's totally same with pg_restore. Because pgAdmin4 is using postgresql commands! Just you can check all the options via GUI.
