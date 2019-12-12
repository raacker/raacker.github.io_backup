---
layout: post
title: "When CMakeList cannot find your library"
date: "2019-12-12 20:00:19 +0900"
location: "Suwon, South Korea"
commentIssueId: 58
category: 3D
tag: [library, point_cloud, cmake]
---
This post is just a quick note for myself and also for someone how has problem with building [libE57Format](https://github.com/asmaloney/libE57Format)(as I did) which is a fork version of original libe57. Or also for someone who is suffering from cmake when it's not looking for your library with no reason.

FYI, [e57 format](http://www.libe57.org/) is very important format for whom is dealing with PointCloud world. For the large size of PointCloud, most of the time you should use e57 to compress the data.

On CMakeList.txt, it will look for dependency libraries from cmake/module directory.

If it's still not looking for your library on environment variable or any relative path or any of absolute path, put your library on cmake directory and just put this line in CMakeList.txt at the beginning.

{% highlight C++ %}
set (CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_SOURCE_DIR}/xerces-c-3.2.2")

or

set (CMAKE_INSTALL_PREFIX "${CMAKE_CURRENT_SOURCE_DIR}/{your-library-path}/{to-somewhere}")
{% endhighlight %}
