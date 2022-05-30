# Java网络编程


### 目录

<!--GFM-TOC -->
* [网络编程概述](#网络编程概述): 计算机网络, 网络编程, Socket套接字, 网络编程三要素(IP, 端口号, 传输协议), UDP与TCP协议 
* [InetAddress](#inetaddress): 
* [](#): 
* [](#): 
* [](#): 
<!--GFM-TOC -->



## 网络编程概述
- ### 计算机网络
  - 是指将地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，
  - 在网络操作系统，网络管理软件及网络通信协议的管理和协调下，
  - 实现资源共享和信息传递的计算机系统

- ### 网络编程
  - 就是用来实现网络互连的不同计算机上运行的程序间可以进行数据交换
  - 又称Socket编程或套接字编程

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
  - `static InetAddress[]	getAllByName(String host)`: 
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
      - getByName(主机名)：获取主机名
      - getByName(主机名)：仍然获取IP地址
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
    - 在连接中进行大数据量传输；
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

- ### TCP协议接收数据
  - 


- ### TCP收发数据的注意事项
  - 




<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->







### END
