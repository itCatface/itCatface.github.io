File
1.什么是File类
File类对象可以代表一个路径, 此路径可以是文件也可以是文件夹, 该类方法可以对这个路径进行各种操作
2.创建对象
给File类构造函数传一个String类型的路径就可以创建对象
路径分为两种: 绝对路径, 相对路径
绝对路径: 从盘符开始, 是一个固定的路径
相对路径: 不从盘符开始, 相对于某个位置. 在Eclipse中的Java工程如果使用相对路径, 那么就相对于工程根目录. cmd则相对应于当前目录.
3.常用方法
*****boolean exists()       判断是否存在
boolean isAbsolute();       是否是绝对路径
*****boolean isDirectory(); 是否是文件夹
*****boolean isFile();      是否是文件
boolean isHidden();         是否是隐藏

getAbsolutePath();          获取绝对路径
getFreeSpace();             获取当前盘符剩余空间
getTotalSpace();            获取当前盘符总空间
getUsableSpace();           获取当前盘符可用空间
*****getParent());          获取父级路径
*****getName());            获取文件或文件夹名

setReadable(false);         设置是否可读
setWritable(false);         设置是否可写
setExecutable(false);       设置是否可执行
canRead();                  是否可读
canWrite();                 是否可写
canExecute();               是否可执行

setLastModified();          设置文件的最后修改时间
*****lastModified();        获取文件的最后修改时间     
*****createNewFile()        创建文件
*****mkdir();               创建文件夹(仅一级)
*****mkdirs();              创建文件夹(父级不存在也创建)

**renameTo();               改名, 可以移动文件
*****delete()               删除, 文件可以直接删除, 文件夹只能删空的
*****length()               文件大小

String[] list() 
*****File[] listFiles() 
 

一.IO流
1.概念
IO流用来处理设备之间的数据传输
Java对数据的操作是通过流的方式
Java用于操作流的类都在IO包中
流按流向分为两种：输入流，输出流。
流按操作类型分为两种：
字节流 : 字节流可以操作任何数据,因为在计算机中任何数据都是以字节的形式存储的
字符流 : 字符流只能操作纯字符数据，比较方便。
2.IO流常用父类
字节流的抽象父类：
InputStream
OutputStream
字符流的抽象父类：
Reader
Writer
3.IO程序书写
使用前，导入IO包中的类
使用时，进行IO异常处理
使用后，释放资源
二.字节流
1.常用方法
InputStream:
read() 读取一个字节
read(byte[]) 读取若干(数组长度)字节
available() 获取可读的字节数
close() 关闭流, 释放资源
OutputStream:
write(int) 写出一个字节
write(byte[]) 写出数组中的所有字节
write(byte[],start,len);
close() 关闭流, 释放资源
2.读取文件
创建FileInputStream对象, 指定一个文件. 文件必须存在, 不存在则会抛出FileNotFoundException
使用read()方法可以从文件中读取一个字节. 如果读取到文件末尾会读到-1
读取结束后需要释放资源, 调用close()方法关闭输入流
输入流代码
FileInputStream fis = new FileInputStream("xxx.txt");       //创建流对象,关联xxx.txt文件
int b;
while((b = fis.read()) != -1) {                             //将每次读到的结果赋值给b
    System.out.println(b);
}

fis.close();
为什么read方法返回是int而不是byte类型呢?
因为如果读取的是视频文件或音频文件或图片文件等,在读取过程中很有可能会遇到11111111,也就是byte类型的-1,那么遇到-1程序就会停止读取,会漏掉文件,为了防止这种情况出现,把byte类型提升为int类型,在这个字节前补上24个0,把遇到的-1变成255,这样可以保证将整个文件读完
3.写出文件
创建FileOutputStream对象, 指定一个文件. 文件不存在会创建新文件, 存在则清空原内容. 如果需要追加, 在构造函数中传入true.
使用write()方法可以向文件写出一个字节.
写出结束后同样需要调用close()
输出流代码
FileOutputStream fos = new FileOutputStream("aaa.txt"); //创建流对象,关联aaa.txt
fos.write(100);                                         //写出数据的时候会将前面24个0去掉,写出的是一个字节
fos.write(98);
fos.write(99);
fos.close();                                            //关闭流,释放资源
4.拷贝文件

