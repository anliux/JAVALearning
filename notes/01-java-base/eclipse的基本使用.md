# eclipse的基本使用


## eclipse的概述
- 是一个集成开发环境 IDE (integrated development environment)
- 集成了代码的编写功能，分析功能，编译功能，调试功能等一体化的开发软件。
- 特点：免费，纯Java语言编写，免安装(解压使用)，扩展性强(可以添加各种功能的插件)
- 下载和安装：http://eclipse.org/ ; 绿色版，解压就可以使用。
- 使用：
  - exe启动 - workspace选择 - 新建project项目(项目配置) - 新建package包(注意命名唯一性) - 包新建class类(类配置) - 写代码(实时编译，只需手动运行即可) - 运行 (run as: java application) - 下方控制台显示结果 
  - 详见下方第一个图文参考博文



## 图文参考链接：
- [【JAVA】eclipse-使用入门及常用快捷键](https://www.cnblogs.com/anliux/p/11525981.html)
- [【学习总结】Eclipse常用快捷键](https://www.cnblogs.com/anliux/p/11436568.html)	



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
			
	C:窗体给弄乱了，怎么办?
		window -- Perspective -- Reset Perspective
			
	D:控制台找不到了，怎么办?
		Window--Show View—Console

	
		
## 快捷键

	内容辅助键	alt+/
		main	然后alt+/
		syso	然后alt+/
  
	提供解决方案	ctrl+1（数字1）
		对小红叉提供解决方案：导包；异常处理；光标定位变量并重命名。
		大红叉是语法错误，必须修改代码。
	快捷键
		注释
			单行	选中内容，ctrl+/, 再来一次取消
			多行	选中内容，ctrl+shift+/, 取消 ctrl+shift+\
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
		打印	选中+alt+/：可选自动把选中部分放入输出语句中
				    即，可以通过生成的菜单选中sysout将选中语句放入输出语句
		tab	tab或者shift+tab	选中代码整体后移或者前移


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



## 自动生成构成函数和getset方法
	A：自动生成构成方法：
		代码区域右键 -- Source -- Generate Constructors from Superclass.. ： 无参构造函数
		代码区域右键 -- Source -- Generate Constructors using Fields...: 带参构造函数
	B：自动生成get、set方法：
		代码区域右键 -- Source -- Generate Getters and Setters.. -- select all


## 已创建类的重命名
- 1.首先要进行选中java类名称，然后进行右键
- 2.弹出了下拉菜单中,进行选择为refactor的选项。
- 3.弹出了下一个菜单中进行选择为rename的选项。
- 4.弹出了一个提示,那么就可以对类名进行重新修改。
- 5.修改完成之后,然后进行按键盘中的enter的键




