---
layout:       post
title:        "JavaScript页面行为简述"
subtitle:     "通过JavaScript即可完成界面交互"
date:         2015-01-01 12:00:00
author:       "catface"
header-img:   "img/black-bg.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ed
tags:
    - 前端
---

# JavaScript简介

- **简介**

	- 是脚本语言.
	- 是一种轻量级的编程语言.
	- 是可插入 HTML 页面的编程代码.
	- 插入 HTML 页面后，可由所有的现代浏览器执行.

- **JavaScript和java的区别**

	|java |JavaScript|
	|---|---|
	|sun公司，现为oracle公司   |  网景公司|
	|面向对象            |   基于对象|
	|运行需要虚拟机           |直接使用浏览器就能运行|
	|强类型语言                |弱类型语言|
	|定义变量`int i=10;`但`int i="10";`是错误的|没有限制`var j=10; var j="10"; var j=true;`|
	
- **三个特点**

	交互、安全、跨平台、大小写敏感

- **三个组成部分**

	- ECMAScript：欧洲计算机协会.由此组织制定了js规范(包含语句、语法).
	- BOM(Browser Object Model)：浏览器对象模型.
	- DOM(Document Object Model)：文档对象模型.
	
- **大致作用**

	- 写入 HTML 输出：`document.write`
	- 对事件作出反应：`onclick="alert('Welcome!')"`
	- 改变 HTML 内容：`innerHTML`
	- 改变 HTML 图像
	- 改变 HTML 样式：`document.getElementById("demo").style.color="#f00"; `
	- 验证输入：`if isNaN(x) {alert("Not Numeric")};`
	
- **两种结合方式**

	- 使用html的标签`<script type="text/script">js代码</script>`
	- `<script type="text/script" src="js文件路径"></script>`
	
- **数据类型和变量声明**

	**查看变量类型：`typeof(变量名称)`**
	
	|类型|声明|
	|---|---|
	|String|var str="aaa";|
	| Number|`var i=10.01;`|
	|boolean|`var flag=true;`|
	| null|`var data=null;`|
	| undefined|`var m;`|
	|Array|`var cars=new Array();`|
	|Object|`var person= new Object;`|
	
- **语句**

	- 条件语句
		- ```if```
		- ```if ... else ...```
		- ```if ... else if ...  else ...```
		- ```switch ... (default)```
	- 循环语句
		- ```for```
		- ```for ... in```
			``` js
			var person={fname:"John",lname:"Doe",age:25};
			
			for (x in person)
			{
				txt=txt + person[x];
			}
			```
		
		- `while ...`
		- `do ... while ...`
		- `break & continue`
	- 异常语句
		- ```try ... catch & throw```
		
- **函数**

	- `function add1(a,b,c) { return a+b+c; }`
	- 动态函数：`var add = new Function(ars,method);`
	- 匿名函数：`var add = function(a,b) { return a+b; }`
	- 重载：方法名称相同，参数列表不同.
		- js中不存在重载，但是可以通过arguments数组来模拟重载的效果.

# JavaScript对象

- **Array**

	- 创建
	
		- `new Array();`
		- `new Array(5);`
		- `new Array("a", true, ..., 7);`
		
	**属性**
	
	| 属性 | 描述 |
	|---|---|
	|constructor| 返回对创建此对象的数组函数的引用|
	|**length** |设置或返回数组中元素的数目|
	|prototype |使您有能力向对象添加属性和方法| 
		
	**方法**

	|方法 |描述|
	|---|---|
	|**concat()** |连接两个或更多的数组，并返回结果|
	|join() |把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔|
	|pop() |删除并返回数组的最后一个元素 |
	|push() |向数组的末尾添加一个或更多元素，并返回新的长度|
	|reverse()| 颠倒数组中元素的顺序|
	|shift() |删除并返回数组的第一个元素 |
	|slice() |从某个已有的数组返回选定的元素 |
	|sort()| 对数组的元素进行排序 |
	|splice()| 删除元素，并向数组添加新元素| 
	|toSource() |返回该对象的源代码| 
	|**toString()**| 把数组转换为字符串，并返回结果|
	|toLocaleString()| 把数组转换为本地数组，并返回结果| 
	|unshift()| 向数组的开头添加一个或更多元素，并返回新的长度|
	|valueOf() |返回数组对象的原始值 |
		
