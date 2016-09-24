---
layout: post
title: "During the Algorithmic Thinking"
date: "2016-09-24 16:18:46 +0900"
category: TIL, Python
tags: [Self-study, python, til]
---

1. Return None automatically.

if self.outstack:

It will return boolean value that outstack is exist or not.


2. Double matching

('{' , '}')
if (open, close) in matches:

Python is available in double matching in if or while statement.

Also swap function can be..
a, b = b, a


3. Instance sorting

cluster_list.sort(key = lambda cluster : cluster.vert_center())

It is possible to make a sorting factor via lambda. Even classes.
Above code is showing that cluster_list would be sorted in ascending with vert_center value.


4. Generate empty set list

setList = [set() for i in range(len(cluster_list))]

It will generate list of sets


5. Make dictionary for key list and value list

key = [1, 2, 3]
value  = [11, 12, 13]
list_a = dict(zip(key, value))

zip method will concatenate key and value list for each corresponding element.


6. String list and random.shuffle()

In python, string is also a list.

l = "hello" is ['h', 'e', 'l', 'l', 'o']

and random.shuffle(l)

will generate a list that contains random element of argument list.


7. Set generator

A list can be changed to set.

l = 'hello'
s = set(l)

will generate

set[('h', 'e', 'l', 'o')]
