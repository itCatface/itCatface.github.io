---
layout:       post
title:        "linux常用命令小结"
subtitle:     "总结linux中常用命令，如关机重启，文件操作，用户和组管理，进程管理等操作中经常用到的命令"
date:         2015-01-01 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ing
tags:
    - linux
---

# vi和vim编辑器

## vi和vim简介

- vi：是一款由加州大学伯克利分校，Bill Joy 研究开发的文本编辑器

- vim：是一个类似于vi的著名的功能强大、高度可定制的文本编辑器，在vi的基础上改进和增加了很多特性

## vi和vim的三种模式

1. 正常模式

	vim打开文件默认进入正常模式，在该模式下可以使用快捷键，如复制行，删除行等操作

2. 插入/编辑模式

	在正常模式下输入i/I/o/O/a/A中的任一字母会进入插入模式，在该模式下可以对文本进行编辑

3. 命令模式

	在该模式下可以执行相关指令，如保存文本，退出vim，显示/隐藏行号等指令

## 案例-使用vi和vim编写一个helloworld文件

1. `bash#vim helloworld`打开文本编辑器

2. 编写内容

		echo "hello world!"

3. 在命令行模式下输入`:wq`保存并退出vim

## vi和vim三种模式的转换方式

进入vim编辑器默认是正常模式，正常模式下输入`i/I/o/O/a/A`任一字母进入插入模式，输入`:`或者`/`进入命令模式，在插入/命令模式下按esc键进入正常模式

在命令模式下可进行以下操作：

1. `:q`：退出不保存，命令行会有提示

2. `:q!`：退出不保存，命令行不会提示

3. `:wq`：退出并保存

## 相关快捷键

### 正常模式下

- `yy`：拷贝当前行

- `5yy`：拷贝当前及向下总共5行

- `p`：粘贴

- `dd`：删除当前行

- `5dd`：删除当前及向下总共5行

- `G`：光标移至文本末行

- `gg`：光标移至文本首行

- `u`：撤销前一次编辑内容

### 命令模式下

- `set nu`：显示行号

- `set nonu`：不显示行号

- 光标定位到指定第7行

	1. 命令模式下输入指令`:set nu`显示行号
	
	2. 输入7
	
	3. 输入shift+g

# 关机、重启、登录和注销

## 关机

- `shutdown -h now`：立即关机

- `shutdown -h 7`：7分钟后关机

- `halt`：关机

## 重启

- `reboot`：立即重启

- `shutdown -r now`：立即重启

- `shutdown -r 7`：7分钟后重启

## sync
	
注意关机/重启前先执行该命令，将内存数据同步至磁盘中，防止数据丢失

## 登录

平时使用linux尽量避免使用root系统管理员账户登录，防止操作失误，可以用普通账户登录后使用`su - 用户名`命令来切换成系统管理员身份

## 注销

- `logout`：在系统运行级别为3时有效，图形运行级别下无效

# 用户和用户组管理

1. linux系统是多用户多任务的操作系统，任一需要使用资源的用户都须向系统管理员申请帐号后进入系统

2. linux的用户需要至少属于一个组

## 用户

### 添加用户

- `useradd [options] username`

		useradd zhangsan

- `useradd -d dir username`：给创建的用户指定家目录

		useradd -d /home/lisi lisi

### 给用户指定或修改密码

- `passwd username`

		passwd zhangsan
		// 执行指令后会让输入新密码

### 删除用户

- `userdel usernmae`：删除用户并保留该用户家目录

		userdel zhangsan

- `userdel -r usernmae`：删除用户并删除该用户家目录(实际操作中推荐保留被删除用户的家目录)

		userdel -r lisi

### 查询用户信息

- `id username`

		id zhangsan
		// 会显示如uid=0(root) gid=0(root) 组=0(root)
		// 分别为用户id、用户所在组id、组名
		// 当用户不存在时会返回"无此用户"

### 切换用户

- `su - username`

	从权限高的账户切换至权限低的不用输密码

		su - zhangsan

- `exit`

	当需要返回原来的账户时使用该指令

		exit

### 查看当前账户信息

- `who am i`

		who am i

## 用户组

可用于对多个具有共性的用户进行分组以便统一管理

### 增加组

