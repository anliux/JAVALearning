# Java介绍

### 目录

<!--GFM-TOC -->
* [发展史](#发展史)
* [Java语言跨平台原理](#java语言跨平台原理)
* [常用dos命令](#常用dos命令)
* [JDK下载安装与路径配置](#jdk下载安装与路径配置)
* [Java程序执行流程](#java程序执行流程)
* [HelloWorld](#helloworld)
* [notepad安装与配置](#notepad安装与配置)
* [其他](#其他)
<!--GFM-TOC -->



## 发展史
- 发展史：SUN->推出各个版本->oracle收购
- Java语言平台：J2SE, J2ME,J2EE



## Java语言跨平台原理
- 平台：操作系统 (windows, linux, mac)
- 跨平台：Java程序可以在任意操作系统上运行，一次编写到处运行
- 原理：实现跨平台需要依赖Java的虚拟机 JVM，在不同的系统安装jvm即可运行Java程序。
- JVM (Java Virtual Machine)：Java虚拟机 
- JRE (Java Runtime Environment)：Java运行环境 = JVM + 核心类库 
- JDK (Jave Development Kit)：Java开发工具包 = JRE + 开发工具
- 概述为：使用JDK写完的开发程序，交给JRE中运行，有JRE中的JVM保证运行



## 常用dos命令
- 打开控制台：win + R，然后cmd回车
- 常用命令
  - d: 回车，盘符切换，切换到d盘
  - dir(directory): 列出当前目录下的文件以及文件夹
  - cd (change directory)改变指定目录(进入指定目录)
    - 进入  cd 目录；cd 多级目录
    - 回退  cd..；cd\ 回退多级 (注：使用单杠’/‘或双杠'//'分割不同级文件夹均可)
  - cls : (clear screen)清屏
  - exit : 退出dos命令行



## JDK下载安装与路径配置
- ### 下载安装
  - 官网下载(建议安装32位版本) -- 傻瓜式安装 -- 完成后不必再装jre

- ### 路径配置
  - 需要让javac和java可以在任意目录下访问。
  - 测试是否配置成功同理。

- ### path配置
  - 创建新的变量名称：JAVA_HOME
    - 计算机-右键属性-高级系统设置-高级-环境变量-系统变量
  - 为JAVA_HOME添加变量值：JDK安装目录
  - 在path环境变量最前面添加如下内容：`%JAVA_HOME%\bin;，则javac可以在任意路径下访问
  - 注意：cmd窗口保持打开时的配置状态，中途重新配置后需要关闭重新打开才会生效。

- ### classpath配置
  - 临时：在cmd窗口中用set设置，可以用于在别人电脑中配置路径，具体操作略。
  - 永久配置：同path配置，此处涉及配置后路径查找顺序问题。

- ### 测试是否配置成功
  - cmd窗口任意目录下键入‘java’回车不报错



## Java程序执行流程
- `.java`源文件 -- 编译器 -- 字节码文件 -- 解释器 -- 控制台显示结果
- 编译器和解释器：bin目录下的javac和java命令，只能在bin目录下访问。
  - `javac + xxx.java` 生成字节码文件；
  - `java + classname` 执行字节码文件，不需要添加`.class`后缀。
- 主方法main：入口方法，用于执行程序。
- 代码常见错误：单词大小写；非法中文字符比如中文分号等。
- 执行流程：
  - `javac xxx.java` --> 编译生成class文件
  - `java xxx` --> 执行class文件



## HelloWorld
```java
public class HelloWorld{
	public static void main(String[] args){
		System.out.println(“HelloWorld”);
	}
}
```



## notepad安装与配置
- 官网下载 -- 傻瓜式安装
- 配置：设置-- 首选项 -- 新建 -- 默认语言与编码: 系统(windows or mac); 默认语言Java；编码ANSI.
- 配置好后，在notepad中写代码比在白板写体验好一些。



## 其他
- eclipse的常规使用、键盘录入等使用详见：[eclipse的基本使用.md](https://github.com/anliux/JAVALearning/blob/master/notes/01-java-base/eclipse%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.md)



### END
