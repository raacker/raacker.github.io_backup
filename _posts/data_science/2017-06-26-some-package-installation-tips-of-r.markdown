---
layout: post
title: "Some package installation tips of R"
date: "2017-06-26 22:18:16 +0900"
commentIssueId: 14
category: DataScience
tags: [R, data science]
---

R supports a lot of packages. There are tons of them and we can use them with just this simple typing,

{% highlight R %}
install.packages('tm')
{% endhighlight %}

But sometimes, there are dependencies of each of packages. It will lead you to exit code 1 or blue mood. Because it is kind of really tricky part to solve them. Some of my friends spent 2 days to install just one package.

Here's tips of some package installation that I tried before.

<h3>1. ggmap</h3>

[ggmap](https://github.com/dkahle/ggmap) is really amazing tool. You can use google map and draw circles or any things for good looking plots. But if you face impossible-to-solve problems? here we go.

Most of case, just these two were problem. Almost every packages will be installed without any scream.

{% highlight bash %}
$ sudo apt-get install libpng-dev libjpeg-dev
{% endhighlight %}

ggmap draws google map image for you. But sometimes, your machine doesn't have these library. Just install them manually.

<h3>2. tm</h3>

When I was making a WordCloud program, I was using [KoNLP](https://github.com/haven-jeon/KoNLP). It's a Korean NLP package for R and quite amazing project. But you need other tools before using it.

{% highlight bash %}
$ sudo apt-get install r-cran-slam gfortran libblas-dev liblapack-dev

in R

install.packages('slam')
install.packages('tm')
{% endhighlight %}

tm uses slam. But just installing it in R will shout you out really badly. Just install it in bash and follow above steps.

<h3>3. KoNLP</h3>

Well because I mentioned KoNLP above, I should write about KoNLP either.

It's simple but the 'java part' will be the hardest time for you.

{% highlight bash %}
$ sudo apt-get install r-cran-rjava libbz2-dev libpcre3-dev
{% endhighlight %}

install rjava and other libraries. I spent 3 hours to find what to install.

then,

{% highlight bash %}
$ sudo R CMD javareconf

in R

install.packages('rJava')
install.packages('devtools')
install.packages('KoNLP')
{% endhighlight %}

You might face some problems with rjava. You should solve it first and after that, you should success with R CMD javareconf. That's all.

<h3>4. XML</h3>

My god... xml is really simple and well-known file format! right? But I failed at installing it at the first time.. :)

You need this.

{% highlight bash %}
$ sudo apt-get install libxml2-dev
{% endhighlight %}

These are all I have yet. If you are struggling with your R package, feel free to leave a comment. Love to help you :)
