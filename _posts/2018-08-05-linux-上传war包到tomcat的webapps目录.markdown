---
layout:       post
title:        "上传war包到tomcat的webapps目录"
subtitle:     "在windows系统下，使用VMware和linux系统镜像文件安装linux虚拟机"
date:         2018-08-05 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      false
multilingual: false
tags:
    - linux
---

# 操作步骤

1. **使用Xftp看下服务器中的旧war包，然后把它删掉**
    **<br>我们的目标是将本机的新war包替换服务器中的旧war包**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwOTA2MjE1NzU1NDU1)

2. **使用Xshell连接服务器，`ps`看下tomcat进程是否正在运行，如果在运行我们把他关闭，然后再看下进程中tomcat不在运行了**

3. **然后将tomcat的webapps目录下的文件都删除(旧war包和其对应的文件夹(也就是war包自动解压出来的文件夹))**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwOTA2MjE1ODEwNDUx)

4. **再回到Xftp，将新war包复制到服务器tomcat的webapps目录下**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwOTA2MjE1ODIxMjk2)

5. **开启服务器上的tomcat，然后使用`ps`看下tomcat有没有开启，最后主要看一下tomcat的catalina.out文件中tomcat的开启信息，以确保tomcat确实是开启的了(如最后一张图中看到catalina中的信息：tomcat在2:36成功启动了)**

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwOTA2MjE1ODMxODQ1)

	![这里写图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwOTA2MjE1ODQyMTI1)

> 总结使用到的命令

1. **# ps -ef|grep tomcat**

2. **# ../bin/shutdown.sh**

3. **# ../bin/startup.sh**

4. **# tailf ../logs/catalina.out** 