可以从文件中逐个字节读取, 逐个字节写出, 但这样做效率非常低
我们可以定义一个数组作为缓冲区, 一次读取多个字节装入数组, 然后再一次性把数组中的字节写出1byte = 8bit
1,逐个字节拷贝

FileInputStream fis = new FileInputStream("致青春.mp3");       //创建输入流对象,关联致青春.mp3
FileOutputStream fos = new FileOutputStream("copy.mp3");    //创建输出流对象,关联copy.mp3

int b;
while((b = fis.read()) != -1) {                             //将每次读到的赋值给b
    fos.write(b);                                           //将b中的字节写出去
}

fis.close();                                                //关流,释放资源
fos.close();  
2,自定义数组拷贝

FileInputStream fis = new FileInputStream("致青春.mp3");       //创建输入流对象,关联致青春.mp3
FileOutputStream fos = new FileOutputStream("copy.mp3");    //创建输出流对象,关联copy.mp3
byte[] arr = new byte[1024 * 8];                            //自定义数组
int len;
while((len = fis.read(arr)) != -1) {                            //将数据读到字节数组中
    fos.write(arr, 0, len);                                 //从字节数组中将数据写到文件上
    //fos.write(arr);
}

fis.close();                                                //关流,释放资源
fos.close();

int len = read(arr);如果文件上有数据返回的就是读到有效的字节个数,如果文件上没有数据返回的就是-1
3,定义一个大数组拷贝,数组和文件的字节个数一样大

//fis.available();一次获取读的文件的大小
FileInputStream fis = new FileInputStream("致青春.mp3");
FileOutputStream fos = new FileOutputStream("copy.mp3");
byte[] arr = new byte[fis.available()];                     //虽然可以拷贝,但是在开发时不建议,有可能会导致内存溢出
fis.read(arr);
fos.write(arr);
fis.close();
4,带缓冲区的拷贝

FileInputStream fis = new FileInputStream("致青春.mp3");       //创建输入流对象,关联致青春.mp3
BufferedInputStream bis = new BufferedInputStream(fis);     //对fis进行包装,内置一个8192大小的字节数组      
FileOutputStream fos = new FileOutputStream("copy.mp3");    //创建输出流对象,关联copy.mp3
BufferedOutputStream bos = new BufferedOutputStream(fos);   //对fos进行包装,内置一个8192大小的字节数组

int b;
while((b = bis.read()) != -1) {                             //read一次会先将文件上的数据读到缓冲区中,再从缓冲区一个一个的赋值给b
    bos.write(b);                                           //write一次,是将b中的字节数据写到缓冲区,缓冲区写满再一次写到文件上
}

bis.close();                                                //只需要关掉包装后的即可
bos.close();
5.BufferedInputStream

BufferedInputStream内置了一个缓冲区(数组)
从BufferedInputStream中读取一个字节时
BufferedInputStream会一次性从文件中读取8192个, 存在缓冲区中, 返回给程序一个
程序再次读取时, 就不用找文件了, 直接从缓冲区中获取
直到缓冲区中所有的都被使用过, 才重新从文件中读取8192个
6.BufferedOutputStream
BufferedOutputStream也内置了一个缓冲区(数组)
程序向流中写出字节时, 不会直接写到文件, 先写到缓冲区中
直到缓冲区写满, BufferedOutputStream才会把缓冲区中的数据一次性写到文件里
7.读中文
字节流只读中文有弊端,可能会出现半个中文
解决办法
1,用字符流只读
2,将文件上的所有的字节数据都读到缓冲区中,然后在转换成字符串ByteArrayOutputStream
FileInputStream fis = new FileInputStream("bbb.txt");
byte[] arr = new byte[4];
int len;
while((len = fis.read(arr)) != -1) {
    System.out.println(new String(arr,0,len));
}

