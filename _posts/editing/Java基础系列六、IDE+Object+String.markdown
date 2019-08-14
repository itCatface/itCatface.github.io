Eclipse组成

整体叫做视图，每一个小窗口叫做视窗。在eclipse中要想爽一下，必须先有项目(工程)
(1)视图，视窗
(2)视图就是某些视窗的组合
A：Java视图
B：Debug视图
C：JavaEE视图
(3)视图还原
在视图操作中，我有可能有误操作。这个时候怎么办？
Window--Reset重置视图
Java透视图
(1)Package Explorer 包资源管理器
A：该视图中显示当前工作空间中的所有项目以及项目中的文件。但不显示项目下bin目录中的运行文件
B：可以直接在该视图中创建项目，包，类，接口等
(2)Outline 大纲视窗
A：该视图中显示当前代码视图中源文件中定义的类或者接口。以及定义的所有成员
B：当代码过长时，查找代码中的某一个类或者成员，在该视窗中是最方便的
C：在代码中出现多次的名称要同一更改，也可以在该视窗中完成。同时其他代码如果使用了该变量，那么也会一并改变
(3)Console 控制台视窗
A：用于显示程序的运行结果，相当于DOS命令
B：如果有多个控制台同时运行。比如：服务器端和客户端。可以通过控制台上的小屏幕按钮进行控制台的切换
C：通过点击小方框，进行控制台的强制停止，相当于DOS中的Ctrl+C
(4)Hierarchy 层次视窗
A：用于显示类之间的层次(继承)关系。
B：在当前类上，按F4就可以切换到该视窗，并查看层次关系
查看原码，当前类上F3，或者Ctrl+鼠标点击
对工作空间进行基本配置
注意：在工作空间的设置对于该空间中的所有项目都有效。更换了工作空间，需要重新设置
(1)配置Java的编译和运行环境版本
windows--perference-Java
Compiler 设置成5.0以上，要和运行环境版本一致
Installed JREs：可以指定多个jre环境，但是仅有一个是当前执行的。要和编译器一致，或者高于编译器版本
如果采用高版本编译，用低版本jre运行，会出现异常
(2)代码视窗加上行号
A：首选项--常规--编辑器--文本编辑器
B：在当前类中，左侧，右键。Show Line Numbers
(3)调整字体
windows--perference(首选项)-General(标准)--Appearance(外观)--Color and Fonts(颜色和字体)
右边选择Java。编辑即可
字体选择 Courier New 比较标准，个人爱好
(4)取消悬浮提示

在首选项设置面板中
Java--Editor--Hovers
右边将Combined Hover勾去掉

这样代码的悬浮框就不会自动出现了

如果想看提示，将光标悬浮在代码上，按F2即可
(5)取消默认注释
在首选项设置面板中
Java--Code Style--Code Templates
右边选择Code，将不希望出现默认注释的代码块中的注释去掉。
(6)类名高亮 可以这样配置在“java”→“enditor”→“syntac”，右边展开“java”→“classes”，勾上“Enable”这个选项，选择自己喜欢的颜色即可
(7)preference->general->editors->texteditor selection backgroud color
常用的提高开发的操作
(1)创建面板 定义类和接口，权限，父类已经实现的接口等

syso：然后alt+/就能出现输出语句(回车 到行尾,shift+回车 到下行的行首),如果单独敲回车就是到下行的行首
main：然后alt+/就能出主方法
自己也可以定义。
步骤：windows--perference-Java-Editor-Templates--New
(2)常用的快捷键 (A,E,F必须掌握)

