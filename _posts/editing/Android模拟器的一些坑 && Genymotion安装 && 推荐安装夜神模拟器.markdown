# Android模拟器的一些坑

### 1. DDMS中模拟器文件目录无法打开的解决办法

1. 如图中命令，先进入手机的Linux系统，然后使用 **chmod 755** 命令层层将文件夹的权限改为可操作，再用 **chmod 777** 命令将目标文件的权限改为可操作，最后就能将目标文件导出到电脑上了(但我这样最后还是没能够将文件导出到电脑，并在DDMS中报了 <font color=red>Failed to pull selection: open failed: Permission denied</font> 错误，在此建议使用第二种方式解决)
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwNjE2MTE0MTE3MzE2)

2. **使用命令 adb root 完事**，命令运行后，DDMS中所有文件夹均可轻松打开，所有文件也可轻松导出
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwNjE2MTE0NjM0NzI2)
			
---

# 安装Genymotion

1. **来到官网首页点击注册.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMjI4NDU2)

2. **注册帐号并登录.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMjM4MjY5)

3. **获取证书.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMjQ0NzU0)

4. **选择个人基本版>>因为免费.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMjUxNDI2)

5. **下载带有VirtualBox的完整版本>>安装到自定位置.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMjU4NDI2)

- 安装完成后打开Genymotion会出现如下错误：

	1. <font color=red>**因为安装的VM  VirtualBox是官网绑定的版本，安装后可能会出现计算机宽带无法连接问题.**
		- 解决方法：安装不带VM的安装包，首次打开Genymotion会提示系统缺少VM，此时点击提示中的链接到VM官网下载当页的新版本VM安装即可.
		- 在VM安装完成，并且装好后不会影响计算机宽带问题的情况下，即可在Genymotion面板中添加相应API版本的模拟器.
	2. 上述最后步骤中下载模拟器时，会出现如下错误：
`Unable to create virtual device,Server returned HTTP status code 0.`
此时不要惊慌，只要<font color=red>**将本机DNS设置为自动获取即可.** 如下
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDEyMzA1Njc4)

	3. 此时可见正常下载界面>>下载完成，即可运行模拟器.
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDE0NjQ5Njg5)

6. **跑起来的模拟器.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDIwNDI0ODM2)


7. **最后一个补充说明：下图中路径为模拟器下载位置.**
![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTYwMzA2MDE0NTAxNTE2)

---

# 推荐夜神模拟器，方便省事