fis.close(); 
8.写中文
字节流是可以写字符串的
但是必须将字符串转换成字节数组写出去
FileOutputStream fos = new FileOutputStream("bbb.txt");
fos.write("你要减肥,造吗".getBytes());
fos.close();
9.finally嵌套
1.6版本及以前的标准的异常处理代码

FileInputStream fis = null; 
FileOutputStream fos = null; 
try {
    fis = new FileInputStream("aaa.txt");
    fos = new FileOutputStream("bbb.txt");

    int b;
    while((b = fis.read()) != -1) {
        fos.write(b);
    }
}finally {
    try {
        if(fis != null) 
            fis.close();
    } finally {
        if(fos != null)
            fos.close();
    }
}
10.try close
1.7版本的标准的异常处理代码

try(
    FileInputStream fis = new FileInputStream("aaa.txt");
    FileOutputStream fos = new FileOutputStream("bbb.txt");
    MyClose mc = new MyClose();
){
    int b;
    while((b = fis.read()) != -1) {
        fos.write(b);
    }
}
三.今日重点
1.拷贝文件
a.使用FileInputStream和FileOutputStream, 逐个字节拷贝,效率太低了
b.使用FileInputStream和FileOutputStream, 定义一个大数组(length等于文件大小), 一次性拷贝,有可能会内存溢出
c.使用FileInputStream和FileOutputStream, 定义一个小数组(例如1024), 多次拷贝
d.使用BufferedInputStream和BufferedOutputStream内置的缓冲区, 逐个字节拷贝
2.标准化IO流操作的代码
a.finally嵌套
b.try close
四.练习
1.从键盘输入接收一个文件路径, 把该文件的内容拷贝到工程中
2.从键盘接收输入, 把键盘输入的数据写到文件, 直到输入quit时退出

一.字符流
1.字符流是什么
字符流是可以直接读写字符的IO流
字符流读取字符, 就要先读取到字节数据, 然后转为字符. 如果要写出字符, 需要把字符转为字节再写出.
2.FileReader, FileWriter
FileReader类的read()方法可以按照字符大小读取
FileReader fr = new FileReader("aaa.txt");              //创建输入流对象,关联aaa.txt
int ch;
while((ch = fr.read()) != -1) {                         //将读到的字符赋值给ch
    System.out.println((char)ch);                       //将读到的字符强转后打印
}

fr.close();                                             //关流 
FileWriter类的write()方法可以自动把字符转为字节写出
3.什么情况下使用字符流
字符流也可以拷贝文本文件, 但不推荐使用. 因为读取时会把字节转为字符, 写出时还要把字符转回字节.
程序需要读取一段文本, 或者需要写出一段文本的时候可以使用字符流
4.字符流是否可以拷贝非纯文本的文件
不可以拷贝非纯文本的文件
因为在读的时候会将字节转换为字符,在转换过程中,可能找不到对应的字符,就会用?代替,写出的时候会将字符转换成字节写出去
如果是?,直接写出,这样写出之后的文件就乱了,看不了了
5.自定义字符数组的拷贝
FileReader fr = new FileReader("aaa.txt");          //创建字符输入流,关联aaa.txt
FileWriter fw = new FileWriter("bbb.txt");          //创建字符输出流,关联bbb.txt

int len;
char[] arr = new char[1024*8];                      //创建字符数组
while((len = fr.read(arr)) != -1) {                 //将数据读到字符数组中
    fw.write(arr, 0, len);                          //从字符数组将数据写到文件上
}