A：alt+/ 内容辅助键,补充类或者接口名，帮我们起变量名，new 后面直接提示等。
B：ctrl+/ 单行注释，再按一次，取消单行注释
C：ctrl+shift+/ 对选中的区域进行多行注释的封装
D：ctrl+shift+\ 用于取消多行注释，只要光标在多行注释中即可
E：ctrl+shift+o 对使用了其他包中的类或者接口进行自动导入
F：ctrl+shift+f 对代码进行格式化
G: ctrl + alt + 上键 向上复制当前行或选中行
H: ctrl + alt + 下键 向下复制当前行或选中行
I：alt+上键 向上移动当前行或者选中行
J：alt+下键 向下移动当前行或者选中行
K：ctrl+d 删除当前行，或者删除选中行
L：ctrl+shift+x 将选中部分的字母大写
M：ctrl+shift+y 将选中部分的字母小写
N：ctrl+1 光标放在编译中出现红色波浪线提示的内容上，在该快捷键可以获取建议的处理方式
代码生成的快捷键alt+shift+s
出现source
1：在区域中右键
2：alt+shift+s
(1)私有字段的get/set 重点 (2)构造方法 (3)重写父类方法 重点 @Override 注解 表明此方法是重写父类的

(4)添加注释 /** 回车 (5)方法的重构 右键--refactor--Extract Method

int sum = a + b;
System.out.println(sum);

// 选中a+b 扩展可以生成带返回值的
Debug 调试程序
注释找错误
输出打印调试程序
程序不是写出来的,是改出来的
(1)让我们调试程序更加方便
(2)想要调试，需要在程序中加入断点
(3)运行debug as，打开debug视图
(4)快捷键
f5：跳入
f6：跳过
f7：跳出
(5)清除断点
在Breakpoints视窗中清除指定断点或者所有断点
打jar包，导入jar包，及jar包的使用。
1：打jar包
选中项目--右键--Export--Java--jar--next--自己写jar包的名字和选择路径--finish
2：jar包的使用
导入jar包
1：单独添加jar
把jar复制,然后粘贴到项目路径下
一定要把jar添加至classpath路径中
怎么添加呢?
右键jar包--添加构建路径项目下：.classpath文件中可以看到
如果,这写jar不用了,那么,就从构建路径中把jar包移除
选中项目--右键--首选项--Java Build Path--library--选中其中的jar包,给remove
2：为了方便管理多个jar包
通常建立一个目录，名字建立定义为lib
将jar都存放在该目录下
如果要使用jar包，只要将该jar导入到eclipse的classpath路径下
右键至添加构建路径 项目下：.classpath文件中可以看到
导入已有的项目
空白区域--右键--import--General--Existing Project into Workspace--选中你的项目目录--finish--OK
删除项目中有两种。 选中和不选中删除硬盘上的项目
请不要选中删除硬盘上的项目。
Object类
getClass()
Demo d = new Demo();
Class clazz1 = d.getClass(); // 返回对象的运行时类
Class clazz2 = Demo.class;
System.out.println(clazz1 == clazz2);
hashCode()

Demo d = new Demo();
int hashCode = d.hashCode();
System.out.println(hashCode);
toString()

Demo d = new Demo();
System.out.println(d); // 当对对象的引用打印时,会默认调用对象的toString方法,如果
System.out.println(d.toString()); // 该对象所属的类中没有toString方法,会调用Object类中(父类)

int[] arr = new int[5]; // 数组的父类也是Object
System.out.println(arr);
System.out.println(arr.toString());
equals()
public boolean equals(Object obj) {
return (this == obj);
}
==号和equals方法的区别、===(即比较值也比较地址)
1, ==号是一个符号,比较运算符,equals是一个方法
2, ==：比较基本数据类型比较的是值,比较引用数据类型比较的是地址值
3, ===：既比较值也比较地址
4, equals方法只能比较引用数据类型,比较对象的属性
finalize()

class DemoA {
    @Override
    public void finalize(){
        System.out.println("垃圾被清扫了");
    }
}
以下为字符串简介
几道小题
1. 判断定义为String类型的s1和s2是否相等
String s1 = "abc";
String s2 = "abc";
System.out.println(s1 == s2); // true
System.out.println(s1.equals(s2)); // true
2. 下面这句话在内存中创建了几个对象?
String s1 = new String("abc");
3. 判断定义为String类型的s1和s2是否相等
String s1 = new String("abc");
String s2 = "abc";
System.out.println(s1 == s2); // false
System.out.println(s1.equals(s2)); // true
4.判断定义为String类型的s1和s2是否相等
String s1 = "a" + "b" + "c";
String s2 = "abc";
System.out.println(s1 == s2); ?
System.out.println(s1.equals(s2)); 
5.判断定义为String类型的s1和s2是否相等
String s1 = "ab";
String s2 = "abc";
String s3 = s1 + "c";
System.out.println(s3.equals(s2)); // true
构造函数
1. 字节数组
byte[] arr = { 97,98,99 };
String str = new String(byte[]);  // 解码,让我们看的懂的,通过默认的编码表,将字节数组转换成字符串
String(byte[], String);  // 解码,通过指定的编码表,将字节数组转换成字符串
String(byte[], int offset, int length, String); // 解码,截取字节数组,offset是开始索引,length是截取的长度
2. 字符数组
String(char[]) // 将字符数组转换成字符串
String(char[], int offset, int length) // 截取字符数组,offset是开始的索引,length是截取的长度
String类的常用方法
1. 判断

1.1 boolean equals(Object); // 传入的字符串是否与调用的字符串字符序列是否相同
1.2 boolean equalsIgnoreCase(string); // 传入的字符串是否与调用的字符串字符序列是否相同,不区分大小写
1.3 boolean contains(string); // 传入的字符串是否被调用的字符串包含
1.4 boolean startsWith(string); // 调用的字符串是否以传入的字符串开头
1.5 boolean endsWith(string); // 调用的字符串是否以传入的字符串结尾
1.6 boolean isEmpty(); // 字符串是否为空
2. 获取

2.1 int length(); // 获取字符串的长度
2.2 char charAt(index); // 通过索引获取对应的字符
2.3
int indexOf(int ch); // 通过传入int数或者是字符找对应索引
int idnexOf(int ch, fromIndex); // 在指定fromIndex的位置查找传入的字符
2.4
int indexOf(string str); // 通过传入字符串查找字符串所对应的索引
int idnexOf(string str, fromIndex); // 通过指定fromIndex的位置查找传入的字符串
2.5
int lastIndexOf(ch); // 从后向前第一次找到的索引值返回
int lastIndexOf(ch, fromIndex): // 通过指定fromIndex的位置,从后向前第一次找到的索引值返回
2.6
int lastIndexOf(string); // 通过传入的字符串,将第一次找到字符串中第一个字符的索引返回
int lastIndexOf(string, fromIndex): // 通过指定fromIndex的位置,将第一次找到字符串中第一个字符的索引返回
2.7
String substring(start); // 通过传入的索引值开始向后截取,截取的是索引到length
String substring(start, end); // 通过传入的两个索引值截取,左闭右开
3. 转换

3.1
byte[] getBytes(); // 编码,让计算机看的懂的,用默认的编码表,将字符串转换成字节数组
byte[] getBytes(String); // 用指定的编码表进行编码
3.2 char[] toCharArray(); // 将字符串转换成字符数组
3.3
static String copyValueOf(char[]); // 将字符数组转换成字符串
static String copyValueOf(char[] data, int offset, int count);// 将字符数组转换字符串,通过offset开始,截取count个
3.4
static String valueOf(char[]); // 将字符数组转换成字符串
static String valueOf(char[] data, int offset, int count);// 将字符数组转换字符串,通过offset开始,截取count个
3.5

static String valueOf(int); // 将一个int数转换成字符串
static String valueOf(double);
static String valueOf(boolean); ...
3.6

static String valueOf(object);
和object.toString(); // 结果是一样的
3.7
String toLowerCase(): // 将字符串全部转换为小写
String toUpperCase(): // 将字符串全班转换为大写
3.8 "abc".concat("kk"); // 将两个字符串相连接,产生新的字符串
4. 替换

4.1 String replace(oldChar, newChar); // 将newChar替换OldChar,如果OldChar不存在,原字符串直接赋值给替换后字符串
4.2 String replace(string, string);
5. 切割

String[] split(regex); // 通过regex切割字符串,切割后会产生一个字符串数组
String s = "金三胖 郭美美 李天一";
String[] arr = s.split(" ");
6. 去除字符串两空格

String trim();
7. 比较

String str1 = "ab";
String str2 = "bc";
int num = str1.compareTo(str2); // 如果str比str1大的话,返回的正数
正则表达式
1. 什么是正则表达式
一种字符串的约束格式, 例如邮箱提示输入不合法
2. 匹配
String里的matches() 验证一个字符串是否匹配指定的正则表达式"18612345678".matches("1[34578]\d{9}");
3. 分割
String里的split() 用指定正则表达式能匹配的字符作为分隔符, 分割字符串
4. 替换
String里的replaceAll(" ", " ") 把字符串中能匹配正则表达式的部分替换为另一个字符串
5. 查找
Pattern.compile() 创建正则表达式对象
Pattern.matcher() 用正则表达式匹配一个字符串, 得到匹配器
Matcher.find() 查找字符串中是否包含能匹配正则表达式的部分
Matcher.group() 获取匹配的部分
StringBuffer的常用方法
1. 添加

1.1 StringBuffer append(int x); // 在缓冲区的末尾追加
1.2 StringBuffer insert(int index, String str); // 在指定索引位置添加
2. 删除

2.1 StringBuffer delete(int start, int end); // 包含头索引,不包含尾部索引
2.2 StringBuffer delete(0, sb.length); // 清空缓冲区
sb = new StringBuffer();
sb.append("aaaaa");
sb = new StringBuffer();
2.3 StringBuffer deleteCharAt(int index); // 根据指定的索引删除索引对应的元素
3. 修改

3.1 StringBuffer replace(int start,int end,string); // 用String替换,包含头不包含尾
3.2 void setCharAt(int index ,char); // 修改,把指定索引位置的值改成传入的char值
3.3 StringBuffer reverse(); // 将缓冲区的元素反转
3.4 void setLength(int len); //根据传入的len值截取缓冲区的长度
3.5 toString(); // 转换成String
4. 查找

4.1 int indexOf(str); // 查找str在缓冲区第一次出现的位置
4.2 int lastIndexOf(str); // 从后向前查找查找str在缓冲区第一次出现的位置
StringBuilder和StringBuffer
1. StringBuilder和StringBuffer与String的区别
StringBuilder和StringBuffeer是可变字符序列
String是不变得,一但被初始化,就不能改变
2. StringBuilder和StringBuffer的区别
StringBuilder是线程不安全的,所以效率比较高,1.5版本出现
StringBuffer是线程安全的,效率相对较低,1.0版本出现的
包装类
1. 什么是包装类
8种基本数据类型都会对应一个包装类
int是Integer, char是Character, 其他都是首字母大写double Double short Short boolean Boolean...
2. 什么时候使用
集合的泛型中只能写包装类型。JDK5之后, 基本数据类型和包装类之间可以自动的互相转换了
3. 包装类常用的方法
static int parseInt(String s) // 将数字字符串转换成数字,如果是非数字字符串会转换失败,抛异常
Integer.toBinaryString() // 将一个十进制数字,转换成二进制的字符串
Integer.toOctalString() // 将一个十进制数字,转换成八进制的字符串
Integer.toHexString() // 将一个十进制数字,转换成十六进制的字符串
static long parseLong(String s)
static double parseDouble(String s)
static char forDigit(int digit, int radix) // radix代表的是进制例如二进制就传2,八进制就传8,digit代表后面进制里面的元素,而且不能超出后面进制的范围
String s = "123";
int x = Integer.parseInt(s);
String s = "abc";
char ch = Character.parseChar(s);
