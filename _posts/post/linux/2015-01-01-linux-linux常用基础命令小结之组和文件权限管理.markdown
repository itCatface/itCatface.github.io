---
layout:       post
title:        "linux常用基础命令小结之组和文件权限管理"
subtitle:     "简介linux文件的读写修改权限，包括更换文件所属用户和所属组等"
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

# 文件

- 所有者

- 所在组

- 其他组

- 改变用户所在组

# 文件/目录所有者

- 一般为文件的创建者，谁创建了该文件，就自然的称为该文件的所有者

- 查看文件所有者：ls -ahl

- 修改文件所有者：chown username filename

 - 文件所在组不一定是文件所有者

# 组的创建

- groupadd groupname

# 文件/目录所在组

- 修改文件所在组：chgrp groupname filename

# 其他组

- 除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组

# 改变用户所在组

- 在添加用户时，可以指定将该用户添加到哪个组中，同样的用root的管理权限可以改变某个用户所在的组

- 改变用户所在组：usermod -g groupname username

- 改变用户登录的初始目录：usermod -d directoryname username

# 权限的基本介绍

- 文件类型：

	- -：普通类型
	
	- d：目录
	
	- l：软连接
	
	- c：字符设备【键盘、鼠标等】
	
	- b：块文件【硬盘】

- ls -l 显示内容说明：

	- rw-：表示文件所有者权限（rw，读写）
	
	- r--：表示文件所在组的用户的权限（r，只有读的权限）
	
	- r--：表示文件其他组的用户的权限（r，只有读的权限）
	
	- 1：如果是文件，表示硬连接的数；如果是目录则表示该目录的子目录个数
	
	- tom：文件所有者
	
	- bandit：文件所在组
	
	- 0：文件的大小，0个字节；如果是目录，则统一为4096
	
	- July 1 13：40：文件最后的修改时间
	
	- ok.txt：文件名

# rwx权限详解

- rwx作用到文件：

	- r：read，可读读取查看
	
	- w：write，可以修改但不代表可以删除该文件删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除该文件
	
	- x：execute，可执行可以被执行

- rwx作用到目录：

	- r：可以读取，ls查看目录内容
	
	- w：可以修改，目录内创建+删除+重命名目录
	
	- x：可执行，可以进入该目录

# 修改权限chmod

- 修改文件或者目录的权限

- u：所有者；g：所在组；o：其他人；a：所有人（u、g、o的总和）

- chmod u=rwx，g=rx，o=x 文件目录名：分别权限

- chmod o+w 文件目录名：给其他人都增加写的权限

- chmod a-x 文件目录名：给所有的用户都减掉执行权限

# 通过数字变更权限

- 规则：r=4 w=2 x=1 rwx=4+2+1=7

- chmod u=rwx，g=rx，o=x 文件目录名 等价于 chmod 751 文件目录名

# 修改文件所有者chown

- chown newowner file：改变文件的所有者

- chown newowner：newgroup file：改变用户的所有者和所在组

- -R：如果是目录，则使其下所有子文件或目录递归生效

# 修改文件所在组chgrp

- chgrp newgroup file：改变文件的所有组

- -R：如果是目录，则使其下所有子文件或目录递归生效