fr.close();                                         //关流释放资源
fw.close();  
6.带缓冲的字符流
BufferedReader的read()方法读取字符时会一次读取若干字符到缓冲区, 然后逐个返回给程序, 降低读取文件的次数, 提高效率
BufferedWriter的write()方法写出字符时会先写到缓冲区, 缓冲区写满时才会写到文件, 降低写文件的次数, 提高效率
BufferedReader br = new BufferedReader(new FileReader("aaa.txt"));  //创建字符输入流对象,关联aaa.txt
BufferedWriter bw = new BufferedWriter(new FileWriter("bbb.txt"));  //创建字符输出流对象,关联bbb.txt

int ch;             
while((ch = br.read()) != -1) {     //read一次,会先将缓冲区读满,从缓冲去中一个一个的返给临时变量ch
    bw.write(ch);                   //write一次,是将数据装到字符数组,装满后再一起写出去
}

br.close();                         //关流
bw.close();  
flush方法与close方法的区别
flush是用来刷新缓冲区的,刷完之后还可以写出
close方法是用来关闭流的,在关闭之前会刷新一次缓冲区,刷完之后关闭,不可以再写出
BufferedReader的readLine()方法可以读取一行字符(不包含换行符号)
BufferedWriter的newLine()可以输出一个跨平台的换行符号"\r\n"
BufferedReader br = new BufferedReader(new FileReader("aaa.txt"));
BufferedWriter bw = new BufferedWriter(new FileWriter("bbb.txt"));
String line;
while((line = br.readLine()) != null) {
    bw.write(line);
    //bw.write("\r\n");                 //只支持windows系统
    bw.newLine();                       //跨平台的
}

br.close();
bw.close();  
7.LineNumberReader
LineNumberReader是BufferedReader的子类, 具有相同的功能, 并且可以统计行号
调用getLineNumber()方法可以获取当前行号
调用setLineNumber()方法可以设置当前行号
LineNumberReader lnr = new LineNumberReader(new FileReader("aaa.txt"));
String line;
lnr.setLineNumber(100);                                 //设置行号
while((line = lnr.readLine()) != null) {
    System.out.println(lnr.getLineNumber() + ":" + line);//获取行号
}

lnr.close(); 
8.装饰设计模式
interface Coder {
    public void code();
}

class Student implements Coder {

    @Override
    public void code() {
        System.out.println("javase");
        System.out.println("javaweb");
    }

}

class ItcastStudent implements Coder {
    private Student s;                      //获取到被包装的类的引用
    public ItcastStudent(Student s) {       //通过构造函数创建对象的时候,传入被包装的对象
        this.s = s;
    }
    @Override
    public void code() {                    //对其原有功能进行升级
        s.code();
        System.out.println("数据库");
        System.out.println("ssh");
        System.out.println("安卓");
        System.out.println(".....");
    }

}  
9.使用指定的码表读写字符
FileReader是使用默认码表读取文件, 如果需要使用指定码表读取, 那么可以使用InputStreamReader(字节流,编码表)
FileWriter是使用默认码表写出文件, 如果需要使用指定码表写出, 那么可以使用OutputStreamWriter(字节流,编码表)
BufferedReader br =                                     //高效的用指定的编码表读
        new BufferedReader(new InputStreamReader(new FileInputStream("UTF-8.txt"), "UTF-8"));
BufferedWriter bw =                                     //高效的用指定的编码表写
        new BufferedWriter(new OutputStreamWriter(new FileOutputStream("GBK.txt"), "GBK"));
int ch;
while((ch = br.read()) != -1) {
    bw.write(ch);
}

br.close();
bw.close();
二.今日重点
1.会用BufferedReader读取GBK码表和UTF-8码表的字符
2.会用BufferedWriter写出字符到GBK码表和UTF-8码表的文件中
3.会使用BufferedReader从键盘读取一行

一.序列流
1.什么是序列流
序列流可以把多个字节输入流整合成一个, 从序列流中读取数据时, 将从被整合的第一个流开始读, 读完一个之后继续读第二个, 以此类推.
2.使用方式

