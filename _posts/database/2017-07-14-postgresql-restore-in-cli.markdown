---
layout: post
title: "postgresql restore in CLI"
date: "2017-07-14 17:00:47 +0900"
location: "Daejeon, South Korea"
commentIssueId: 16
category: Database
tags: [postgresql, pgAdmin]
---

My company is using flask for web application and we use postgresql as our DB.
If you have ever used postgresql, you must be heard about or use 'pgadmin' before. It's open source database management tool.  
It's really useful and I found no problems with it.

Except this...

I couldn't restore database via web page! well I got no solution yet but it's actually annoying.

So, if you want to restore database in CLI or have a trouble with web, try pg_restore

{% highlight bash %}
$ pg_restore

for example,

$ pg_restore --no-acl --no-owner -h localhost -d new_database --jobs=1 ~/rental_db
{% endhighlight %}

There are a few options, check the options via pg_restore --help
