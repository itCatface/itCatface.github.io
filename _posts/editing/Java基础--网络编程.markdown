
import java.net.*;
import java.io.*;
class IpDemo{
	public static void main(String[] args) throws Exception{
		InetAddress i = InetAddress.getLocalHost();
		System.out.println(i.toString());		//计算机名+ip地址
		
		InetAddress ia = InetAddress.getByName("ivan-PC");
		System.out.println("ip:"+ia.getHostAddress());
		System.out.println("name:"+ia.getHostName());
	}
}

/*
需求：通过UDP传输方式，将一段文字数据发送出去(定义一个UDP发送端)
思路：
	1，建立udpsocket服务
	2，提供数据，并将数据封装到数据包中
	3，通过socket服务的send()将数据包发送出去
	4，关闭资源
*/
class UDPSend{
	public static void main(String[] args) throws Exception{
		//创建UDP服务，通过DatagramSocket对象
		DatagramSocket ds = new DatagramSocket(0001);
		//确定数据，并封装成数据包
		byte[] buff = "ca ni mei de".getBytes();
		DatagramPacket dp = new DatagramPacket(buff,buff.length,InetAddress.getByName("ivan-PC"),0002);
		//通过socket服务，通过send()将数据包发送出去
		ds.send(dp);
		//关闭资源
		ds.close();
	}
}

/*
需求：接受UDP协议传输的数据并处理
思路：
	1，建立udpsocket服务，并监听一个端口
	2，定义一个数据包，用于存储收到的字节数据
	3，通过socket服务的receive()将收到的数据存入定义好的数据包对象中
	4，操作数据包对象
	5，关闭资源
*/
class UDPReceive{
	public static void main(String[] args) throws Exception{
		//创建UDPsocket，建立端点
		DatagramSocket ds = new DatagramSocket(0002);
		while(true){
			//定义数据包，用于存储数据
			byte[] buff = new byte[1024];
			DatagramPacket dp = new DatagramPacket(buff,buff.length);
			//通过receive()方法将收到的数据存入数据包中(阻塞式方法)
			ds.receive(dp);
			//通过数据包的方法获取其中的数据
			String ip = dp.getAddress().getHostAddress();
			String data = new String(dp.getData(),0,dp.getLength());
			int port = dp.getPort();
			System.out.println(ip+"::"+data+"::"+port);
		}
		//ds.close();
	}
}

/*
需求：通过UDP发送一段键盘输入并对方收到打印于控制台
*/
class UDPSend2{
	public static void main(String[] args) throws Exception{
		DatagramSocket ds = new DatagramSocket();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String line = null;
		while((line=br.readLine())!=null){
			if("over".equals(line)){
				break;
			}
			byte[] buff = line.getBytes();
			DatagramPacket dp = new DatagramPacket(buff,buff.length,InetAddress.getByName("ivan-PC"),10001);
			ds.send(dp);
		}
		ds.close();
	}
}
class UDPReceive2{
	public static void main(String[] args) throws Exception{
		DatagramSocket ds = new DatagramSocket(10001);
		while(true){
			byte[] buff = new byte[1024];
			DatagramPacket dp = new DatagramPacket(buff,buff.length);
			ds.receive(dp);
			String ip = dp.getAddress().getHostAddress();
			String name = new String(dp.getData(),0,dp.getLength());
			System.out.println(ip+"::"+name);
		}
	}
}

/*
需求：聊天程序：收发同时执行(多线程技术)
	  因收和发动作是不一致的→定义两个run()并封装到不同的类中
*/
class Send implements Runnable{
	private DatagramSocket ds;
	public Send(DatagramSocket ds){
		this.ds = ds;
	}
	public void run(){
		try{
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			String line = null;
			while((line=br.readLine())!=null){
				byte[] buff = line.getBytes();
				DatagramPacket dp = new DatagramPacket(buff,buff.length,InetAddress.getByName("ivan-PC"),10086);
				ds.send(dp);
				if("over".equals(line)){
					break;
				}
			}
		}
		catch(Exception e){
			throw new RuntimeException("send failed");
		}
	}
}
class Receive implements Runnable{
	private DatagramSocket ds;
	public Receive(DatagramSocket ds){
		this.ds = ds;
	}
	public void run(){
		try{
			while(true){
				byte[] buff = new byte[1024];
				DatagramPacket dp = new DatagramPacket(buff,buff.length);
				ds.receive(dp);
				String ip = dp.getAddress().getHostAddress();
				String data = new String(dp.getData(),0,dp.getLength());
				if("over".equals(data)){
					System.out.println(ip+"....离开聊天室");
					break;
				}
				System.out.println(ip+"::"+data);
			}
		}
		catch(Exception e){
			throw new RuntimeException("receive failed");
		}
	}
}
class ChatDemo{
	public static void main(String[] args) throws Exception{
		DatagramSocket sendSocket = new DatagramSocket();
		DatagramSocket receiveSocket = new DatagramSocket(10086);
		
		new Thread(new Send(sendSocket)).start();
		new Thread(new Receive(receiveSocket)).start();
	}
}

/*
需求：给服务端发送一文本数据
思路：
	1，建立socket服务，并指定要连接的主机的端口
*/
class TCPClient{
	public static void main(String[] args) throws Exception{
		//创建客户端的socket服务，指定目的主机的端口
		Socket s = new Socket("ivan-PC",10080);
		//为了发送数据，应该获取socket流中的输出流
		OutputStream os = s.getOutputStream();
		os.write("ca ca ni mei".getBytes());
		s.close();
	}
}

