# eclipse的基本使用


## 目录：
<!--GFM-TOC -->
* [eclipse的概述](#eclipse的概述)
* [图文参考链接](#图文参考链接)
* [基本使用](#基本使用)
* [基本配置](#基本配置)
* [快捷键](#快捷键)
* [删除和导入项目](#删除和导入项目)
* [自动生成代码](#自动生成代码)
* [已创建类的重命名](#已创建类的重命名)
* [键盘录入](#键盘录入)
* [输出语句](#输出语句)
* [随机数](#随机数)
* [断点调试](#断点调试)
<!--GFM-TOC -->



## eclipse的概述
- 是一个集成开发环境 IDE (integrated development environment)
- 集成了代码的编写功能，分析功能，编译功能，调试功能等一体化的开发软件。
- 特点：免费，纯Java语言编写，免安装(解压使用)，扩展性强(可以添加各种功能的插件)
- 下载和安装：http://eclipse.org/ ; 绿色版，解压就可以使用。
- 使用：
  - exe启动 - workspace选择 - 新建project项目(项目配置) - 新建package包(注意命名唯一性) - 包新建class类(类配置) - 写代码(实时编译，只需手动运行即可) - 运行 (run as: java application) - 下方控制台显示结果 
  - 详见下方第一个图文参考博文

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 图文参考链接
- [【JAVA】eclipse-使用入门及常用快捷键](https://www.cnblogs.com/anliux/p/11525981.html)
- [【学习总结】Eclipse常用快捷键](https://www.cnblogs.com/anliux/p/11436568.html)	

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 基本使用
	A:创建Java项目：
		点击File或者在最左侧空白处，选择Java项目，在界面中写一个项目名称，然后Finish即可。
	B:创建包：展开项目，在**源包src下**建立一个包com.itheima
	C:创建类：在com.ithiema包下建立一个类HelloWorld
		在界面中写一个类名：HelloWorld，然后finish即可。
	D:编写代码
		在HelloWorld类写main方法，在main方法中写一条输出语句：我是黑马程序员，我骄傲，我自豪。
	E:编译
		自动编译，在保存的那一刻帮你做好了
	F:运行
		选择要运行的文件或者在要运行的文件内容中
		右键 -- Run as - Java Application即可

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 基本配置
	A:行号的显示和隐藏
		显示：在代码区域的最左边的空白区域，右键 -- Show Line Numbers即可。
		隐藏：把上面的动作再做一次。
			
	B:字体大小及颜色
		a:Java代码区域的字体大小和颜色：
			window -- Preferences -- General -- Appearance -- Colors And Fonts -- Java -- Java Edit Text Font
		b:控制台
			window -- Preferences -- General -- Appearance -- Colors And Fonts -- Debug -- Console font
		c:其他文件
			window -- Preferences -- General -- Appearance -- Colors And Fonts -- Basic -- Text Font
		- mac里的字体编辑：(相似，大致一样，有一些不同)
			Eclipse(上方第一个) -- Preferences -- Genaral -- Appearance -- Colors and Fonts -- Basic -- Text Font -- edit或双击进行选择 -- ...
			
	C:窗体给弄乱了，怎么办?
		window -- Perspective -- Reset Perspective
			
	D:控制台找不到了，怎么办?
		Window--Show View—Console

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->


		
## 快捷键

	内容辅助键	alt+/  (Mac: option+/ 效果同)
		main	然后alt+/
		syso	然后alt+/
  
	提供解决方案	ctrl+1（数字1）
		对小红叉提供解决方案：导包；异常处理；光标定位变量并重命名。
		大红叉是语法错误，必须修改代码。
	
	快捷键
		注释
			单行	选中内容，ctrl+/ (Mac: command+/), 再来一次取消
			多行	选中内容，ctrl+shift+/ (Mac: Shift+command+/), 取消 ctrl+shift+\
			- Mac多行快捷键不灵，设置以后仍然是没反应，还取消了系统原来的help，先这样吧。。
			- [mac下设置多行注释快捷键](https://www.cnblogs.com/maijunjin/archive/2013/04/24/3039463.html)
		格式化	ctrl+shift+f 或者 右键 -- source -- format
		导包    ctrl+shift+o
		
		光标	shift+enter	将光标切换至下一行起始处。
		复制	ctrl+alt+向上箭头	光标处代码向上复制
			 ctrl+alt+向下箭头	光标处代码向下复制
		移动	ctrl+向上/向下箭头	光标处的代码向上或向下移动
		删除	ctrl+d	删除选中行
				注：单行光标定位，多行选中，可不全选
		
		大小写	ctrl+shift+x	选中部分全部大写
			  ctrl+shift+y	选中部分全部小写
		
		source	alt+shift+s	调出source快捷菜单
		看源码	光标定位+ctrl+双击	打开定位处的源码 
		代码结构查看和检索    ctrl/command + o: 展示代码结构(类、变量、方法等)，搜索输入可以查找
		
		快速抽取函数       win: alt+shift+M / Mac: option+command+M

		打印	选中+alt+/：可选自动把选中部分放入输出语句中
				    即，可以通过生成的菜单选中sysout将选中语句放入输出语句
		tab	tab或者shift+tab	选中代码整体后移或者前移

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 删除和导入项目
	A:删除项目
		选中项目 – 右键 – 删除
			从项目区域中删除
			从硬盘上删除
	B:导入项目
		在项目区域右键找到import
		找到General，展开，并找到
			Existing Projects into Workspace
		点击next,然后选择你要导入的项目
			注意：这里选择的是项目名称

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 自动生成代码
	A：自动生成构造方法：
		代码区域右键 -- Source -- Generate Constructors from Superclass.. ： 无参构造函数
		代码区域右键 -- Source -- Generate Constructors using Fields...: 带参构造函数
	B：自动生成get、set方法：
		代码区域右键 -- Source -- Generate Getters and Setters.. -- select all
	C：自动重写toString 和 equals方法：
		代码区域右键 -- Source -- Generate toString -- 选择变量 -- 自动生成重写的toString方法 
		代码区域右键 -- Source -- Generate HashCode() and equals() -- 选择变量 -- 自动生成重写的两个方法

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 已创建类的重命名
- 1.首先要进行选中java类名称，然后进行右键
- 2.弹出了下拉菜单中,进行选择为refactor的选项。
- 3.弹出了下一个菜单中进行选择为rename的选项。
- 4.弹出了一个提示,那么就可以对类名进行重新修改。
- 5.修改完成之后,然后进行按键盘中的enter的键

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 键盘录入
- ### 使用步骤：
  - 导包：手动`import java.util.Scanner;` 快捷键：`ctrl+shift+o`
    - 位置放到class定义的上面：`package>import>class`
  - 创建对象: `Scanner sc = new Scanner(System.in);`
  - 接收int数据: `int x = sc.nextInt(); //对象调用方法`
  - 接受String数据：`String s = sc.nextLine(); //获取键盘录入的字符串数据`

- ### 参考链接：
  - [github: OJ输入输出总结](https://github.com/anliux/PracticePool/blob/master/base/docs/io.md)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 输出语句
- println():ln是换行。
- 可以在println()的括号中添加分隔符：比如制表符`\t`

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 随机数
- ### 作用：
  - 用于产生一个随机数

- ### 使用步骤(和Scanner类似)
  - 导包：`import java.util.Random;`
  - 创建对象：`Random r = new Random();`
  - 获取随机数：`int number = r.nextInt(10);`
    - 产生的数据在0到10之间，包括0，不包括10。(惯例左闭右开)
    - 括号里面的参数n：产生0-n的左闭右开区间内的数据。

- ### 示例：
  - 产生1-100的随机数：
    - Random(): 产生是的0到n-1的数，则1-100 可以在原来基础上+1
    - `int i = r.nextInt(100)+1;`
  - 猜数字小游戏：系统产生一个1-100的随机数，猜出这个数：
  	```
  	package test.demo;
	import java.util.Random;
	import java.util.Scanner;
	public class RandomDeom {
		public static void main(String[] args) {
			Random r = new Random();		
			int i = r.nextInt(100)+1;
			while(true) {
				System.out.println("输入要猜的数：");
				Scanner sc = new Scanner(System.in);
				int guessNum = sc.nextInt();
				if(guessNum > i) {
					System.out.println("输入的数"+guessNum+"太大了");
				}else if(guessNum < i) {
					System.out.println("输入的数"+guessNum+"太小了");
				}else {
					System.out.println("猜对啦！");
					break;
				}		
			}
		}

	}
  
 	 ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



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
  - 位置：上方工具栏 -- 黄色半圆环向下箭头为step over键
  - step over (F6)：按照代码流程执行
    - 法一：点击 工具栏中的Step Over (执行下一行)
    - 法二：快捷键F6 看到每一步程序的执行过程
    - 下同有此两种方法。
  - step into (F5)：进入本行代码调用的方法中
    - 可以用于当有调用方法，但是被调用方法没有设置断点的情况。
  - step return (F7)：从被调用函数返回调用被方法的代码行。
    - 可以用于从被调用函数返回调用该方法的代码行
      - 注：仍然顺序执行被调用方法中的代码行直到结束，没结束前作用等同于step over，但高亮代码有区别，不会像step over一样跳到当前语句。
    - 只有在有调用方法的debug中才有可用，若没有，则是灰的。

- ### 重点关注区域：
  - 看代码区域：对照看程序执行步骤；
  - 看Debug区域：对照看程序执行步骤；
  - 看varable区域：观察变量的创建、赋值、销毁；
    - 引用型变量的值后面会有一个(id=xx)，可以看作对象地址值。
  - 看console区域：看程序的输入输出。

- ### 断点调试运行界面:
  - ![断点调试运行界面](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/debug/%E6%96%AD%E7%82%B9%E8%B0%83%E8%AF%95%E8%BF%90%E8%A1%8C%E7%95%8C%E9%9D%A2.bmp)

- ### debug停止
  - debug完毕后，需要保证本次debug停止，即左上方菜单栏的红色停止按钮为灰；
  - 自动停止：一直"step over"直到程序最后一个花括号结束，会自动停止，并自动删去thread线程和对应的变量值；
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
    - 加断点：在程序开始处双击加断点
    - 观察变量：step over观察变量变化，for循环中不再使用的临时变量在退出循环后就消失了，以示使用完毕。
    - 完毕后去掉断点：在breadpoint窗口点双叉，或者在程序加断点处双击
    - 注意：循环断点的变量会变色，高亮以示上面的变量值又有变化。
  - 方法调用debug注意点：
    - 想看被调用方法的执行流程，则被调用方法也需要加断点
      - 按顺序自动进入所调用的方法中，且在左侧的debug视窗生成新的线程thread
      - 方法中执行完毕后自动跳回main方法，且该方法的debug线程会自动消失
    - 如被调用方法中不加断点，则按顺序执行程序不进入调用的方法；
      - 如需进入，则需要在用到该方法的代码行使用"step into (F5)"，以手动进入。
    - 如仅在所调用的方法中加断点，也可以执行debug
      - 开始时，thread列表自动生成主方法和调用方法两个debug线程，以及对应的变量值
      - 从断点处的方法语句开始执行，并按顺序跳回main方法继续，直到结束。
    - debug执行到带有输入的语句时：如果不在控制台输入，则step over按钮变灰，等待输入完成。
  - 方法调试图示：
    ![断点调试之方法调试](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/debug/%E6%96%AD%E7%82%B9%E8%B0%83%E8%AF%95%E6%96%B9%E6%B3%95%E8%B0%83%E8%AF%95.bmp)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END


