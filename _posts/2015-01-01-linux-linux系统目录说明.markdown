---
layout:       post
title:        "linux系统目录说明"
subtitle:     "简单介绍linux系统的各个系统目录"
date:         2015-01-01 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ed
tags:
    - linux
---

# linux目录结构简介

> linux中一切皆文件
> <br>linux的目录中有且仅有一个根目录/(windows中可以有多个根目录c:、d:等)

![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjA0MTU5ODc0)

1. **bin(abbr of Binary) -> 谨慎操作**
	**存放最常用的命令(系统用户使用的程序)**

2. **boot**
**存放启动linux时使用的一些核心文件(包括一些连接文件以及镜像文件)**

3. **dev(abbr of Device)**
**存放的是linux的外部设备(在linux中访问设备的方式和访问文件的方式是相同的)**

4. **etc -> 谨慎操作**
**存放所有的系统管理所需要的配置文件和子目录**

5. **home**
**用户的主目录，在linux中，每个用户都有一个自己的目录(一般该目录名是以用户的账号命名的)**

6. **lib**
**存放着系统最基本的动态连接共享库(类似于Windows里的.dll)且几乎所有的应用程序都需要用到这些共享库**

7. **media**
**linux系统会将自动识别的设备(如U盘、光驱等)挂载到该目录下**

8. **mnt**
**让用户临时挂载别的文件系统(如将光驱挂载在该目录下)**

9. **opt**
**这是给安装额外软件的目录(如ORACLE数据库可安装在该目录下)**

10. **proc**
**这是虚拟目录，它是系统内存的映射(不在硬盘上)，我们可以通过直接访问这个目录来获取系统信息**

	**可以通过命令来屏蔽主机的ping命令，使别人无法ping你的机器**
	**<br>`echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all`**

11. **root**
**系统管理员(超级权限者)的用户主目录**

12. **run**
**开机时底层程序需向原来的/var/run写入文件，但整个文件系统尚未挂载好，系统启动初期只有一个根分区挂载上来，所以将/run移至根目录单独挂载，且在下次系统运行时重新生成**

13. **sbin(abbr of Super User Binary) -> 谨慎操作**
**存放系统管理员使用的系统管理程序(比较高级的管理程序和系统守护程序)**

14. **srv**
**存放一些服务启动之后需要提取的数据**

15. **sys**

	- **这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统sysfs** 
	
	- **sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统**
	
	- **该文件系统是内核设备树的一个直观反映**
	
	- **当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建**

16. **tmp**
**存放一些临时文件**

17. **usr**
**存放很多应用程序和文件(类似与windows下的program files目录)**

18. **var**
**存放经常被修改日志(/var/log)、文件和目录**

19. **注意**
**bin、usr/bin 是给系统用户使用的指令(除root外的通用户)**
**<br>sbin、 usr/sbin 则是给root使用的指令**

# 各根目录简述

## 文件颜色含义

- **白色：表示普通文件**

- **蓝色：表示目录**

- **绿色：表示可执行文件**

- **红色：表示压缩文件**

- **浅蓝色：链接文件**

- **红色闪烁：表示链接的文件有问题**

- **黄色：表示设备文件**

- **灰色：表示其它文件**

    1. **bin**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjE0NTEyODcy)

    2. **boot**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjE0NzAzNDIz)
    
    3. **dev**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjE1MzQzNDA1)
    
    4. **etc**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjE1OTA1NTUw)
    
    5. **home**
    
        **新建linux虚拟机的该目录下是空的，可以创建自己的文件或目录**
    
    6. **lib**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIwMzIzMzA5)
    
    7. **media**
    
        **新建linux虚拟机的该目录下是空的**
    
    8. **mnt**
    
        **新建linux虚拟机的该目录下是空的**
    
    9. **opt**
    
        **新建linux虚拟机的该目录下是空的**
    
    10. **proc**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIwNTQzODc1)
    
    11. **root**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIwNzMwOTMw)
    
    12. **run**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIwODE5NTQ5)
    
    13. **sbin**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIxNDE3MjQ2)
    
    14. **srv**
    
        **新建linux虚拟机的该目录下是空的**
    
    15. **sys**
        
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIxNzA3MDQx)
    
    16. **tmp**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIxNzQ4ODc3)
        
    17. **usr**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIxODA5MDc2)
        
    18. **var**
    
        ![](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwODMxMjIxODI2MTgz)

	