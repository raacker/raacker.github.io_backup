---
layout: post
title: "Make a shared directory in your virtual machine(virtualbox)"
date: "2017-06-26 16:18:08 +0900"
location: "Daejeon, South Korea"
commentIssueId: 12
category: Linux
tags: [linux, Virtualbox]
---

Sometimes, you might think just downloading some files inside of your virtual machine is useless. That may come from the Internet speed or something special situation( as I experienced when setting up my hadoop clusters. They were connected each other, except  the Internet outside ).

The solution is to make a shared directory! Then you don't have to get experienced of the sh***ty internet problem! ( maybe I'm exaggerating :p Virtualbox or VMware is quite awesome tool. You barely encounter these problems. )

I'll post a way to make shared directory on Virtualbox system. But it will be very similar to VMware way.

Step0. You must install Guest Additions CD program from virtualbox.

Before get started, you must install additional libraries of virtualbox. It only takes 5 minutes.

1. Go [Devices tab -> Click 'Insert Guest Additions CD image']

2. Reboot virtual machine

3. You will be able to find VBOXADDITONS image file and install it.

4. Reboot again

Step1. Give a permission to your user group

{% highlight bash %}
$ usermod -G vboxsf -a "username"
{% endhighlight %}

Step2. Make a directory that you want to use as a shared one.

Go to Devices -> Shared Folders -> Shared Folder Settings

![](/images/Make a shared directory in your virtual machine(virtualbox)-1.PNG)

then check 'Auto-mount' button and press OK.

Step3. Just reboot!

Now you can find the sf_'folder name' on your desktop. If your shared folder keep disappearing always when you boot your machine, try these steps in Virtualbox Manager.

When I tried this with Lubuntu, it didn't work well actually. I think some of linux distribution support automation or shared folder options. If you're facing any problem, feel free to comment below.
