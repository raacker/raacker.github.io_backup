---
layout: post
title: "xls to csv and encoding problem"
date: "2017-06-26 21:55:29 +0900"
location: "Daejeon, South Korea"
commentIssueId: 13
category: DataScience
tags: [python, R, data science, encoding]
---

Well, most of times, you should reprocess your dataset, including cleansing. It can be separate or merge the columns or delete some miss placed data. Recently, lots of people use CSV or TSV format as the datasets' format. But sometimes, what you found in the open data site or somewhere can be excel format, like xls or xlsx. In these situations, you need only one line command.
( with a package :) )

{% highlight bash %}
$ sudo apt-get install gnumeric
{% endhighlight %}

First of all, install gnumeric first. It will provide us a fancy tool, ssconvert.

Next,

{% highlight bash %}
$ ssconvert something.xlsx something.csv
{% endhighlight %}

Done! Totally easy and it works like a charm!

ssconvert or SpreadSheetconvert, is a converting tool for spreadsheet data.

If you want to know what types of format supported, try this. Or just checkout the manual page.

{% highlight bash %}
$ ssconvert --list-importers
$ ssconvert --list-exporters
{% endhighlight %}

Okay It's all done well! Great job. But... my file crashed with bad unicodes..

then try this.

{% highlight bash %}
$ iconv -f "from this encode" -t "to this encode" filename.csv > filename.csv

like this way,

$ iconv -f euc-kr -t utf-8 2015_broken_encode_set.csv > 2015.csv
{% endhighlight %}

It will give you a very simple and perfect result.
