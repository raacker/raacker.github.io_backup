---
layout: post
title: "Sorting Discussion"
date: "2016-09-25 11:33:45 +0900"
category: Algorithm
tags: [til]
---

<h3>1) Insertion Sort</h3>

It is O(n^2) time complexity. Seems bad to use.. Because Merge sort and Quick sort are O(nlogn)!

But there is a key point. <b>Insertion Sort is stable algorithm, and has lower overhead</b>. So It can be used in some cases like nearly sorted data or small size of problem. Usually, it performs as <b>recursive base case solution</b> of other algorithms, higher overhead, Merge sort or Quick sort or Shell Sort.


Reference : [sorting-algorithms](https://www.toptal.com/developers/sorting-algorithms/insertion-sort)
