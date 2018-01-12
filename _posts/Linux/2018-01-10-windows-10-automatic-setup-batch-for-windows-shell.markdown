---
layout: post
title: "Windows 10: Automatic setup batch for Windows shell"
date: "2018-01-10 20:28:42 -0800"
location: "San Diego, CA"
commentIssueId: 38
category: Linux
tags: [linux, windows 10, shell, script, automation]
---

<h3>At my company,</h3>

I had a chance to show my interest of automation script :) but it was "D***" windows command line without git bash patch! *(When you intall git on windows, you can install linux command programs for windows command line)* and I had to write *bat* file for easy to use.

It had to be special program that anyone can use and.. pwwww. If you are already used to linux and have no experience of Windows shell programming, you will also say "D***" to this script. Feels like going back to ancient! But anyway,

![](/images/windows-10-automatic-setup-batch-for-windows-shell.jpg)

WE WILL FIND THE SOLUTION!

So I finally made it and these are some might be useful to you.

**1) Delete Chrome cache data**

First is cleaning up Google Chrome's data. I tried bunch of things but just manually deleting data was better. If you have better idea, please suggest me!

Chrome data are located at

```
C:\Users\[user_name]\AppData\Local\Google\Chrome\"User Data"\
```

But the tricky thing is if someone has logged in Chrome before, not google website, actual Chrome account sync, it will be differ.

{% highlight text %}
Never logged in =>
C:\Users\[user_name]\AppData\Local\Google\Chrome\"User Data"\Default

Logged in once =>
C:\Users\[user_name]\AppData\Local\Google\Chrome\"User Data"\"Profile 1" (or more profiles)
{% endhighlight %}

Okay, so if you figured out which directory you should delete, delete these files.

- Preferences, Cookies, "Web Data", "Login Data", "Current Tabs", "Current Session", History, Favicons, "Visited Links"

script will be like this,

{% highlight text %}
del C:\Users\haven\AppData\Local\Google\Chrome\"User Data"\"Profile 1"\"Current Tabs"
{% endhighlight %}

Lastly, delete cache directory.

{% highlight text %}
rmdir /S /Q C:\Users\haven\AppData\Local\Google\Chrome\"User Data"\"Profile 1"\Cache
{% endhighlight %}

<br/>
**2) Kill process**

When you want to clean Chrome data, chrome shouldn't be running at same time. So if you want to kill current Chrome process,

{% highlight text %}
Taskkill /IM chrome.exe /F
{% endhighlight %}

then it will force shutdown chrome processes

<br/>
**3) Don't show what shell is doing**

If you do above commands, shell will be too chitchatty. Saying everything that it is running something.

{% highlight text %}
C:\Users\haven\Desktop: dir hello
C:\Users\haven\Desktop: del hello
...
{% endhighlight %}

to shut all noises off, put

{% highlight text %}
@echo off
{% endhighlight %}

at the top of batch file

<br/>
**4) Print empty line**

{% highlight text %}
echo(
{% endhighlight %}

That's it

<br/>
**5) Delete directory(using wildcard)**

Well.. there is wildcard in windows but it won't be like you imagined.

just deleting single directory is enough with "rmdir" or "rd". But if you have to delete multiple device via wildcard,

{% highlight text %}
for /F %%i in ('dir /a:d /S /B C:\Users\haven\Desktop\temp\A002*') do rmdir /S /Q %%i
{% endhighlight %}

Reference: [Superuser - Using wildcards with the rmdir or rd command](https://superuser.com/questions/764348/using-wildcards-with-the-rmdir-or-rd-command)

**Don't forget to add one more % to use it in batch file**

It will get directory only names via for loop and run rmdir for each of them.

<br/>
**6) Empty trash can**

This command will attempt to empty whole trash cans for every users but if you don't have privilege, you are good to go. Other trash can will be just access denied.

{% highlight text %}
rmdir /S /Q %systemdrive%\$Recycle.bin
{% endhighlight %}

Reference: [Stack Overflow - how to empty recyclebin through command prompt?](https://stackoverflow.com/questions/9238953/how-to-empty-recyclebin-through-command-prompt)

<br/>
**7) Copy file or directory**

Windows has special copy program called "xcopy"

If you want to copy file, just copy it. But if you want to copy directory, use **/E** option to copy all subdirectories and files inside.

**/Y** option will be used for overwriting files (saying yes to prompt messages)
**/Q** option is also used for "quiet"

{% highlight text %}
xcopy C:\Users\haven\Desktop\temp\image.png C:\Users\haven\Desktop\release\image.png

xcopy /E C:\Users\haven\Desktop\temp C:\Users\haven\Desktop\release
{% endhighlight %}

<br/>
**8) Change wallpaper**

To change wallpaper, we have to add register key

{% highlight text %}
REG ADD "HKCU\Control Panel\Desktop" /V Wallpaper /T REG_SZ /F /D [image's absolute path]
{% endhighlight %}

If response says 'request successfully completed', you are good to go. If you reboot or logout your computer, you will see changed wallpaper.

If you want to see your background changed immediately,

{% highlight text %}
rundll32.exe user32.dll, UpdatePerUserSystemParameters
{% endhighlight %}

<br/>
**9) Clear Windows cache**

Windows cache means some "Quick access", "History", so on.

First, we have to delete a register key to see AppData\Roaming\Microsoft\Windows\Recent

{% highlight text %}
REG Delete HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths /F
{% endhighlight %}

Then remove all cache data

{% highlight text %}
del /F /Q C:\Users\[user_name]\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations*
del /F /Q C:\Users\[user_name]\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations*
del /F /Q C:\Users\[user_name]\AppData\Roaming\Microsoft\Windows\Recent*
del /F /Q C:\Users\[user_name]\AppData\Local\Microsoft\Windows\History*
del /F /Q C:\Users\[user_name]\Downloads*
{% endhighlight %}

<br/>
**10) Delete bat file itself**

It's like a magic command

{% highlight text %}
del %0
{% endhighlight %}

it will delete itself!

<br/>
If I can use Linux bash shell script, I definitely use it. But you know sometimes.. you have to do what you don't want to do :)
