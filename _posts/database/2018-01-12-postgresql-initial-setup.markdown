---
layout: post
title: "postgresql initial setup"
date: "2018-01-12 07:42:08 -0800"
location: "San Diego, CA"
commentIssueId: 39
category: Database
tags: [postgresql, pgAdmin, database, linux]
---

<h3>Postgresql</h3>

is open source database. It has quite huge community and easy to maintain. I'm using postgresql for my private project. Perfect partner of Flask I guess.

Here is how to install postgresql at the first time.

<br/>
1) Install via apt

{% highlight bash %}
$ sudo apt-get install postgresql
{% endhighlight %}

<br/>
2) Access to database

The default role name is postgres. So we have to use postgres user.

{% highlight bash %}
$ sudo -i -u postgres # change user to postgres
$ psql
{% endhighlight %}

Now you are in postgresql CLI mode.

<br/>
3) Create database

Once postgresql is installed, you can use various command without any effort. Hope it doens't screw your alias.

{% highlight bash %}
$ createdb [db_name] # When you are in postgres bash
{% endhighlight %}

<br/>
\* Make new role

Actually, you can keep using postgres role with alias
{% highlight bash %}
alias psql='sudo -i -u postgres & psql'

$ psql [db_name]  # automatically change to postgres and use database
{% endhighlight %}

But I'm using my username as a superuser role

{% highlight bash %}
$ sudo -u postgres createuser --interactive

--> Enter name of role to add: [new role name]
--> Shall the new role be a superuser? (y/n) [Choose if you want to make it superuser]
{% endhighlight %}

If you make a new role, you can 'sudo' the role name and use psql.
