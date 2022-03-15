# Java介绍

### 目录

<!--GFM-TOC -->
* [发展史](#发展史)
* [Java语言跨平台原理](#java语言跨平台原理)
* [常用dos命令](#常用dos命令)
* [JDK下载安装与路径配置](#jdk下载安装与路径配置)
* [Java程序执行流程](#java程序执行流程)
* [notepad安装与配置](#notepad安装与配置)
* [键盘录入](#键盘录入)
* [输出语句](#输出语句)
* [随机数](#随机数)
* [断点调试](#断点调试)
<!--GFM-TOC -->



## 发展史
- 发展史：SUN->推出各个版本->oracle收购
- Java语言平台：J2SE, J2ME,J2EE



## Java语言跨平台原理
- 平台：操作系统 (windows, linux, mac)
- 跨平台：Java程序可以在任意操作系统上运行，一次编写到处运行
- 原理：实现跨平台需要依赖Java的虚拟机 JVM （Java Virtual Machine），在不同的系统安装jvm即可运行Java程序。
- JVM：Java虚拟机
- JRE：Java运行环境 = jvm + 核心类库 
- JDK：Java开发工具包 = jre + 开发工具



## 常用dos命令
- 打开控制台：win + R，然后cmd回车
- 常用命令
  - d: 回车，盘符切换，切换到d盘
  - dir(directory): 列出当前目录下的文件以及文件夹
  - cd (change directory)改变指定目录(进入指定目录)
    - 进入  cd 目录；cd 多级目录
    - 回退  cd..；cd\ 回退多级
  - cls : (clear screen)清屏
  - exit : 退出dos命令行



## JDK下载安装与路径配置
- ### 下载安装
  - 官网下载(建议安装32位版本) -- 傻瓜式安装 -- 完成后不必再装jre

- ### 路径配置
  - 需要让javac和java可以在任意目录下访问。

- ### path配置
  - 创建新的变量名称：JAVA_HOME
    - 计算机-右键属性-高级系统设置-高级-环境变量-系统变量
  - 为JAVA_HOME添加变量值：JDK安装目录
  - 在path环境变量最前面添加如下内容：`%JAVA_HOME%\bin;`

- ### classpath配置
  - 临时：在cmd窗口中用set设置，可以用于在别人电脑中配置路径，具体操作略。
  - 永久配置：同path配置，此处涉及配置后路径查找顺序问题。



## Java程序执行流程
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
  - 接收int数据: `int x = sc.nextInt(); //对象调用方法`
  - 接受String数据：`String s = sc.nextLine(); //获取键盘录入的字符串数据`

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



## 断点调试
- ### 断点：
  - 一个标记

- ### 作用：
  - 查看程序的执行流程；
  - 调试程序。

- ### 加断点
  - 哪里加：想看哪个语句的执行结果就在该语句前面加(哪里不会加哪里)。
  - 如何加：代码区域左边的空白位置 双击即可。

- ### 运行加断点的程序
  - 代码区域右键 -- Debug as -- Java Application
  - 显示一个页面，提示是否进入调试页面？ 是否记住当前操作？是(Yes)是（勾选复选框）

- ### debug执行：
  - step over：按照代码流程执行
    - 法一：点击 工具栏中的Step Over (执行下一行)
    - 法二：快捷键F6 看到每一步程序的执行过程
    - 下同有此两种方法。
  - step into：进入本行代码调用的方法中
    - 可以用于当有调用方法，但是被调用方法没有设置断点的情况。
  - step return：从被调用函数返回调用被方法的代码行。
    - 可以用于从被调用函数返回调用该方法的代码行。

- ### 重点关注区域：
  - 看代码区域：对照看程序执行步骤；
  - 看Debug区域：对照看程序执行步骤；
  - 看varable区域：观察变量的创建、赋值、销毁；
    - 引用型变量的值后面会有一个(id=xx)，可以看作对象地址值。
  - 看console区域：看程序的输入输出。

- ### debug停止
  - debug完毕后，需要保证本次debug停止，即左上方菜单栏的红色停止按钮为灰；
  - 自动停止：一直"step over"会自动停止；
  - 手动停止：按左上方菜单栏的红色停止按钮。
    - 注意：如果不停止，会在java代码界面的行号位置出现蓝色debug箭头并显示`Debug Current Instruction Pointer`，影响之后的debug。
  - debug停止之后，记得删除断点。

- ### 消除断点：
  - 法一：把设置断点的方式再执行一遍；
  - 法二：切换到Debug视图，选择 Breakpoints -- Remove All Breakpoints 就是2个XX的图标
    - 注：如果上面最小化了，这里重新打开debug视图

- ### 注意：
  - 断点必须加在有效的语句上。
    - 例如：如果在注释行加断点，则会自动加在注释下的第一个有效语句行。

- ### debug示例：
  - for循环执行流程：
    - 观察变量：for循环中不再使用的临时变量在退出循环后就消失了，以示使用完毕。
  - 方法调用流程：
    - 想看被调用方法的执行流程，则被调用方法也需要加断点；
    - 如果被调用方法中不加断点，则需要在用到该方法的代码行使用"step into"，以手动进入。
    - debug执行到带有输入的语句时：如果不在控制台输入，则step over按钮变灰，等待输入完成。



### END
