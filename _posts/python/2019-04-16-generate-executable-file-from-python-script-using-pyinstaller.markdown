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

{% highlight bash %}
$ pip install pyinstaller
{% endhighlight %}
<br/>

For detailed options, check this [manual link](https://pyinstaller.readthedocs.io/en/stable/usage.html#options)

Basically you can just do

{% highlight bash %}
$ pyinstaller your_file.py

or

# if you are using windows command prompt
$ pyinstaller.exe your_file.py
{% endhighlight %}

Then it will generate exe file out of your script. But what you see is not going to be... just simple exe.

![](/images/Generate_executable_file_from_Python_script_using_pyinstaller.png)

etc...

These files are intermediate files to generate exe file. Just imagine when you compile c++ or java code, bunch of obj files or bytecodes. But to run, you still need several files from that.

To create one single file for making your life easier, add --onefile option.

That's all! You just add --icon option to assign your fancy icon and also you can hide consoles by --noconsole if you have some GUI.






Nope that was not all actually.

My program was trying to access "Program Files" to adjust some of config file I installed. But that means I need privildge elevation or UAC control (User Access Control) or "Run as Administrator"!

This is not easy with pyinstaller actually (Seems like a bug still).

Here's how I did. [Reference](https://stackoverflow.com/questions/43068920/pyinstaller-uac-not-working-in-onefile-mode)

If you don't use --onefile option, then you still have chance to generate privildge program with --uac-admin option.

{% highlight bash %}
$ pyinstaller your_file.py --uac-admin
{% endhighlight %}

Then you can just extract your file which you need including .manifest file.

I wrote a batch file to proceed all automatically and clean up files.

{% highlight bash %}
SET installer_name=MyUACInstaller

pyinstaller.exe --onefile --icon=./my_uac_installer.ico --noconsole %installer_name%.py
pyinstaller.exe --uac-admin %installer_name%.py
cp ./dist/%installer_name%/%installer_name%.exe.manifest ./
cp ./dist/%installer_name%.exe ./
rmdir /S /Q pycache
rmdir /S /Q build
rmdir /S /Q dist
del %installer_name%.spec
PAUSE
{% endhighlight %}

Then it will remain your beautiful .exe file and .manifest only!

Now it gets easy huh? :)

Happy Hacking
