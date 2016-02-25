---
layout: post
author: Ericson
date: 2015-12-12 13:15
title: Android View方法执行过程
category: Android
tag: [android,development,view]
---

View中有许多方法，比如：onFinishInflate,onSizeChanged,onDraw等，看下面程序：
{%highlight java%}
public class TestView extends View {
    public TestView(Context context) {
        super(context);
        Log.d("mDebug", "TestView context");
    }  
    public TestView(Context context, AttributeSet attrs, int defStyle) {
        super(context, attrs, defStyle);
        Log.d("mDebug", "TestView context,attrs,defStyle attrs="+attrs.getAttributeValue(0));
    }
    public TestView(Context context, AttributeSet attrs) {
        super(context, attrs);
        Log.d("mDebug", "TestView context, attrs="+attrs.getAttributeValue(0));
    }
    @Override
    protected void onDraw(Canvas canvas) {
        // TODO Auto-generated method stub
        super.onDraw(canvas);
        Log.d("mDebug", "onDraw");
    }
    @Override
    protected void onFinishInflate() {
        // TODO Auto-generated method stub
        super.onFinishInflate();
        Log.d("mDebug", "onFinishInflate");
    }
    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        // TODO Auto-generated method stub
        super.onSizeChanged(w, h, oldw, oldh);
        Log.d("mDebug", "onSizeChanged,w="+w+",h="+h+",oldw="+oldw+",oldh="+oldh);
    }
}
{%endhighlight%}
执行结果如下：
{%highlight java%}
12-05 22:23:03.587: D/mDebug(9715): TestView context, attrs=@2131034112  
12-05 22:23:03.597: D/mDebug(9715): onFinishInflate  
12-05 22:23:03.667: D/mDebug(9715): onSizeChanged,w=240,h=282,oldw=0,oldh=0  
12-05 22:23:03.727: D/mDebug(9715): onDraw  
12-05 22:23:03.757: D/mDebug(9715): onDraw
{%endhighlight%}
可以看到先执行构造函数，然后解析xml文件，尺寸变化函数，最后执行onDraw函数绘制UI界面。下面是View构造函数的研究：一般有三个构造函数：

>public void CustomView(Context context){}
>public void CustomView(Context context,AttributeSet attrs){}
>public void CustomView(Context context,AttributeSet attrs,int defStyle){}

下面转载自[网页](http://blog.csdn.net/z103594643/article/details/6755017)

![View Constructor](/public/img/android/android_view_constructor.jpeg)