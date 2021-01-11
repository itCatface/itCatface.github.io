---
temp-layout:       post
temp-title:        "四大组件之BroadcastReceiver(广播)"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 简介 

- 是 Android 四大组件之一，主要用于接收系统或者 app 发送的广播事件

- 内部通信实现机制：通过 Android 系统的 Binder 机制实现通信

- 广播分两种：有序广播和无序广播
	
	- **无序广播**：完全异步，逻辑上可以被任何广播接收者接收到

		- 优点是效率较高
		
		- 缺点是一个接收者不能将处理结果传递给下一个接收者，并无法终止广播 intent 的传播

	- **有序广播**：按照接收者的优先级顺序，在接收者中依次传播
	    
	    - 每个接收者有权终止广播，比如一个接受者终止广播，下面就接收不到广播

		- 每个接受者接收到广播后可以对结果对象进行操作，再往下传递
		
		- 在通过 `sendOrderedBroadcast` 时我们可以指定 `resultReceiver` 广播接收者，这个接收者我们可以认为是最终接收者. 通常情况下比他优先级更高的接收者如果没有终止广播，那么他的 `onReceive` 会被执行两次，第一次是正常的按照优先级顺序执行，第二次是作为最终接收者接收. 如果比他优先级高的接收者终止了广播，那么他依然能接收到广播. 在我们的项目中经常使用广播接收者接收系统通知，比如开机启动、sd挂载、低电量、外播电话、锁屏等. 如果我们做的是播放器，那么监听到用户锁屏后我们应该将我们的播放器暂停等

# 注册 BroadcastReceiver 的两种方式

- **静态注册**(清单文件中，只要 app 在系统中运行则一直可以接受到广播消息)
	
	```xml
	<receiver android:name=".MyReceiver" >
		<intent-filter>
			<action android:name="android.intent.action.BOOT_COMPLETED"  />
		</intent-filter>
	</receiver>

	// 监听到手机重启完成发出的广播后在 MyReceiver的 onReceive 方法中处理即可
	```

- **动态注册**(当注册的 Activity 或者 Service 销毁了那么就接收不到广播了)

	```java
	private NetChangeReceiver mNetChangeReceiver;
	
	private void netObserver() {
	    IntentFilter filter = new IntentFilter();
	    filter.addAction("android.net.conn.CONNECTIVITY_CHANGE"); // 监听网络状态的广播
	    // 需要 ACCESS_NETWORK_STATE 权限
	
	    // 接收广播并在 mNetChangeReceiver 中对网络状态的变化做出处理
	    mNetChangeReceiver = new NetChangeReceiver();
	    this.registerReceiver(mNetChangeReceiver, filter);
	}
	
	
	class NetChangeReceiver extends BroadcastReceiver {
	    @Override public void onReceive(Context context, Intent intent) {
	        ConnectivityManager manager = (ConnectivityManager) getSystemService(CONNECTIVITY_SERVICE);
	        NetworkInfo networkInfo = manager.getActiveNetworkInfo();
	        if (networkInfo != null && networkInfo.isAvailable()) {
	            Log.d("netnetnet", "net is TRUE");
	        } else {
	            Log.d("netnetnet", "net is FALSE");
	        }
	    }
	}
	
	// 动态注册的广播必须手动注销
	@Override protected void onDestroy() {
	    super.onDestroy();
	    this.unregisterReceiver(mNetChangeReceiver);
	}
	```

# 生命周期

1. 广播接收者的生命周期非常短暂的，在接收到广播的时候创建，`onReceive()` 方法结束之后销毁

2. 广播接收者中不要做一些耗时的工作，否则会弹出 Application No Response 错误对话框

3. 最好也不要在广播接收者中创建子线程做耗时的工作，因为广播接收者被销毁后进程就成为了空进程，很容易被系统杀掉

4. 耗时的较长的工作最好放在服务中完成

# 只让指定的 app 接收广播

