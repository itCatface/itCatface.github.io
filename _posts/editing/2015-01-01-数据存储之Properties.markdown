---
temp-layout:       post
temp-title:        "数据存储之Properties"
temp-subtitle:     ""
temp-date:         2015-01-01 12:00:00
temp-header-img:   "img/color-android-robot-green.png"
temp-tags:
    - android
---

# 常用方式

1. **config.properties文件中内容如下**

	```
	# 要拉取日志的目录[#内为注释]
	logdir=/sdcard/mydir/log
	# 随便加再加几个键值对
	name=rose
	age=18
	sex=female
	```

2. **Java代码中获取配置文件的内容**

    ```java
    // 创建Properties实例
    Properties properties = new Properties(); 
    
    // 加载配置文件流
    InputStream is = new FileInputStream("D:\\config.properties");
    
    // 将文件流加载进properties实例
    properties.load(is);
    
    // 使用properties实例通过配置文件中key获取对应的value值
    String logdir= properties.getProperty("logdir");
    String name= properties.getProperty("name");
    String age= properties.getProperty("age");
    String sex= properties.getProperty("sex");
    
    System.out.println(logdir + " - " + name + " - " + age + " - " + sex); // /sdcard/mydir/log - rose - 18 - female
    ```

### <a href="https://developer.android.google.cn/reference/java/util/Properties.html" target="_blank">没事点我看看Properties的官方文档吧</a>