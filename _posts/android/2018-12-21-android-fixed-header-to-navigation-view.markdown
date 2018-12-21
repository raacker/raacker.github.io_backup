---
layout: post
title: "Android: Fixed header to Navigation View"
date: "2018-12-21 15:35:13 +0900"
location: "Seoul, Korea"
commentIssueId: 49
category: Android
tags: [android, java, tips]
---

<h3>Add a fixed header on top of your navigation view</h3>

1. Add navigation header layout into layout directory

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:background="@android:color/black"
    android:gravity="bottom"
    android:orientation="horizontal">

    <Button
        android:id="@+id/navigation_view_fixed_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"
        android:text="button" />
</RelativeLayout>
```
navigation_header.xml

2. add 'include' header layout into NavigationView

```xml
...
  <android.support.design.widget.NavigationView
      android:id="@+id/selector_view"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:layout_gravity="start"
      android:fitsSystemWindows="true"
      app:menu="@menu/menus" >

      <include layout="@layout/navigation_header"/>
  </android.support.design.widget.NavigationView>
...
```

And add blank item into your menus

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:showIn="navigation_view">
    <item
        android:enabled="false"
        android:title=" " />

    <item
        android:id="@+id/selectable_list"
        android:title="my list">
        <menu />
    </item>
</menu>
```

* References

[Fixed Navigation header in navigation drawer while scrolling through items](https://stackoverflow.com/questions/37122753/fixed-navigation-header-in-navigation-drawer-while-scrolling-through-items)