整合两个: SequenceInputStream(InputStream, InputStream)
FileInputStream fis1 = new FileInputStream("a.txt");            //创建输入流对象,关联a.txt
FileInputStream fis2 = new FileInputStream("b.txt");            //创建输入流对象,关联b.txt
SequenceInputStream sis = new SequenceInputStream(fis1, fis2);  //将两个流整合成一个流
FileOutputStream fos = new FileOutputStream("c.txt");           //创建输出流对象,关联c.txt

int b;
while((b = sis.read()) != -1) {                                 //用整合后的读
    fos.write(b);                                               //写到指定文件上
}

sis.close();
fos.close(); 
整合多个: SequenceInputStream(Enumeration)
FileInputStream fis1 = new FileInputStream("a.txt");    //创建输入流对象,关联a.txt
FileInputStream fis2 = new FileInputStream("b.txt");    //创建输入流对象,关联b.txt
FileInputStream fis3 = new FileInputStream("c.txt");    //创建输入流对象,关联c.txt
Vector<InputStream> v = new Vector<>();                 //创建vector集合对象
v.add(fis1);                                            //将流对象添加
v.add(fis2);
v.add(fis3);
Enumeration<InputStream> en = v.elements();             //获取枚举引用
SequenceInputStream sis = new SequenceInputStream(en);  //传递给SequenceInputStream构造
FileOutputStream fos = new FileOutputStream("d.txt");
int b;
while((b = sis.read()) != -1) {
    fos.write(b);
}

sis.close();
fos.close();    
二.内存输出流*****
1.什么是内存输出流
该输出流可以向内存中写数据, 把内存当作一个缓冲区, 写出之后可以一次性获取出所有数据
2.使用方式

创建对象: new ByteArrayOutputStream()
写出数据: write(int), write(byte[])
获取数据: toByteArray()
FileInputStream fis = new FileInputStream("a.txt");
ByteArrayOutputStream baos = new ByteArrayOutputStream();
int b;
while((b = fis.read()) != -1) {
    baos.write(b);
}

//byte[] newArr = baos.toByteArray();               //将内存缓冲区中所有的字节存储在newArr中
//System.out.println(new String(newArr));
System.out.println(baos);
fis.close();
黑马面试题

FileInputStream fis = new FileInputStream("a.txt");             //创建字节输入流,关联a.txt
ByteArrayOutputStream baos = new ByteArrayOutputStream();       //创建内存输出流
byte[] arr = new byte[5];                                       //创建字节数组,大小为5
int len;
while((len = fis.read(arr)) != -1) {                            //将文件上的数据读到字节数组中
    baos.write(arr, 0, len);                                    //将字节数组的数据写到内存缓冲区中
}
System.out.println(baos);                                       //将内存缓冲区的内容转换为字符串打印
fis.close();
三.对象操作流
1.什么是对象操作流
该流可以将一个对象写出, 或者读取一个对象到程序中. 也就是执行了序列化和反序列化的操作.
2.使用方式

写出: new ObjectOutputStream(OutputStream), writeObject()

public class Demo3_ObjectOutputStream {

    /**
     * @param args
     * @throws IOException 
     * 将对象写出,序列化
     */
    public static void main(String[] args) throws IOException {
        Person p1 = new Person("张三", 23);
        Person p2 = new Person("李四", 24);
//      FileOutputStream fos = new FileOutputStream("e.txt");
//      fos.write(p1);
//      FileWriter fw = new FileWriter("e.txt");
//      fw.write(p1);
        //无论是字节输出流,还是字符输出流都不能直接写出对象
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("e.txt"));//创建对象输出流
        oos.writeObject(p1);
        oos.writeObject(p2);
        oos.close();
    }

}
读取: new ObjectInputStream(InputStream), readObject()
public class Demo3_ObjectInputStream {

