---
layout: post
title: "Functional Programming with Python"
date: "2016-07-30 21:35:47 +0900"
category: Python
tags: [python study]
---

Python is also really great functional programming language.

<h2> Higher-order Function </h2>

In functional language, function is <b>Higher-order Function</b>. function can be passed as an argument and also returned in function. Function can be a object itself!

{% highlight python %}
def run_twice(func, arg):
    return func(func(arg))

def multi_two(x):
	return x * 2

print run_twice(multi_two(5))
>>>20

{% endhighlight %}

multi_two is function. Same as run_twice. But run_twice takes function as an argument and returns function.

Python's function is <b>Higher-order Function</b>



<h2> Referential Transparency </h2>

It is also called <b>pure function</b>. Functions can take arguments. But sometimes, given arguments can be changed while running functions.

Pure function means it doesn't change or effect to anything, even arguments. So as we already know well, y = f(x), given x makes exactly same y always.

And also x will never effected by function.

{% highlight python %}
def add_element_to_list(arg_list):
    arg_list.append("Appended by function")

test_list = ["Hello"]
print add_element_to_list(test_list)
print add_element_to_list(test_list)

>>>["Hello", "Appended by function"]
>>>["Hello", "Appended by function", "Appended by function"]

{% endhighlight %}

As we can see above, add_element_to_list is not a pure function 'cause it changes the given argument 'test_list'


It may seem pure function is really great feature. Yes. It has really great advantages.

* Easier to test and run. It will always give same result to same argument
* Easier to run in parallel.

But also have disadvantages.

* There are too much cases that need to affect to others. Including, IO tasks.. etc.