- **Boolean**

	- 创建
		- `new Boolean(value);	// 构造函数`
		- `Boolean(value);		// 转换函数`

	**属性**

	|属性 |描述|
	|---|---|
	|constructor |返回对创建此对象的 Boolean 函数的引用| 
	|prototype |使您有能力向对象添加属性和方法| 

	**方法**

	|方法|描述|
	|---|---|
	|toSource() |返回该对象的源代码|
	|**toString()**| 把逻辑值转换为字符串，并返回结果|
	|valueOf()| 返回 Boolean 对象的原始值|

- **Data**

	- 创建
	
		- `var myDate=new Date();`

	**属性**

	|属性 |描述|
	|---|---|

	**方法**

	|方法|描述|
	|---|---|
	|Date() |返回当日的日期和时间|
	|getDate() / setData() |从 Date 对象返回一个月中的某一天 (1 ~ 31)|
	|getDay() |从 Date 对象返回一周中的某一天 (0 ~ 6)| 
	|getMonth() / s |从 Date 对象返回月份 (0 ~ 11)|
	|getFullYear() / s  |从 Date 对象以四位数字返回年份| 
	|getHours() / s| 返回 Date 对象的小时 (0 ~ 23)|
	|getMinutes() / s |返回 Date 对象的分钟 (0 ~ 59)| 
	|getSeconds() / s |返回 Date 对象的秒数 (0 ~ 59)|
	|getMilliseconds() / s|返回 Date 对象的毫秒(0 ~ 999)| 
	|getTime() / s| 返回 1970 年 1 月 1 日至今的毫秒数|
	|getTimezoneOffset() |返回本地时间与格林威治标准时间 (GMT) 的分钟差| 
	|getUTCDate() / s| 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)|
	|getUTCDay() / s |根据世界时从 Date 对象返回周中的一天 (0 ~ 6)| 
	|getUTCMonth() / s |根据世界时从 Date 对象返回月份 (0 ~ 11)| 
	|getUTCFullYear() / s |根据世界时从 Date 对象返回四位数的年份| 
	|getUTCHours() / s |根据世界时返回 Date 对象的小时 (0 ~ 23)| 
	|getUTCMinutes() / s |根据世界时返回 Date 对象的分钟 (0 ~ 59)| 
	|getUTCSeconds() / s |根据世界时返回 Date 对象的秒钟 (0 ~ 59)|
	|getUTCMilliseconds() / s |根据世界时返回 Date 对象的毫秒(0 ~ 999)| 
	|parse() |返回1970年1月1日午夜到指定日期（字符串）的毫秒数|  
	|toSource() |返回该对象的源代码|
	|toString()| 把 Date 对象转换为字符串|
	|toTimeString() |把 Date 对象的时间部分转换为字符串| 
	|toDateString() |把 Date 对象的日期部分转换为字符串|
	|toGMTString() |请使用 toUTCString() 方法代替| 
	|toUTCString() |根据世界时，把 Date 对象转换为字符串|
	|toLocaleString() |根据本地时间格式，把 Date 对象转换为字符串|
	|toLocaleTimeString()|根据本地时间格式，把 Date 对象的时间部分转换为字符串| 
	|toLocaleDateString() |根据本地时间格式，把 Date 对象的日期部分转换为字符串|
	|UTC()| 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数| 
	|valueOf() |返回 Date 对象的原始值| 

