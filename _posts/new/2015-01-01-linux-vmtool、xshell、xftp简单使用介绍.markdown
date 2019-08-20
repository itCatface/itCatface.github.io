---
layout:       post
title:        "vmtool、xshell、xftp简单使用介绍"
subtitle:     "vmtool可为母机和linux虚拟机设置共享文件夹、xshell和xftp为常用的维护linux虚拟机的应用软件"
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

# vmtool

## vmtool安装

1. 进入linux虚拟机

2. 点击VMware菜单的install vmware tools

3. 解压linux虚拟机上出现的vm安装包

4. 进入vm解压后的目录(目录地址为/root/桌面/vmware-tools-distrib/)

5. 安装 ./vmware-install.pl，过程全部选默认

6. 安装完成后reboot linux虚拟机即可使用该共享文件夹

## vmtool设置母机与linux虚拟机的共享文件夹

1. 点击VMware菜单的vm-->setting设置为always enabled

2. 共享win系统下的 d:/share 目录

3. 该共享文件夹在linux下的目录为 /mnt/hgfs/ 下

# xshell

# xftp