/*
需求：定义断点接收数据并打印在控制台上
思路：
	1，建立socket服务。ServerSocket()，并监听一端口
	2，连接客户端对象。ServerSocket的accept()【阻塞式方法】
	3，服务器使用对应的客户端对象，并获取数据打印于控制台
	4，关闭服务端(可选)
*/
class TCPServer{
	public static void main(String[] args) throws Exception{
		//建立服务端socket服务，并监听一个端口
		ServerSocket ss = new ServerSocket(10080);
		//通过accept()获取链接过来的客户端对象
		while(true){
			Socket s = ss.accept();
			String ip = s.getInetAddress().getHostAddress();
			System.out.println(ip+"......connected");
			//获取客户端发送过来的数据
			InputStream is = s.getInputStream();
			byte[] buff = new byte[1024];
			int len = is.read(buff);
			System.out.println(new String(buff,0,len));
			s.close();
		}
		//ss.close();
	}
}

/*
需求：客户端给服务器发数据，服务端收到后给客户反馈信息
思路：
	1，建立socket服务。指定要连接的主机和端口
	2，获取socket流中的输出流。将数据写到该流中，通过网络发送给服务器
	3，获取socket流中的输出流，将服务器反馈的数据获取到并打印
	4，关闭客户端资源
*/
class TCPClient2{
	public static void main(String[] args)throws Exception{
		Socket s = new Socket("ivan-PC",12001);
		OutputStream os = s.getOutputStream();
		os.write("wo ca ni mei".getBytes());
		InputStream is = s.getInputStream();
		byte[] buff = new byte[1024];
		int len = is.read(buff);
		System.out.println(new String(buff,0,len));
		s.close();
	}
}
class TCPServer2{
	public static void main(String[] args)throws Exception{
		ServerSocket ss = new ServerSocket(12001);
		Socket s = ss.accept();
		String ip = s.getInetAddress().getHostAddress();
		System.out.println(ip+"......connected");
		InputStream is = s.getInputStream();
		byte[] buff = new byte[1024];
		int len = is.read(buff);
		System.out.println(new String(buff,0,len));
		OutputStream os = s.getOutputStream();
		Thread.sleep(10000);
		os.write("watch that".getBytes());
		s.close();
		ss.close();
	}
}

/*
需求：建立一个文本转换服务器。
客户端给服务器发送文本，服务器将文本转换成大写并返给客户端
而且客户端可以不断的进行文本转换，当客户端输入over时转换结束

思路：
	1，建立服务
	2，获取键盘录入
	3，将数据发送给服务器
	4，服务器返回大写数据
	5，关闭资源
*/
class TransClient{
	public static void main(String[] args)throws Exception{
		Socket s = new Socket("ivan-PC",10033);
		//定义读取键盘数据的流对象
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		//定义目的，将数据写入到socket输出流，发给服务端
		PrintWriter pw = new PrintWriter(s.getOutputStream(),true);
		//定义socket读取流，读取服务端返回的大写信息
		BufferedReader brin = new BufferedReader(new InputStreamReader(s.getInputStream()));
		String line = null;
		while((line=br.readLine())!=null){
			if("over".equals(line)){
				break;
			}
			out.println(line);
			String str = brin.readLine();
			System.out.println("server:"+str);
		}
		br.close();
		s.close();
	}
}
class TransServer{
	public static void main(String[] args)throws Exception{
		ServerSocket ss = new ServerSocket(10033);
		Socket s = ss.accept();
		String ip = s.getInetAddress().getHostAddress();
		System.out.println(ip+"......connected");
		//读取socket读取流中的数据
		BufferedReader brin = new BufferedReader(new InputStreamReader(s.getInputStream()));
		//目的socket输出流，将大写数据写入到socket输出流，并发送给客户端
		PrintWriter pw = new PrintWriter(s.getOutputStream(),true);
		String line = null;
		while((line=brin.readLine())!=null){
			System.out.println(line);
			out.println(line.toUpperCase());
		}
		s.close();
		ss.close();
	}
}
/*
该例子出现的问题。
现象：客户端和服务端都在莫名的等待。
为什么呢？
因为客户端和服务端都有阻塞式方法。这些方法么没有读到结束标记。那么就一直等
而导致两端，都在等待。
*/

/*
上传文件
*/
class Upload{
	public static void main(String[] args)throws Exception{
		Socket s = new Socket("ivan-PC",10099);
		BufferedReader br = new BufferedReader(new FileReader("IpDemo.java"));
		PrintWriter pw = new PrintWriter(s.getOutputStream(),true);
		String line = null;
		while((line=br.readLine())!=null){
			out.println(line);
		}
		s.shutdownOutput();
		BufferedReader brin = new BufferedReader(new InputStreamReader(s.getInputStream()));
		String str = bufIn.readLine();
		System.out.println(str);
		bufr.close();
		s.close();
	}
}
class Server{
	public static void main(String[] args) throws Exception{
		ServerSocket ss = new ServerSocket(10099);
		Socket s = ss.accept();
		String ip = s.getInetAddress().getHostAddress();
		System.out.println(ip+"......connected");
		BufferedReader bufIn = new BufferedReader(new InputStreamReader(s.getInputStream()));
		PrintWriter out  = new PrintWriter(new FileWriter("server.txt"),true);
		String line = null;
		while((line=bufIn.readLine())!=null){
			out.println(line);
		}
		PrintWriter pw = new PrintWriter(s.getOutputStream(),true);
		pw.println("上传成功");
		out.close();
		s.close();
		ss.close();
	}
}

