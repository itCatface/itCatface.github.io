# CSS简介

>**Cascading Style Sheets：层叠样式表.**
>
>**功能一、将样式和html分开编写.**
>**功能二、样式强大，弥补html属性的不足.**

# css的四种引入方式

1. 在每个html标签中都有一个属性style，在style属性中写css代码.
	```
	<div style="backgroud:black;color:white">GG思密达</div>
	```

2. 在html的head标签内实现.

	```
	<style type="text/css">
		div {
			background:black;
			color:white;
		}
	</style>
	```

3. 单独创建css文件，其次用html的标签实现.

	```<style type="text/css"> @import url(css路径)</style>```
	
4. 引入外部的资源文件，使用头标签link标签链接外部的css文件.

	```<link rel="stylesheet" type="text/css" href="css路径"/>```

# CSS选择器

- 标签选择器：把标签作为选择器的名称.

	```
	div {
		background:black;
		color:white;
	}
	```
- class选择器：使用class属性的值作为选择器的名称.

	```
	.cls_name {
		backgroud:black;
		color:white;
	}
	```
	
- id选择器：使用id属性的值作为选择器的名称.
	```
	# id_name {
		backgroud:black;
		color:white;
	}
	```

- 关联选择器：标签中嵌套一个标签，设置内标签的样式.

	```
	div p {
		...
	}
	```

- 组合选择器：设置不同的标签具有相同的样式.

	```
	div,p {
		...
	}
	```

- 伪元素选择器：实现简单的动态效果.
 
	```link   hover   active   visited：原始   悬停   点击   击后```

- CSS基本选择器优先级

	```style > id > class > 标签选择器```.

# CSS的盒子模型

- 首先需要把数据都封装到一块区域，这个区域一般使用div进行封装.
- 边框：使用属性border：统一设置border-width、border-style、border-color.
- 分别设置上下四条边的属性border-top、border-bottom、border-left、border-right.
- 内边距：padding：统一设置，分别设置：length.
- 外边距：margin：统一设置，分别设置：length.

# CSS的布局

- 漂浮
	- float属性
		- left：当前设置这个属性的div的位置居左，后面的标签飘到右边.
		- right：当前设置这个属性的div的位置居右，后面的标签飘到左边.
          
- 定位
	- position属性
		- absolute：将对象从文档流中拖出.
		- relative：不会将对象从文档流中拖出.