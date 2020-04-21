---
layout: post
title: "Flutter hot reload doesn't work!"
date: "2020-04-21 22:52:19 +0900"
location: "Suwon, South Korea"
commentIssueId: 59
category: Flutter
tag: [flutter, study_note]
---

Once apon a time, there was one guy who regretted stop learning flutter a while ago. And he met an old man with long curly white hair who was about to fall into the cliff, saying

Time to get back to studying you fool!

![](/images/post59_flutter_you_fool.jpg)

So after the guy heard the voice, he bought "Another" flutter course from udemy and make himself to accomplish this course for the first time!

...

And that was my actual story. I've been through lots of stuffs but still have very bad habit that I don't finish something that I started!

Well but no luck with my new virtual devices? Somehow, hot reload didn't work which was I've never had to care about.

![](/images/post59_not_working.png)

As you can see, hot reload icon is blacked out, non-clickable and also console is saying there was a problem with connecting to host.

"Error connecting to the service protocol blahblah..."

If you also see this message, you might want to look at your device's api version which that message never shows you. At this moment (April 2020), highest supported api level is 28.

![](/images/post59_device_list.png)

You will have a quick fix after switching to lower api device!

![](/images/post59_now_it_works.png)

Happy flutter-ing
