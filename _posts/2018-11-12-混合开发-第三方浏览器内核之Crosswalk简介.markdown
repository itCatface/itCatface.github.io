---
layout:       post
title:        "第三方浏览器内核之Crosswalk简介"
subtitle:     "由于安卓4.4版本之前的浏览器内核性能较差，故通过intel的Crosswalk浏览器内核进行页面渲染的效率更高"
date:         2018-08-02 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      true
multilingual: false
tags:
    - 混合开发
---

> 本篇分为三部分：

1. 介绍**Crosswalk背景**

2. 介绍**Crosswalk集成步骤**

3. **为了减小体积，仅集成兼容ARM的Crosswalk(针对X86同理)**

# Crosswalk背景介绍

> Web技术的优势可想而知. 
> 
> 1. 当下app开发模式偏向Android/IOS原生壳+Web. 浏览器内核性能至关重要
> 2. 这样开发的优势很明显，当出现bug或者app要升级时不需要用户下载安装包，而是在服务器后台维护即可，极大的增强了开发的灵活性和用户粘性

- **Crosswalk的优势**

	1. 采用Chromium内核并持续更新维护，使基于Crosswalk的Web应用充分享有Chromium的功能与性能优势，以及较好的平台一致性. 同时，支持最新的H5的API(WebGL，WebAudio，WebRTC，Gamepad，WebSocket，Presentation等)。并且在低端Android设备上也能流畅运行
	
	2. 支持通过编写原生的Java代码来创建新的Web API
	
	3. 支持与Cordova的整合(已有大量的成熟的API实现供开发者使用)
	
	4. 允许Web开发者将他们的应用打包成系统的应用安装包，获得与本地应用一致的体验. 同时也支持多个应用同时使用一个Crosswalk库的共享模式，仅当应用第一次启动并且发现系统还没有相应的Crosswalk库时才提示用户下载安装. 目前是大多数情况下开发者将Crosswalk直接嵌入到应用本身。在这种嵌入模式下Web应用开发者可以完全控制Crosswalk的更新

- **与WebView的区别**

	- 系统自带的WebView组件在H5的解析能力上相比Safari for iOS、Chrome for Android都要差很多. 另外在Android平台上，由于系统碎片化比较严重，不同Android版本的WebView的H5解析能力也有较大差异，导致相应的HTML5应用一致性难以保证. 作为第三方的独立引擎Crosswalk有较好的H5性、功能支持，较好的平台一致性，以及近似原生应用的系统整合体验. 另外Crosswalk提供了共享模式来减少应用的大小

- **补充**

	- WebView自Android 4.4起已经采用了Chromium内核，但这与Crosswalk比起来目前仍存在两大缺陷：1.不被4.4之前的Android支持；2.性、功能(性能和功能)与Crosswalk有较大差别

- **Crosswalk与Cordova**

	- Cordova(PhoneGap)作为第三方的H5应用开发框架工具的代表，极大促进了H5应用的发展. 提供了方便的跨平台应用打包/发布服务、实用的API、灵活的扩展机制、以及积累下来的丰富的第三方API实现. 然而Cordova使用的web引擎是系统的WebView. 如果开发者正在使用Cordova并且渴望更好的性能和更新的功能，如WebGL，那么Crosswalk是一个很好的选择! Crosswalk支持开发者在Cordova中用Crosswalk替换原生的WebView，并将两者完美的融合. 当然，它也支持Crodova的扩展机制. 目前Crosswalk采用提供定制过的Cordova开发包来支持Cordova中Crosswalk引擎的使用
	
# Crosswalk集成步骤

- **新建项目**

	`Minimum SDK 选择 "API 19"`
	
- **配置gradle**

	``` gradle
	repositories {
	    maven {
	        url 'https://download.01.org/crosswalk/releases/crosswalk/android/maven2'
	    }
	}
	```
	``` gradle
	compile 'org.xwalk:xwalk_core_library:10.39.235.15'
	```
	> 配置结果参考下图
	>
	> ![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTEyMTUzMzEzNTYy)

