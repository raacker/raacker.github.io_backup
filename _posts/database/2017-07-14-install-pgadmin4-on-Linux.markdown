---
layout: post
title: "Install pgAdmin4 on Linux"
date: "2017-07-14 21:57:09 +0900"
location: "Daejeon, South Korea"
commentIssueId: 19
category: Database
tags: [pgAdmin, postgresql, python, linux]
---

pgAdmin is really awesome open source database management tool. Maybe not that amazing but still quite useful to use on Linux. This is an installation guide.

go [pgAdmin official website](https://www.pgadmin.org/download/pgadmin-4-python-wheel/)

and download any version you want!

and as written on the page,

{% highlight bash %}
$ pip install [your pgadmin version]-py2.py3-none-any.whl

for example,

$ pip install pgadmin4-1.3-py2.py3-none-any.whl
{% endhighlight %}

It's all! Simple right? That's why we use wheeeeeeeeeeel Sorry


You can find your pgadmin in package folder

{% highlight bash %}
$ /usr/local/lib/python2.7/dist-packages/pgadmin4/
$ /usr/local/lib/python3.5/dist-packages/pgadmin4/

or in your virtual environment's package folder
{% endhighlight %}

to run pgAdmin,

{% highlight bash %}
$ python /usr/local/lib/python3.5/dist-packages/pgadmin4/pgAdmin4.py
{% endhighlight %}

Well you can make a PATH to bash but I just added alias because you may only need pgAdmin4.py only.

{% highlight bash %}
alias pgAdmin4='python3 /usr/local/lib/python3.5/dist-packages/pgadmin4/pgAdmin4.py'
{% endhighlight %}

Have fun with your database!
