---
layout: post
author: Ericson
date: 2015-12-6 19:19
title: include,merge,ViewStub标签讲解
category: Android
tag: [android,development,layout]
---

在布局优化中，Android的官方提到了这三种布局\<include/\>,\<merge/\>,\<ViewStub/\>，并且介绍了这三种布局的优势，下面简单介绍下：

###布局重用\<include/\>:

{%highlight html%}
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" 
    android:layout_width=”match_parent”
    android:layout_height=”match_parent”
    android:background="@color/app_bg"
    android:gravity="center_horizontal">

    <include layout="@layout/titlebar"/>

    <TextView android:layout_width=”match_parent”
              android:layout_height="wrap_content"
              android:text="@string/hello"
              android:padding="10dp" />
</LinearLayout>
{%endhighlight%}
\<include/\>标签中可以添加属性覆盖重用的布局。

###减少视图层级\<merge/\>

\<merge/\>标签在UI的结构优化中起着非常重要的作用，它可以减少多余的层级。\<merge/\>多用于替换FrameLayout或者当一个布局包含另一个时，\<merge/\>标签消除视图层次结构中多余的视图。多余的视图会减慢你的UI表现。
{%highlight html%}
<merge xmlns:android="http://schemas.android.com/apk/res/android">

    <Button
        android:layout_width="fill_parent" 
        android:layout_height="wrap_content"
        android:text="@string/add"/>

    <Button
        android:layout_width="fill_parent" 
        android:layout_height="wrap_content"
        android:text="@string/delete"/>

</merge>
{%endhighlight%}

###需要时使用\<ViewStub/\>

\<ViewStub/\>标签最大的优点是当你需要时才会加载，使用它并不会影响UI初始化时的性能。各种不常用的布局像进度条、显示错误消息等可以使用该标签。
{%highlight html%}
<ViewStub
    android:id="@+id/stub_import"
    android:inflatedId="@+id/panel_import"
    android:layout="@layout/progress_overlay"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:layout_gravity="bottom" />
{%endhighlight%}