---
@@@-layout:       post
title:        "java入门06-Object、String、包装类"
subtitle:     "简介java的Object、String对象和包装类"
date:         2015-01-09 12:00:00
author:       "catface"
header-img:   "img/color-black.png"
header-mask:  0.3
catalog:      true
multilingual: false
edit status:  ed
tags:
    - java
---

# Object类
- getClass()
	
	``` java
	Demo d = new Demo();
	Class clazz1 = d.getClass(); // 返回对象的运行时类
	Class clazz2 = Demo.class;
	System.out.println(clazz1 == clazz2);
	```

- hashCode()

	``` java
	Demo d = new Demo();
	int hashCode = d.hashCode();
	System.out.println(hashCode);
	```

- toString()

	``` java
	Demo d = new Demo();
	System.out.println(d); // 当对对象的引用打印时，会默认调用对象的toString方法，如果
	System.out.println(d.toString()); // 该对象所属的类中没有toString方法，会调用Object类中(父类)
	
	int[] arr = new int[5]; // 数组的父类也是Object
	System.out.println(arr);
	System.out.println(arr.toString());
	```

- equals()

	``` java
	public boolean equals(Object obj) {
	return (this == obj);
	}
	```

- ==号和equals方法的区别、===(即比较值也比较地址)

	- ==号是一个符号，比较运算符，equals是一个方法
	
	- ==：比较基本数据类型比较的是值，比较引用数据类型比较的是地址值
	
	- ===：既比较值也比较地址
	
	- equals方法只能比较引用数据类型，比较对象的属性

- finalize()

	``` java
	class DemoA {
	    @Override
	    public void finalize(){
	        System.out.println("垃圾被清扫了");
	    }
	}
	```

# String

- 几道小题

	- 判断定义为String类型的s1和s2是否相等
	
		``` java
		String s1 = "abc";
		String s2 = "abc";
		System.out.println(s1 == s2);	// true
		System.out.println(s1.equals(s2));	// true
		```
	
	- 下面这句话在内存中创建了几个对象?
	
		``` java
		String s1 = new String("abc");
		```
	
	- 判断定义为String类型的s1和s2是否相等
	
		``` java
		String s1 = new String("abc");
		String s2 = "abc";
		System.out.println(s1 == s2);	// false
		System.out.println(s1.equals(s2));	// true
		```
	
	- 判断定义为String类型的s1和s2是否相等
	
		``` java
		String s1 = "a" + "b" + "c";
		String s2 = "abc";
		System.out.println(s1 == s2); ?
		System.out.println(s1.equals(s2)); 
		```
	
	- 判断定义为String类型的s1和s2是否相等
	
		``` java
		String s1 = "ab";
		String s2 = "abc";
		String s3 = s1 + "c";
		System.out.println(s3.equals(s2));	// true
		```

- 构造函数

	- 字节数组

		``` java
		byte[] arr = { 97，98，99 };
		String str = new String(byte[]);	// 解码，让我们看的懂的，通过默认的编码表，将字节数组转换成字符串
		String(byte[], String);		// 解码，通过指定的编码表，将字节数组转换成字符串
		String(byte[], int offset, int length, String);	// 解码，截取字节数组，offset是开始索引，length是截取的长度
		```

	- 字符数组

		``` java
		String(char[])	// 将字符数组转换成字符串
		String(char[], int offset, int length)		// 截取字符数组，offset是开始的索引，length是截取的长度
		```

