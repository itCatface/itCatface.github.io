---
temp-layout:       post
temp-title:        "requestWindowFeature()使用简介"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 一、requestWindowFeature()功能及参数简介

- **功能：设置当前窗体的显示特征(如全屏、无标题等)**

- **参数：Window类中定义的常量，每个常量对应一种窗体显示类型**

# 二、介绍源码中定义的相关参数

1. **首先引用源码中所有以`FEATURE_`开始的常量参数，后面展示实际应用效果**
	```java
	public abstract class Window {
	    // 默认配置
	    public static final int FEATURE_OPTIONS_PANEL = 0;
	    // 无标题
	    public static final int FEATURE_NO_TITLE = 1;
	    // 进度指示器功能
	    public static final int FEATURE_PROGRESS = 2;
	    // 标题栏左侧图标
	    public static final int FEATURE_LEFT_ICON = 3;
	    // 标题栏右侧图标
	    public static final int FEATURE_RIGHT_ICON = 4;
	    // 不确定的进度 
	    public static final int FEATURE_INDETERMINATE_PROGRESS = 5;
	    // 默认配置. 启用context menu
	    public static final int FEATURE_CONTEXT_MENU = 6;
	    // 自定义标题. Cannot combine with other title features
	    public static final int FEATURE_CUSTOM_TITLE = 7;
	    // 用ActionBar代替TitleBar
	    public static final int FEATURE_ACTION_BAR = 8;
	    // 要求ActionBar覆盖窗口内容
	    public static final int FEATURE_ACTION_BAR_OVERLAY = 9;
	    // 当一个动作栏不存在,指定操作的行为模式
	    public static final int FEATURE_ACTION_MODE_OVERLAY = 10;
	    public static final int FEATURE_SWIPE_TO_DISMISS = 11;
	    public static final int FEATURE_CONTENT_TRANSITIONS = 12;
	    public static final int FEATURE_ACTIVITY_TRANSITIONS = 13;
	    .
	    .
	    .
	}
	```

2. **实际应用效果的展示**

	1. **默认显示：带标题栏**
	
		```java
		@Override protected void onCreate(Bundle savedInstanceState) {
			requestWindowFeature(Window.FEATURE_OPTIONS_PANEL);
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
		}
		```
		```java
		@Override protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
		}
		```
		>上面贴出的两段代码效果相同，如图
		>![这里写图片描述](https://img-blog.csdnimg.cn/img_convert/915b41bb813b9ecbbb377fb5628fa14c.png)
	
	2. **无标题**
		
		```java
		@Override protected void onCreate(Bundle savedInstanceState) {
			requestWindowFeature(Window.FEATURE_NO_TITLE);
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
		}
		```
		>![这里写图片描述](https://img-blog.csdnimg.cn/img_convert/d9375d75396e1fdca24d1ef51bdf53f0.png)
	
	3. **全屏显示**
		```java
		@Override protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);
			setContentView(R.layout.activity_main);
		}
		```
		>![这里写图片描述](https://img-blog.csdnimg.cn/img_convert/55f2519998f74e1f4cd09326c8a45e64.png)