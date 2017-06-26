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
java -Xmx1024M -Xms2014M -jar minecraft_server.1.11.2.jar nogui
{% endhighlight %}

You can find this code on official website. [https://minecraft.net/en-us/download/server](https://minecraft.net/en-us/download/server)

Now we want to run minecraft server as background!

then shell script will be like this.

{% highlight bash %}
nohup java -Xmx1024M -Xms2014M -jar minecraft_server.1.11.2.jar nogui &
{% endhighlight %}

You can't find this process via single ps command.

use

{% highlight bash %}
ps -ef | grep nohup
{% endhighlight %}

the logs will be included in nohup.out in the same directory where your file located.

Happy mining! I actually died by spider a few hours ago... lost all diamond....

<div id="comments">
  <h2>Comments</h2>
  <div id="header">
    Want to leave a comment? Visit <a href="https://github.com/raacker/raacker.github.io/issues/{{page.commentIssueId}}"> this post's issue page on GitHub.</a>
  </div>
</div>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/datejs/1.0/date.min.js"></script>

<script type="text/javascript">
  function loadComments(data) {
    for (var i=0; i<data.length; i++) {
      var cuser = data[i].user.login;
      var cuserlink = "https://www.github.com/" + data[i].user.login;
      var clink = "https://github.com/raacker/raacker.github.io/issues/{{page.commentIssueId}}#issuecomment-" + data[i].url.substring(data[i].url.lastIndexOf("/")+1);
      var cbody = data[i].body_html;
      var cavatarlink = data[i].user.avatar_url;
      var cdate = Date.parse(data[i].created_at).toString("yyyy-MM-dd HH:mm:ss");
      $("#comments").append("<div class='comment'><div class='commentheader'><div class='commentgravatar'>" + '<img src="' + cavatarlink + '" alt="" width="20" height="20">' + "</div><a class='commentuser' href=\""+ cuserlink + "\">" + cuser + "</a><a class='commentdate' href=\"" + clink + "\">" + cdate + "</a></div><div class='commentbody'>" + cbody + "</div></div>");
    }
  }
  $.ajax("https://api.github.com/repos/raacker/raacker.github.io/issues/{{page.commentIssueId}}/comments?per_page=100", {
    headers: {Accept: "application/vnd.github.v3.html+json"},
    dataType: "json",
    success: function(msg){
      loadComments(msg);
   }
  });
</script>
