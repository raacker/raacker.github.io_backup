---
layout: post
title: "String Methods"
date: "2016-07-30 21:04:30 +0900"
location: "Daejeon, South Korea"
commentIssueId: 8
category: Python
tags: [python]
---

Python has really various string methods. It is really useful and powerful. Must be handy!

{% highlight python %}
print ",".join(["Hello", "World!"])
>>> Hello, World!

{% endhighlight %}
join method is like string generator. Given arguments will be concatenated with join's caller

{% highlight python %}
s1 = "It is pretty awesome"
s1.replace(" ", "")
>>> Itisprettyawesome

{% endhighlight %}
replace method is string substituting. First argument value will be substitute with second argument.

{% highlight python %}
print s1.startswith("It")
>>> True

print s1.endswith("awesome")
>>> True

{% endhighlight %}
startswith and endswith are boolean methods that return if caller string starts with given argument or ends with.

{% highlight python %}
print s1.upper()
>>> IT IS PRETTY AWESOME

print s1.lower()
>>> it is pretty awesome

{% endhighlight %}
upper and lower return capitalized string or lowercased string.

{% highlight python %}
print s1.split(" ") #print s1.split()
>>> ['It', 'is', 'pretty', 'awesome']

{% endhighlight %}
split divides string into substrings by given argument. And split's default deliminator is blank