- **配置权限**

	``` xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	```

- **在application标签中声明开启硬件加速**

	`android:hardwareAccelerated="true"`
	
- **布局文件**

	``` xml
	<LinearLayout 
		xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:background="#000000"
	    android:orientation="vertical">
	
	    <org.xwalk.core.XWalkView
	        android:id="@+id/xWalkWebView"
	        android:layout_width="match_parent"
	        android:layout_height="match_parent"
	        android:background="#000000"
	        android:orientation="vertical" />
	
	</LinearLayout>
	```

- **Activity中**
	
	- **需要监听系统事件(生命周期、Intent、ActivityResult)**

	- **必须显示调用 `onDestroy()`，防止浏览器引擎的内存泄漏**

		``` java
		public class MainActivity extends Activity {
		
		    @Bind(R.id.xWalkWebView) XWalkView xWalkWebView;
		
		    @Override protected void onCreate(Bundle savedInstanceState) {
		        super.onCreate(savedInstanceState);
		        setContentView(R.layout.activity_main);
		        ButterKnife.bind(this);
		
		        xWalkWebView.load("http://sina.com.cn", null);
		
		        // 开启调试
		        XWalkPreferences.setValue(XWalkPreferences.REMOTE_DEBUGGING, true);
		    }
		
		    /**通过Activity管理XWalkWebView的声明周期*/
		    @Override protected void onPause() {
		        super.onPause();
		        if (xWalkWebView != null) {
		            xWalkWebView.pauseTimers();
		            xWalkWebView.onHide();
		        }
		    }
		
		    @Override protected void onResume() {
		        super.onResume();
		        if (xWalkWebView != null) {
		            xWalkWebView.resumeTimers();
		            xWalkWebView.onShow();
		        }
		    }
		
		    @Override protected void onDestroy() {
		        super.onDestroy();
		        if (xWalkWebView != null) {
		            xWalkWebView.onDestroy();
		        }
		    }
		    
			@Override protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		        super.onActivityResult(requestCode, resultCode, data);
		        if (xwv != null) {
		            xwv.onActivityResult(requestCode, resultCode, data);
		        }
		    }
		
		    @Override protected void onNewIntent(Intent intent) {
		        super.onNewIntent(intent);
		        if (xwv != null) {
		            xwv.onNewIntent(intent);
		        }
		    }
		}
		```
		
# 兼容ARM的Crosswalk集成简要

1. **先看<a href="https://download.01.org/crosswalk/releases/crosswalk/android/maven2/org/xwalk/xwalk_core_library/" target="_blank">官方Crosswalk的各个版本</a>**
	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTI0MTc0NjM5OTg2)


2. **点进**<a href="https://download.01.org/crosswalk/releases/crosswalk/android/maven2/org/xwalk/xwalk_core_library/15.44.384.13/" target="_blank">**当前最新版本**</a>

	>**可以看到完整包39m，arm包20m. 我们在此选择第一个arm包**
	>
	>![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTI2MTExMDUxNTYx)

3. **将下载好的arm.aar包放入工程的libs目录下**

4. **在builde.gradle中添加配置**

	``` gradle
	flatDir {
		dirs 'libs'
	}
	```
	``` gradle
	compile 'org.xwalk:xwalk_core_library:15.44.384.13-arm@aar'
	```
	> 配置结果参考下图
	> ![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTI2MTExOTMwNzg1)

5. **重新编译打包，可见结果如下(集成完整Crosswalk与仅集成ARM包)**

	 ![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTI2MTEyMzE0OTk0)

# 补充说明

- **1.众所周知，Crosswalk的体积是个恼人的问题. 可以针对针对ARM、X86分别引入对应的库文件，减少不必要的空间浪费**

- **2.可以使用动态库加载**

