IO

|--Writer

|--FileWriter

void write(int c) 写入单个字符。

void write(char[] cbuf, int off, int len) 将字符写入数组的某一部分。

void write(String str, int off, int len) 写入一部分字符串。

void flush() 刷新该流的缓冲。

void close() 关闭此流，但要先刷新它。

|--BufferedWriter

void newLine() 写入一个行分隔符。

|--OutputStreamWriter

|--Reader

|--FileReader 两种读取方法（两种复制方法）

|--BufferedReader 特有读取方法（复制方法）

String readLine()  读取一个文本行。

|--LineNumberReader 带行号读取方法

void setLineNumber(int lineNumber) 设置当前行号。



|--OutputStream

|--FileOutputStream

|--BufferedOutputStream

|--InputStream

|--FileInputStream 三种读取方法

|--BufferedInputStream





import java.io.*;
class FileWriterDemo{
	public static void main(String[] args)throws IOException{
		//通过FileWriter类像将字符串写入demo.txt文件中
		FileWriter fw = new FileWriter("demo.txt");
		fw.write("Hello world");
		fw.close();
	}
}

//IO异常处理方式
FileWriter fw = null;
try{
	fw = new FileWriter("test.txt");
	fw.write("Hello world");
}
catch(IOException e){
	sop("catch"+e.toString());
}
finally{
	try{
		if(fw!=null){
			fw.close();
		}
	}
	catch(IOException e){
		sop(e.toString());
	}
}

//对已有文件续写
FileWriter fw = new FileWriter("test.txt",true);
fw.write("hehe");
fw.close();

//FileReader读取两种方式：
FileReader fr = new FileReader("test.txt");
//方式一：一次读一个字符
int ch = 0;
while((ch=fr.read())!=-1){
	sop((char)ch);
}
fr.close();
//方式二：存储到字符数组，再将其打印到控制台
char[] buff = new char[1024];
int len = 0;
while((len=fr.read(buff))!=-1){
	sop(new String(buff,0,len));
}
fr.close();

//文件复制的两种方法：
	//方式一：一次复制一个字符
FileReader fr = new FileReader("test.txt");
FileWriter fw = new FileWriter("copy.txt");
int ch = 0;
while((ch=fr.read())!=-1){
	fw.write(ch);
}
fr.close();
fw.close();
	//存储到字符数组，再将其复制到指定文件中