1. 当前应用(A)在发送广播的时候给广播添加自定义权限，假设权限名为: `cc.catface.android.permission`，然后在 A 的 AndroidManifest.xml 中声明如下权限

	```xml
	<permission android:name="cc.catface.android.permission" android:protectionLevel="normal"></permission>
	<uses-permission android:name="cc.catface.android.permission"/> 
	```

2. 其他应用(B)如果想接收该广播，那么就必须知道 A 广播使用的权限. 然后在 B 的清单文件中如下配置

	```xml
	<uses-permission android:name="cc.catface.android.permission"/>
	```

	 或者在 AndroidManifest.xml 的 `<receiver>` 标签中进行如下配置
	
	```xml
	<receiver android:name="cc.catface.android.broadcastReceiver.MyReceiver" 
		android:permission="cc.catface.android.permission">
		<intent-filter >
			<action android:name="cc.catface.mybroadcast"></action>
		</intent-filter>
	</receiver>
	```
          
	> 每个权限通过 `protectionLevel` 来标识保护级别

1. **normal**: 低风险权限，只要申请了就可以使用(在 AndroidManifest.xml 中添加 `<uses-permission>`标签)，安装时不需要用户确认

2. **dangerous**: 高风险权限，安装时需要用户的确认才可使用

3. **signature**: 只有当申请权限的应用程序的数字签名与声明此权限的应用程序的数字签名相同时(如果是申请系统权限，则需要与系统签名相同)，才能将权限授给它

4. **signatureOrSystem**: 签名相同，或者申请权限的应用为系统应用(在 system image 中)

	>上述四类权限级别同样可用于自定义权限中. 如果开发者需要对自己的应用程序(或部分应用)进行访问控制，则可以通过在 AndroidManifest.xml 中添加 `<permission>` 标签，将其属性中的 `protectionLevel` 设置为上述四类级别中的某一种来实现

# 最终广播接收者

&emsp;&emsp;最终广播是我们自己应用发送有序广播时通过 `ContextWrapper.sendOrderedBroadcast()` 方法指定的当前应用 下的广播，该广播可能会被执行两次，第一次是作为普通广播按照优先级接收广播，第二次是作为 final receiver 必须 接收一次

# 广播的优先级对无序广播生效吗

&emsp;&emsp;生效. 广播的优先级推荐的范围是: [-1000,+1000]，但如果设置的优先级值超过这个范围也是可以的

# 动态注册的广播优先级谁高

&emsp;&emsp;谁先注册谁优先级高

# 如何判断当前 BroadcastReceiver 接收到的是有序广播还是无序广播

&emsp;&emsp;在 BroadcastReceiver 类中 `onReceive()` 方法中，可以调用 `boolean b = isOrderedBroadcast();` 该方法是 BroadcastReceiver 类中提供的方法，用于告诉我们当前的接收到的广播是否为有序广播

# Android 引入广播机制的用意

1. 从 MVC 的角度考虑(应用程序内)，android 现有的四大组件， 即现在的移动开发模型基本上是照搬的 web 那套 MVC 架构，只不过是稍作修改. android 的四大组件本质上就是为了实现移动或者说嵌入式设备上的 MVC 架构，它们之间有时候是一种相互依存的关系，有时候又是一种补充关系，引入广播机制可以方便几大组件的信息和数据交互

2. 程序间互通消息(例如在自己的应用程序内监听系统来电)

3. 效率上(参考 UDP 的广播协议在局域网的方便性)

4. 设计模式上(反转控制的一种应用，类似监听者模式)

# 网络状态改变是无序广播，安装了 app 没启动过，会接受这个广播么

&emsp;&emsp;不会. android 在 3.0 之后，对广播增加了一个标记: `Intent.FLAG_EXCLUDE_STOPPED_PACKAGES`，这个是为了加强了对“停止”状态 APP 的管理(比如 app 安装后未启动或者被用户强制停止). 广播加上这个 Flag 之后，处于“停止”状态的 APP 是无法收到广播的，系统发出的广播基本都有这个 Flag. 因此该类广播我们在使用的时候主要是采用动态注册的方式
