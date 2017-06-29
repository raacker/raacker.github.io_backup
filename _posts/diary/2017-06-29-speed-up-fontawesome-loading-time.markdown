---
layout: post
title: "Speed up FontAwesome loading time"
date: "2017-06-29 10:41:40 +0900"
location: "Daejeon, South Korea"
commentIssueId: 15
category: Diary
tags: [diary, jekyll, FontAwesome]
---

I just updated my blog with [FontAwesome](http://fontawesome.io/). It's quite amazing toolkit! You can easily use lots of icons for free. But when I implemented at the first time, It gets really bad. Page loaded first and after that, icons were slowly updated. It's not that slow(about 0.3 secs) but a bit annoying. Here's how I resolved this problem.

1. asynchronous update
![](/images/speed up fontawesome loading time 1.PNG)

When you register your account at CDN, you can manage your embed code. then you can turn on the asynchronous option. It will make the icons load in background.

2. don't miss the stylesheet!

Yeah. Honestly, this was my problem. Don't miss to put style sheet in your html.

{% highlight html %}
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"/>
{% endhighlight %}

Yes. If you miss this line, jekyll will try to find the css's link and it will take a few moment!

I spent too many times because of that one single line.. never miss it! now it works like a charm.
