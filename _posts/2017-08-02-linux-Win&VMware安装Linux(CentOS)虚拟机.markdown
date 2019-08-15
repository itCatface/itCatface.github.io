---
layout:       post
title:        "Win&VMware安装Linux(CentOS)虚拟机"
subtitle:     "在windows系统下，使用VMware和linux系统镜像文件安装linux虚拟机"
date:         2017-08-02 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      true
multilingual: false
tags:
    - linux
---

# 准备工具

1. **VMware**

2. **Linux镜像**

# 安装过程

1. **选择自定义安装(不带界面 / 典型安装是带界面的)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzAwMTYy)

2. **选择Workstation 12.x**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzE2OTcz)

3. **选择稍后安装OS**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzI5MzY0)

4. **选择Linux**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzQxOTU3)

5. **选择要安装的位置**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwNzU0ODUw)

6. **选择1 / 1 / 1(好机子可以选择数量多一点，但一般不需要的，三个1够了)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODEwNzU4)

7. **选择1024m虚拟机内存(好机子自己按心情增加吧)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODQxODU4)

8. **选择使用网络地址转换(NAT)(使用主机分配的ip，很方便)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwODU0ODE5)

9. **选择LSI Logic**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTA1ODAw)

10. **选择SCSI**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTE3NjM5)

11. **选择创建新虚拟磁盘**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTMwMzM4)

12. **磁盘大小设置为20GB，选择将虚拟磁盘存储为单个文件**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTQyNzk0)

13. **默认选项，就用自己带出的位置点击下一步即可**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjEwOTUzNDQ5)

14. **展示将要创建的虚拟机信息**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDA1MDcz)

15. **上述步骤完成后，在VMware点击编辑虚拟机设置**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDE2MTM0)

16. **虚拟机设置->硬件->勾中启动时连接，选择使用ISO镜像文件**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDI2ODEy)

17. **点击开启此虚拟机，进行Linux系统安装过程**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDM3NDc3)

18. **选择Install CentOS Linux7模式进行安装**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMDQ5NzQz)

19. **选择安装过程中的语言(仅在安装过程有效)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTAwODc5)

20. **点击INSTALLATION DESTINATION，弹出下面界面点击蓝色Done按钮即可**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTExNTk1)

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTI0Njgy)

21. **SOFTWARE SELECTION选择最小安装模式(无界面，仅安装Linux核心及基本组件，推荐使用该模式) / NETWORK & HOST NAME选择Not connected(选择在OS安装完成后进行网络设置)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTM2OTIz)

22. **在安装过程中可以添加ROOT PASSWORD(管理员密码)、USER CREATION(其他用户)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTQ3ODEz)

23. **安装完成选择重启**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMTU3ODQ3)

24. **恭喜！重启后进入Linux系统**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjExMjA3Mzg3)

25. **网络设置**

	1. **# ip addr：得到mac地址 00:0c:29:35:dc:c9**
	
		![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE0NTA0OTg1)

	2. **# vi /etc/sysconfig/network-scripts/ifcfg-ensXXX**
		(XXX是在># ip addr<中有对应的那个数字，如我这里的33)

		![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE1MTM5NjE5)

		1. **ONBOOT 值改为 yes**
		
		2. **添加 HWADDR 值为 上述mac地址**

	3. **# service network restart：重启网络后即可使用网络进行工作**

		**主机访问Linux**
	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjIwNjI4OTYw)

		**Linux访问外网和主机**
	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjE1OTU3NDcy)

		**Xshell访问并操作Linux**
	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODI5MjIwOTM3ODQ2)

# 重启Linux需重启网络配置

1. **在windows服务中开启VMware的所有服务**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjAzNjI0ODUw)

2. **在Linux中重启网络服务**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjAzNzEzMDUy)

	**如图，重启网络服务后，即可使用 # ip addr 查看到虚拟机ip地址**
