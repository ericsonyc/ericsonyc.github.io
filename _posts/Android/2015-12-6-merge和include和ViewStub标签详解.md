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
\<include/\>标签中可以添加属性覆盖重用的布局。一般可以覆盖以下几个属性：android:id,android:layout_*。

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
使用\<merge/\>标签时，必须让\<merge/\>标签本身表示的Layout和parent表示的Layout是一样的，比如\<merge/\>标签本身代表的是FrameLayout，而parent使用的是LinearLayout，这时候就不可以把\<merge/\>标签应用到该LinearLayout中。具体请参考[Android Developers' blog](http://android-developers.blogspot.com/2009/03/android-layout-tricks-3-optimize-by.html)

该标签还可以和\<include/\>标签一起使用，我们使用下面的示例来说明：
{%highlight html%}
<merge
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:okCancelBar="http://schemas.android.com/apk/res/com.example.android.merge">

    <ImageView  
        android:layout_width="fill_parent" 
        android:layout_height="fill_parent" 
    
        android:scaleType="center"
        android:src="@drawable/golden_gate" />
    
    <com.example.android.merge.OkCancelBar
        android:layout_width="fill_parent" 
        android:layout_height="wrap_content" 
        android:layout_gravity="bottom"

        android:paddingTop="8dip"
        android:gravity="center_horizontal"
        
        android:background="#AA000000"
        
        okCancelBar:okLabel="Save"
        okCancelBar:cancelLabel="Don't save" />

</merge>
{%endhighlight%}

{%highlight html%}
<merge xmlns:android="http://schemas.android.com/apk/res/android">
    <include
        layout="@layout/okcancelbar_button"
        android:id="@+id/okcancelbar_ok" />
        
    <include
        layout="@layout/okcancelbar_button"
        android:id="@+id/okcancelbar_cancel" />
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