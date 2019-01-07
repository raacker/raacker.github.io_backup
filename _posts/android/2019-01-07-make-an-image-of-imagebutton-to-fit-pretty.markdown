---
layout: post
title: "Make an image of ImageButton to fit pretty"
date: "2019-01-07 22:27:00 +0900"
location: "Seoul, South Korea"
commentIssueId: 51
category: Android
tags: [android, java, tip]
---

<h3>Make your image to fill your button (without breaking size)</h3>

When you want to make buttons with image, not an ugly text, you should use [ImageButton](https://developer.android.com/reference/android/widget/ImageButton). Like this.

![](/images/make-an-image-of-imagebutton-to-fit-pretty-0.PNG)

This image is saying it's an add button! pretty straight forward and easy to catch up.

But most of the time, the size won't let you to make your life easier.

```xml
<LinearLayout
    android:id="@+id/test_button_add1"
    android:layout_width="match_parent"
    android:layout_height="40dp"
    android:layout_alignParentTop="true">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="add1" />
    <ImageButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:srcCompat="@drawable/ic_new_button"/>
</LinearLayout>
```

This is a simple 'Add' button view. But as you can see,

![](/images/make-an-image-of-imagebutton-to-fit-pretty-1.PNG)

even though the image's size is square, it will be broken because of your view size.

To solve this problem, magic keywords are

```xml    
<ImageButton
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  app:srcCompat="@drawable/ic_new_button"
  android:padding="0dp"
  android:scaleType="fitCenter"
  android:adjustViewBounds="true" />
```

scaleType="fitCenter" and adjustViewBounds="true".

[scaleType](https://developer.android.com/reference/android/widget/ImageView.ScaleType) makes Android to scale the image. If it's not provided, android will just show the actual size of your image as you can see above.

[adjustViewBounds](https://developer.android.com/reference/android/widget/ImageView#attr_android:adjustViewBounds) is to allow Android to adjust your View's outline, default is false.

So if you provide a bigger image than the view size, view's bound will be smaller than image and thus, image will overflow the view. That's why we set scaleType to 'fitCenter' (there are more attributes you can use. Check the link) for scaling image to center and adjust view bounds. Pretty simple!

And ImageButton has its default padding. So if you set it to 0, it will perfectly fit to image's size, without any boundaries.

Happy coding :)

References:

[Fit Image in ImageButton in Android](https://stackoverflow.com/questions/15116393/fit-image-in-imagebutton-in-android/15117536#15117536)
