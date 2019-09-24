---
layout:       post
title:        "android动画框架lottie简介"
subtitle:     "方便以后运用lottie动画，并添加一个简单案例，详细操作手册参考官网就ok了"
date:         2014-12-30 12:00:00
author:       "catface"
header-img:   "img/android_robot_green.png"
header-mask:  0.3
catalog:      false
multilingual: false
edit status:  ed
tags:
    - android
---

# 相关网址

1. [github](https://github.com/airbnb/lottie-android)
    
2. [说明文档](http://airbnb.io/lottie/#/)
    
3. [动画案例](https://lottiefiles.com/)
    
# 入门案例

按照上面的说明文档，做个简单的案例供集成参考
    
1. gradle中添加依赖

    ``` gradle
    implementation 'com.airbnb.android:lottie:3.0.7'
    ```

2. 布局(参数顾名思义)

    ``` xml
    <?xml version="1.0" encoding="utf-8"?>
    <layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto">
    
        <data />
    
        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">
    
            <com.airbnb.lottie.LottieAnimationView
                android:id="@+id/lav_"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:lottie_autoPlay="true"
                app:lottie_fileName="427-happy-birthday.json"
                app:lottie_loop="true"
                app:lottie_repeatMode="reverse" />
    
        </androidx.constraintlayout.widget.ConstraintLayout>
    </layout>
    ```
    
3. 从动画案例网址中下载示例json放入项目assets目录

    ![](http://itCatface.github.io/img/android/lottie1.png)
    
4. activity中控制播放

    ``` java
    mBinding.lav.addAnimatorUpdateListener(animation -> {
    
    });
    mBinding.lav.addAnimatorListener(new Animator.AnimatorListener() {
        @Override public void onAnimationStart(Animator animation) {
    
        }
    
        @Override public void onAnimationEnd(Animator animation) {
    
        }
    
        @Override public void onAnimationCancel(Animator animation) {
    
        }
    
        @Override public void onAnimationRepeat(Animator animation) {
    
        }
    });
    mBinding.lav.playAnimation();
    ```
    
5. 效果

    ![](http://itCatface.github.io/img/android/lottie2.gif)

    