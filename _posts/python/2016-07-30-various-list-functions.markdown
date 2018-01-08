---
layout: post
title: "Various List Functions"
date: "2016-07-30 21:20:10 +0900"
location: "Daejeon, South Korea"
commentIssueId: 9
category: Python
tags: [python]
---

There are a lot of list functions.

Let's see some cheat-sheet.


**1) Negative value**

{% highlight python %}
test_array = [1,2,3,4,5,6]
print (test_array[::-1])

>>> [6,5,4,3,2,1]

{% endhighlight %}

using negative value gives reversed way to list. When the third value is negative, it iterates reversely.

{% highlight python %}
test_array = [1,2,3,4,5,6]
print (test_array[1:-1])

>>> [2,3,4,5]

{% endhighlight %}

When negative comes to first or second place, it means count from the end of list. So, above code returns sublist which deleted first and last value.


**2) all and any**

{% highlight python %}
test_array = [10,30,50,60,70]
if all([elem >= 10 for elem in test_array]):
    print ("All elements are greater than 10")
>>> All elements are greater than 10

if any([elem % 2 == 0 for elem in test_array]):
    print "All elements are even number"
>>> All elements are even number

{% endhighlight %}

all and any methods can be used to determine if list satisfies given boolean expression. all( [i >= 10 for elem in test_array] ) is checking the lists' elements are all greater than 10.


**3) enumerate**

{% highlight python %}
test_array = [10,30,50,60,70]
for v in enumerate(test_array):
  print (v)

  >>>(0,10)
     (1,30)
     (2,50)
     (3,60)
     (4,70)

{% endhighlight %}

enumerate method makes list into tuples which are index, value pairs


**4) map**

{% highlight python %}
def multi_two(value):
    return value * 2

test_list = [10,20,30,40]
print (list(map(multi_two, test_list)))
>>> [20,40,60,80]

# Using lambda would be ideal
print (list(map(lambda x : x * 2, test_list)))
>>> [20,40,60,80]

{% endhighlight %}

map built-in function runs function to each element of list.

As above code, map applies multi_two function to each element 10, 20, 30, 40 in test_list.
So the result is [20,40,60,80]


**5) filter**

{% highlight python %}
test_list = [10,13,15,20]

print (list(filter(lambda x : x % 2 == 0, test_list)))
>>> [10, 20]

{% endhighlight %}

filter is really simple built-in function. It applies boolean expression to list to filter element out by that expression. Kid stuff right? :)
