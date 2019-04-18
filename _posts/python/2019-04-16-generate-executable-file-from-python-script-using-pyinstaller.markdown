---
layout: post
title: "Generate executable file from Python script using pyinstaller"
date: "2019-04-16 20:34:41 +0900"
location: "Seoul, South Korea"
commentIssueId: 55
category: Python
tags: [python, study_note]
---

For me, it's very okay to use just .py script with python interpreter. Very quick and easy.

But sometimes, you might figure out that you eventually want to convert script to executable file to have it as standalone.

What we can use in this case is "pyinstaller".
<br/>


{% highlight bash %}
$ pip install pyinstaller
{% endhighlight %}
<br/>

First, install pyinstaller using pip. Then you can run pyinstaller on terminal.

There are several options you can re

{% highlight bash %}
$ pip install pyinstaller
{% endhighlight %}
<br/>

SET setup_name=SteamVR_Setup

pyinstaller.exe --onefile --icon=./polyga_logo.ico --noconsole %setup_name%.py
pyinstaller.exe --uac-admin %setup_name%.py
cp ./dist/%setup_name%/%setup_name%.exe.manifest ./
cp ./dist/%setup_name%.exe ./
rmdir /S /Q pycache
rmdir /S /Q build
rmdir /S /Q dist
del %setup_name%.spec
PAUSE
