---
layout: post
title: "Python Reminders[1]: Built-in Functions and Basics"
date: "2018-01-07 16:00:49 -0800"
location: "San Diego, CA"
commentIssueId: 37
category: Python
tags: [python, study]
---

<h3>I've been doing Java</h3>

for 4 years. Yes I also tried C, C++, Python, JavaScript.. so on but since I restarted my python study, I had to restudy it. Almost forgot and sometimes too confused with JavaScript.

These are some of my renewals and also useful functions or examples.

<br/>
**[1] Set operations**

Set is a kind of dict which only have keys. And due to its special characteristic, we can do speical operations.

{% highlight python %}
new_set = {1, 2, 3, 4}
new_set2 = {3, 4, 5, 6}

# AND operation
new_set.intersection(new_set2) # equals to new_set & new_set2
>>> {3, 4}

# A - B operation
new_set.difference(new_set2) # equals to new_set - new_set2
>>> {1, 2}

# OR operation
new_set.union(new_set2) # equals to new_set | new_set2
>>> {1, 2, 3, 4, 5, 6}

# XOR or exclusive OR operation
new_set.symmetric_difference(new_set2) # equals to new_set ^ new_set2
>>> {1, 2, 5, 6}


new_set_sub = {1, 2}

new_set.issuperset(new_set_sub) # equals to new_set > new_set_sub
>>> True                  

new_set_sub.issubset(new_set) # equals to new_set_sub < new_set
>>> True
{% endhighlight %}

As we do on bit-wise operations and also on diagrams, we can use AND, OR, XOR operations and subset operations.

<br/>
**[2] Single tuple creation**

If you want to make a tuple, just use tuple constructor.

{% highlight python %}
new_list = [1, 2, 3, 4, 5]
new_set = {5, 4, 6, 8}
new_dict = {1: "one", 2: "two"}

tuple(new_list)
>>> (1, 2, 3, 4, 5)

tuple(new_set)
>>> (8, 4, 5, 6)

tuple(new_dict)
>>> (1, 2)

new_tuple = 1, 2, 3, 4, 5
>>> (1, 2, 3, 4, 5)
{% endhighlight %}

But if you want to make a single element tuple, you should put comma after.

{% highlight python %}
single_tuple = (1) # 1
single_tuple = (1,) # (1,)
single_tuple = 1,  # You can omit parentheses if you add comma.
{% endhighlight %}

<br/>
**[3] Put your if else to reduce code lines**

You can use if else anywhere(almost anywhere) if you think you need (This is why I think Python is like a magic)

{% highlight python %}
def foo(number):
  return "Greater than 10" if number > 10 else "Lower than or equals to 10"

foo(10)
>>> "Lower than or equals to 10"

foo(11)
>>> "Greater than 10"
{% endhighlight %}

Also during the comprehensions.

{% highlight python %}
new_list = [x for x in range(5) if x % 2 == 0]
>>> [0, 2, 4]


class User():
    def __init__(self, name, age):
        self.name = name
        self.age = age

users = [User('Haven', 24), User('Tom', 25), User('Eddy', 28), User('John', 21), User('Alex', 21)]

over_23 = {u.name : u for u in users if u.age > 23}
print(list(over_23))
>>> ['Haven', 'Tom', 'Eddy']
{% endhighlight %}

<br/>
**[4] Defaults for Dictionary**

We use dict a lot. But sometimes, it's quite annoying when you don't have specific key. 'cause it will occur Exceptions.

There are a few things you can prevent it.

1) Use get method
{% highlight python %}
age_dict = {'Haven': 24, 'Eddy' : 25, 'Kim' : 22}

#elle_age = age_dict['Elle'] # KeyError!!

haven_age = age_dict.get('Haven') # Default is None
elle_age = age_dict.get('Elle', "data not exist") # Set return value

if haven_age:
  print("Haven's age : ", haven_age)
if elle_age:
  print("Elle's age : ", elle_age)

{% endhighlight %}

{% highlight text %}
>>> Haven's age : 24
    Elle's age : data not exist
{% endhighlight %}

If you use key value directly, it may cause KeyError easily.

But if you use get method, it will return None if element not exists. You can also choose return value when it doesn't exist.

2) Use [defaultdict](https://docs.python.org/3.5/library/collections.html#collections.defaultdict)

defaultdict is really useful and best option if you need to count frequency.

{% highlight python %}
new_dict = dict()
new_dict['a'] = new_dict['a'] + 1 # KeyError!!


from collections import defaultdict
new_defaultdict = defaultdict(int)
new_defaultdict['a'] = new_defaultdict['a'] + 1 # No Error
{% endhighlight %}

defaultdict is a subclass of dict. And it overrides __missing__ method and have one additional attribute, **default_factory**.

If you set default_factory to int, it will automatically make int for missing key. If you set to list, it will automatically make list for missing key.

{% highlight python %}
new_dict = dict()
new_dict['a'].append(10) # KeyError!


from collections import defaultdict
new_defaultdict = defaultdict(list)
new_defaultdict['a'].append(10)
new_defaultdict['a'].append(20)
print(new_defaultdict)
{% endhighlight %}
{% highlight text %}
>>> [10, 20]
{% endhighlight %}
