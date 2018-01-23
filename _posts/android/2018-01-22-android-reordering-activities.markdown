---
layout: post
title: "Android: Reordering Activities"
date: "2018-01-22 20:38:13 -0800"
location: "San Diego, CA"
commentIssueId: 40
category: Android
tags: [java, android]
---

<h3>When you want to</h3>

reuse your activities, it's actually not easy. You have to care about than you thoughts.

Let's see this example.

![](images/reordering_activities.PNG)

Let's say we have to build an application which has Username, Main, Setup activities.

At the start up, 'Username activity' launches and ask user to put username. Then 'Main activity' receive it through intent and retrieve username relevant data from database.

And when user wants to change username, go though 'Setup activity' and go to 'Username activity' again. That makes sense right? we cannot make separate activities for this because it is mainly doing equal.

Okay so far it seems all good right? So we put some flags and pass it through intent that shows it is first app launch or during the 'Setup activity'. But here is the problem.

![](images/reordering_activities2.PNG)

All previous activities will remain behind! Even though we don't need them anymore, activity stack doesn't know it. So if you press "go back" button a few more it will bring you back to old one which still have previous username.

Then what we can do? Remove all previous activities when submitting new username.

At AndroidManifest.xml, put

{% highlight xml %}
<uses-permission android:name="android.permission.REORDER_TASKS" />
{% endhighlight %}

And put intent flag where you want to clear up all activities.

{% highlight java %}
intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);>
{% endhighlight %}

Happy coding ;p
