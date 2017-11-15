---
layout: post
title: "React Study [2] : install and build "
date: "2017-11-15 11:14:13 -0800"
location: "San Diego, CA"
commentIssueId: 26
category: React
tags: [react, web, study, ui, library]
---

<h2>Requirement</h2>

Basically, react is JavaScript. So we need npm, but I'd like to use yarn as substitute of npm.

[npm](https://www.npmjs.com/)
{% highlight bash %}
sudp apt-get install npm
{% endhighlight %}

[nodejs](https://nodejs.org/en/)

yarn is based on nodejs so you might need to update nodejs or install it first.
I recommend you to install version 8.
{% highlight bash %}
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
{% endhighlight %}

[yarn](https://yarnpkg.com/en/)
{% highlight bash %}
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

and

sudo apt-get update && sudo apt-get install yarn
{% endhighlight %}

<h2>Install create-react-app</h2>

{% highlight bash %}
npm install -g create-react-app

or

yarn add create-react-app
{% endhighlight %}

<h2>Generate react project</h2>

create-react-app support the easiest way to create your Front-end project based on react.
{% highlight bash %}
create-react-app "app-name"
cd "app-name"
yarn start
{% endhighlight %}

If you start the app, it will compile with babel and build your default react page on localhost.