- `groupadd groupname`

		groupadd female

### 删除组

- `groupdel groupname`

		groupdel female

### 新增用户时直接加上组

- `useradd -g groupname username`

		useradd -g female xiaohong

### 修改用户所在组

- `usermod -g groupname username`

		usermod -g groupname username

### /etc/passwd、/etc/shadow、/etc/group文件

- /etc/passwd：

	用户的配置文件，记录用户信息

	每行的含义：用户名|口令|用户标识号|注释性描述|主目录|登录shell

- /etc/shadow

	口令的配置文件

	每行的含义：登录名|加密口令|最后一次修改时间|最小时间间隔|最大时间间隔|警告时间|不活动时间|失效时间|标志

- /etc/group

	组的配置文件，记录组信息

	每行含义：组名|口令|组标识号|组内用户列表

# 常用指令

## 系统运行级别

- 关机

- 单用户(找回丢失的密码)

- 多用户无网络

- 多用户有网络

- 系统保留未使用

- 图形界面

- 系统重启 

	> 系统的运行级别配置文件：/etc/inittab

	> 切换到指定的系统运行级别：init[0-6]

	> 找回丢失的root密码：进入单用户模式后使用passwd来重置root密码

## 帮助指令

### `man`指令

- `man 命令/配置文件`

		man ls

### `help`指令

- `help 命令`

		help cd

## 文件目录类指令

### `pwd`

- print working directory，显示当前工作目录的绝对路径

### `ls [options] [file or directory]`

- `-a`：显示当前目录所有的文件和目录，包括隐藏的

- `-l`：以列表的方式显示信息

### `cd [params]`

- change directory，切换目录

- `cd ~`/`cd `：回到家目录

- `cd ..`：回上一级目录

- `cd /root`：通过绝对路径回/root目录

- `cd ../../root`：通过相对路径回/root目录

### `mkdir [options] directoryname`

- `mkdir animal`：在当前目录下新建animal目录

- `mkdir -p animal/dog/haski`：在当前目录下新建多级目录/animal/dog/haski目录

### `rmdir directoryname`

- `rmdir animal`：删除animal目录

	不能删除非空的目录，要删除非空目录使用指令`rm -rf animal`

### `rm [options] file/directoryname`

- `-r`：递归删除整个目录

- `-f`：强制删除不提示

		rm -rf animal

### `touch filename`

- `touch name.txt`：新建name.txt空文件

- `touch name1.txt song.mp3`：新建name1.txt、song.mp3两个空文件

### `cp [options] file/directoryname directoryname`

- `cp name.txt /opt/temp`：将name.txt单个文件复制进/opr/temp目录下

- `cp -r animal /opt.temp`：将animal整个目录递归复制进/opt/temp目录下

- `\cp ...`：强制覆盖不提示

### `mv`

- `mv oldfilename newfilename`：重命名

		mv name.txt newname.txt

- `mv file/directoryname directoryname`：移动文件/目录至新的目录下

		mv name.txt /opt/temp

### `cat [options] filename`

- 只能浏览文件内容不能修改

- `-n`：显示行号

		cat -n /etc/profile | more
		// more为分页显示

### `more filename`

- 基于vi编辑器的文本过滤器，快捷键如下：

- 支持快捷键如下

	- space：下一页
	
	- enter：下一行
	
	- q：离开more
	
	- ctrl+f：向下滚动一屏
	
	- ctrl+b：向上滚动一屏
	
	- =：输出当前行号
	
	- :f：输出文件名和当前行号

### `less filename`

- 显示文件内容时不会将整个文件加载后再显示，而是按需加载显示内容，对于显示大文件效率较高

- 支持快捷键如下

	- space：向下翻一页
	
	- [pagedown]：向下翻一页
	
	- [pageup]：向上翻一页
	
	- /字串：向下搜索字串，n向下查找，N向上查找
	
	- ?字串：向上搜索字串，n向上查找，N向下查找
	
	- q：离开less

### `>`和`>>`指令

- `>`：覆盖内容，文件不存在时会自动创建

		ls -l > temp.txt