FileReader fr = null;
FileWriter fw = null;
try{
	fr = new FileReader("test.txt");
	fw = new FileWriter("copy.txt");
	char[] buff = new char[1024];
	int len = 0;
	while((len=fr.read(buff))!=-1){
		fw.write(buff,0,len);
	}
}
catch(IOException e){
	throw new RuntimeException("failed");
}
finally{
	try{
		if(fr!=null){
			fr.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
	try{
		if(fw!=null){
			fw.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
}

//缓冲区(有newLine()、记得刷新)：BufferedWriter
BufferedWriter bw = new BufferedWriter("test.txt");
for(int i=0;i<5;i++){
	bw.write("abcd"+i);
	bw.newLine();
	bw.flush();
}

//BufferedReader读取
FileReader fr = new FileReader("test.txt");
BufferedReader br = new BufferedReader(fr);
[BufferedReader br = new BufferedReader(new FileReader("test.txt"));]
String line = null;
while((line=br.readLine())!=null){
	sop(line);
}
br.close();

//通过缓冲区复制一个文件
BufferedReader br = null;
BufferedWriter bw = null;
try{
	br = new BufferedReader(new FileReader("test.txt"));
	bw = new BufferedWriter(new FileWriter("copy.txt"));
	String line = null;
	while((line=br.readLine())!=null){
		bw.write(line);
		bw.newLine();
		bw.flush();
	}
}
catch(IOException e){
	throw new RuntimeException("failed");
}
finally{
	try{
		if(br!=null){
			br.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
	try{
		if(bw!=null){
			bw.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
}

///装饰设计模式：模拟一个BufferedReader类XXXXXXXXXXXXXXXXX
class MyBR extends BufferedReader{
	private Reader r;
	MyBR(Reader r){
		this.r = r;
	}
	public String myReadLine() throws IOException{
		StringBuilder sb = new StringBuilder();
		int ch = 0;
		while((ch=r.read())!=-1){
			if(ch='\r'){
				continue;
			}
			if(ch='\n'){
				return sb.toString();
			}else{
				sb.append((char)ch);
			}
			return null;
		}
	}
	public int read(char[] cb,int off,int len)throws IOException{
		return r.read(cb,off,len);
	}
	public void myClose()throws IOException{
		r.close();
	}
}
class Demo{
	public static void main(String[] args){
		MyBR mbr = new MyBR(new FileReader("test.txt"));
		String line = null;
		while((line=mbr.readLine())!=null){
			sop(line);
		}
		mbr.close();
	}
}


//LineNumberReader读取一个文件(带行号)
FileReader fr = new FileReader("test.txt");
LineNumberReader lnr = new LineNumberReader(fr);
String line = null;
lnr.setLineNumber(7);
while((line=lnr.readLine())!=null){
	sop(lnr.getLineNumber()+"::"+line);
}
lnr.close();
///模拟一个LineNumberReader类XXXXXXXXXXXXXXXXXXXXXX
class MyLineNumberReader extends Reader{
	private Reader r;
	MyLineNumberReader(Reader r){
		this.r = r;
	}
	public String myReadLine()throws IOException{
		lineNumber++;
		return super.myReadLine();
	public void setLineNumber(int lineNumber)
	{
		this.lineNumber = lineNumber;
	}
	public int getLineNumber()
	{
		return lineNumber;
	}
	}
}


//InputStreaam、OutputStream 字节
//FileOutputStream写字节文件
FileOutputStream fos = new FileOutputStream("test.txt");
fos.write("dcfvgb".getBytes());
fos.close();
//FileInputStream读取三种方式：
FileInputStream fis = new FileInputStream("test.jpg");
	//方式一：一次复制一个字节
int ch = 0;
while((ch=fis.read())!=-1){
	sop((char)ch);
}
fis.close();
	//方式二：存储到字节数组，再将其打印到控制台
byte[] buff = new byte[1024];
int len = 0;
while((len=fis.read(buff))!=-1){
	sop(new String(buff,0,len));
}
fis.close();
	//定义一个刚刚好的缓冲区，不需要再循环
byte[] buff = new byte[fis.available()];
fis.read(buff)
sop(new String(buff));
fis.close();

//字节流复制图片
FileInputStream fis = null;
FileOutputStream fos = null;
try{
	fis = new FileInputStream("test.jpg");
	fos = new FileOutputStream("copy.jpg");
	byte[] buff = new byte[1024];
	int len = 0;
	while((len=fis.read(buff))!=-1){
		fos.write(buff,0,len);
	}
}
catch(IOException e){
	throw new RuntimeException("failed");
}
finally{
	try{
		if(fis!=null){
			fis.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
	try{
		if(fos!=null){
			fos.close();
		}
	}
	catch(IOException e){
		throw new RuntimeException("failed");
	}
}

//字节流复制mp3(通过缓冲区)
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("test.mp3"));
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(copy.mp3));
int ch = 0;
while((ch=bis.readLine)!=-1){
	fos.write((char)ch);
}
bis.close();
bos.close();
[long start = System.currentTimeMillis()]	//系统当前时间

//模拟一个BufferedInputStreamXXXXXXXXXXXXXXXXXXXXXXX
class MyBI{
	private InputStream is;
	private byte[] buff = new byte[1024];
	private int pos = 0, count = 0;
	MyBI(InputStream is){
		this.is = is;
	}
	//一次读一个字节，从缓冲区(字节数组)获取
	public int myRead()throws IOException{
		if(count == 0){
			count = is.read(buff);
			if(count < 0){
				return -1;
			}
			pos = 0;
			byte b = buff[pos];
			count--;
			pos++;
			return b&255;
		}
		else if(count > 0){
			byte b = buff[pos];
			count--;
			pos++
			return b&0xff;
		}
		return -1;
	}
	public void myClose()throws IOException{
		is.close();
	}
}


//**键盘录入**
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
String line = null;
while((line=br.readLine())!=null){
	if(!"over".equals(line)){
		bw.write(line);
	}
}

//为提高效率，将字节流转换成字符流，再使用BufferedReader(使用readLine())
InputStreamReader  		     VS  		     OutputStreamWriter

/*
读取键盘录入
System.in		标准输入设备：键盘
System.out		标准输出设备：控制台
*/
InputStream is = System.in;
StringBuilder sb = new StringBuilder();
while(true){
	int ch = is.read();
	if(ch='\r'){
		continue;
	}
	if(ch='\n'){
		String s = sb.toString();
		if("over".equals(s)){
			break;
		}
		sop(s.toUpperCase());
		sb.delete(0,len.length());
	}else{
		sb.appen((char)ch);
	}
}

///ExceptionInfo

import java.io.*;
import java.util.*;
import java.text.*;
class  ExceptionInfo
{
	public static void main(String[] args)throws IOException 
	{
		try
		{
			int[] arr = new int[2];
			System.out.println(arr[3]);
		}
		catch (Exception e)
		{
			
			try
			{
				Date d = new Date();
				SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
				String s = sdf.format(d);

				PrintStream ps = new PrintStream("exeception.log");
				ps.println(s);
				System.setOut(ps);

				
			}
			catch (IOException ex)
			{
				throw new RuntimeException("日志文件创建失败");
			}
			e.printStackTrace(System.out);
		}
	}
}
///SystemInfo
import java.util.*;
import java.io.*;
class  SystemInfo
{
	public static void main(String[] args) throws IOException
	{
		Properties prop = System.getProperties();

		//System.out.println(prop);
		prop.list(new PrintStream("sysinfo.txt"));
	}
}

/*
File类
创
	boolean creatNewFile():指定位置创建文件，若已存在→不创建，返回false
	boolean mkdir()		  :创建文件夹
	boolean mkdirs()	  :创建多级文件夹
删
	boolean delete()	  :若文件正在被操作等→删除失败返回false
	void deleteOnExit():  :退出程序时删除指定文件
判
	boolean exists()	  :文件是否存在
	
	isFile()
	isDirectory()
	is Hidden()
	isAbsolute()
查
	getName()
	getPath()
	getParent()
	getAbsolutePath()
	long lastModified()
	long length()
	
	路径\\→File.seperator
	f2.renameTo(f1);
*/




BufferedReader br = new BufferedReader(new InputStream(System.in))

BufferedWriter bw = new BufferedWriter(new OutputStream(System.out))