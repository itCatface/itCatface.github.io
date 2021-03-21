---
@@@-layout:       post
title:        "Win&VMware安装linux(CentOS)虚拟机"
subtitle:     "在windows系统下，使用VMware和linux系统镜像文件安装linux虚拟机"
date:         2015-01-01 12:00:00
author:       "catface"
header-img:   "img/color-black.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ed
tags:
    - linux
---

# 准备工具

1. **VMware**

2. **linux镜像**

# 安装过程

1. **选择自定义安装(不带界面 / 典型安装是带界面的)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzAwMTYy)

2. **选择Workstation 12.x**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzE2OTcz)

3. **选择稍后安装OS**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzI5MzY0)

4. **选择linux**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzQxOTU3)

5. **选择要安装的位置**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzU0ODUw)

6. **选择1 / 1 / 1(好机子可以选择数量多一点，但一般不需要的，三个1够了)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODEwNzU4)

7. **选择1024m虚拟机内存(好机子自己按心情增加吧)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODQxODU4)

8. **选择使用网络地址转换(NAT)(使用主机分配的ip，很方便)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODU0ODE5)

9. **选择LSI Logic**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTA1ODAw)

10. **选择SCSI**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTE3NjM5)

11. **选择创建新虚拟磁盘**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTMwMzM4)

12. **磁盘大小设置为20GB，选择将虚拟磁盘存储为单个文件**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTQyNzk0)

13. **默认选项，就用自己带出的位置点击下一步即可**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTUzNDQ5)

14. **展示将要创建的虚拟机信息**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDA1MDcz)

15. **上述步骤完成后，在VMware点击编辑虚拟机设置**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDE2MTM0)

16. **虚拟机设置->硬件->勾中启动时连接，选择使用ISO镜像文件**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDI2ODEy)

17. **点击开启此虚拟机，进行linux系统安装过程**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDM3NDc3)

18. **选择Install CentOS linux7模式进行安装**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDQ5NzQz)

19. **选择安装过程中的语言(仅在安装过程有效)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTAwODc5)

20. **点击INSTALLATION DESTINATION，弹出下面界面点击蓝色Done按钮即可**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTExNTk1)

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTI0Njgy)

21. **SOFTWARE SELECTION选择最小安装模式(无界面，仅安装linux核心及基本组件，推荐使用该模式) / NETWORK & HOST NAME选择Not connected(选择在OS安装完成后进行网络设置)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTM2OTIz)

22. **在安装过程中可以添加ROOT PASSWORD(管理员密码)、USER CREATION(其他用户)**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTQ3ODEz)

23. **安装完成选择重启**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTU3ODQ3)

24. **恭喜！重启后进入linux系统**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMjA3Mzg3)

25. **网络设置**

	1. **# ip addr：得到mac地址 00:0c:29:35:dc:c9**
	
		![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE0NTA0OTg1)

	2. **# vi /etc/sysconfig/network-scripts/ifcfg-ensXXX**
		(XXX是在># ip addr<中有对应的那个数字，如我这里的33)

		![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE1MTM5NjE5)

		1. **ONBOOT 值改为 yes**
		
		2. **添加 HWADDR 值为 上述mac地址**

	3. **# service network restart：重启网络后即可使用网络进行工作**

		**主机访问linux**
	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjIwNjI4OTYw)

		**linux访问外网和主机**
	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE1OTU3NDcy)

		**Xshell访问并操作linux**
	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjIwOTM3ODQ2)

# 重启linux需重启网络配置

1. **在windows服务中开启VMware的所有服务**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjAzNjI0ODUw)

2. **在linux中重启网络服务**

	![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjAzNzEzMDUy)

	**如图，重启网络服务后，即可使用 # ip addr 查看到虚拟机ip地址**
	
# 补充说明

参考安装步骤第8.步，配置网络连接时的三种方式说明如下：

1. 桥连接：为linux分配的ip地址与母机处于同网段，可以和其他系统进行通信，但是存在问题，如果母机所在局域网有250台主机，每台主机都安装了虚拟机并都是用桥连接，那么ip会发生冲突(如母机ip为192.168.0.55，linux虚拟机ip为192.168.0.92)

2. NAT：为linux分配的ip地址与母机处于不同网段，但linux虚拟机可以访问外网且不会造成ip冲突(如母机ip为192.168.0.55，linux虚拟机ip为192.168.100.32)

3. 主机模式：linux为独立的主机，不可访问外网