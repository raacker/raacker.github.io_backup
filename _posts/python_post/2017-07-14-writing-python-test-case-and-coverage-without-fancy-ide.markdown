---
layout: post
title: "Writing python test case and coverage without fancy IDE"
date: "2017-07-14 21:15:58 +0900"
commentIssueId: 18
category: Python
tags: [python, test_case, TDD]
---

Writing test case is really important. I mean.. TDD! or Test Driven Development. I've never used this development method yet. But I truly understand why it is powerful and time saving.

Yes, no exception for python. We need test case for all the projects! all the time! So... why are we hesitating?

{% highlight bash %}
$ pip install pytest
{% endhighlight %}

and write your first test case!

{% highlight python %}
import unittest

class FirstTestClass(unittest.TestCase):
    def setUp(self):
        # it will help you to prepare resources to be tested
        self.test_user = 'haven'

    def test_is_my_name_really_haven(self):
        assert self.test_user == 'haven'

if __name__ == '__main__':
    unittest.main()
{% endhighlight %}

Awesome! and to run your test case,

{% highlight bash %}
$ pytest test.py
{% endhighlight %}

then you can see

{% highlight bash %}
=========================== 1 passed in 0.07 seconds ======================
{% endhighlight %}

yay! our test case is working and it passed.

Well these are just basic test case right? When you write real test cases for your project, you are gonna write tons of test cases! and those test cases will cover the program's code. We call it coverage. How much your code are tested by test cases.

{% highlight bash %}
$ pip install pytest-cov
{% endhighlight %}

and run pytest with coverage

{% highlight bash %}
$ pytest --cov [coverage target] [test files]
{% endhighlight %}

then coverage result will be reported via shell.

{% highlight bash %}
----------- coverage: platform linux, python 3.5.2-final-0 -----------
Name                     Stmts   Miss  Cover
--------------------------------------------
my_web/app.py               10      2    80%
--------------------------------------------
TOTAL                       10      2    80%
{% endhighlight %}

I think you can find which statements are not covered yet in each files but much more more more more better way is using other platform! for instance.. html!

{% highlight bash %}
$ pytest --cov-report html --cov [coverage target] [test files]
{% endhighlight %}

then it will create htmlcov directory in where you ran the pytest. And just open the index.html! you can see the coverage results and each files' code coverage results. Isn't it great? :) I used PyCharm before but as my student account is on a deadline, I had to find other ways to do coverage. Here is it!
