---
layout: post
title: "Install Flutter on Linux"
date: "2019-04-15 19:56:49 +0900"
location: "Seoul, South Korea"
commentIssueId: 53
category: Flutter
tag: [flutter, opensource, app, study_note]
---

On this post, I will demonstrate how to install flutter on Ubuntu distribution flawlessly + android SDK installation.

Well, I just tried to follow the description on Flutter docs but didn't work for me :( after spending some hours, finally got it work on my Elementary OS. So wanna share it as keeping it as my self-note.

Before get started, if you like intelliJ and very okay with android studio, just installing Android studio would be much of time saver. Because I manually installed Android SDK to make flutter app on VSCode without ginormous Android studio.

**1) Clone Flutter repository**

{% highlight bash %}
$ git clone -b stable https://github.com/flutter/flutter.git
{% endhighlight %}


**2) Move flutter repo to wherever you want**
Since I usually put my programs into '/usr/local/bin', I'll try that.

FYI, If your user account have no authority to /usr/local/bin, try this

{% highlight bash %}
$ sudo chown $(whoami):$(whoami) /usr/local && sudo chown -R $(whoami):$(whoami) /usr/local
{% endhighlight %}

It will change /usr/local directory's owner to your user account & user group. If you know about File Permission, just modify that script, because I assume that's just basic account which has group of same name.
<br/>

**3) Add flutter into environment PATH**

{% highlight bash %}
$ export PATH="$PATH:(flutter path)/flutter/bin"
{% endhighlight %}

If you want it to keep on forever, put the line under bottom of your .zshrc or .bashrc.
<br/>
<br/>

**4) Run flutter to download dart SDK automatically.**

{% highlight bash %}
$ flutter
{% endhighlight %}

After dart download, try

{% highlight bash %}
$ flutter doctor
{% endhighlight %}

It will yell at you that you don't have android toolchain or Android SDK.
<br/>

**5) Install Android SDK - 1. Install Java**

{% highlight bash %}
$ sudo apt install openjdk-8-jdk
{% endhighlight %}

You can try to install default-jdk. But on my case, I had to revert the version to 8.
<br/>

**6) Install Android SDK - 2. Install Android SDK**

Go to [Android Developer download](https://developer.android.com/studio/#downloads), donwload sdk-tools-linux.zip and unzip it.

{% highlight bash %}
$ unzip sdk-tools-linux-(your downloaded version).zip
{% endhighlight %}
<br/>

**7) Install Android SDK - 3. Add to PATH**

Move Android SDK folder to desired location and add to PATH also.

{% highlight bash %}
$ export PATH="$PATH:(Folder path)/tools:(Folder path)/tools/bin:(Folder path)/platform-tools"
$ export ANDROID_HOME="(Folder path)"
{% endhighlight %}
<br/>

**8) Install Android SDK - 4. Make repositories.cfg file**

{% highlight bash %}
$ touch ~/.android/repositories.cfg
{% endhighlight %}

It will be needed to run sdkmanager and install libraries.<br/>


**9) Install Android SDK - 5. Install packages**

{% highlight bash %}
$ sdkmanager --list
{% endhighlight %}

list command will show you which tools you can install. To run flutter, you need to install latest sdk version. SDK 28 is latest on this post so command will be

{% highlight bash %}
$ sdkmanager "platform-tools" "platforms;android-28" "build-tools;28.0.3"
{% endhighlight %}
<br/>

**10) Install Android SDK - 5.1. If you got error to run sdkmanager**

If your sdkmanager got error while running on commands, try this

Open sdkmanager with vim or nano.

{% highlight bash %}
$ vi sdkmanager
{% endhighlight %}

Next, find DEFAULT_JVM_OPTS variable and add this line at the end of the line. Be careful with small quote.

{% highlight bash %}
DEFAULT_JVM_OPTS='"-Dcom.android.sdklib.toolsdir=$APP_HOME"'
->
DEFAULT_JVM_OPTS='"-Dcom.android.sdklib.toolsdir=$APP_HOME" -XX:+IgnoreUnrecognizedVMOptions --add-modules java.se.ee'
{% endhighlight %}

[reference](https://stackoverflow.com/questions/47150410/failed-to-run-sdkmanager-list-android-sdk-with-java-9/47150411)

And try running sdkmanager command again.<br/>

If you are going to make Android emulator either, do the same step on "avdmanager".<br/>

**11) Android licenses accept**

{% highlight bash %}
$ flutter doctor --android-licenses
{% endhighlight %}

Read the licenses and type "y".<br/>


All set!

Well if you just install android studio, you don't have to worry about most of the steps I posted. But if you did same what I did (I had to set my Elementary OS size to 128GB while giving 300GB to my Windows...) and just want to use Visual Studio code as flutter development, it worth to try.