- `>>`：追加不覆盖内容，文件不存在时会自动创建

		ls -l >> temp.txt
		
		// 将temp_a.txt文件内容追加至temp_b.txt文件末尾
		cat temp_a.txt >> temp_b.txt

		// 将字串hello追加至temp_b.txt文件末尾
		echo hello >> temp_b.txt

		// 将日历信息追加至temp_b.txt文件末尾
		cal >> temp_b.txt
		

### `echo [options] content`

	// 打印hello world
	echo hello world
	
	// 打印$PATH环境变量
	echo $PATH

### `head [options] filename`

- 显示文件开头部分

- `-n 7`：查看行数

		head name.txt
		
		// 显示文件开头7行
		hean -n 7 name.txt

### `tail [options] filename`

- 显示文件尾部部分

- `-n 7`：查看行数

- `-f`：实时追踪文档的所有更新

		tail name.txt
		
		// 显示文件尾部7行
		tail -n 7 name.txt
		
		// 实时监控文件变化
		tail -f name.txt

### `ln -s file/directoryname linkname`

- 给源文件或目录创建一个软链接

		ln -s /root lk2root

### `history`

- 查看执行过的历史命令

- `history 7`：显示最近使用过的7个命令

- `!7`：执行编号为7的历史命令

## 时间日期类指令

### `date`

- `date`：显示当前日期和时间

- `date "+%Y"`：显示当前年份

- `date "+%d"`：显示当前月份

- `date "+%Y-%m-%d %H:%M:%S"`：显示年-月-日 时：分：秒

- `date -s "日期时间"`：设置日期(如`date -s "2012-01-01 11:22:33"`)

### `cal [options]`

- `cal` 查看日历

- `cal 2012`：查看2012一整年的日历

## 搜索查找类指令

### `find scope [options]`

从指定目录向下递归的遍历其各个子目录，打印满足条件的文件或者目录

- `find scope -name filename`：按照指定的文件名查找模式查找文件

		find / -name name.txt

- `find scope -user username`：按照指定的用户名查找模式查找文件

		find / -user zhangsan

- `find scope -size (+/-/)`：按照指定的文件大小查找模式查找文件（大于多少/小于多少/等于多少）

		find / -size 20M

- `find / -name *.txt`：查询/目录下所有.txt文件

### `locate filename`

- 基于数据库搜索文件，搜索速度快，使用前须调用`updatedb`命令更新数据库

		updatedb

		locate name.txt

### `grep [options] content filename`和管道符号`|`

- 过滤查找，常和管道一起使用

		// 在name.txt文件中查找字串zhangsan所在行号且不区分大小写
		cat name.txt | grep -ni zhangsan

- `-n`：显示匹配行及行号

- `-i`：忽略大小写

## 压缩解压类指令

### `gzip`/`gunzip`

- 只能将文件压缩为.gz文件，且压缩/解压均不会保留源文件

		// 压缩
		gzip name.txt
		
		// 解压
		gunzip name.txt.gz

### `zip`/`unzip`

- `-r`：递归压缩，即压缩目录

		// 将/home目录压缩为homepackage.zip压缩文件
		zip  -r homepackage.zip /home
		
		// 将homepackage.zip文件解压至/opt/temp目录下
		unzip -d /opt/temp/ homepackage.zip

### `tar [options] xxx.tar.gz file/directorynames`

- `-c`：产生.tar压缩文件

- `-v`：显示详细信息

- `-f`：指定压缩后的文件名

- `-z`：打包同时压缩

- `-x`：解压.tar文件

- `-C`：指定解压目录，目录须存在

		// 压缩两个文件
		tar -zcvf animal.tar.gz dog.txt cat.txt
		
		// 压缩一个文件和目录
		tar -zcvf temp.tar.gz dog.txt /home
		
		// 解压到当前目录
		tar -zcvf temp.tar.gz

		// 解压到指定目录/opt下
		tar -zcvf temp.tar.gz -C /opt/

# 组管理和权限管理

## `ll`/`ls -ahl`查看文件所有者

## `chown username filename`修改文件所有者

# `crontab`任务调度指令

# 进程管理

## `ps`指令

## `kill`指令

## `killall`指令

## `pstree`指令

## `service`指令

## `chkconfig`指令

## `top`指令

## `netstat`指令

# `rpm`和`yum`指令

## `rpm`指令

## `yum`指令