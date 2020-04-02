# Java介绍

### 目录

<!--GFM-TOC -->
* []()
* []()
* []()
* []()
* []()
* []()
* []()
* []()
* []()


<!--GFM-TOC -->



## 发展史


## Java语言跨平台原理
- 平台：操作系统
- 跨平台：Java程序可以在任意操作系统上运行，一次编写到处运行
- 原理：实现跨平台需要依赖Java的虚拟机 JVM （Java Virtual Machine），在不同的系统安装jvm即可运行Java程序。
- JVM：Java虚拟机
- JRE：Java运行环境 = jvm + 核心类库 
- JDK：Java开发工具包 = jre + 开发工具


## 常用dos命令
- 打开控制台：win + R，然后cmd回车
- 常用命令
  - d: 回车，盘符切换，切换到d盘
  - dir(directory):列出当前目录下的文件以及文件夹
  - cd (change directory)改变指定目录(进入指定目录)
    - 进入  cd 目录；cd 多级目录
    - 回退  cd..；cd\ 回退多级
  - cls : (clear screen)清屏
  - exit : 退出dos命令行


## JDK下载安装与路径配置
- 官网下载(建议安装32位版本) -- 傻瓜式安装 -- 完成后不必再装jre


## 路径配置
- 需要让javac和java可以在任意目录下访问。
- ### path配置
  - 创建新的变量名称：JAVA_HOME
    - 计算机-右键属性-高级系统设置-高级-环境变量-系统变量
  - 为JAVA_HOME添加变量值：JDK安装目录
  - 在path环境变量最前面添加如下内容：`%JAVA_HOME%\bin;`
- ### classpath配置
  - 临时：在cmd窗口中用set设置，可以用于在别人电脑中配置路径，具体操作略。
  - 永久配置：同path配置，此处涉及配置后路径查找顺序问题。


## Java程序流程图
- `.java`源文件 -- 编译器 -- 字节码文件 -- 解释器 -- 控制台显示结果
- 编译器和解释器：bin目录下的javac和java命令，只能在bin目录下访问。
  - `javac + xxx.java` 生成字节码文件；
  - `java + classname` 执行字节码文件，不需要添加`.class`后缀。
- 主方法main：入口方法，用于执行程序。
- 代码常见错误：单词大小写；非法中文字符比如中文分号等。


## notepad安装与配置
- 官网下载 -- 傻瓜式安装
- 配置：设置-- 首选项 -- 新建 -- 默认语言与编码


## 键盘录入
- ### 使用步骤：
  - 导包：手动`import java.util.Scanner;` 快捷键：`ctrl+shift+o`
    - 位置放到class定义的上面：`package>import>class`
  - 创建对象: `Scanner sc = new Scanner(System.in);`
  - 接收数据: `int x = sc.nextInt(); //对象调用方法`

- ### 参考链接：
  - [github: OJ输入输出总结](https://github.com/anliux/PracticePool/blob/master/base/docs/io.md)

## 输出语句
- println():ln是换行。
- 可以在println()的括号中添加分隔符：比如制表符`\t`

## 随机数
- ### 作用：用于产生一个随机数

- ### 使用步骤(和Scanner类似)
  - 导包：`import java.util.Random;`
  - 创建对象：`Random r = new Random();`
  - 获取随机数：`int number = r.nextInt(10);`
    - 产生的数据在0到10之间，包括0，不包括10。(惯例左闭右开)
    - 括号里面的参数n：产生0-n的左闭右开区间内的数据。
  - 产生1-100的随机数：`int i = r.nextInt(100)+1;`

