---
layout: post
author: Ericson
date: 2015-12-9 15:30
title: Android Animation Property
category: Android
tag: [android,development,animation]
---

![Android Animation Property](/public/img/android/android_animation_property.jpeg)

详细内容可以参考[官方文档](http://developer.android.com/guide/topics/graphics/prop-animation.html)

组合动画示例：

{%highlight java%}
ObjectAnimator anim = ObjectAnimator.ofFloat(v, "hello", 1.0f, 0.0f).setDuration(1000);
anim.start();
anim.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator animation) {
        float cVal=(Float)animation.getAnimatedValue();
        v.setAlpha(cVal);
        v.setScaleX(cVal);
        v.setScaleY(cVal);
        v.setRotationX(cVal*360);
    }
});
{%endhighlight%}
