---
layout: post
title: "New things during the Algorithmic Thinking"
date: "2016-09-24 16:18:46 +0900"
location: "Daejeon, South Korea"
commentIssueId: 11
category: Python
tags: [python study, til]
---

Check out amazing coursera course [Algorithmic Thinking Part 1](https://www.coursera.org/learn/algorithmic-thinking-1) and [Algorithmic Thinking Part 2](https://www.coursera.org/learn/algorithmic-thinking-2).

<h3>1) Return None automatically.</h3>

{% highlight python %}
if self.outstack:
{% endhighlight %}

It will return boolean value that outstack is exist or not.


<h3>2) Double matching</h3>

{% highlight python %}
('{' , '}')
if (open, close) in matches:
{% endhighlight %}

Python is available in double matching in if or while statement.

Also swap function can be..

{% highlight python %}
a, b = b, a
{% endhighlight %}


<h3>3) Instance sorting</h3>

{% highlight python %}
cluster_list.sort(key =
    lambda cluster : cluster.vert_center())
{% endhighlight %}

It is possible to make a sorting factor via lambda. Even classes.
Above code is showing that cluster_list would be sorted in ascending with vert_center value.


<h3>4) Generate empty set list</h3>

{% highlight python %}
setList = [set() for i in range(len(cluster_list))]
{% endhighlight %}

It will generate list of sets

also, it can be
{% highlight python %}
setList = [set()] * len(cluster_list)
{% endhighlight %}

<h3>5) Make dictionary for key list and value list</h3>

{% highlight python %}
key = [1, 2, 3]
value  = [11, 12, 13]
list_a = dict(zip(key, value))
{% endhighlight %}

zip method will concatenate key and value list for each corresponding element.


<h3>6) String list and random.shuffle()</h3>

In python, string is also a list.

{% highlight python %}
l = "hello" is ['h', 'e', 'l', 'l', 'o']
{% endhighlight %}

and

{% highlight python %}
random.shuffle(l)
{% endhighlight %}

will generate a list that contains random element of argument list.


<h3>7) Set generator</h3>

A list can be changed to set.

{% highlight python %}
l = 'hello'
s = set(l)
{% endhighlight %}

will generate

{% highlight python %}
set[('h', 'e', 'l', 'o')]
{% endhighlight %}
