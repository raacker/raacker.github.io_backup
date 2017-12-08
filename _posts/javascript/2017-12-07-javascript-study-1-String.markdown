---
layout: post
title: "JavaScript study [1] : String"
date: "2017-12-07 16:55:51 -0800"
location: "San Diego, CA"
commentIssueId: 28
category: JavaScript
tags: [javascript, study]
---

Hmm.. maybe because I've been doing Java for lots of years, JavaScript is a bit familiar. But when I get through details, as we all already know, they are still completely different languages.

These study notes are just a simple summary of new information I got from [MDN web doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript) while I was struggling with [codewars' kata](https://www.codewars.com).

<h2>String</h2>

1)  [includes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)

str.includes(searchString[, position])

* Check whether searchString is included within str or not.
* if position is not zero, it searches from position index.
* **case sensitive**

As you can find in doc page, its name was 'contains' but it caused error a few years ago and now it is totally replaced with 'includes'.

{% highlight javascript %}
let s = "Hello world!";
console.log(s.includes("Hello")); // True
console.log(s.includes("hello")); // false
{% endhighlight %}

2)  [indexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

str.indexOf(searchValue[, fromIndex])

* **case sensitive**
* if searchValue does not exist, **return -1**
* if searchValue is ""(emptyString), just return fromIndex

indexOf also can be used to check whether str contains substring or not.

{% highlight javascript %}
let s = "Hello world!";
console.log(s.indexOf("Hello")); // 0
console.log(s.indexOf("Hello", 1)); // -1
{% endhighlight %}

3)  [padStart](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart), [padEnd](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd)

str.padStart(targetLength[, padString])
str.padEnd(targetLength[, padString])

* give padding to str with white space or padString in length. But it will reserve original string's place first. So if targetLength is lower than string's length, there will be no padding. And padString will be used only left over places.

{% highlight javascript %}
let s = "Good";
console.log(s.padStart(6)); // '  Good'
console.log(s.padEnd(6)); // 'Good  '
console.log(s.padStart(1)); // 'Good'
console.log(s.padStart(6, "Great")); // 'GrGood'
console.log(s.padEnd(10, "abc")); // 'Goodabcabc'
{% endhighlight %}

4)  [repeat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat)

str.repeat(count);

* Easy method. Duplicate str for count times.
* count must be zero or positive.

{% highlight javascript %}
let s = "Good";
console.log(s.repeat(0)); // ''
console.log(s.repeat(1)); // 'Good'
console.log(s.repeat(3)); // 'GoodGoodGood'
console.log(s.repeat(-1)); // RangeError
{% endhighlight %}

5)  [split](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)

str.split([separator[, limit]])

* **if separator is ""(emptyString), return single characters array**
* if separator is null, same string will be returned
* you can limit split items by limit.

{% highlight javascript %}
let s = "Hello people! California weather is great as always";
console.log(s.split(" "));
// ["Hello", "people!", "California", "weather", "is", "great", "as", "always"]
s = "Good to see you";
console.log(s.split(""));
// ["G", "o", "o", "d", " ", "t", "o", " ", "s", "e", "e", " ", "y", "o", "u"]
console.log(s.split(" ", 2));  
// ["Good", "to"]
{% endhighlight %}

6)  [trim](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim)

str.trim()

* Just remove white spaces of left and right edge! You can use trimLeft() or trimRight() for separated way

{% highlight javascript %}
let s = "    Good      ";
console.log(s.trim()); // 'Good'
{% endhighlight %}
