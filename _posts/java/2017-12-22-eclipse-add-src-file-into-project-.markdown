---
layout: post
title: "Eclipse: Add src file into project "
date: "2017-12-22 15:48:32 -0800"
location: "San Diego, CA"
commentIssueId: 31
category: Java
tags: [java, eclipse]
---

**Sometimes(most of time)**, we need to look up the original source code of JDK. Maybe you want to compare performance of your own logic and provided method, or you want to know why your crash happened inside of library.

Let's add source code into your eclipse and make it easy to browse. (you may find [grepcode.com](http://grepcode.com) is also useful)

1. Go [Window tab -> Preferences -> Java -> Installed JREs]

![](/images/eclipse_add_src_file_into_project-1.PNG)

You will see your JRE directory which is added to eclipse already.

If not(I'm pretty sure there must be at least one JRE because eclipse is also Java program!), please add JRE directory first.

2. Click your JRE and click 'Edit' button

3. Below the library list, find rt.jar

![](/images/eclipse_add_src_file_into_project-2.PNG)

4. Click 'Source Attachment' and find your JDK directory's 'src.zip' file.

![](/images/eclipse_add_src_file_into_project-3.PNG)

5. Click 'Finish' and 'Apply'

All set! Now you can immediately move onto the library source class by pressing 'F3' key.

Happy coding :)
