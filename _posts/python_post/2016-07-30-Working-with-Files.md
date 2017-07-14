---
layout: post
date:   2016-07-30 18:14:10 +0900
location: "Daejeon, South Korea"
commentIssueId: 10
title: Working with Files
category: Python
tags: [python]
---

Python supports easiest file handling modules.

For easy opening,

{% highlight python %}
with open("filename.txt") as f:
  print(f.read())
{% endhighlight %}

just open 'filename.txt' and use it instantly!
