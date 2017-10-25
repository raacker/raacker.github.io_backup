---
layout: post
title: "real-time update!"
date: "2017-10-24 21:46:10 -0700"
location: "San Diego, CA"
commentIssueId: 23
category: Android
tags: [java, android, asynctask, handler]
---
This post continues from [AsyncTask](https://raacker.github.io/android/2017/10/25/async-update/). When you use SwipeRefreshLayout, it's quite useful! You can refresh as much as you want. But if your app is for tracking data in real-time? user will get annoyed easily. It should provide the way to update for every 1 or 2 seconds without any controls. Handler stands for this.

[Handler](ttps://developer.android.com/reference/android/os/Handler.html) is like a queue system. You can implement Runnable class that does what you want to do in every unit time and use postDelayed method to run it.

{% highlight java %}
private Runnable runnable = new Runnable() {
    @Override
    public void run() {
        // do whatever you want.
        handler.postDelayed(this, 1000);
    }
};
{% endhighlight %}

So this is runnable and to begin the handler, call postDelayed for the first time.

{% highlight java %}
handler = new Handler();
handler.postDelayed(runnable, 1000);
{% endhighlight %}

then runnable can call postDelayed method and it will continuously repeated.

If you want to stop this(like when you start another activity, you might not want to keep this),

{% highlight java %}
handler.removeCallbacks(runnable);
{% endhighlight %}

call removeCallbacks() to delete whole callbacks pending on.
