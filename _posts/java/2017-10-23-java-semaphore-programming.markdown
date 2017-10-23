---
layout: post
title: "Java semaphore programming"
date: "2017-10-23 08:33:02 -0700"
location: "San Diego, CA"
commentIssueId: 21
category: Java
tags: [java, thread]
---

When you are working on actual program, you cannot avoid multi-threading. Bunch of threads are combined together and to process background work or handling multiple stuffs always require multi-threading.

But the biggest and hardest problem is when more than 2 threads are trying to access the same object or variables, or sometimes, those threads need to work in a specific order. Like a few lines of first thread must be run before second thread begins. This part is super tricky and if your code is hiding something, you even can't start debugging and figure out what is the problem.

The way to handle threads' priority and functionality is using semaphore, which we learned and heard tons of time at the Operating System class. Give a rock to first thread and second thread will wait until it can achieve the rock. Or philosophers' knives.

In Java programming, CountDownLatch class is used for semaphore handler. [CountDownLatch Java doc](http://docs.oracle.com/javase/8/docs/api//java/util/concurrent/CountDownLatch.html)

You can use countDown method for giving the rock back, and await method to wait until CountDownLatch can retrieve the rock.

{% highlight java %}
CountDownLatch countDownLatch = new CountDownLatch(1);
SwingUtilities.invokeLater(() -> {
    getTheValue();
    countDownLatch.countDown();
});
countDownLatch.await();
printTheValue();
{% endhighlight %}

The constructor require amount of rocks. We normally use only 1 rock, right?

Then your first thread will start. **You must run your thread via ExecutorService or any other class which will run your thread for you.**

{% highlight java %}
ExecutorService executor = Executors.newSingleThreadExecutor();
executor.submit(runnable);
{% endhighlight %}

My example code is using SwingUtilities which is called by AWT thread.

Then countDownLatch will wait until it can retrieve the rock. After countDown method is called, your first thread will continue and run printTheValue method.

With this flow, you can control the logic flow of threads and manipulate the multiple threads' data or anything else.
