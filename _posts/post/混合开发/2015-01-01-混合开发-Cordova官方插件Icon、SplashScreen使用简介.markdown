---
temp-layout:       post
temp-title:        "Cordova官方插件Icon、SplashScreen使用简介"
subtemp-title:     "介绍Cordova官方提供的插件的使用方法"
date:         2015-01-01 12:00:00
author:       "catface"
header-img:   "img/color-black.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ed
tags:
    - 混合开发
---

# Cordova快速添加Icon图标和Splash闪屏页

><a target="_blank" href="https://cordova.apache.org/docs/en/latest/config_ref/images.html">**官方Configuring Icons in the CLI文档**</a>
>
>&emsp;&emsp;图标的配置仅需在项目的config.xml文件中添加文件路径即可.

><a target="_blank" href="http://cordova.apache.org/docs/en/dev/reference/cordova-plugin-splashscreen/">**官方cordova-plugin-splashscreen文档**</a>


1. **安装插件(命令行的两种方式)**
	
	- **cordova plugin add cordova-plugin-splashscreen**

	- **cordova plugin add https://github.com/apache/cordova-plugin-splashscreen.git**
	

2. **在项目第一级目录(与platform同级)的config.xml中做如下配置**

	- **A_添加各平台闪屏页文件的相对路径.**

		``` xml
		<platform name="android">
			<!-- 图标 -->
			<icon src="res/screen/android/ic_launcher.png" density="ldpi" />
	        <icon src="res/screen/android/ic_launcher.png" density="mdpi" />
	        <icon src="res/screen/android/ic_launcher.png" density="hdpi" />
	        <icon src="res/screen/android/ic_launcher.png" density="xhdpi" />
	        
			<!-- 闪屏页 -->
		    <splash src="res/screen/android/launch.png" density="land-hdpi"/>
		    <splash src="res/screen/android/launch.png" density="land-ldpi"/>
		    <splash src="res/screen/android/launch.png" density="land-mdpi"/>
		    <splash src="res/screen/android/launch.png" density="land-xhdpi"/>
		
		    <splash src="res/screen/android/launch.png" density="port-hdpi"/>
		    <splash src="res/screen/android/launch.png" density="port-ldpi"/>
		    <splash src="res/screen/android/launch.png" density="port-mdpi"/>
		    <splash src="res/screen/android/launch.png" density="port-xhdpi"/>
		</platform>
		
		<platform name="ios">
			<!-- 图标 -->
            <!-- iOS 8.0+ -->
            <!-- iPhone 6 Plus  -->
            <icon src="res/ios/icon-60@3x.png" width="180" height="180" />
            <!-- iOS 7.0+ -->
            <!-- iPhone / iPod Touch  -->
            <icon src="res/ios/icon-60.png" width="60" height="60" />
            <icon src="res/ios/icon-60@2x.png" width="120" height="120" />
            <!-- iPad -->
            <icon src="res/ios/icon-76.png" width="76" height="76" />
            <icon src="res/ios/icon-76@2x.png" width="152" height="152" />
            <!-- iOS 6.1 -->
            <!-- Spotlight Icon -->
            <icon src="res/ios/icon-40.png" width="40" height="40" />
            <icon src="res/ios/icon-40@2x.png" width="80" height="80" />
            <!-- iPhone / iPod Touch -->
            <icon src="res/ios/icon.png" width="57" height="57" />
            <icon src="res/ios/icon@2x.png" width="114" height="114" />
            <!-- iPad -->
            <icon src="res/ios/icon-72.png" width="72" height="72" />
            <icon src="res/ios/icon-72@2x.png" width="144" height="144" />
            <!-- iPhone Spotlight and Settings Icon -->
            <icon src="res/ios/icon-small.png" width="29" height="29" />
            <icon src="res/ios/icon-small@2x.png" width="58" height="58" />
            <!-- iPad Spotlight and Settings Icon -->
            <icon src="res/ios/icon-50.png" width="50" height="50" />
            <icon src="res/ios/icon-50@2x.png" width="100" height="100" />
	        
			<!-- 闪屏页 -->
		    <splash src="res/screen/ios/Default~iphone.png" width="320" height="480"/>
		    <splash src="res/screen/ios/Default@2x~iphone.png" width="640" height="960"/>
		    <splash src="res/screen/ios/Default-Portrait~ipad.png" width="768" height="1024"/>
		    <splash src="res/screen/ios/Default-Portrait@2x~ipad.png" width="1536" height="2048"/>
		    <splash src="res/screen/ios/Default-Landscape~ipad.png" width="1024" height="768"/>
		    <splash src="res/screen/ios/Default-Landscape@2x~ipad.png" width="2048" height="1536"/>
		    <splash src="res/screen/ios/Default-568h@2x~iphone.png" width="640" height="1136"/>
		    <splash src="res/screen/ios/Default-667h.png" width="750" height="1334"/>
		    <splash src="res/screen/ios/Default-736h.png" width="1242" height="2208"/>
		    <splash src="res/screen/ios/Default-Landscape-736h.png" width="2208" height="1242"/>
		</platform>
		
		<platform name="windows">
		    <splash src="res/screen/windows/splashscreen.png" width="620" height="300"/>
		    <splash src="res/screen/windows/splashscreenphone.png" width="1152" height="1920"/>
		</platform>
		
		<platform name="blackberry10">
		    <rim:splash src="res/screen/blackberry/splashscreen.png"/>
		</platform>
		```

 - **B_闪屏页显示配置**

	1. **AutoHideSplashScreen(default-true)：true为闪屏页显示结束时，自动隐藏.**
	
		`<preference name="AutoHideSplashScreen" value="true|false" />`
	
	2. **SplashScreenDelay(default-3000)：控制闪屏页的显示时长.**
	
		`<preference name="SplashScreenDelay" value="3000" />`
	
	3. **SplashMaintainAspectRatio：false为拉伸闪屏页以适应屏幕宽高.**
	
		`<preference name="SplashMaintainAspectRatio" value="true|false" />`
	
	4. **SplashShowOnlyFirstTime(default-true)：true为仅第一次进入APP才显示闪屏页.**
	
		`<preference name="SplashShowOnlyFirstTime" value="true|false" />`
	
	5. **FadeSplashScreen(default-true)：true为允许使用渐变动画来隐藏闪屏页.**
	
		`<preference name="FadeSplashScreen" value="true|false"/>`
	
	6. **FadeSplashScreenDuration(default-3000)：闪屏页结束前value时间内开始渐变动画.**
	
		`<preference name="FadeSplashScreenDuration" value="3000"/>`
	
	7. **ShowSplashScreenSpinner (default-true)：true为闪屏页显示的时候，同时也会显示进度条Bar.**
	
		`<preference name="ShowSplashScreenSpinner" value="true|false"/>`
		

3. **在JS中可做如下配置**

	- **显示闪屏页**
		```js
		navigator.splashscreen.show();
		```

	- **隐藏闪屏页**

		- **A-渐变隐藏**

			```js
			window.setTimeout(function () {
			    navigator.splashscreen.hide();
			}, splashDuration - fadeDuration);
			// 闪屏页显示时长 - 渐变时长 = 闪屏开始渐变隐藏的时刻
			```

		- **B-直接隐藏**
			
			```js
			navigator.splashscreen.hide();
			```