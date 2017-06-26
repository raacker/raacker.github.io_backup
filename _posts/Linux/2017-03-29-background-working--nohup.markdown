---
layout: post
title: "Background working : Nohup"
date: "2017-03-29 21:06:31 +0900"
location: "Daejeon, South Korea"
commentIssueId: 1
category: Linux
tags: [linux, server]
---
<h4>In my data science class,</h4>
one of the graduate students of my professor developed fitcraft, fitbit with minecraft. It is just same as actual minecraft game but in that server, players can earn resources via 'step data' of fitbit. Go work out for more stuffs! Quite cool idea as Pokemon Go does :)

But me and my gamer group(other two friends :) ) wanted our own server! To make diamond sword and pick to travel our world and dig into deeeeeeeep dark.

Our plan was as below.

1. Make Amazon EC2 ubuntu server.
2. Run Minecraft server java program that Mojang provides.
3. Enjoy it!

But as we, computer guys, always do in everyday, we had to face the problem. We wrote shell script to run it but when we close shell session, it also shutdown! Even if we ran it as a background process.

The answer was using **nohup**.

{% highlight text %}
nohup is a POSIX command to ignore the HUP (hangup) signal. The HUP signal is, by convention, the way a terminal warns dependent processes of logout.

{% endhighlight %}
Reference : [https://en.wikipedia.org/wiki/Nohup](https://en.wikipedia.org/wiki/Nohup)

In other words, noHUP is used for background process which needs to be run whenever the shell is logout or not.

Our server startup code was like this.

{% highlight bash %}
$ java -Xmx1024M -Xms2014M -jar minecraft_server.1.11.2.jar nogui
{% endhighlight %}

You can find this code on official website. [https://minecraft.net/en-us/download/server](https://minecraft.net/en-us/download/server)

Now we want to run minecraft server as background!

then shell script will be like this.

{% highlight bash %}
$ nohup java -Xmx1024M -Xms2014M -jar minecraft_server.1.11.2.jar nogui &
{% endhighlight %}

You can't find this process via single ps command.

use

{% highlight bash %}
$ ps -ef | grep nohup
{% endhighlight %}

the logs will be included in nohup.out in the same directory where your file located.

Happy mining! I actually died by spider a few hours ago... lost all diamond....