    /**
     * @param args
     * @throws IOException 
     * @throws ClassNotFoundException 
     * @throws FileNotFoundException 
     * 读取对象,反序列化
     */
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("e.txt"));
        Person p1 = (Person) ois.readObject();
        Person p2 = (Person) ois.readObject();
        System.out.println(p1);
        System.out.println(p2);
        ois.close();
    }

}
3.注意

要写出的对象必须实现Serializable接口才能被序列化
不用必须加id号
四.打印流*****
1.什么是打印流

该流可以很方便的将对象的toString()结果输出, 并且自动加上换行, 而且可以使用自动刷出的模式
System.out就是一个PrintStream, 其默认向控制台输出信息

PrintStream ps = System.out;
ps.println(97);                 //其实底层用的是Integer.toString(x),将x转换为数字字符串打印
ps.println("xxx");
ps.println(new Person("张三", 23));
Person p = null;
ps.println(p);                  //如果是null,就返回null,如果不是null,就调用对象的toString()
2.使用方式

打印: print(), println()
自动刷出: PrintWriter(OutputStream out, boolean autoFlush, String encoding)
打印流只操作数据目的

PrintWriter pw = new PrintWriter(new FileOutputStream("g.txt"), true);
pw.write(97);
pw.print("大家好");
pw.println("你好");
pw.close();
五.标准输入输出流
1.什么是标准输入输出流
System.in是InputStream, 标准输入流, 默认可以从键盘输入读取字节数据
System.out是PrintStream, 标准输出流, 默认可以向Console中输出字符和字节数据
2.修改标准输入输出流

修改输入流: System.setIn(InputStream)
修改输出流: System.setOut(PrintStream)
System.setIn(new FileInputStream("a.txt"));             //修改标准输入流
System.setOut(new PrintStream("b.txt"));                //修改标准输出流

InputStream in = System.in;                             //获取标准输入流
PrintStream ps = System.out;                            //获取标准输出流
int b;
while((b = in.read()) != -1) {                          //从a.txt上读取数据
    ps.write(b);                                        //将数据写到b.txt上
}

in.close();
ps.close();
六.数据输入输出流
1.什么是数据输入输出流
DataInputStream, DataOutputStream可以按照基本数据类型大小读写数据
例如按Long大小写出一个数字, 写出时该数据占8字节. 读取的时候也可以按照Long类型读取, 一次读取8个字节.
2.使用方式

DataOutputStream(OutputStream), writeInt(), writeLong()

DataOutputStream dos = new DataOutputStream(new FileOutputStream("b.txt"));
dos.writeInt(997);
dos.writeInt(998);
dos.writeInt(999);

dos.close();
DataInputStream(InputStream), readInt(), readLong()

DataInputStream dis = new DataInputStream(new FileInputStream("b.txt"));
int x = dis.readInt();
int y = dis.readInt();
int z = dis.readInt();
System.out.println(x);
System.out.println(y);
System.out.println(z);
dis.close();
七.Properties
1.向内存中存入值,并通过键获取值setProperty(key,value) getProperty(key);
2.通过load方法,读取配置文件,propertyNames获取所有的key,返回Enumeration
3.根据键改值,并重新存入到配置文件setProperty(key,value),list(new PrintStream())
System.getProperties();获取系统属性,propertyNames将所有的键返回到枚举里,就可以迭代了
八.递归
递归的好处:
可以不知道循环次数(方法调用次数)
递归的弊端:
有可能会栈内存溢出
构造函数是否可以用递归?
构造函数不能使用递归,因为如果可以,那将不断创建对象,永不停止
递归调用是否必须有返回值?
递归调用可以有返回值也可以没有
九.IO总结
1.字节流
FileInputStream, FileOutputStream, 自定义数组拷贝文件
BufferedInputStream, BufferedOutputStream, 内置缓冲区拷贝文件
2.字符流
FileReader, FileWriter
InputStreamReader, OutputStreamWriter
BufferedReader, BufferedWriter
会读写各种码表的文件中的文本数据
3.File
掌握文件夹递归
拷贝一个带内容的文件夹