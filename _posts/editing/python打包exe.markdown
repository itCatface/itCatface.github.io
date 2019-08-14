### 1、安装[`pip install pyinstaller`]

<center>
![这里写图片描述](https://img-blog.csdn.net/20180326114734325?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2l0Q2F0ZmFjZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 2、打包成exe文件[`pyinstaller xxx.py`]

<center>
![这里写图片描述](https://img-blog.csdn.net/2018032611491079?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2l0Q2F0ZmFjZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 3、测试打包好的exe文件

<center>
![这里写图片描述](https://img-blog.csdn.net/20180326114956566?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2l0Q2F0ZmFjZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 4、打包方式

1. 例: **`pyinstaller -F xxx.py` // 生成单个exe文件**

2. 常用参数


	1.  **-F：制作独立的可执行程序**
	
	2. -D：制作出的档案存放在同一个文件夹下（默认值）
	
	3. -K：包含TCL/TK（对于使用了TK的，最好加上这个选项，否则在未安装TK的电脑上无法运行）
	
	4. -w：制作窗口程序
	
	5. -c：制作命令行程序（默认）
	
	6. -X：制作使用UPX压缩过的可执行程序（推荐使用这个选项，需要下载UPX包，解压后upx.exe放在Python(非PyInstaller)安装目录下，下载upx308w.zip）
	
	7. -o：DIR指定输出SPEC文件路径（这也决定了最后输出的exe文件路径）
	
	8. **--icon=[ICO文件路径]：指定程序图标**
	
	9. -v [指定文件]：指定程序版本信息
	
	10. -n [指定程序名]：指定程序名称
	
	11. 多个存在调用关系的py文件，只需要打包主文件