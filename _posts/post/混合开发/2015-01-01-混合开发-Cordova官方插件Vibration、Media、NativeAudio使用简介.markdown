---
layout:       post
title:        "Cordova官方插件Vibration、Media、NativeAudio使用简介"
subtitle:     "介绍Cordova官方提供的插件的使用方法"
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

# <a target="_blank" href="http://cordova.apache.org/docs/en/latest/reference/cordova-plugin-vibration/index.html">**cordova-plugin-vibration**</a>

1. **安装(通过命令行)**
	
	**cordova plugin add cordova-plugin-vibration**

2. **使用**

	**navigator.vibrate(time)** or **navigator.vibrate([time])**

	[例：navigator.vibrate(3000);]

3. **注意**

	- **IOS无法控制震动时长(系统固定) && Windows和Blackberry时长范围(5000ms 至 8000ms).**

	- **Android和Windows可设定震动模式**

		**navigator.vibrate(pattern);**
		
		[例：navigator.vibrate([1000, 1000, 3000, 1000, 5000]);]

4. **取消**

	**navigator.vibrate(0);** or **navigator.vibrate([]);** or **navigator.vibrate([0]);**

# <a target="_blank" href="http://cordova.apache.org/docs/en/latest/reference/cordova-plugin-media/index.html">**cordova-plugin-media(可后台播放)**</a>

1. **安装**

	**cordova plugin add cordova-plugin-media**

2. **使用**

	1. **初始化Media**

		```js
		var media;
		media = new Media("/android_asset/www/media/example.mp3", 
			function() {
				alert("Media Init Success");
			}, 
			function(err) {
				alert("Error: " + err);
			}
		);
		```

	2. play()：**media.play();**

	3. pause()：**media.pause();**

	4. stop()：**media.stop();**

	5. release()[当Media资源不需要用时应该释放]：**media.release();**

	6. setVolume()[范围(0.0 - 1.0)]：**media.setVolume(volume);**

	7. seekTo()[手动设置播放位置]：**media.seekTo(milliseconds);**

	8. **getDuration()：返回Media时长(s)，异常返回-1**

		```js
		var length= media.getDuration();
		if (duration > -1) {
			alert("length== " + length);
		};
		```

	9. **getCurrentPosition()**

		```js
		media.getCurrentPosition(
			function(position) {
				if (position > -1) {
					alert("position");
				}
			}, 
			function(err) {
				alert(err);
			}
		);
		```

	10. **startRecord() & stopRecord()**

		```js
		// 创建文件对象
		var recordMedia = new Media(
			"storage/emulated/0/record.mp3", 
			function() {
				alert("Success");
			}, 
			function(e) {
				alert("Error" + e);
			}
		);
		
		// 开始录音
		recordMedia.startRecord();
		```

		```
		// 停止录音
		recordMedia.stopRecord();
		```

# <a target="_blank" href="https://www.npmjs.com/package/cordova-plugin-nativeaudio#roadmap">**cordova-plugin-nativeaudio(针对HTML5游戏和音频应用所需的最小延迟，复调和并发)**</a>

1. **安装**

	**cordova plugin add cordova-plugin-nativeaudio**
	

2. **使用**

	1. **preloadSimple()**：优化短视频/单镜头(最多五秒). 不能停止/循环.
	
	2. **preloadComplex()**：可以停止/循环和用于多个声音. 可以在使用延迟参数的时间和使用.

	3. **play: function (id, successCallback, errorCallback, completeCallback)`**

	4. **loop: function (id, successCallback, errorCallback)**

	5. **stop: function (id, successCallback, errorCallback)**

	6. **unload: function (id, successCallback, errorCallback)**
	
	7. **setVolumeForComplexAsset: function (id, volume, successCallback, errorCallback)**

3. 使用案例

	```js
	if( window.plugins && window.plugins.NativeAudio ) {
		
		// Preload audio resources 
		window.plugins.NativeAudio.preloadComplex( 'music', 'audio/music.mp3', 1, 1, 0, function(msg){
		}, function(msg){
			console.log( 'error: ' + msg );
		});
		
		window.plugins.NativeAudio.preloadSimple( 'click', 'audio/click.mp3', function(msg){
		}, function(msg){
			console.log( 'error: ' + msg );
		});
	 
		// Play 
		window.plugins.NativeAudio.play( 'click' );
		window.plugins.NativeAudio.loop( 'music' );
	 
		// Stop multichannel clip after 60 seconds 
		window.setTimeout( function(){
	 
			window.plugins.NativeAudio.stop( 'music' );
				
			window.plugins.NativeAudio.unload( 'music' );
			window.plugins.NativeAudio.unload( 'click' );
	 
		}, 1000 * 60 );
	}
	```