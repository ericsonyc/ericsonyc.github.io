---
layout: post
author: Ericson
date: 2015-12-6 11:22
title: Activity生命周期总结
category: Android
tag: [android,activity,development]
---

Activity是Android中的四大重要组件之一，必须了解的点，主要是它的生命周期：
![Activity LifeCycle](/public/img/android/activitylifecycle.gif)
主要有一下几个过程：

1. 启动Activity：系统会先调用onCreate方法，然后调用onStart方法，最后调用onResume，Activity进入运行状态。
2. 当前Activity被其他Activity覆盖其上或被锁屏：系统会调用onPause方法，暂停当前Activity的执行，并继续执行onStop方法。
3. 当前Activity由被覆盖状态回到前台或解锁屏：系统会调用onRestart方法，再次进入运行状态。
4. 当前Activity转到新的Activity界面或按Home键回到主屏，自身退居后台：系统会先调用onPause方法，然后调用onStop方法，进入停滞状态。
5. 用户后退回到此Activity：系统会先调用onRestart方法，然后调用onStart方法，最后调用onResume方法，再次进入运行状态。
6. 当前Activity处于被覆盖状态或者后台不可见状态，即第2步和第4步，系统内存不足，杀死当前Activity，而后用户退回当前Activity：再次调用onCreate方法、onStart方法、onResume方法，进入运行状态。
7. 用户退出当前Activity：系统先调用onPause方法，然后调用onStop方法，最后调用onDestory方法，结束当前Activity。

但是知道这些还不够，我们必须亲自试验一下才能深刻体会，融会贯通。下面是示例：

###启动时：
![Activity Start](/public/img/android/activitystart.jpg)
###锁屏时：
![Activity Lock](/public/img/android/activitylock.jpg)
###解锁时：
![Activity Unlock](/public/img/android/activityunlock.jpg)
其中还有一个onSaveInstanceState方法，该方法调用是在onPause方法之后，主要有三种情况调用：

1. 在Activity被覆盖或退居后台之后，系统资源不足将其杀死，此方法会被调用；
2. 在用户改变屏幕方向时，此方法会被调用；
3. 在当前Activity跳转到其他Activity或者按Home键回到主屏，自身退居后台时，此方法会被调用。

当屏幕旋转时，android会先销毁当前Activity，再建一个新的，log如下：
![Activity Rotate](/public/img/android/activityrotate.jpg)


