---
layout: post
title: "python virtual environment"
date: "2017-07-14 20:56:08 +0900"
location: "Daejeon, South Korea"
commentIssueId: 17
category: Python
tags: [python, virtualenv]
---

When you use python frameworks, like flask or django, you need some specific packages to run and sometimes, it depends on what your project is for. So, most of the time, using virtual environment is really useful! If you make a directory and generate virtual environment in it, you can use completely different python version and also packages included with in your python.

{% highlight bash %}
$ sudo apt-get install python-virtualenv

or

$ pip install virtualenv
{% endhighlight %}

you can check your virtual environment version.

{% highlight bash %}
$ virtualenv --version
{% endhighlight %}

what's next? just make a directory for sandbox(you can just play with virtual environment python. Just everything! That's why it is sandbox).

{% highlight bash %}
$ mkdir [your directory]
{% endhighlight %}

All setup done!

{% highlight bash %}
Activate virtualenv
$ source [your sandbox]/bin/activate

Deactivate virtualenv
$ deactivate
{% endhighlight %}

When you activate virtualenv, your python will be changed as sandbox version. So you have to deactivate it before using your local python! But when you close terminal, it will automatically shutdown. So don't worry!

I'm using virtual environment with my flask application. And for simple usage, added alias in .bashrc

{% highlight bash %}
alias act-vir='source /home/haven/virtual_py/bin/activate'
alias deact-vir='deactivate'
{% endhighlight %}

I think I'm a alias-holic :p It feels like.. some kind of.. making my own linux cheat-sheet ;)
