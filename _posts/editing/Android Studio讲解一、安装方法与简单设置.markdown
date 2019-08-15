**<font size=5>一、Android Studio的安装**

- **第〇步：需要本机已安装配置好JDK7及以上的版本(切记配置JAVA_HOME)**
><a href="http://www.oracle.com/" target="_blank">JDK官方网站下载</a>
- **第一步：下载Android Studio**
><a href="http://www.androiddevtools.cn/ " target="_blank">下载地址一：www.androiddevtools.cn</a>
><a href="http://tools.android-studio.org/ " target="_blank">下载地址二：tools.android-studio.org</a>

- **第二步：安装方式.本篇介绍推荐的第二种方式**
	- 1.通过.exe文件安装，安装过程中需手动选择简单配置(不推荐)
	- 2.通过解压包进行绿色安装(推荐)

- **第三步：运行AS **

	- <font color="#f00">注意，这是在检查SDK，由于要翻墙才能访问，所以需要关闭检查</font>
>AS安装目录>bin>idea.properties>>在文件最后追加：**disable.android.first.run=true**
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDg1OTA1MjYw)
	
	
	- 当看到如下界面，说明已安装成功
>选项1 ： 创建一个Android Studio项目
>选项2 ： 打开一个Android Studio项目
>选项3 ： 导入官方样例，会从网络上下载代码(建议学习)
>选项4 ： 从版本控制系统中导入代码
>选项5 ： 导入非Android Studio项目(Eclipse， IDEA项目)
<font color="#a12">PS：若Eclipse 项目使用官方建议导出(即使用 Generate Gradle build files 的方式导出)，建议使用选项2导入.</font>
>选项6 ： 设置
>选项7 ： 帮助文档
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDkxNTE1OTYx)

<br>
**<font size=5>二、Android Studio的简单设置**

- **默认的AS为灰色界面，可以选择使用炫酷的黑色界面**

>Settings>Appearance>Theme >>选择Darcula主题
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDkzOTI4MzYx)

- **智能感知，不区分大小写**

>Editor>General>Code Completion>>Case sensitive completion设置为none
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTExMTEwMTI3NDQ5)
>PS这是补充的哦，看我截图顶部，先前是win10的惨白色...

- **系统字体及大小设置**

>Settings>Appearance>>勾选Override default fonts by (not recommended)>>选择系统字体、大小.
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDk0NDMyNTk0)

- **编程字体及大小设置**

>Settings>Editor>Colors & Fonts>Font. 
>注意：默认Scheme为Defualt，不能编辑，需要点击右侧的Save As...，保存一份自己的，并在当中设置.
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDk1MDE1NTU1)

- **快捷键(建议使用默认AS的，也可以选择其他IDE的快捷键[将在下一篇同AS插件一起介绍])**

>Settings>Keymap>>进行选择
>如果与系统其他快捷键冲突的话，可以单独设置
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MTA0ODI5OTMx)

- **代码格式化时显示的样式**

>Scheme中默认的配置无法修改，同上需要创建一份自己的配置，然后进行修改
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDk1NTU3NzY4)

- **默认文件编码**

>Settings中搜索file encoding>>系统默认是GBK，当然建议改成UTF-8统一编码格式
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MDk1OTA4MTU2)

<br>
**<font size=5>三、其他设置**

- **隐藏竖线 + 显示行号 + 显示空格**

>Settings>Editor>Appearance 
>1.Show right margin：官方建议一行代码不要超过该线，但是有点碍眼
2.Show line numbers：这样就能看出缩进是tab还是空格缩进
3.Show whitespaces
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MTAwNjAyMDMz)

- **版本更新(建议关闭)**

>正式版本通道：Stable Channel
测试版本通道：Beta Channel
开发发布通道：Dev Channel
预览发布通道：Canary Channel
>![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MTAzMzI0MDcx)

- **自动导入类的引用**

>当复制了一段代码到AS中，默认AS不会自动导入代码中的类的引用. 
>我们可以勾选Add unambiguous improts on the fly.
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MTA0MDIwOTI2)

- **手动添加JDK或者SDK目录(注：本人刚开始，NDK还没搞起来)**

>File>Other Settings>Default Project Structure>>手动添加目录
![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTUxMTA5MTA0NTE4MDQ3)

<br>
<font color="#92a" size=5>	以上。如有错误和疑问，欢迎指正提出。	
catface.wyh@gmail.com	</font>