<font size=4>**简介**

>Angular JS(以下简称AJ)是一个JavaScript(以下简称JS)框架，通过script标签添加到页面中
>`<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>`


1. 指令系统：AJ通过指令`ng-directives`扩展了HTML.
2. 双向数据绑定：通过指令`ng-model`和表达式绑定数据到HTML.
3. 模块化：通过`ng-app`、`ng-controller`、`ng-model`实现MVC.

<font size=4>**正题**

1. AJ表达式
	- 写在`{{ ... }}`内
	- 类似JavaScript表达式，可以包含文字、运算符和变量
	- AJ的数字类似JS的数字
	- AJ的字符串类似JS的字符串
	- AJ的对象类似JS的对象
	- AJ的数组类似JS的数组
	- AJ的表达式和JS也有区别
		- AJ表达式可写在HTML中
		- AJ表达式不支持条件判断、循环和异常
		- AJ表达式支持过滤器`filter`

2. AJ指令
	- AJ通过指令扩展HTML属性，并可以自定义指令
	- `ng-app`：初始化一个AJ应用
	- `ng-init`：初始化应用程序数据，不常用，常用控制器或模块替代
	- `ng-model`：绑定元素值到应用程序
		- 为应用程序数据提供类型验证(number、email、required)
		- 为应用程序数据提供状态(invalid、dirty、touched、error)
		- 为HTML元素提供CSS类
		- 绑定HTML元素到HTML表单
	- `ng-repeat`：重复HTML元素(数组、对象等)
	- `ng-controller`：
待续。。。。。。。。。。