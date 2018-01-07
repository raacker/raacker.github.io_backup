---
layout: post
title: "Flask[2]: Your first Flask app"
date: "2018-01-06 13:18:26 -0800"
location: "San Diego, CA"
commentIssueId: 36
category: Flask
tags: [python, flask, study, back-end, web, framework]
---

===========================================================<br/>
**[[ Flask Study Notes ]]**<br/>
[1) Introduction](https://raacker.github.io/flask/2017/12/27/flask1-introduction/)<br/>
**[2) Your first Flask app](https://raacker.github.io/flask/2018/01/06/flask2-your-first-flask-app/)<br/>**
3) HTTP request and CRUD<br/>
4) Useful programs that help you out<br/>
5) What is RESTful API? and about Flask_RESTful<br/>
6) HTTP status code<br/>
7) Authentication<br/>
8) TBD<br/>
*These Flask post series contain basic of Flask app and building theory*<br/>
===========================================================

<h3>As I mentioned on</h3>
[previous Post](https://raacker.github.io/flask/2017/12/27/flask1-introduction/), Flask is micro web framework. It aims to simplicity and easy to maintain.

But who knows that Flask is simple and easy to use? Let's try now

**First**, we should install Flask

{% highlight shell %}
$ pip install Flask
{% endhighlight %}

Wait.. are you on virtualenv or virtual environment? if not, I recommend you to use virtualenv for flask app or any python project. Because when libraries get updated, it may cause your app error. You might want to keep these versions and maintain it yourself. And also, you might not want to mess up your desktop with python libraries. It's actually mess if you install any libraries you want. Imagine it.. web.. scipy.. numpy.. pandas.. game.. you don't need game libraries for Flask(just for now)

If you have no idea how to do virtualenv, check out [my post](https://raacker.github.io/python/2017/07/14/python-virtual-environment/).

<br/>
**Next step** is to write app.py

{% highlight python %}
from flask import Flask

app = Flask(__name__)
{% endhighlight %}

__name__ will be package name of your python. And as a convention, we usually name Flask object as 'app'

<br/>
**Now**, let's make our web site respond to basic request.

Most of site have index page or homepage, like www.google.com/ or www.linkedin.com/. But the WWW part is just only base URL, not an index page url. The last part '/' is indicating index page and it's called 'end point'.

Thus our URL is made of **Base URL** + **End Point**. (for example, play.google.com/music. https://www.youtube.com/channel/UCm6r_b2K5jn1JGkwDcwJXrQ (Ten second song. My favorite channel))

And basically, accessing to web site uses GET request. I'll talk about HTTP request on next post. Flask's default request is GET.

{% highlight python %}
@app.route('/')
def homepage():
    return "Hello, World!"
{% endhighlight %}

@ is python decorator. If you don't know, [check this out](https://www.python.org/dev/peps/pep-0318/)

Flask uses @app.route decorator to add following method to be called when specific URL is requested. [flask/app.py #1165](https://github.com/pallets/flask/blob/master/flask/app.py#L1165)

So our method homepage will be called when our Flaks app requested '/' URL.

**Final** step is to run!

{% highlight python %}
from flask import Flask

app = Flask(__name__)

@app.route('/')
def homepage():
    return "Hello, World!"

app.run(port=5000)
{% endhighlight %}

Basic port number is 5000 but if it's already occupied, try another. And you can put kwarg, debug. If you set debug flag to True, you will be able to see Werkzeug debug messages when your app crashes or faced error.

Finally, when you run app.py, it will run web server through your localhost and you can see "Hello, World!" on your localhost:5000.
