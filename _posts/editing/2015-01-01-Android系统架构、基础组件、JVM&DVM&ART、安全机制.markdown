---
temp-layout:       post
temp-title:        "Android系统架构、基础组件、JVM&DVM&ART、安全机制"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# Android 系统架构 

1. Android 是一个完整的操作系统，包含中间件和一些关建的应用程序

2. Android 有四层架构，五块区域. 其中架构层自上至下依次为
	
	- **应用层 Application**

	- **应用框架层 Application Framework**
	
	- **函数库 Library** 

	- **Linux 内核**

3. 下面依次简介各层及区域

	| 层级/区域 | 简介 |
	| ---- | --- |
	| **Linux Kernel** | Android 系统是基于 Linux2.6 内核修改而来，此层大多都是操作相关的硬件驱动 |
	| **Libraries** | 由 C/C++ 编写的完成 Android 核心功能的相关类库 |
	| **Application Framework** | 由 Java 语言编写，包含供开发人员调用的各种 API |
	| **Applications** | 日常安装的所有应用程序都属于该层 |
	| **Android Runtime** | 安卓运行时环境 |
	| **Core Libraries** | 核心类库 |
	| **Dalvik Virtual Machine** | Android 底层都是 Linux 系统，使用 C、C++ 语言编写的，所以 Android 程序要在 Linux 上运行就需要虚拟机，即 DVM，其针对手机内存、CPU 性能有限等情况做了优化处理 |

	![Android系统架构图](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA1MTYzNTMxODU0?x-oss-process=image/format,png)

4. **一个小例子介绍 Android 工作流程**

	- 闹钟应用实际上就是定时播放音乐
	- 闹钟应用调用 Application Framework 层的 MediaPlayer
	- MediaPlayer 访问 Libraries 层中的 Media Framework
	- Media Framework 再使用C语言操作 Linux Kernel 层的 Audio Drivers 去播放音乐

# Android 提供了哪些东西 

1. **四大组件**

	- **Activity - 界面**
	
	- **Service - 服务**

	- **BroadcastReceiver - 广播接收者**
	
	- **ContentProvider - 内容提供者**

2. **丰富的系统控件**

	- **RelativeLayout - 相对布局**
	
	- **LinearLayout - 线性布局**

	- **EditText - 编辑文本框**
	
	- **WebView - 网页控件**

	- ……

3. **SQLite 数据库**

4. **定位：GPS(Android 自带)、LBS(基于位置服务-网络)……**

5. **多媒体：视频、音频、录音、拍照、闹铃……**

6. **传感器：光线、重力、陀螺仪、指纹、3D TOUCH……**

7. **简单基本组件介绍** 

	- **View**：所有 UI 控件、容器控件的基类，View 组件就是 Android 应用中用户实实在在看到的部分

	- **Activity**：负责显示界面并与用户交互

	- **Service**：通常位于后台运行，一般不需要与用户交互，因此 Service 组件没有图形用户界面

	- **BroadcastReceiver**：监听器，其监听的事件源是 Android 应用中的其他组件

	- **ContentProvider**：一个应用使用 ContentProvider 暴露自己的数据，另一个应用程序通过 ContentResolver 来访问数据

	- **Intent 和 IntentFilter**：Activity、Service、BroadcastReceiver 三种组件之间的通讯载体


# Eclipse-ADT 的项目结构 

![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwNTEyMDk1MjQ2Mjc5?x-oss-process=image/format,png)

# JVM 和 DVM 的区别[->ART-Android Runtime(4.4引进，5.0取代 DVM)] 

|JVM(Java Virtual Machine)|DVM(Dalvik Virtual Machine)|
|-|-|
|JVM 基于堆栈 | DVM 基于寄存器  | 
||通过 Zygote 预加载类完成虚拟机的启动|
|运行 java 字节码 | 运行 dex 字节码(减少了 class 文件中的冗余信息，DX 工具整合所有 class 文件到一个文件以提高性能，最后将资源文件和 dex 文件等打包成 apk 安装包)|
|每个 class 文件都有一个 Header(保存了 class 文件的初始信息) | apk 文件中的 dex 文件只有一个 Header，所有 class 文件的初始化信息都保存在其中，效率更高
|有218个机器指令        | 有200个机器指令(使用等长的指令，提高解析速度)|
|每个类中都有一个常量池 | 只有一个统一的常量池(打包慢，读取快)|

- Dalvik 虚拟机主要是完成对象生命周期、堆栈、线程、安全和异常的管理，以及垃圾回收等重要功能

- Dalvik 虚拟机适用于内存容量和数据处理能力较小的机器(移动终端)

- Dalvik 虚拟机一般包含寄存器地址，所以指令比 java 更长

- Dalvik 虚拟机负责进程隔离和线程管理，每一个 Android 应用在底层都会对应一个独立的 Dalvik 虚拟机实例，其代码在虚拟机的解释下得以执行

- 不同于 Java 虚拟机运行 java 字节码，Dalvik 虚拟机运行的是其专有的文件格式 Dex

- dex 文件格式可以减少整体文件尺寸，提高 I/O 操作的类查找速度

- odex 是为了在运行过程中进一步提高性能，对 dex 文件的进一步优化

- 所有的 Android 应用的线程都对应一个 Linux 线程，虚拟机因而可以更多的依赖操作系统的线程调度和管理机制

- 有一个特殊的虚拟机进程 Zygote，他是虚拟机实例的孵化器.它在系统启动的时候就会产生，它会完成虚拟机的初始化，库的加载，预制类库和初始化的操作.如果系统需要一个新的虚拟机实例，它会迅速复制自身，以最快的数据提供给系统.对于一些只读的系统库，所有虚拟机实例都和 Zygote 共享一块内存区域

# DVM 和 ART 虚拟机的区别 

- **DVM**：应用程序每次运行，字节码都需通过即时编译器转换为机器码(C 指令)，拖慢速度

- **ART(Android runtime)**：应用程序第一次安装时，字节码预先编译成机器码(Java 语言翻译成 C 指令)，使其成为真正的本地应用，其启动、执行速度明显提升. 弊端即 ART 需要存储 Java 和 C 两份指令，消耗内存

# Android 的安全机制

1. Android 是基于 Linux 内核的，因此 Linux 对文件权限的控制同样适用于 Android. 在 Android 中每个应用都有自己的 /data/data/包名文件夹，该文件夹只能该应用访问，而其他应用则无权访问

2. Android 的权限机制保护了用户的合法权益. 如果我们的代码想拨打电话、发送短信、访问通信录、定位、访问 sdcard 等所有可能侵犯用于权益的行为都是必须要在 AndroidManifest.xml 中进行声明的，这样就给了用户一个知情权

3. Android 的代码混淆保护了开发者的劳动成果

# Android 的四大组件都需要在清单文件中注册吗

> Activity 、Service 、ContentProvider 如果要使用则必须在 AndroidManifest.xml 中进行注册，而 BroadcastReceiver 则有两种注册方式，静态注册和动态注册. 其中静态注册就是指在 AndroidManifest.xml 中进行注册，而动态注册时通过代码注册

# 在Android 中进程的级别

1. **Foreground process** - 前台进程
2. **Visible process** - 可见进程
3. **Service process** - 服务进程
4. **Background process** - 后台进程
5. **Empty process** - 空进程