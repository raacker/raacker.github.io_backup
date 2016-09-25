---
layout: post
title: "Sorting Discussion"
date: "2016-09-25 11:33:45 +0900"
category: Algorithm
tags: [Self-study, til]
---

<h3>1) Insertion Sort</h3>

It is O(n^2) time complexity. Seems bad to use.. Because Merge sort and Quick sort are O(nlogn)!

But there is a key point. Insertion Sort is stable algorithm, and has lower overhead. So It can be used in some cases like nearly sorted data or small size of problem. Usually, it performs as recursive base case solution of other algorithms, higher overhead, Merge sort or Quick sort.
