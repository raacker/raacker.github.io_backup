---
layout: post
title: "Async update"
date: "2017-10-24 20:29:59 -0700"
location: "San Diego, CA"
commentIssueId: 22
category: Android
tags: [java, android, asynctask]
---
Handling data is always important. Especially, when app needs to get data from server and handle it, sending, receiving and control the time gap always matter. So, sometimes, using async task is useful to make it easy.

[AsyncTask](https://developer.android.com/reference/android/os/AsyncTask.html) allows you to perform background works while your UI, activity, is working on another thing. You don't need any semaphore control or thread handling, just AsyncTask will bring the result to you when it's ready. But keep it mind, AsyncTask is not a magic. You can't use this class for every problems you need to solve.

For example, when you have a method that is drawing plot of chart data from server, you need to wait on receiving data completely. If some other logic is following after, like user prompt or showing result activity, you need to block the process until your plot shows up. This is not a proper way to use AsyncTask. If you can wait on the response whenever it arrives, that's the perfect case!

{% highlight java %}
private class BackgroundProcess extends AsyncTask <Double, Integer, Long>
    @Override
    protected Long doInBackground(Double... params) {
        // ... what you want to do in background. Get data from server via
        // http request? cool
    }

    @Override
    protected void onProgressUpdate(Integer... progress) {
        // what you want to do while in the progress
    }

    @Override
    protected void onPostExecute(Long o) {
        super.onPostExecute(o);
        // what you want to do when you get the result
    }
}
{% endhighlight %}

Usually, AsyncTask class is declared as nested or inner class.

One thing you have to mind, **Must set the generic types!** Setting generic types is most important thing you have to care about.

{% highlight java %}
AsyncTask< Task Parameter, Progress Parameter, Result Type >
{% endhighlight %}

You can guess what you should put on those three generics. If you can set these types, it will provide you the better and easy life to debug.

So when your background task is ready to use,

{% highlight java %}
BackgroundProcess bgProcess = new BackgroundProcess();
bgProcess.executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR);
{% endhighlight %}

try to use [executor service](https://developer.android.com/reference/java/util/concurrent/Executor.html)! There are two types of executor, [SERIAL_EXECUTOR and THREAD_POOL_EXECUTOR](https://developer.android.com/reference/android/os/AsyncTask.html#SERIAL_EXECUTOR). You can choose what type of executor you need. And also AsyncTask has [status](https://developer.android.com/reference/android/os/AsyncTask.Status.html), FINISHED, PENDING, RUNNING. You might want to use these status for checking availability of AsyncTask. 