- String类的常用方法

	- 判断
	
			boolean equals(Object); // 传入的字符串是否与调用的字符串字符序列是否相同
			boolean equalsIgnoreCase(string); // 传入的字符串是否与调用的字符串字符序列是否相同，不区分大小写
			boolean contains(string); // 传入的字符串是否被调用的字符串包含
			boolean startsWith(string); // 调用的字符串是否以传入的字符串开头
			boolean endsWith(string); // 调用的字符串是否以传入的字符串结尾
			boolean isEmpty(); // 字符串是否为空
	
	- 获取
	
			int length(); // 获取字符串的长度
			char charAt(index); // 通过索引获取对应的字符
			
			int indexOf(int ch); // 通过传入int数或者是字符找对应索引
			int idnexOf(int ch, fromIndex); // 在指定fromIndex的位置查找传入的字符
			
			int indexOf(string str); // 通过传入字符串查找字符串所对应的索引
			int idnexOf(string str, fromIndex); // 通过指定fromIndex的位置查找传入的字符串
			
			int lastIndexOf(ch); // 从后向前第一次找到的索引值返回
			int lastIndexOf(ch, fromIndex): // 通过指定fromIndex的位置，从后向前第一次找到的索引值返回
			
			int lastIndexOf(string); // 通过传入的字符串，将第一次找到字符串中第一个字符的索引返回
			int lastIndexOf(string, fromIndex): // 通过指定fromIndex的位置，将第一次找到字符串中第一个字符的索引返回
			
			String substring(start); // 通过传入的索引值开始向后截取，截取的是索引到length
			String substring(start, end); // 通过传入的两个索引值截取，左闭右开
	
	- 转换
	
			byte[] getBytes(); // 编码，让计算机看的懂的，用默认的编码表，将字符串转换成字节数组
			byte[] getBytes(String); // 用指定的编码表进行编码
		
			char[] toCharArray(); // 将字符串转换成字符数组
		
			static String copyValueOf(char[]); // 将字符数组转换成字符串
			static String copyValueOf(char[] data, int offset, int count);// 将字符数组转换字符串，通过offset开始，截取count个
			
			static String valueOf(char[]); // 将字符数组转换成字符串
			static String valueOf(char[] data, int offset, int count);// 将字符数组转换字符串，通过offset开始，截取count个
			
			static String valueOf(int); // 将一个int数转换成字符串
			static String valueOf(double);
			static String valueOf(boolean); ...
			
			static String valueOf(object);
			object.toString(); // 结果是一样的
			
			String toLowerCase(): // 将字符串全部转换为小写
			String toUpperCase(): // 将字符串全班转换为大写
			
			"abc".concat("kk"); // 将两个字符串相连接，产生新的字符串
	
	- 替换
	
			String replace(oldChar, newChar); // 将newChar替换OldChar，如果OldChar不存在，原字符串直接赋值给替换后字符串
			String replace(string, string);
	
	- 切割
	
			String[] split(regex); // 通过regex切割字符串，切割后会产生一个字符串数组
			String s = "金三胖 郭美美 李天一";
			String[] arr = s.split(" ");
	
	- 去除字符串两空格
	
			String trim();
	
	- 比较
	
			String str1 = "ab";
			String str2 = "bc";
			int num = str1.compareTo(str2); // 如果str比str1大的话，返回的正数

- 正则表达式
	
	- 什么是正则表达式
		一种字符串的约束格式， 例如邮箱提示输入不合法
	
	- 匹配

		String里的matches() 验证一个字符串是否匹配指定的正则表达式"18612345678".matches("1[34578]\d{9}");

	- 分割

		String里的split() 用指定正则表达式能匹配的字符作为分隔符， 分割字符串

	- 替换

		String里的replaceAll(" ", " ") 把字符串中能匹配正则表达式的部分替换为另一个字符串

	- 查找

		Pattern.compile() 创建正则表达式对象
		Pattern.matcher() 用正则表达式匹配一个字符串， 得到匹配器
		Matcher.find() 查找字符串中是否包含能匹配正则表达式的部分
		Matcher.group() 获取匹配的部分

- StringBuffer的常用方法

	- 添加
	
			StringBuffer append(int x); // 在缓冲区的末尾追加
			StringBuffer insert(int index, String str); // 在指定索引位置添加

	- 删除
	
			StringBuffer delete(int start, int end); // 包含头索引，不包含尾部索引
			StringBuffer delete(0, sb.length); // 清空缓冲区
		
			sb = new StringBuffer();
			sb.append("aaaaa");
			sb = new StringBuffer();
			
			StringBuffer deleteCharAt(int index); // 根据指定的索引删除索引对应的元素

	- 修改
	
			StringBuffer replace(int start, int end, string); // 用String替换，包含头不包含尾
			void setCharAt(int index, char); // 修改，把指定索引位置的值改成传入的char值
			StringBuffer reverse(); // 将缓冲区的元素反转
			void setLength(int len); //根据传入的len值截取缓冲区的长度
			toString(); // 转换成String

	- 查找
	
			int indexOf(str); // 查找str在缓冲区第一次出现的位置
			int lastIndexOf(str); // 从后向前查找查找str在缓冲区第一次出现的位置

- StringBuilder和StringBuffer

	- StringBuilder和StringBuffer与String的区别
	
		StringBuilder和StringBuffeer是可变字符序列
		
		String是不变得，一但被初始化，就不能改变
	
	- StringBuilder和StringBuffer的区别
	
		StringBuilder是线程不安全的，所以效率比较高，1.5版本出现
		
		StringBuffer是线程安全的，效率相对较低，1.0版本出现的

# 包装类

- 什么是包装类

	八种基本数据类型都会对应一个包装类

	int是Integer， char是Character， 其他都是首字母大写double Double short Short boolean Boolean...

- 什么时候使用

	集合的泛型中只能写包装类型。JDK5之后， 基本数据类型和包装类之间可以自动的互相转换了

- 包装类常用的方法

		static int parseInt(String s) // 将数字字符串转换成数字，如果是非数字字符串会转换失败，抛异常
		Integer.toBinaryString() // 将一个十进制数字，转换成二进制的字符串
		Integer.toOctalString() // 将一个十进制数字，转换成八进制的字符串
		Integer.toHexString() // 将一个十进制数字，转换成十六进制的字符串
		static long parseLong(String s)
		static double parseDouble(String s)
		static char forDigit(int digit, int radix) // radix代表的是进制例如二进制就传2，八进制就传8，digit代表后面进制里面的元素，而且不能超出后面进制的范围
		String s = "123";
		int x = Integer.parseInt(s);
		String s = "abc";
		char ch = Character.parseChar(s);
