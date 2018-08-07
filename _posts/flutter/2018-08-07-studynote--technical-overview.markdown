---
layout: post
title: "StudyNote - Technical Overview"
date: "2018-08-07 23:06:50 +0900"
location: "Seoul, South Korea"
commentIssueId: 44
category: Flutter
tags: [flutter, opensource, app, study_note]
---

<h3>Technical Overview</h3>

*This study note is a summary of [technical-overview](https://flutter.io/technical-overview/) page from [flutter.io](https://flutter.io)*

- What is Flutter?
Flutter is a <b>mobile app SDK</b>. Since React is a UI library and React Native is a framework to build native app with fancy UI library, concept of flutter and React native is almost equal.

It aims to achieve High-performance, High-fidelity(for who doesn't know fidelity as I did, it means do what apps have to do and do it right, not doing something else), good apps.


- What is advantage of Flutter?
  * High productive: It's good to prototyping and test your initial idea and show MVP(Minimum Viable Project) test. (It's truly fast)
  * Beautiful and highly-customized UX: Flutter's basic design is Material UI and it supports Cupertino widgets which are of iPhone designs. Well it's true that Flutter support 'highly customized UX' but it's still Material design based. It's cool, I like it but it can be a disadvantage for some developers.


- Basic Principle of flutter

1. Everything is Widget.
Widgets are 'building block' of flutter. flutter app is made of widgets from bottom to top. For example, even Aligning your Text component is also Widget(Alignment Widget) and Font, Color, Padding.. etc. all Widgets. * Widgets don't separate views, models, controllers. They all consist as individual and equal Widgets. So if you want to make centered Text widget, wrap Text widget inside of Center widget.
  * Structured elements are Widget (Button, PopupMenu..)
  * Stylistic elements are also Widget (Font, ColorScheme..)
  * Aspect of layout also. (Padding, Margin, Center..)

Widgets make a tree structure so that when event occurs, build method of widget is called and update whole subtree by calling build method recursively.

2. Layered framework

![](/images/flutter_study_1.png)
*image from [technical-overview](https://flutter.io/technical-overview/)*

flutter engine is made of Dart, Skia, Text (C, C++, Objective-C, Java engine). And above engine, Framework is stacked with several layers which work separately and step-by-step. It means if you want to make your custom widget, make a widget on 'widgets layer' then you are good to go!


- Building widgets

Widget classes (StatefulWidget, StatelessWidget..) have 'build function'

{% highlight dart %}
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Hello Flutter!',
      body: Text('good to see ya'),
    );
  }
}
{% endhighlight %}

You should override the bulid function and put everything you want to render on the widget. The return type is also a Widget and that means it might have also a few sub widget behind.
When build function is called, flutter will determine whether to call sub widget's build function and call them recursively. After build function call, merge all result and return the root of the subtrees.

Especially, build function must be free out of side-effect. Whatever the state of widget is, build function should return same widget tree! (Under the hood, flutter has a system that compare old tree and new tree structure to find 'to be updated' widget)
