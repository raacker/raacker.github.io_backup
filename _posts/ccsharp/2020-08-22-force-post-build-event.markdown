---
layout: post
title: "Force Post Build Event to run"
date: "2020-08-22 12:10:50 -0800"
location: "Vancouver, BC, Vancouver"
commentIssueId: 61
category: C++
tag: [c++, visualstudio]
---

PostBuild event and PreBuild event in VisualStudio are very useful if you need to automate commands while you are working on c++ programs. Dlls, pdbs, headers or any of files you need for debugging or run.

{% highlight text %}
xcopy /Y /F /D "$(TargetDir)$(TargetName).dll" "$(ProjectDir)..\Output\bin\$(PlatformTarget)\$(Configuration)\"
xcopy /Y /F /D "$(TargetDir)$(TargetName).lib" "$(ProjectDir)..\Output\lib\$(PlatformTarget)\$(Configuration)\"
xcopy /Y /F /D "$(TargetDir)$(TargetName).pdb" "$(ProjectDir)..\Output\pdb\$(PlatformTarget)\$(Configuration)\"
{% endhighlight %}

But if you need to link external project to your new solution and if you need all those files into your working copy, I bet you know how big pain it is. Let's hack VisualStudio Solution & Project to make it easy!

CAUTION! This is just one of the solution to make it work. If you find any better solution, please share!

<b>1) Create empty project to your solution. And add this option under <PropertyGroup Label="Global"></b>

{% highlight text %}
<DisableFastUpToDateCheck>true</DisableFastUpToDateCheck>
{% endhighlight %}

{% highlight text %}
<PropertyGroup Label="Globals">
  <VCProjectVersion>15.0</VCProjectVersion>
  <ProjectGuid>{00000000-0000-0000-00000000-91BC08E963AF}</ProjectGuid>
  <RootNamespace>TestProject</RootNamespace>
  <WindowsTargetPlatformVersion>10.0.17763.0</WindowsTargetPlatformVersion>
  <DisableFastUpToDateCheck>true</DisableFastUpToDateCheck>
</PropertyGroup>
{% endhighlight %}

You might want to try it in your code project also but I don't recommend it since it will disable fast up to date checking.

{% highlight text %}
A boolean value that applies to Visual Studio only. The Visual Studio build manager uses a process called FastUpToDateCheck to determine whether a project must be rebuilt to be up to date. This process is faster than using MSBuild to determine this. Setting the DisableFastUpToDateCheck property to true lets you bypass the Visual Studio build manager and force it to use MSBuild to determine whether the project is up to date.
{% endhighlight %}

Reference:[Always run post build event commands in visual studio 2017](https://stackoverflow.com/questions/51228443/always-run-post-build-event-commands-in-visual-studio-2017/51230663)

<b>2) Put build event commands and add this project to your code project build dependency.</b>

Build Dependencies... -> Project Dependencies... and add your new project.

<b>3) All set! </b>

Now everytime you want to change external project and copy any updated files from that project, your copy project will only does its job to check and try to copy them without rebuilding everything.

Happy hacking!
