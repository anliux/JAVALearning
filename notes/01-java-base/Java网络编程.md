# Java网络编程


### 目录

<!--GFM-TOC -->
* [网络编程概述](#网络编程概述): 计算机网络, 网络编程, Socket套接字, 网络编程三要素(IP, 端口号, 传输协议), UDP与TCP协议 
* [InetAddress](#inetaddress): InetAddress概述, InetAddress常用方法 (getAllByName, getByName, getHostAddress, getHostName, getLocalHost)
* [UDP协议收发数据](#UDP协议收发数据): UDP收发数据的特点和步骤, DatagramSocket类, DatagramPacket类, UDP收发数据的代码示例, 注意事项
* [TCP协议收发数据](#TCP协议收发数据): TCP收发数据的特点和步骤, Socket类, ServerSocket类, TCP收发数据的代码示例, TCP收发数据并返回的案例分析
* [模拟用户登录](#模拟用户登录): 题目, 收发步骤, 收发代码示例, 改进(更加面向对象 + 数据库思想)
<!--GFM-TOC -->



## 网络编程概述
- ### 计算机网络
  - 是指将地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，
  - 在网络操作系统，网络管理软件及网络通信协议的管理和协调下，
  - 实现资源共享和信息传递的计算机系统

- ### 网络编程
  - 就是用来实现网络互连的不同计算机上运行的程序间可以进行数据交换
    - 又称Socket编程或套接字编程
  - 网络编程的底层：IO流

- ### Socket(套接字)  
  - 用于描述IP地址和端口，是一个通信链的句柄。
    - 在Internet上的主机一般运行了多个服务软件，同时提供几种服务。
    - 每种服务都打开一个Socket，并绑定到一个端口上，
    - 不同的端口对应于不同的服务。
  - Socket：
    - 就是为网络编程提供的一种机制；
    - 通信的两端都有Socket；
    - 网络通信其实就是Socket间的通信；
    - 数据在两个Socket间通过IO传输。

- ### 网络通信三要素
  - IP地址: InetAddress
    - 网络中设备的标识，不易记忆，可用主机名
    - 类似'192.168.1.1'：点分十进制表示法
  - 端口号：
    - 用于标识进程的逻辑地址，不同进程的标识
  - 传输协议：
    - 通讯的规则
    - 常见协议：TCP，UDP

- ### IP地址：
  - 要想让网络中的计算机能够互相通信，必须为每台计算机指定一个标识号，通过这个标识号来指定要接受数据的计算机和识别发送的计算机，
  - 在TCP/IP协议中，这个标识号就是IP地址
  - IP地址分为网络地址和主机地址：
    - 通过这两个地址来确保IP地址的全球唯一性 
  - IPv4和IPv6：
    - IPv4: 4个字节可能不够用
    - IPv6: 16个字节可以用很久了
  - 公共地址和内网(局域网)地址
    - 根据安全性不同可以分为这两种 
  - 如何获取和操作IP地址呢？
    - 为了方便对IP地址的获取和操作，java提供了一个 类InetAddress 供我们使用
  - cmd窗口查询：ipconfig
    - 注：mac系统不灵 
  
- ### 端口号
  - 物理端口: 网卡口
  - 逻辑端口: 我们指的就是逻辑端口
    - 每个网络程序都会至少有一个逻辑端口
    - 用于标识进程的逻辑地址，不同进程的标识
    - 有效端口：0~65535，其中0~1024系统使用或保留端口
  - 可以通过360软件可以查看端口号

- ### 传输协议
  - UDP协议
    - 将数据源和目的封装成数据包中，不需要建立连接；
    - 每个数据报的大小在限制在64k；
    - 因无连接，是不可靠协议；
    - 不需要建立连接，速度快
  - TCP协议
    - 建立连接，形成传输数据的通道；
    - 在连接中进行大数据量传输；
    - 通过三次握手完成连接，是可靠协议；
    - 必须建立连接，效率会稍低
  - 三次握手：
    - A-B：A给B发送数据
    - B-A：B收到A发送的数据，再给A发送一条数据
    - A-B：A收到B发送的数据后，再给B发送一条自己收到了的数据

- ### UDP与TCP协议 
  - UDP协议：
    - DatagramSocket与DatagramPacket
    - 建立发送端，接收端。
    - 建立数据包。
    - 调用Socket的发送接收方法。
    - 关闭Socket。
    - 发送端与接收端是两个独立的运行程序。
  - TCP协议：
    - Socket和ServerSocket
    - 建立客户端和服务器端
    - 建立连接后，通过Socket中的IO流进行数据的传输
    - 关闭socket
    - 同样，客户端与服务器端是两个独立的应用程序
    - 注：
      - TCP协议中的数据传输管道：指IO流 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## InetAddress 
- ### InetAddress概述
  - 此类表示互联网协议 (IP) 地址。
    - IP 地址是 IP 使用的 32 位或 128 位无符号数字，它是一种低级协议，UDP 和 TCP 协议都是在它的基础上构建的
    - "32 位或 128 位" 分别对应IPv4和IPv6
  - java.net包下
  - 子类：Inet4Address, Inet6Address
  - 无构造方法：静态调用或子类实现

- ### InetAddress常用方法
  - `static InetAddress[] getAllByName(String host)`: 
    - 静态，类名调用
    - 在给定主机名的情况下，根据系统上配置的名称服务返回其 IP 地址所组成的数组。
    - 返回数组：是因为主机名不唯一，可能返回多个IP地址
  - `static InetAddress	getByName(String host)`:
    - 静态，类名调用
    - throws UnknownHostException
    - 在给定主机名的情况下确定主机的 IP 地址。
      - 即传入主机名，返回主机名和IP地址 
    - 注：此方法，如果传入的是IP地址，则获取到的是IP地址
    - 代码示例：
    ```java
      import java.net.InetAddress;
      import java.net.UnknownHostException;

      public class InetAddressDemo {
        public static void main(String[] args) throws UnknownHostException {
          //分别传入主机名和IP地址
          InetAddress address = InetAddress.getByName("Mac_liuxuan");
          System.out.println(address);//Mac_liuxuan/192.168.0.106
          
          InetAddress address2 = InetAddress.getByName("192.168.0.106");
		      System.out.println(address2);//192.168.0.106
        }
      }    
    ```
  - `String getHostAddress()`
    - 非静态，对象调用
    - 返回 IP 地址字符串（以文本表现形式）
    - 代码示例：getByName传入的参数不同，获取到的结果都是IP地址
      - getByName(主机名)或getByName(IP地址)：getHostAddress()获取到的都是IP地址
    ```java
    InetAddress address = InetAddress.getByName("Mac_liuxuan"); 
    String hostAddress = address.getHostAddress();//192.168.0.106`    
    ```
    
    ```java
    InetAddress address2 = InetAddress.getByName("192.168.0.106");
    String hostAddress = address2.getHostAddress();//192.168.0.106
    ```
  - `String getHostName()`: 
    - 非静态，对象调用
    - 获取此 IP 地址的主机名
    - 代码示例：getByName传入的参数不同，获取到的结果不同
      - getByName(主机名)：getHostName()获取主机名
      - getByName(IP地址)：getHostName()仍然获取IP地址
    ```java
    InetAddress address = InetAddress.getByName("Mac_liuxuan"); 
    String hostName = address.getHostName();//Mac_liuxuan
    ```
    
    ```java
    InetAddress address2 = InetAddress.getByName("192.168.0.106");
    String hostName = address2.getHostName();//192.168.0.106
    ```
  - `static InetAddress	getLocalHost()`: 
    - 静态，类名调用
    - 返回本地主机的 IP 地址。
    - 示例：
      - `InetAddress adds = InetAddress.getLocalHost(); System.out.println(adds);//Mac_liuxuan/192.168.0.106`
    - 与`static InetAddress getByName(String host)`的区别：
      - getByName: 可以返回其他的IP地址，比如别的主机的IP地址
      - getLocalHost: 只能获取本机的IP地址

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## UDP协议收发数据
- ### UDP协议收发数据分析 
  - 回顾UDP协议收发数据的特点：
    - 打包发送数据：将数据和地址、长度、端口都打包到一起
    - 不建立连接，只管发送，不管是否收到
    - 每个数据包有大小限制：64k
  - UDP协议发送数据的步骤
    - 创建发送端的Socket对象
    - 创建数据并打包
    - 发送数据
    - 释放资源
  - UDP协议接收数据的步骤
    - 创建接收端的Socket对象
    - 接收数据
    - 解析数据
    - 输出数据
    - 释放资源

- ### 注：datagram
  - 数据报的意思 

- ### DatagramSocket类
  - 此类表示用来发送和接收数据报包的套接字。
  - 在 DatagramSocket 上总是启用 UDP 广播发送. 即基于UDP协议
  - 构造方法：
    - `DatagramSocket()`: 
      - 构造数据报套接字并将其绑定到本地主机上任何可用的端口。随机分配端口
      - 发送端可用
    - `DatagramSocket(int port)`: 
      - 创建数据报套接字并将其绑定到本地主机上的指定端口。
      - 接收端可用
    - `new DatagramSocket();`: 会抛出异常SocketException, 其父类是IOException

- ### DatagramPacket类
  - 由DatagramSocket对象调用的send方法查看源码得知，send传入的是DatagramPacket对象
  - 此类表示数据报包。数据报包用来实现无连接包投递服务
  - 构造方法：
    - `DatagramPacket(byte[] buf, int length, InetAddress address, int port)`:
      - 构造数据报包，用来将长度为 length 的包发送到指定主机上的指定端口号。
      - 可用于发送端打包
      - 具备UDP收发数据的数据包需要的各种参数：数据，长度，IP，端口...
        - 数据：`byte[] buf`
        - 设备的地址：IP
        - 进程的地址：端口号
    - `DatagramPacket(byte[] buf, int length)`
      - 简单的构造方法，可用于接收端接收数据 
  - 解析接收到的数据：
    - 可用以下几个getXxx()方法 
  - `InetAddress getAddress()`:
    - 返回某台机器的 IP 地址，此数据报将要发往该机器或者是从该机器接收到的。 
    - 获取发送端的IP地址
  - `byte[] getData()`: 
    - 返回数据缓冲区，即用字节数组接收发送来的数据
    - 也可以直接使用创建包对象时的数组
  - `int getLength()`:
    - 返回将要发送或接收到的数据的长度
    - 获取具体收到的字节的个数

- ### UDP收发数据的代码示例
  - 发送端
    ```java
	//SendDemo.java
	import java.io.IOException;
	import java.net.DatagramPacket;
	import java.net.DatagramSocket;
	import java.net.InetAddress;
	import java.net.SocketException;

	public class SendDemo {
		public static void main(String[] args) throws SocketException, IOException {
			//创建发送端Socket对象
			DatagramSocket ds = new DatagramSocket();

			//创建数据并打包
			//DatagramPacket(byte[] buf, int length, InetAddress address, int port) 
			String s = "Hello UDP, im coming!";
			byte[] bys = s.getBytes();
			int length = bys.length;
			InetAddress address = InetAddress.getByName("Mac_liuxuan");
			int port = 8888;//接收端是什么就是哪个端口号
			//打包
			DatagramPacket dp = new DatagramPacket(bys,length,address,port);

			//发送数据
			ds.send(dp);

			//释放资源
			ds.close();		
		}
	}    
    ```
  - 接收端 
    ```java
	import java.io.IOException;
	import java.net.DatagramPacket;
	import java.net.DatagramSocket;
	import java.net.InetAddress;

	public class ReceiveDemo {
		public static void main(String[] args) throws IOException {
			//创建接收端Socket对象
			DatagramSocket ds = new DatagramSocket(8888);

			//接收数据
			byte[] bys = new byte[1024];
			DatagramPacket dp = new DatagramPacket(bys,bys.length);

			System.out.println("阻塞前");
			ds.receive(dp);//阻塞中
			System.out.println("阻塞后");

			//解析数据
			InetAddress address = dp.getAddress();//获取IP地址
			byte[] data = dp.getData();//获取数据
			int length = dp.getLength();//获取发送或接收到的数据的长度

			//输出数据
			System.out.println("sender:"+address.getHostAddress());
			System.out.println(new String(data,0,length));//加length防止输出上面字节数组的1024个元素，即后面的空字符(直接复制会有)
			System.out.println(new String(bys,0,length)); //或者直接输出接收数据的字节数组也可
			/* 阻塞前
				阻塞后
				sender:192.168.0.106
				Hello UDP, im coming!
			*/

			//释放资源
			ds.close();	
		}
	}    
    ```
  - 注意：
    - 需要先启动接收端，再启动发送端
    - 接收端卡在此条语句：`ds.receive(dp);//阻塞中` -- 阻塞
      - 接收端开始运行后，程序会在receive()方法这里有一个阻塞，即等待 
  - 注意控制台：多条程序会有多个控制台
    - 接收数据的结果在ReceiveDemo.java的控制台可以看到

- ### UDP收发数据的注意事项
  - 端口号错误：不报错，但是数据收不到
    - 对比主机名异常：会报错抛异常`java.net.UnknownHostException`
  - 接收端程序在运行的过程中，再次启动接收端程序，则抛异常：
    - `java.net.BindException: Address already in use (Bind failed)`
    - 该端口已经在使用中了，再次运行，已占用，绑定失败，抛异常
    - 端口号：标记线程，不能重复，否则就不知道指的是哪条进程了
    - 同理，需要注意常见程序已占用的端口号，否则同样会抛上述异常

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## TCP协议收发数据
- ### TCP协议收发数据分析
  - 回顾TCP协议收发数据的特点：
    - 必须建立连接，形成传输数据的通道；
    - 在连接中进行大数据量传输: 没有大小限制了
    - 通过三次握手完成连接
  - TCP协议发送数据的步骤(客户端)
    - 创建发送端Socket对象（创建连接）
    - 获取输出流对象
    - 发送数据
    - 释放资源
  - TCP协议接收数据的步骤(服务端)
    - 创建接收端Socket对象(ServerSocket类)
    - 监听(阻塞)：等着客户端过来
    - 获取输入流对象
    - 获取数据
    - 输出数据
    - 释放资源

- ### Socket类
  - java.net.Socket包下
  - 此类实现客户端套接字（也可以就叫“套接字”）。
    - 套接字是两台机器间通信的端点。
  - 构造方法：`Socket(InetAddress address, int port)` 
    - 创建一个流套接字并将其连接到指定 IP 地址的指定端口号。
    - 是所需的构造方法和参数

- ### ServerSocket类
  - java.net.ServerSocket包
  - 此类实现服务器套接字，可用于TCP接收端
    - 服务器套接字等待请求通过网络传入。它基于该请求执行某些操作，然后可能向请求者返回结果。
  - 构造方法：`ServerSocket(int port)` 
    - 创建绑定到特定端口的服务器套接字。
    - 这个有参构造适用于TCP接收端
  - `Socket accept()`:
    - 侦听并接受到此套接字的连接。
    - 由于需要操作输入流输出流，而ServerSocket并没有相关的方法，因此需要先获取到Socket

- ### TCP协议收发数据代码
  - 发送端/客户端
      ```java
  	//ClientDemo.java
	import java.io.IOException;
	import java.io.OutputStream;
	import java.net.InetAddress;
	import java.net.Socket;

	public class ClientDemo {
		public static void main(String[] args) throws IOException{
			//发送数据
			//创建发送端Socket对象（创建连接）
			Socket s = new Socket(InetAddress.getByName("Mac_liuxuan"),9999);
			//获取输出流对象: 需要一个可以传送任意类型数据的IO流
			OutputStream os = s.getOutputStream();
			//发送数据
			String str = "hello TCP, im coming";
			os.write(str.getBytes());
			//释放资源
			os.close();//这条不关也可，s.close()会帮助做这条
			s.close();

			//没有连接到接收端时报错：
			//java.net.ConnectException: Connection refused
		}
	}  
      ```
  - 接收端/服务端
      ```java
	//ServerDemo.java
	import java.io.IOException;
	import java.io.InputStream;
	import java.net.InetAddress;
	import java.net.ServerSocket;
	import java.net.Socket;

	public class ServerDemo {
		public static void main(String[] args) throws IOException {
			//接收数据
			//创建接收端Socket对象(等待连接)
			ServerSocket ss = new ServerSocket(9999);
			//监听(阻塞)
			Socket s = ss.accept();
			//获取输入流对象
			InputStream is = s.getInputStream();
			//获取数据
			byte[] bys = new byte[1024];
			int len;//用于存储读到的字节个数
			len = is.read(bys);
			//输出数据
			InetAddress address = s.getInetAddress();
			System.out.println("client:" + address.getHostName());//192.168.0.106 - 似乎应该返回主机名但仍是IP地址
			System.out.println(new String(bys,0,len));//hello TCP, im coming
			//释放资源
			s.close();
			ss.close();//服务端可以不关
		}
	}  
      ```

- ### TCP收发数据并返回的案例分析
  - 题目：
    - 使用TCP协议发送数据，并将接收的数据转换成大写返回 
  - 步骤：
    - 客户端发出数据；
    - 服务端接收数据；
    - 服务端转换数据；
    - 服务端发出数据；
    - 客户端接收数据 
  - 注意：
    - 客户端和服务端交换功能以后，步骤仍是相似的
    - 代码运行之后：
      - 客户端(发送端)的控制台也会输出一条接收到的数据 
  - 代码示例：
    - 发送端/客户端代码：
    ```java
	//ClientDemo.java
	import java.io.IOException;
	import java.io.InputStream;
	import java.io.OutputStream;
	import java.net.InetAddress;
	import java.net.Socket;

	public class ClientDemo {
		public static void main(String[] args) throws IOException{
			//创建发送端Socket对象
			Socket s = new Socket(InetAddress.getByName("Mac_liuxuan"),9999);
			//获取输出流对象
			OutputStream os = s.getOutputStream();
			//发送数据
			os.write("tcp, im coming again!!".getBytes());

			//接收返回的大写数据: 与接收端接收数据的步骤相同
			//获取输入流对象
			InputStream is = s.getInputStream();
			byte[] bys = new byte[1024];//接收数据
			int len;//存储读取到的字节个数
			//获取数据
			len = is.read(bys);

			//输出数据
			System.out.println(new String(bys,0,len));//TCP, IM COMING AGAIN!!

			//释放资源
			s.close();
		}
	}    
    ```
    - 接收端/服务端代码：
    ```java
	//ServerDemo.java
	import java.io.IOException;
	import java.io.InputStream;
	import java.io.OutputStream;
	import java.net.ServerSocket;
	import java.net.Socket;

	public class ServerDemo {
		public static void main(String[] args) throws IOException {
			//创建接收端Socket对象
			ServerSocket ss = new ServerSocket(9999);
			//监听
			Socket s = ss.accept();
			//获取输入流对象
			InputStream is = s.getInputStream();
			//获取数据
			byte[] bys = new byte[1024];
			int len;
			len = is.read(bys);
			String str = new String(bys,0,len);
			//输出数据
			System.out.println(str);//tcp, im coming again!!

			//转换数据
			String upperStr = str.toUpperCase();//s中的内容转换为大写

			//获取输出流对象：传输数据是通过IO流
			OutputStream os = s.getOutputStream();
			//返回数据(即发出数据)
			os.write(upperStr.getBytes());

			//释放资源
			s.close();
			ss.close();//服务端一般不关闭
		}
	}    
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 模拟用户登录
- ### 题目：
  - 模拟用户登录

- ### 收发的步骤
  - 客户端/发送端的步骤：
    - 创建客户端Socket对象
    - 获取用户名和密码
    - 写出数据
    - 获取输入流对象
    - 获取服务器返回的数据
    - 释放资源
  - 服务端/接收端的步骤： 
    - 创建服务器端Socket对象
    - 监听
    - 获取输入流对象
    - 获取用户名和密码
    - 判断用户名和密码是否正确
    - 返回判断信息
    - 释放资源 

- ### 收发代码示例：
  - 客户端/发送端代码：
      ```java
	//ClientTest.java
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.PrintWriter;
	import java.net.Socket;

	public class ClientTest {
		public static void main(String[] args) throws IOException{
			//创面客户端Socket对象
			//Socket s = new Socket(InetAddress(),8888);
			Socket s = new Socket("Mac_liuxuan",8888);//查看底层代码可知，直接传入主机名也可，会自动传入上一行代码所示InetAddress()中

			//获取用户名和密码：使用输入流
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));//标准格式，可以记下来直接用
			System.out.println("请输入用户名：");
			String username = br.readLine();
			System.out.println("请输入密码：");
			String password = br.readLine();

			//获取输出流对象
			//BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(s.getOutputStream()));
			//嫌麻烦的话，下述打印流可以直接打印数据，且可以换行
			PrintWriter out = new PrintWriter(s.getOutputStream(),true);//参数true表示自动换行
			//写出数据
			out.println(username);
			out.println(password);

			//获取输入流对象
			BufferedReader serverBr = new BufferedReader(new InputStreamReader(s.getInputStream()));
			//获取服务器返回的数据
			String result = serverBr.readLine();
			System.out.println(result);
			//释放资源
			s.close();
			/*
				请输入用户名：
				admin
				请输入密码：
				123456
				登录失败

				请输入用户名：
				itheima
				请输入密码：
				123456
				登录成功
			 * */
		}
	}  
      ```
  - 服务端/接收端代码：
      ```java
	//ServerTest.java
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.PrintWriter;
	import java.net.ServerSocket;
	import java.net.Socket;

	public class ServerTest {
		public static void main(String[] args) throws IOException {
			//创建服务器端Socket对象
			ServerSocket ss = new ServerSocket(8888);
			//监听
			Socket s = ss.accept();
			//获取输入流对象
			BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
			//获取用户名和密码
			String username = br.readLine();
			String password = br.readLine();
			//判断用户名和密码是否正确
			boolean flag = false;
			if("itheima".equals(username) && "123456".equals(password)) {
				flag = true;
			}
			//获取输出流对象
			PrintWriter out = new PrintWriter(s.getOutputStream(),true);

			//返回判断信息
			if(flag) {
				out.println("登录成功");
			}else {
				out.println("登录失败");
			}

			//释放资源
			s.close();
			//ss.close();//服务器端不关闭，你不用别人可能还要用
		}
	}  
      ```

- ### 改进
  - 上述代码中，对正确的用户名和密码进行了写死，不符合实际需求。
  - 改进：
    - 加入数据库思想，另建User类和UserDB类，放入若干用户名和密码 
  - User类：
      ```java
	public class User {
		private String username;//用户名
		private String password;//密码
		public User() {
			super();
			// TODO Auto-generated constructor stub
		}
		public User(String username, String password) {
			super();
			this.username = username;
			this.password = password;
		}
		public String getUsername() {
			return username;
		}
		public void setUsername(String username) {
			this.username = username;
		}
		public String getPassword() {
			return password;
		}
		public void setPassword(String password) {
			this.password = password;
		}

		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			User other = (User) obj;
			if (password == null) {
				if (other.password != null)
					return false;
			} else if (!password.equals(other.password))
				return false;
			if (username == null) {
				if (other.username != null)
					return false;
			} else if (!username.equals(other.username))
				return false;
			return true;
		}
	}  
      ```
  - UserDB类：
      ```java
	import java.util.ArrayList;
	import java.util.List;

	public class UserDB {
		private static List<User> users = new ArrayList<User>();//因为要用下面的静态代码块初始化，这里也定义为static

		static {//在类加载时初始化
			users.add(new User("zhangsan","123456"));
			users.add(new User("lisi","888888"));
			users.add(new User("itheima","123456"));
			users.add(new User("admin","password"));

		}

		public static List<User> getUsers(){
			return users;
		}
	}  
      ```
  - ServerSocket改进代码：
      ```java
	/*
	if("itheima".equals(username) && "123456".equals(password)) {//写死的用户名和密码
		flag = true;
	}*/

	//改进代码：
	List<User> users = UserDB.getUsers();
	User user = new User(username, password);
	if(users.contains(user)) {//查看contains方法的实现源码发现涉及equals，需要重写此equals()方法
				//ctrl+contains -- implement -- ArrayList -- ..
		//匹配成功
		flag = true;
	}  
      ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