- **Math**

	**属性**

	|属性 |描述|
	|---|---|
	|E |返回算术常量 e，即自然对数的底数（约等于2.718）|
	|LN2 |返回 2 的自然对数（约等于0.693）| 
	|LN10 |返回 10 的自然对数（约等于2.302）| 
	|LOG2E| 返回以 2 为底的 e 的对数（约等于 1.414）| 
	|LOG10E |返回以 10 为底的 e 的对数（约等于0.434）| 
	|PI |返回圆周率（约等于3.14159）| 
	|SQRT1_2| 返回返回 2 的平方根的倒数（约等于 0.707）|
	|SQRT2 |返回 2 的平方根（约等于 1.414）|

	**方法**

	|方法|描述|
	|---|---|
	|abs(x)| 返回数的绝对值| 
	|acos(x)| 返回数的反余弦值| 
	|asin(x) |返回数的反正弦值|
	|atan(x) |以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值| 
	|atan2(y,x)| 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）|
	|ceil(x) |对数进行上舍入|
	|cos(x) |返回数的余弦| 
	|exp(x) |返回 e 的指数|
	|floor(x) |对数进行下舍入| 
	|log(x) |返回数的自然对数（底为e）| 
	|max(x,y) |返回 x 和 y 中的最高值|
	|min(x,y) |返回 x 和 y 中的最低值| 
	|pow(x,y) |返回 x 的 y 次幂| 
	|random()| 返回 0 ~ 1 之间的随机数| 
	|round(x) |把数四舍五入为最接近的整数|
	|sin(x) |返回数的正弦|
	|sqrt(x) |返回数的平方根|
	|tan(x) |返回角的正切| 
	|toSource() |返回该对象的源代码| 
	|valueOf() |返回 Math 对象的原始值| 


- **Number**

	**属性**

	|属性 |描述|
	|---|---|
	|constructor| 返回对创建此对象的 Number 函数的引用|
	|MAX_VALUE |可表示的最大的数| 
	|MIN_VALUE| 可表示的最小的数| 
	|NaN| 非数字值|
	|NEGATIVE_INFINITY |负无穷大，溢出时返回该值|
	|POSITIVE_INFINITY |正无穷大，溢出时返回该值| 
	|prototype| 使您有能力向对象添加属性和方法| 

	**方法**

	|方法|描述|
	|---|---|
	|toString| 把数字转换为字符串，使用指定的基数| 
	| toLocaleString|  把数字转换为字符串，使用本地数字格式顺序| 
	| toFixed | 把数字转换为字符串，结果的小数点后有指定位数的数字| 
	| toExponential | 把对象的值转换为指数计数法|
	| toPrecision|  把数字格式化为指定的长度| 
	| valueOf | 返回一个 Number 对象的基本数字值| 

- **String**

	**属性**

	|属性 |描述|
	|---|---|
	|constructor| 对创建该对象的函数的引用 |
	|length| 字符串的长度 |
	|prototype| 允许您向对象添加属性和方法 |

	**方法**

	|方法|描述|
	|---|---|
	|anchor() |创建 HTML 锚| 
	|big()| 用大号字体显示字符串|
	|blink() |显示闪动字符串|
	|bold() |使用粗体显示字符串|
	|charAt() |返回在指定位置的字符|
	|charCodeAt() |返回在指定的位置的字符的 Unicode 编码|
	|concat() |连接字符串|
	|fixed() |以打字机文本显示字符串| 
	|fontcolor() |使用指定的颜色来显示字符串|
	|fontsize() |使用指定的尺寸来显示字符串| 
	|fromCharCode()| 从字符编码创建一个字符串|
	|indexOf() |检索字符串|
	|italics()| 使用斜体显示字符串| 
	|lastIndexOf() |从后向前搜索字符串|
	|link() |将字符串显示为链接| 
	|localeCompare() |用本地特定的顺序来比较两个字符串| 
	|match() |找到一个或多个正则表达式的匹配|
	|replace() |替换与正则表达式匹配的子串| 
	|search() |检索与正则表达式相匹配的值| 
	|slice() |提取字符串的片断，并在新的字符串中返回被提取的部分| 
	|small() |使用小字号来显示字符串|
	|split()| 把字符串分割为字符串数组| 
	|strike() |使用删除线来显示字符串| 
	|sub() |把字符串显示为下标|
	|**substr()** |从起始索引号提取字符串中指定数目的字符|
	|**substring()** |提取字符串中两个指定的索引号之间的字符| 
	|sup() |把字符串显示为上标|
	|toLocaleLowerCase()| 把字符串转换为小写| 
	|toLocaleUpperCase() |把字符串转换为大写| 
	|toLowerCase() |把字符串转换为小写| 
	|toUpperCase() |把字符串转换为大写| 
	|toSource() |代表对象的源代码| 
	|toString() |返回字符串| 
	|valueOf() |返回某个字符串对象的原始值| 