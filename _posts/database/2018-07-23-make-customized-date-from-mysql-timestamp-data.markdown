---
layout: post
title: "Make customized date from MySQL timestamp data"
date: "2018-07-23 00:32:05 +0900"
location: "Seoul, South Korea"
commentIssueId: 42
category: Database
tags: [mysql, database, JavaScript, sequelize, linux]
---

<h3>Javascript</h3>

has date Object.

{% highlight javascript %}
const curDate = new Date();
// default is new Date(Date.now())
{% endhighlight %}

But if you fetch timestamp data from MySQL, format would be a bit different.

{% highlight javascript %}
const result = await sequelize.query(
    `
    SELECT
        createDate
    FROM table
    `,
    { type: Sequelize.QueryTypes.SELECT },
);
// { createDate: 2018-07-23T00:30:00.000Z },
{% endhighlight %}

actual data will be on that format, it is called 'ISO format'

{% highlight javascript %}
const date = (new Date()).toISOString();
// 2018-07-22T15:42:57.249Z
{% endhighlight %}

ISO format consists to have UTC time (+00:00) and it always will be if you're going to gather from MySQL timestamp.

But don't worry. As we all know,

![](/images/windows-10-automatic-setup-batch-for-windows-shell.jpg)

It's actually easy to make date object. Just put it into contructor then it will generate all data based on your environment setting.

{% highlight javascript %}
const dateObject = new Date(data.createDate);
{% endhighlight %}

And call getMonth() and getDate()

{% highlight javascript %}
const month = dateObject.getMonth();
const day = dateObject.getDay();
// 7 and 23
{% endhighlight %}

Good! But sometimes, you want to make zero padding

{% highlight javascript %}
const month = (`0${(dateObject.getMonth() + 1)}`).slice(-2);
const day = (`0${(dateObject.getDate())}`).slice(-2);
// 07 and 23
{% endhighlight %}

Then you are now ready to make any of date format with string template!

{% highlight javascript %}
const result = `${dateObject.getFullYear()}년 ${month}월 ${day}일`;
// 2018년 07월 23일

const result2 = `${month}.${day}.${dateObject.getFullYear()}`;
// 07.23.2018
{% endhighlight %}
