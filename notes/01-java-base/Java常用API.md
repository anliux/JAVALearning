# Java常用API

### 目录


<!--GFM-TOC -->
* [API概述](#api概述): API概述，Scanner获取字符串
* [String类](#string类): String概述, 构造方法(4种)及对比, 判断功能(4种), 获取功能(5种), 转换功能(3种), 其他功能(2种), 相关典型问题
* [StringBuilder](#stringbuilder): 和String的区别, 特点和优势, 构造方法, 功能(查询添加反转), 和String相互转换, 典型问题(字符串反转, 回文串), StringBuffer
* [对象数组的练习](#对象数组的练习): eclipse自动生成构造函数、get()/set()方法
* [集合类与ArrayList](#集合类与arraylist): 集合类概述, ArrayList概述, 构造方法, 添加/增删改查/遍历的方法
* [ArrayList案例分析](#arraylist案例分析): 获取满足要求的元素, 存储自定义对象并遍历, 键盘录入数据存储并遍历
* [集合版学生管理系统](#集合版学生管理系统): 学生类增删改查练习，含完整代码，篇幅较长可选择性跳过
* [IO流](#io流): 概述IO流, FileWriter构造方法, 写数据方法, 换行, 追加写入, FileReader, 读数据方法(单个字符/字符数组), 字符缓冲流及特殊方法, 复制文本的5种方法, 集合数据的读写
* [IO流版学生管理系统](#io流版学生管理系统): 用IO流改进学生管理系统
* [Object](#object): 
* [System](#system):
* [Date](#date):
* [DateFormat](#dateFormat):
* [Calendar](#calendar): 
* []()
<!--GFM-TOC -->



## API概述
- ### 定义
  - API(Application Programming Interface)：应用程序编程接口
    - 类似于厂商已经定义好，现在直接提供给我们使用的类
    - 我们只需要了解如何使用这些类即可 
  - Java API指的就是JDK中提供的各种功能的Java类。
    - 这些类将底层的实现封装了起来
    - 不需要关心这些类是如何实现的，只需要学习这些类如何使用。
  - 可以通过查帮助文档来了解Java提供的API如何使用
    - 相当于厂商Java给定义好的类的说明书

- ### API使用 (以Random为例)
  - 1:打开帮助文档。
  - 
  - 2:点击显示，找到索引，看到输入框。
  - 3:在搜索框中里面输入需要学习的内容。
    - 举例：Random
  - 4:看包：”java.lang包“下的类在使用的时候是不需要导包的，其他均需要。
  - 5:看类的描述：
    - Random类是用于生成随机数的类
  - 6:看构造方法：
    - Random():无参构造方法 -- `Random r = new Random();`
  - 7:看成员方法
    - `public int nextInt(int n)`: 产生的是一个[0,n)范围内的随机数
  - 8:调用方法：
    - 看返回值类型：返回什么类型，就用什么类型接收
    - 看方法名：名字不要写错了
    - 看形式参数：要几个参数，就给几个，要什么数据类型的，就给什么数据类型的
    - 示例：根据第7点 成员方法的形式，给出调用 `int number = r.nextInt(100);`

- ### Scanner获取字符串
  - Scanner: 用于获取键盘录入的数据（基本数据类型，字符串类型）
  - public String nextLine(): 获取键盘录入的字符串数据
  - 接受String数据：`String s = sc.nextLine(); //获取键盘录入的字符串数据`

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## String类
- ### String类概述
  - lang包中的类
  - 字符串是由多个字符组成的一串数据，字符串可以看成是”字符数组“
  - 字符串是一种比较特殊的引用数据类型，直接输出字符串对象输出的是该对象中的数据(即字符串数据，而不是地址值)。

- ### 构造方法：通过构造方法创建字符串对象的4种方法
  - 方式1：`public String(String original)`
    - 把字符串数据original封装成字符串对象
    - 示例：`String s1 = new String("helloworld");//s1=hello`
  - 方式2：`public String(char[] value)`
    - 把字符数组value的数据封装成字符串对象
    - `char[] chs = {'h','e','l','l','o'};`
    - `String s2 = new String(chs);//s2=hello`
  - 方式3：`public String(char[] value,int index,int count)`
    - 把字符数组value中的一部分数据封装成字符串对象，index是开始的索引，count是截取的长度(即字符串长度)。
    - `char[] chs = {'h','e','l','l','o'};`
    - `String s3 = new String(chs, 0, chs.length);//s3=hello`
    - `String s3 = new String(chs, 1, 3);//s3=ell`
  - 方式4：直接赋值也可以是一个对象 <最简单最常用>
    - `String s4 = "hello";//s4=hello`

- ### String创建的两种方法对比
  - 通过构造方法创建字符串对象和直接赋值创建字符串对象的区别：
    - 通过构造方法创建字符串对象：
      - `String s1 = new String("hello");`
    - 直接赋值创建字符串对象
      - `String s2 = "hello";`
      - `String s3 = "hello";`
  - `==`:
    - 基本数据类型：比较的是基本数据类型的值是否相等。
    - 引用数据类型：比较的是引用数据类型的地址值是否相等。
  - 比较结果：`s1==s2:false;` `s1==s3:false;` `s2==s3:true;`
    - 两种构造方法生成的字符串内容("hello")：都存储在方法区的常量池中，为了方便字符串的重复使用。
      - s1: new存入堆内存中地址值为001并开辟空间，而这个空间里存的不是"hello", 而是这个字符串在方法区的常量池中的地址值002
    - 直接赋值：存储在常量池。
    - 多次直接赋值：将存储在常量池中的"hello"的地址传递给s变量，且常量池已有的字符串公用。
  - 总结：
    - 通过构造方法创建字符串对象是在堆内存；
    - 通过直接赋值创建对象是在方法区的常量池 <方便字符串的重复使用>。
  - 图解
    ![字符串对象构造方法创建和直接赋值的区别](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/api/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%AF%B9%E8%B1%A1%E6%9E%84%E9%80%A0%E6%96%B9%E6%B3%95%E5%88%9B%E5%BB%BA%E5%92%8C%E7%9B%B4%E6%8E%A5%E8%B5%8B%E5%80%BC%E7%9A%84%E5%8C%BA%E5%88%AB.bmp)

- ### Object类
  - Object是类层次结构的根类，所有的类都直接或间接继承自该类。
  - 如果一个方法的形式参数是Object，即表示可以传递它的任意子类。
  - String是Object的子类。

- ### String的判断功能
  - `boolean equals(Object obj)`：
    - 功能：比较字符串的内容是否相同，严格区分大小写。
    - 与"=="区别(比较地址值)，且本方法可以重写。
    - 示例：
      - 定义字符串：`s1 = "hello;"`,`s2="hello;"`,`s3="Hello."//大小写的不同`
      - 判断：`Boolean b1 = s1.equals(s2);//true`,`Boolean b2 = s1.equals(s3);//false`
  - boolean equalsIgnoreCase(String str)
    - 功能：比较字符串的内容是否相同，且忽略大小写。
    - 示例：
      - 判断：`Boolean b1 = s1.equalsIgnoreCase(s2);//true`,`Boolean b2 = s1.equalsIgnoreCase(s3);//true`
  - boolean startsWith(String str)
    - 功能：判断字符串对象是否以指定的str开头。
    - 示例：
      - `s = "hello"; syso(s.startsWith("he");//true`，`Boolean b = s.startWith("abc");//false`
  - boolean endsWith(String str)
    - 功能：判断字符串对象是否以指定的str结尾。
    - 示例: 同上
- ### 模拟用户登录案例（使用String的判断功能）
  ```java
    import java.util.Scanner;
    public class StringEqual {
    /*
     * 模拟登录，给三次机会，并提示还有几次
     * 
     * 分析:
     * 		A: 定义两个字符串对象，用于存储已经存在的用户名和密码
     * 		B: 键盘录入用户名和密码
     * 		C: 进行比较，相同则登录成功，不同则显示登录失败，并提示还有几次机会
     * */
    public static void main(String[] args) {
      //定义字符串对象，存储已经存在的用户名和密码
      String usename = "admin";
      String password = "admin";

      //控制循环三次
      for(int i = 0; i < 3; i++) {
        //键盘录入用户名和密码
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入用户名：");
        String name = sc.nextLine();
        System.out.println("请输入密码：");
        String pwd = sc.nextLine();

        if((name.equals(usename)) && (pwd.equals(password))) {
          System.out.println("登录成功!");
          break;//登录成功要及时推出循环
        }else {
          if((2-i)==0)
            System.out.println("账户被锁定，请与管理员联系");
          else
            System.out.println("登录失败，你还有"+(2-i)+"次机会");//2,1,0
          }
        }
      }
    }
  ```
  
- ### String的获取功能
  - `int length()`：
    - 功能：获取字符串的长度，即字符个数。
    - 非常常用。
    - 注意区分属性`arr.length`和方法`str.length()` - 有无小括号
  - `char charAt(int index)`：
    - 功能：获取指定索引处的字符。
    - 可用于对字符串进行遍历。
    - 注：如果传入的索引值越界，会报错`StringIndexOutOfBoundsException`
  - `int indexOf(String str)`：
    - 功能：获取str在字符串对象中第一次出现的索引 <注意：返回的是小字符串的第一个字符的索引值>。
    - 没找到时返回-1.
  - `String substring(int start)`：
    - 功能：从索引值start开始截取字符串(默认截取到末尾)。
  - `String substring(int start,int end)`：
    - 功能：从索引值start开始，到索引值end结束截取字符串，左闭右开<不包含end索引值对应的字符>。
    - 注：如果传入的索引值越界，会报错`StringIndexOutOfBoundsException`
  - 注意：字符串子串截取功能的索引值：超出一个边界值不报错。
    - 例如，当字符串为空时，substring(0)不报错，截取到的子串为空；
    - 当字符串只有一个字符时，substring(0,1)和substring(1)不报错，且substring(1)截取到的子串为空。

- ### String的转换功能
  - `char[] toCharArray()`
    - 功能：把字符串转换为字符数组。
    - 示例：`char[] chs = s.toCharArray(); `
  - `String toLowerCase()`
    - 功能：把字符串转换为小写字符串。
    - 示例：`"helloWORLD".toLowerCase();`
  - `String toUpperCase()`
    - 功能：把字符串转换为大写字符串。
    - 示例：`"helloWORLD".toUpperCase();`
  - 注：转换大小写时，若字符串中有除字母外的其他字符，则其他字符不变。

- ### String的其他功能
  - 去除字符串两端空格：`String trim()`
    - 代码示例：`String s2 = s1.trim();`
    - 注：去除两端的一个或多个空格。
  - 按照指定符号分割字符串：`String[] split(String str)`
    - 代码示例：`String[] strArray = s.split(",");//用逗号分隔字符串并返回字符串数组`
    - 空格分隔的问题：
      - split参数中的空格数量是严格区分的。
      - 当split中仅传入`split("")`，双引号中间没有空格时，会将字符串按照每个字符分隔，包含每个空格。
      - 当split中传入多个空格时，例如`split("   ")`，三个空格，则只会在三个连续空格处分隔。
      - 当split中仅传入一个空格而字符串中包含连续的多个空格时，只会去掉一个空格，中间剩余空格将作为元素占位存入字符串数组。
        - 例如：`ab---c--de`用`split(" ")`分隔后，将得到长度为6的数组，且数组为`[ab, , ,c, ,de]`
      - 去掉不确定数量的空格的代码示例：`String[] strArray = s.split(" +");`
        - 例如：`ab---c--de`用`split(" +")`分隔后，将得到长度为3的数组，且数组为`[ab,c,de]`
      - 注：通过`toString()`得到的数组字符串形式自带方括号，且逗号前自带一个空格。
    - 注意：本方法的返回值类型是字符串数组。

- ### 典型问题
  - 遍历字符串 <字符串获取/字符串转换>
    - 法1：循环；获取长度作为循环边界；获取指定索引字符并传入循环参数进行遍历。
      - `for(int i = 0; i < s.length(); i++){syso(s.charAt(i));}`
    - 法2：先转为字符数组，然后对字符数组进行遍历。
      - `char[] chs = s.toCharArray(); for(int i=0; i<chs.length; i++){}`
  - 统计一个字符串中的大写字符字符、小写字母字符、数字字符的分别的个数 <字符串获取>
    - 定义三个计数器；遍历获取每个字符；对’每个字符‘进行判断，并将相应的计数器+1；返回结果。
    - 设ch是一个字符：对获取到的字符进行`if-else if`的判断。
      - 大写：ch>='A' && ch<='Z';
      - 小写：ch>='a' && ch<='z';
      - 数字：ch>='0' && ch<='9';
      - 注：最初反应是对应A-65,a-97的设定，后来发现直接用字符本体判断即可了。
 
  - #### 打印数组名特例
    - 数值型数组如int型数组：初始化后直接打印数组名，输出的是地址值。
    - char类型数组输出总结:
      - 直接输出数组名：将数组以字符串形式打印；
      - 输出前面加字符：输出的是地址；
      - 输出前面加字符的情况下想要输出数组内容：Arrays.toString(ch)，数组内容将以数组形式输出。
    - 注：直接打印字符串变量名，输出的也是字符串内容；前面加字符串后，输出的仍是字符串内容。
    - 注：字符串数组直接输出的是地址值。
    - 参考：[【JAVA】java中char类型数组用数组名打印结果不是地址值而是数组内容](https://www.cnblogs.com/anliux/p/12641018.html)

  - 将字符串首字母大写，其他字符小写 <字符串转换>
    - 截取字符串片段；分别进行大小写转换；然后用+号连接；
    - 方法：substring(); toUpperCase(); toLowerCase(); + .
    - 代码示例：
      - `String s3 = s1.substring(0,1).toUpperCase() + s1.substring(1).toLowerCase();`
    - 注意：
      - Char同样有类似方法: `char toUpperCase(char ch)`，也可考虑`s1.charAt(0)`截第一个字符，这里讲String方法就统一按String截取了。
      - substring()可能字符串索引越界异常，因此最好进行判断；但当字符串只有一个字符时，以上代码不报错。

  - 字符串反转
    - 思路1：倒着遍历字符串；
      - 倒着遍历，然后拼接字符串。
      - 返回值：String；参数列表：String s。
      - `String ss = "";`
      - `for(int i = s.length()-1; i>=0; i++){ss += s.charAt(i);}`
      - `return ss;`
    - 思路2：把字符串转换为字符数组，对字符数组反转，然后转换为字符串并返回。
      - 双指针交换元素值。
      - 返回值：String；参数列表：String s。
      - `char[] chs = s.toCharArray();`
      - `for(int start=0,end=chs.length-1; start<=end; start++,end--){交换start与end对应字符}`
      - `return new String(chs);`
        - //构造方法，讲字符数组传入即可，可省略定义新的String ss = new String(chs);,直接返回
    - 主函数调用：`String str = reverse(s);`

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## StringBuilder
- ### StringBuilder和String的区别 
  - String: 内容固定，不可变。
  - StringBuilder：可变字符串。
  
- ### StringBuilder类概述
  - 字符串缓冲区，可变字符串。
  - 字符串拼接的弊端
    - String每次拼接，都会构建一个新的String对象，既耗时，又浪费空间；而StringBuilder就可以解决这个问题。
    - 图解：
    ![String拼接浪费空间](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/api/String%E6%8B%BC%E6%8E%A5%E6%B5%AA%E8%B4%B9%E7%A9%BA%E9%97%B4.bmp)

- ### StringBuilder构造方法：
  - 无参构造：`public StringBuilder()`
    - 构造一个不带任何字符的字符串生成器，其初始容量为 16 个字符。
    - 代码示例：`StringBuilder sb = new StringBuilder("xxxx");`

- ### StringBuilder的功能
  - 查询容量：
    - `public int capacity()`：返回当前容量
      - 代码示例：`int n = sb.capacity();`
    - `public int length()`：返回长度（字符数）。
      - 代码示例：`int n = sb.length();`
    - 区别：容量是理论值，长度是实际值。
      - 当字符串缓冲区中还没有存储元素时，容量可能是16(默认值)，但长度是0。

  - 添加功能：`public StringBuilder append(任意类型)`
    - 添加数据，并返回自身对象。(即可变字符串类型的值)
      - 参数可以是任意类型：任意类型拼接过来以后组成新的字符串
      - `StringBuilder sb2 = sb.append("hello"); Boolean b = (sb==sb2);//ture`
    - 代码示例：
      - 单个：`sb.append("hello"); sb.append(true); sb.append(100); //输出：hellotrue100`
      - 链式：`sb.append("hello").append(true).append(100);//输出：hellotrue100`
        - 因为返回值是字符串缓冲区类型，是对象，仍可以调用功能。
    - 注意：需要一次添加多个字符串时，使用链式append，不要再使用`+`连接了。

  - 反转功能：`public StringBuilder reverse()`
    - 代码示例：`sb.reverse();//输出：001eurtolleh`

- ### String和StringBuilder相互转换
  - StringBuilder转为String：
    - `public String toString()`：返回此序列中数据的字符串表示形式。
    - 代码示例：`String s = sb.toString();//sb是字符串缓冲区变量名`
  - String转为StringBuilder：
    - 通过sb的构造方法：`public StringBuilder(String str)`
      - 构造一个字符串生成器，并初始化为指定的字符串内容。
    - 代码示例：`StringBuilder sb = new StringBuilder(s);//s是字符串变量名`

- ### 典型问题
  - 字符串反转：
    - 之前提供过两种思路：倒序遍历并连接到主字符串；转换为字符数组后前后指针获取并交换各值。
    - 思路：利用StringBuilder的reverse()功能
      - String --> StringBuilder --> reverse --> String --> return
    - 注：使用字符串缓冲区的构造方法，将字符串s作为参数传入，以此来转为StringBuilder类型。
  - 判断一个字符串是否是回文串：
    - 思路：反转字符串；与反转前的字符串比较：若相等，说明对称；返回结果。
    - 代码示例：`boolean res = sb.reverse().toString().equals(sb);//s是原字符串，sb是字符串缓冲区变量`

- ### StringBuffer与StringBuilder
  - 功能完全相同。
  - 区别：
    - StringBuilder是非线程安全的，访问速度更快，用于单线程代码。
    - StringBuffer是线程安全的，访问速度慢，用于多线程代码。

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 对象数组的练习
- ### 题目
  - 题目：创建一个学生数组，存储三个学生对象并遍历
  - ObjectArray相关练习

- ### 自动生成构造函数和getXxx(), setXxx()方法
  - A：自动生成构造方法：
    - 无参构造：代码区域右键 -- Source -- Generate Constructors from Superclass.. 
    - 带参构造：代码区域右键 -- Source -- Generate Constructors using Fields...: 
  - B：自动生成get、set方法：
    - 同时生成、可选：代码区域右键 -- Source -- Generate Getters and Setters.. -- select all

- ### 步骤分析
  - 定义学生类
  - 创建学生数组
  - 创建学生对象
  - 把学生对象作为元素赋值给学生数组
  - 遍历学生数组

- ### 代码示例
  - 定义学生类的代码：
	```Java
	package com.itcast;

	public class Student {
		private String name; //成员方法记得写修饰符 (与main方法对应)
		private int age;  //成员方法记得写修饰符 (与main方法对应)
		public Student() {//自动生成的无参构造
			super();//可去掉
			// TODO Auto-generated constructor stub
		}
		public Student(String name, int age) {//自动生成的带参构造
			super();//可去掉
			this.name = name;
			this.age = age;
		}
		
		//自动生成的get/set方法
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public int getAge() {
			return age;
		}
		public void setAge(int age) {
			this.age = age;
		}

	}

	```
  - 学生类演示代码
	```Java
	package com.itcast;

	public class StudentDemo {
		public static void main(String[] args) {
			//创建学生数组
			Student[] students = new Student[3];

			//创建学生对象
			Student s1 = new Student("曹操", 40);
			Student s2 = new Student("刘备", 35);
			Student s3 = new Student("孙权", 30);

			//把学生对象作为元素赋值给学生数组
			students[0] = s1;
			students[1] = s2;
			students[2] = s3;

			//遍历学生数组
			for(int i = 0; i < students.length; i++) {
				Student s = students[i];
				System.out.println(s.getName() + "---" + s.getAge());
				//直接打印对象名输出的是地址值，这里用get方法获取
			}
		}
	}
	```


- ### 对象数组的内存图
  - 图示：
    ![对象数组的内存图](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/api/%E5%AF%B9%E8%B1%A1%E6%95%B0%E7%BB%84%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.bmp)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 集合类与ArrayList
- ### 集合类引入
  - 面向对象语言对事物的描述是通过对象体现的; 为了方便对多个对象进行操作，必须把这多个对象进行存储。
  - 而要想存储多个对象，就不能是一个基本的变量，而应该是一个容器类型的变量。
  - 已经学过的，有哪些是容器类型的呢? 数组和StringBuilder
    - StringBuilder的结果是一个字符串，不一定满足我们的要求，
    - 所以我们只能选择数组，这就是对象数组。
  - 对象数组的弊端：不能适应变化的需求，因为数组的长度是固定的
  - 因此：为了适应变化的需求，Java就提供了 <集合类> 供我们使用。

- ### 集合类的特点：
  - 长度可变 (相比数组的优势)

- ### ArrayList概述  
  - 最常用的集合，通过阅读API学习
  - java.util包下：因此需要导包 `import java.util.ArrayList;`
  - `ArrayList<E>`：大小可变数组的实现。
  - `<E>`：一种特殊的数据类型，泛型。
    - 在出现E的地方，暂时可以使用引用数据类型替换。
    - 举例：`ArrayList<String>`, `ArrayList<Student>`, ...
  - 打印自带小括号：syso输出 'array：[hello, world]'

- ### 构造方法
  - 无参：ArrayList()
    - 示例：`ArrayList<String> array = new ArrayList<String>();//可以参考数组的定义格式`
  - 无参：ArrayList()：

- ### 添加元素
  - `public boolean add(E e)`:
    - 依次添加元素，E根据定义的类型确定，用的多
    - 示例：`array.add("hello"); //这条可作为一行独立代码`
  - `public void add(int index, E element)`:
    - 在指定索引处添加元素，而原位置元素顺次后移一位，用的不多
    - 示例：`array.add(1, "java");//原来索引1处的元素会顺次后移到索引2处`

- ### 添加元素的代码演示：
	```Java
	package com.itcast01;
	import java.util.ArrayList;
	public class ArrayListDemo {
		public static void main(String[] args) {
			ArrayList<String> array = new ArrayList<String>();
			System.out.println("array="+array);//输出：array=[]

			array.add("hello");
			array.add("world");
			System.out.println("array："+array);//array：[hello, world]

			array.add(1, "android");		
			System.out.println("array："+array);//array：[hello, android, world]
		}
	}
	```

- ### 增删改查
  - 获取元素：
    - `public E get(int index)`: 返回指定索引处的元素
      - 注意：get方法不改变原有集合
    - 示例：`System.out.println("get:"+array.get(0));`
  - 集合长度：
    - `public int size()`: 返回集合中的元素的个数
    - 示例：`System.out.println("size:"+array.size());`
  - 删除元素：
    - `public boolean remove(Object o)`: 删除指定的元素，并返回删除是否成功（布尔型）
      - 注意：若存在，即可删除并返回true，否则返回false；成功时仅删除第一个，再次remove时删除下一个该元素。
    - 示例：`array.remove("hello");`
    - `public E remove(int index)`: 删除指定索引处的元素，并返回被删除的元素
      - 注意：输入的是索引值，需要注意越界错误
    - 示例：`System.out.println("remove(index)": + array.remove(i));`
  - 修改元素：
    - `public E set(int index, E element)` -- 修改指定索引处的元素，返回被修改的元素（原来的元素）
    - 示例：`System.out.println("set:"+array.set(1,"python"));`


- ### 增删改查的代码演示
	```Java
	package com.itcast01;
	import java.util.ArrayList;
	public class ArrayListDemo2 {
		public static void main(String[] args) {
			//创建集合对象
			ArrayList<String> array = new ArrayList<String>();

			//添加元素
			array.add("hello");
			array.add("java");
			array.add("world");
			System.out.println("array:"+array);//array:[hello, java, world]

			//获取元素
			System.out.println("get:"+array.get(2));//get:world

			//集合长度
			System.out.println("size:"+array.size());//size:3

			//删除元素
			System.out.println("remove:"+array.remove("hello"));//remove:true
			System.out.println("remove:"+array.remove("hello"));//remove:false
			array.add(0,"hello");

			System.out.println("remove-index:"+array.remove(0));//remove-index:hello
			array.add(0,"hello");

			//修改元素
			System.out.println("set:"+array.set(1, "android"));//set:java (返回被替代的元素)

			System.out.println("array:"+array);//array:[hello, android, world]

		}
	}

	```

- ### 集合遍历
  - 用for循环 + size()方法 + get()方法
  - 注：常规的做法是，输出时，先将get获取到的元素存储在变量中，然后输出变量。

- ### 集合遍历的代码演示
	```Java
	package com.itcast01;
	import java.util.ArrayList;
	public class ArrayListDemo3 {
		public static void main(String[] args) {
			//新建集合
			ArrayList<String> array = new ArrayList<String>();
			array.add("hello");
			array.add("world");
			array.add("java");
			for(int i = 0; i < array.size(); i++) {//size()获取数组集合的大小
				//System.out.println(array.get(i));
				String s = array.get(i);//get()获取数组集合中的元素
				System.out.println(s);//先get()存起来而不是直接输出，是标准用法
			}
		}
	}

	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->


	
## ArrayList案例分析
- ### 获取满足要求的元素
  - 题目：
    - 给定一个字符串数组：{“张三丰”,“宋远桥”,“张无忌”,“殷梨亭”,“张翠山”,“莫声谷”}，
    - 将数组中的元素添加到集合中，并把所有姓张的人员打印到控制台上。
  - 分析：
    - 定义字符串数组；
    - 创建集合对象；
    - 遍历字符串数组，获取每个元素，并添加到集合；
    - 遍历集合：判断字符串元素是否以“张”开头，如果是，就输出。
  - 方法：
    - size()，get(i)，startswith("xxx")，
  - 代码：
  	```Java
	package com.itcast01;
	import java.util.ArrayList;
	public class ArrayListTest {
		public static void main(String[] args) {
			String[] strArray = {"张三丰","宋远桥", "张无忌","殷梨亭","张翠山","莫声谷"};//不是重头戏，直接赋值
			ArrayList<String> array = new ArrayList<String>();
			for(int i = 0; i < strArray.length; i++) {
				array.add(strArray[i]);//遍历添加元素
			}
			System.out.println(array);//
			for(int j = 0; j < array.size(); j++) {
				String s = array.get(j);//遍历获取集合元素
				if(s.startsWith("张"))//判断是否以"张"开头
					System.out.println(s);
			}
		}
	}

 	```

- ### 存储自定义对象并遍历 
  - 自定义Student对象
    - 包括：成员变量name和age，无参构造，带参构造，get、set方法
  - 新建集合，新建Student对象，并将Student对象存入集合
  - 遍历集合并输出
  - 注意点：
    - 创建集合对象：`ArrayList<Student> array = new ArrayList<Student>();`
    - for循环遍历时，接受变量为`Student s = array.get(i);`
    - 输出时，使用Student定义的获取方法：`System.out.println(s.getName()+s.getAge());`

- ### 键盘录入数据存储并遍历
  - 题目：
    - 创建一个集合，存储学生对象，学生对象的数据来自于键盘录入，最后，遍历集合
  - 分析：
    - 定义学生类；
    - 创建集合对象；
    - 键盘录入，创建学生对象，并将键盘录入的数据赋值给学生对象的成员变量；
    - 把学生对象作为元素存储到集合中；
    - 遍历集合。
  - 注：
    - 为了方便使用，这个把学生类中的所有成员变量定义为String类型
    - 将键盘录入方法进行封装
  - 代码：
   ```Java
	//Student.java
	package com.itcast01;
	public class Student {
		private String name;
		private String age;
		public Student() {

		}
		public Student(String name, String age) {
			this.name = name;
			this.age = age;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public String getAge() {
			return age;
		}
		public void setAge(String age) {
			this.age = age;
		}	
	}

   ```

   ```Java
	//ArrayListTest2.java
	package com.itcast01;
	import java.util.ArrayList;
	import java.util.Scanner;
	public class ArrayListTest2 {
		public static void main(String[] args) {
			ArrayList<Student> array = new ArrayList<Student>();

			//调用方法：调用一次方法，执行一次
			addStudent(array);
			addStudent(array);
			addStudent(array);

			for(int i = 0; i < array.size(); i++) {
				Student s = array.get(i);
				System.out.println(s.getName() + "--" + s.getAge());
			}
		}

		/*	为了提高代码复用性，进行封装。
		 * 
		 * 	写方法：两个明确
		 * 		返回值类型： void
		 * 		参数列表：ArrayList<Student> array
		 * */
		private static void addStudent(ArrayList<Student> array) {
			Scanner sc = new Scanner(System.in);
			System.out.println("请输入学生姓名：");
			String name = sc.nextLine();
			System.out.println("请输入学生年龄：");
			String age = sc.nextLine();

			Student s = new Student();
			s.setName(name);
			s.setAge(age);

			array.add(s);
		}
	}
   ```	
	
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->
	
	

## 集合版学生管理系统
- ### 注意：
  - 本部分展示完整代码，因此篇幅较长，可选择性跳过。

- ### 练习概述
  - 题目：学生管理系统的主界面 + 学生类的增删改查
  - 步骤：
    - 两个类：学生类和学生管理系统主类
    - 1. 定义学生类；
    - 2. 学生管理系统的主界面的代码编写；
    - 3. 学生管理系统的查看所有学生的代码编写；
    - 4. 学生管理系统的添加学生的代码编写；
    - 5. 学生管理系统的删除学生的代码编写；
    - 6. 学生管理系统的修改学生的代码编写；

- ### 学生类代码
  - 步骤：定义成员变量，之后生成构造方法(无参/带参)，get()/set()方法
  - 注意成员变量：private修饰，包括”学号，姓名，年龄，居住地“
	
	```Java
	package test.StudentArray;
	//学生类

	public class Student {
		//定义成员变量
		private String id;
		private String name;
		private String age;
		private String address;

		//生成构造函数：无参/带参
		public Student() {

		}
		public Student(String id, String name, String age, String address) {
			this.id = id;
			this.name = name;
			this.age = age;
			this.address = address;
		}

		//生成get()/set()函数
		public String getId() {
			return id;
		}
		public void setId(String id) {
			this.id = id;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public String getAge() {
			return age;
		}
		public void setAge(String age) {
			this.age = age;
		}
		public String getAddress() {
			return address;
		}
		public void setAddress(String address) {
			this.address = address;
		}

	}

	```

- ### 学生管理类代码
  - 步骤：依次定义主界面、查看、添加、删除、修改的代码
  - 主界面：循环，提示语，选项展示，输入及判断
    - 为了回到最初的界面，可加入while(true){}循环，直至退出(`System.exit(0);//JVM退出`)
    - 输入判断用switch更贴合条件；case为String与输入的数据类型对应；记得最后的default。
    - case "5"和default：都输入一条”谢谢“，可以用到case穿透
  - 查看学生类：创建容器(循环外创建即可)，调用自定义的查看方法，并写该方法
    - 输入时加入`\t` 制表符tab键的位置，可以更好地对齐 <注意`\t`在双引号里>
  - 添加学生类：键盘录入，存储，set()方法赋值给学生类对象
    - 学号重复问题：while(true) + flag循环
    - 关键代码：`if(s.getId().equals(id)) {}`
  - 删除学生对象：根据学号删除对应的学生对象
    - 遍历对比，根据索引值remove array集合的对象 
    - 关键代码：`if(s.getId().equals(id)) { array.remove(x); break;	}`
    - 同样注意学号不存在问题：定义flag进行标记，
    - 关键代码：`if(index==-1) syso("要删除的对象不存在")`
  - 修改学生：依然根据学号
    - 加判断考虑学号不存在的情况

	```Java
	package test.StudentArray;

	import java.util.ArrayList;
	import java.util.Scanner;

	public class StudentManager {
		public static void main(String[] args) {
			// 定义存储学生类的集合
			ArrayList<Student> array = new ArrayList<Student>();

			// 这是学生管理系统的主界面
			// 循环直至退出
			while (true) {
				System.out.println("--------欢迎来到学生管理系统--------");
				System.out.println("1. 查看所有学生");
				System.out.println("2. 添加学生");
				System.out.println("3. 删除学生");
				System.out.println("4. 修改学生");
				System.out.println("5. 退出");
				System.out.println("请输入你的选择：");
				// 创建键盘录入对象
				Scanner sc = new Scanner(System.in);
				String choiceString = sc.nextLine();
				// 用switch语句实现选择
				switch (choiceString) {
				case "1":
					// 查看所有学生
					findAllStudents(array);
					break;
				case "2":
					// 添加学生
					addStudent(array);
					break;
				case "3":
					deleteStudent(array);
					// 删除学生
					break;
				case "4":
					// 修改学生
					updateStudent(array);
					break;
				case "5":
					// 退出
					// break;
				default:
					System.out.println("谢谢你的使用 ");
					System.exit(0);// JVM退出
					break;
				}
			}

		}

		//修改学生
		public static void updateStudent(ArrayList<Student> array) {
			//创建键盘录入对象
			Scanner sc = new Scanner(System.in);
			System.out.println("请输入要修改的学号：");
			String id = sc.nextLine();

			//定义索引值，判断是否存在
			int index = -1;
			for(int x = 0; x<array.size(); x++) {
				Student s = array.get(x);
				if(s.getId().equals(id)) {
					index = x;
					break;
				}
			}
			if(index == -1)
				System.out.println("您输入的学号不存在，请重新输入：");
			else {
				System.out.println("请输入新的学生姓名：");
				String name = sc.nextLine();
				System.out.println("请输入新的学生年龄：");
				String age = sc.nextLine();
				System.out.println("请输入新的学生地址：");
				String address = sc.nextLine();

				//创建学生对象
				Student s = new Student();
				s.setId(id);
				s.setName(name);
				s.setAge(age);
				s.setAddress(address);

				//修改集合中的对象
				array.set(index, s);
				System.out.println("修改学生成功");
			}
		}

		// 删除学生
		public static void deleteStudent(ArrayList<Student> array) {
			//创建键盘录入对象
			Scanner sc = new Scanner(System.in);
			System.out.println("请输入要删除对象的学号：");
			String id = sc.nextLine();
			//遍历并对比
			int index = -1;
			for(int x=0; x<array.size(); x++) {
				Student s = array.get(x);
				if(s.getId().equals(id)) {
					index = x;
					break;
				}
			}
			if(index == -1) {
				System.out.println("您输入的学号不存在，请重新输入：");
			}else {
				array.remove(index);
				System.out.println("删除学生成功");
			}
		}

		// 添加学生
		public static void addStudent(ArrayList<Student> array) {
			// 创建键盘录入对象

			Scanner sc = new Scanner(System.in);

			String id;
			// 加入ID是否重复的判断
			while (true) {
				System.out.println("请输入学号：");
				id = sc.nextLine();
				Boolean flag = false;
				for (int x = 0; x < array.size(); x++) {
					Student s = array.get(x);
					if (s.getId().equals(id)) {
						flag = true;
						break;
					}
				}
				if (flag) {
					System.out.println("您输入的学号已被占用，请重新输入：");
				} else
					break;
			}

			System.out.println("请输入姓名：");
			String name = sc.nextLine();
			System.out.println("请输入年龄：");
			String age = sc.nextLine();
			System.out.println("请输入地址：");
			String address = sc.nextLine();

			// 创建学生对象
			Student s = new Student();
			s.setId(id);
			s.setName(name);
			s.setAge(age);
			s.setAddress(address);

			// 把学生对象作为元素添加到集合中
			array.add(s);

			// 给出提示：
			System.out.println("添加学生对象成功");
		}

		// 查看所有学生的方法
		public static void findAllStudents(ArrayList<Student> array) {
			// 首先判断集合中是否有数据，如果没有，就给出提示，并让该方法不继续执行下去
			if (array.size() == 0) {
				System.out.println("不好意思，目前没有学生信息可供查询，请重新选择您的操作");
				return;
			}
			// \t tab键制表符的位置
			System.out.println("学号\t\t姓名\t年龄\t居住地\t");
			for (int x = 0; x < array.size(); x++) {
				Student s = array.get(x);
				System.out.println(s.getId() + "\t" + s.getName() + "\t" + s.getAge() + "\t" + s.getAddress());
			}
		}
	}

	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## IO流

- ### IO流概述和分类
  - 引入：类似ArrayList的集合类，存储数据的有效范围仅为该代码运行期间，在内存中临时存储，再次打开时输入的数据已丢失。而IO流技术可以永久存储。
  - 概述：IO流用来处理设备之间的传输问题，包括文件复制、上传/下载文件等。
  - IO流分类：
    - 输出流 (写数据)：FileWriter
    - 输入流 (读数据)：FileReader
  - 图示：
  ![IO流的作用及分类](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/IO%E6%B5%81%E7%9A%84%E4%BD%9C%E7%94%A8%E5%8F%8A%E5%88%86%E7%B1%BB.bmp)

- ### FileWriter概述  
  - 输出流写数据，通过阅读API学习
  - java.io包下：因此需要导包 `import java.io.FileWriter;`
  - 输出流写数据的步骤：
    - 1. 创建输出流对象；<创建文件时需要调用系统资源>
    - 2. 调用输出流对象的写数据的方法，并flush刷新缓冲区；
    - 3. 释放资源。<即通知系统释放和该文件相关的资源，因为创建输出流对象是调用系统资源创建的>

- ### FileWriter的构造方法和成员方法
  - 构造方法：
    - `FileWriter(String fileName)`: 传递一个文件名称 <或路径+文件名>
  - 成员方法：
    - `void write(String str)`: 写入数据
    - `void flush()`: 刷新缓冲区
      - 数据不会直接写到文件，而是写到了内存缓冲区，flush刷新后显示 
    - `void close()`: 释放调用的系统资源
  - 创建输出流对象做了哪些事情：`FileWriter fw = new FileWriter("d:\\a.txt")`
    - 1. 调用系统资源创建了一个文件；(没有路径所指文件时会自动创建)
    - 2. 创建输出流对象；
    - 3. 把输出流对象指向该文件。
  - 写数据方法的路径问题：
    - 相对路径：相对当前项目而言，在项目的根目录下(注意是"项目")
      - 示例：`FileWriter fw = new FileWriter("a.txt")//不加盘符的文件名;` 
    - eclipse中显示相对路径的文件：
      - 选中项目project -- 右键 -- refresh，即可在项目下出现相应的文件(a.txt)
    - 绝对路径：指明盘符的具体路径
      - 示例：`FileWriter fw = new FileWriter("d:\\a.txt");//加了盘符位置的文件名`
      - 注意：mac中路径为'/users/xx/...'
  - close()和flush()方法：
    - flush(): 刷新缓冲区；之后流对象还可以继续使用。
    - close(): 先刷新缓冲区，后通知系统释放资源；之后流对象不可以再使用了。
      - close()做两步，因此即使write()之后没有flush(), close()的时候也会自动刷新。
      - 写入内容较少时，可以省略flush().
  - 代码示例：(注意导包和导抛出异常)
	  ```Java
	  import java.io.FileWriter;
	  import java.io.IOException;
	  public class FileWriterDemo{
		public static void main(String[] args) throws IOException {
			//创建输出流对象
			FileWriter fw = new FileWriter("d:\\a.txt");//没有该文件时会自动创建，使用绝对路径
				//如果不带盘符地址，默认为所写入的文件在代码项目所在路径下的相对路径
			//调用数据流对象的写数据方法
			fw.write("IO流你好");//写一个字符串数据
			fw.flush();//数据没有直接写到文件，而是写到了内存缓冲区，刷新缓冲区后才会显示
			fw.write("javaee");
			fw.flush();
			fw.close();//释放资源，否则fw会一直占用中
			//fw.write("123"); //close()之后再写数据会报错
			
		}
	  }
	  ```

- ### FileWriter写数据的方法
  - `void write(String str)`: 
    - 写入一个字符串数据
    - 代码示例：`fw.write("abcde");  fw.close(); //写入"abcde"; 此处写入较少可省略flush()` 
  - `void write(String str, int index, int lens)`:
    - 写入一个字符串中的一部分数据，即从索引值index开始，长度为lens的子串
    - 代码示例：`fw.write("abcde", 1, 3);  fw.close(); //可写入"bcd"`  
  - `void write(int ch)`:
    - 写入一个字符数据
    - 为int类型的好处是：既可以写char类型的数据，也可以写char对应的int类型的值，比如'a'和97均可
    - 代码示例：`fw.write('a');`和`fw.write(97);`均可写入字符'a' 
  - `void write(char[] chs)`: 
    - 写入一个字符数组数据
    - 代码示例：`char[] chs = {'a','b','c','d','e'}; fw.write(chs);//写入的数据在文件中的形式是"abcde"不带引号`
  - `void write(char[] chs, int index, int lens)`: 
    - 写入一个字符数组的一部分数据
    - 代码示例：`char[] chs = {'a','b','c','d','e'}; fw.write(chs,2,3);//写入的数据在文件中的形式是"cde"不带引号`

- ### FileWriter写数据的换行
  - 用换行符可以实现换行
    - 代码示例：for循环中：`fw.write(x); fw.write("\r\n");`
  - 不同系统识别的换行符不同：
    - Windows: `\r\n` 
    - linux: `\n`
    - mac: `\r`
    - 注意：如果在Windows用`\n`写入，则自带的记事本打开无法识别，显得的仍然是没有换行的；而用编辑器打开可以识别。
  - 缓冲流有特殊的换行方法
    - BufferedWriter: `void newLine()` -- 可根据系统自动匹配换行符，详见缓冲流的特殊功能部分。
    - 代码示例：`bw.newLine();//取代bw.write("\r\n")；`

- ### FileWriter写数据的追加写入
  - 构造方法：`FileWriter(Sting str, Boolean append)`
    - append默认为false，当需要追加时，可以在第二个参数位置写true
    - 这时再运行，会将新的内容追加到文件中
  - 代码示例：
    - `FileWriter fw = new FileWriter("c.txt",true); //默认为false，写为true时表示追加写入`
    - `fw.write("xxxxxx");//这时会追加新的xxxx内容写入到文件` 

- ### FileReader概述  
  - 输入流写数据，通过阅读API学习
  - java.io包下：因此需要导包 `import java.io.FileReader;`
  - 构造方法：`FileReader(String filename)` -- 传递文件名称
    - 注意：仍然需要导包和抛出异常
  - 输入流写数据的步骤：
    - 创建输入流对象;
    - 调用输入流对象的读数据方法;
    - 释放资源.
  
- ### FileReader读数据的方法：
  - `int read()`: 
    - 一次读取一个字符，且存储类型为int，即字符对应的int值
      - 可通过(char)强转为char类型
    - 再次使用本方法时：自动读取下一个字符 <不需要像写数据一样声明追加>
    - 当没有可读取数据时，返回-1 <可作为读取循环结束的判断条件>
    - 空格、回车等也可以读取到，不需要在输出语句(syso)里加`ln` 
      - 例如：读取某个.java文件，可以在控制台输出带格式的代码 
    - 循环时while语句的妙用：
      - `while((ch = fr.read()) != -1){...}`
      - 做了三步：read()读数据; 读取到的结果赋值给ch; 判断ch的值是否为-1
    - `void close()`: 读取结束后记得关闭释放资源
      - 代码示例：`fr.close();`
    - 读数据常见异常：
      - `java.io.FileNotFoundException: fr.txt (系统找不到指定文件)` 
    - 代码示例：
	  ```Java
	  import java.io.fileNotFoundException;
	  import java.io.FileReader;
	  import java.io.IOException;
	  public class FileReaderDemo{
		public static void main(String[] args) throws IOException{
			FileReader fr = new FileReader("fr.txt");//创建输入流对象; fr.txt内容为："abc"
			/*
			int ch = fr.read();//调用输入流对象的读取方法
			System.out.println(ch);//97
			System.out.println((char)ch);//a
			*/
			int ch;
			while((ch = fr.read()) != -1){//这条语句做了三个步骤
				System.out.print();
			}
			fr.close();//释放资源
			
		}
	  }
	  ```
  - `int read(char[] cbuf)`
    - 一次读取一个字符数组的数据，返回<实际>读取的字符个数
    - 步骤仍然是：创建对象；调用读数据方法；释放资源。
    - `char[] chs = new char[1024];`
      - 自定义字符数组，相当于读取到自定义数组中，数组长度为每次读取的字符个数
      - 通常，数组长度定义为1024或1024的整数倍：因为MB,GB等的换算是1024
    - 读取为空时，返回-1 <可作为循环结束的条件>
    - 会读取回车 `\r\n`，占用2个长度
    - 上一次的读取会被下一次替换，当下一次读取不够全部提黄上一次读取时，上一次的读取会遗留在存储字符数组中
      - 详见下方图解 
    - 输入推荐用`System.out.println(new String(chs,0,len));`
    - 代码示例：
	    ```java 
	    //创建输入流对象
	    FileReader fr = new FileReader("a.txt");
	    char[] chs = new char[1024];
	    int len;
	    while((len = fr.read(chs)) != -1){
		System.out.print(new String(chs,0,len));//注意syso不要写ln，读取了回车等格式符
	    }
	    fr.close();    

	    ```
  - FileReader两种读数据方法对比图解
  ![FileReader读数据的两种方式图解](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/FileReader%E8%AF%BB%E6%95%B0%E6%8D%AE%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F%E5%9B%BE%E8%A7%A3.bmp)

- ### IO流案例：复制文本文件
  - 题目：
    - 文件复制：将相同项目下的a.java中的内容复制到b.java文件中
  - 文件复制的套路：
    - 数据源：a.java -- 读数据 -- FileReader
    - 目的地：b.java -- 写数据 -- FileWriter
  - 注意点：
    - 同时有读写时，close()先关哪个都可，推荐先关write.
  - '一次读取一个字符'的代码示例：
	  ```java 
	  FileReader fr = new FileReader("a.java");//同项目下，用相对路径即可。下同。
	  FileWriter fw = new FileWriter("b.java");
	  //一次读取一个字符的定义方法
	  int ch;//定义返回值flag
	  while((ch = fr.read()) != -1){//参考按单个字符读取的循环
		fw.write(ch);
	  }
	  fw.close();
	  fr.close();
	  ```
  - '一次读取一个字符数组'的代码示例：
	  ```java 
	  FileReader fr = new FileReader("a.java");//同项目下，用相对路径即可。下同。
	  FileWriter fw = new FileWriter("b.java");
	  //一次读取一个字符数组的定义方法
	  char[] chs = new char[1024];//定义读取的字符数组
	  int len;//定义返回值flag
	  while((len = fr.read(chs)) != -1){//参考按单个字符读取的循环
		fw.write(chs,0,len);
	  }
	  fw.close();
	  fr.close();
	  ```	  
	  
- ### 字符缓冲流
  - BufferedWriter:
    - 将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组、字符串的高效写入
    - 代码示例：`BufferedWriter bw = new BufferedWriter(new FileWriter("bw.txt"));`
    - 调用使用同FileWriter()
  - BufferedReader:
    - 从字符输入流中读取文本，缓冲各个字符，从而提供单个字符、数组、行的高效读取
    - 代码示例：`BufferedReader br = new BufferedReader(new FileReader("br.txt"));`
      - 仍然分为读取单个字符和读取字符数组两种方式。
  - 导包：`import java.io.BufferedWriter/BufferedReader;`
  - 用缓冲流复制文件
    - 注意：记得开始导包和抛出异常
    - 数据源：a.java -- 读数据 -- FileReader -- 高效读数据 -- BufferedReader
    - 目的地：b.java -- 写数据 -- FileWriter -- 高效写数据 -- BufferedWriter
    - 代码示例：
	    ```java
	    import java.io.* 
	    ...
	    public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new FileReader("a.java"));
		BufferedWriter bw = new BufferedWriter(new FileWriter("b.java"));
		/*
		//一次读写一个字符
		int ch;
		while((ch = br.read()) != -1){
			bw.write((char)ch);
		}
		*/
		//一次读取一个字符数组
		char[] chs = new char[1024];
		int len;
		while((len = br.read(chs)) != -1){
			bw.write(chs,0,len);//不要忘记参数，防止写入未覆盖的遗留数据
		}
	    }

	    ```

- ### 字符缓冲流的特殊功能
  - 字符缓冲流：
    - 包含缓冲输入/输出流：BufferedWriter 和 BufferedReader
    - 创建缓冲流对象：构造方法参数为对应的基本输入/输出流对象，而不是直接传入文件。 
    - 代码示例：`BufferedReader br = new BufferedReader(new FileReader("br.txt"));`
  - BufferedWriter:
    - `void newLine()`: 写一个换行符，这个换行符由系统决定 
      - 不需要再判断系统换行符，取代之前的`fw.write("\r\n");`
    - 代码示例: `bw.newLine();`
  - BufferedReader:
    - `String readLine()`: 一次读取一行数据，但不读取换行符 (但读取空格)
      - 返回值是字符串格式
      - 读取空格：所以不用担心格式会乱，只需要加上换行即可
      - 读取为空时返回null，可以作为循环结束的判断语句
    - 代码示例：
	    ```java 
	    BufferedReader br = new BufferedReader(new FileReader("br.txt"));
	    String line;
	    while((line = br.readLine()) != null){//这里同时做了三步，同上 (读取、赋值、判断)
		System.out.println();//readLine()不读取换行符，因此syso语句需要加上`ln`
	    }
	    br.close();
	    ```
  - 导包注意点：
    - 用字符缓冲流时，BufferedWriter/BufferedReader和FileWriter/FileReader都需要导入
    - 当然还有IO流异常 IOException 
  - 使用字符缓冲流的特殊方法复制文本文件
    - 代码示例：
	    ```java
	    public class CopyFileDemo{
		public static void main(String[] args) throws IOException{
			//创建缓冲流对象
			BufferedReader br = new BufferedReader(new FileReader("a.txt"));
			BufferedWriter bw = new BufferedWriter(new FileWriter("b.txt"));
			String line;
			while((line = br.readLine()) != null){
				bw.write(line);
				bw.newLine()
				bw.flush();
			}
			bw.close();
			br.close()
		}
	    }
	    ```

- ### 复制文本文件的5种方法
  - 基本流一次读写一个字符
  - 基本流一次读写一个字符数组
  - 缓冲流一次读写一个字符
    - 注意：缓冲流也可以用基本流的方法`br.read()`进行读取
  - 缓冲流一次读写一个字符数组
  - 缓冲流一次读写一个字符串 <推荐，重点掌握>
    - 用缓冲流的特殊方法进行读写 
    - `br.readLine()` and `bw.newLine()`.
  - 注：
    - 写代码时可以将读写的文件名和五种方法单独定义，提高复用性
    - 此处涉及异常抛出注意点：当所调用的方法抛出了异常时，所调用的方法也需要抛出异常，即main方法也需要加`throws IOException`

- ### 集合数据的读取
  - IO流：将集合中的数据写入文本文件
    - 题目：
      - 把ArrayList集合中的字符串数据存储到文本文件，每一个字符串元素作为文件中的一行数据 
    - 步骤：
      - 创建集合对象
      - 往集合中添加元素
      - 创建输出缓冲流对象
      - 遍历集合，得到每一个字符串元素，然后把该字符串元素作为数据写入到文本文件
      - 释放资源
    - 代码示例：
	    ```java
	    import java.io.*; //(ctrl+shift+o大法好)
	    import java.util.ArrayList;

	    public class ArrayListToFile{
		public static void main(String[] args) throws IOException{
			ArrayList<String> array = new ArrayList<>();
			array.add("hello");
			array.add("Java");
			array.add("world");
			BufferedWriter bw = new BufferedWriter(new FileWriter("a.txt"));
			for(int i=0;i<array.size();i++){
				String s = array.get(i);
				bw.write(s);
				bw.newLine();
				bw.flush();
			}
			bw.close();
		}
	    }
	    //运行，并刷新项目
	    ```
  - IO流：将文本文件中的数据读取并存入集合中
    - 题目：
      - 文本文件中读取数据到ArrayList中，并遍历集合；每一行数据作为一个字符串元素。
    - 步骤：
      - 创建输入缓冲流对象；
      - 创建集合对象；
      - 去读数据，每次读取一行数据，把该行数据作为一个元素存储到集合中；
      - 释放资源；
      - 遍历集合.
    - 代码示例：
	    ```java
	    import java.io.*; //(ctrl+shift+o大法好)
	    import java.util.ArrayList;

	    public class ArrayListToFile{
		public static void main(String[] args) throws IOException{
			BufferedReader br = new BufferedReader(new FileReader("a.txt"));
			ArrayList<String> array = new ArrayList<>();
			String line;
			while((line = br.readLine()) != null){
				array.add(line);
			}
			br.close();
			for(int i=0;i<array.size();i++){
				String s = array.get(i);
				System.out.println(s);
			}
		}
	    }
	    //运行，并刷新项目
	    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## IO流版学生管理系统
- ### 图示：
  - 左右为核心部分，中间加入集合作为临时存储，避免频繁读写文件；
  - 左-中：为之前的集合版学生管理系统，代码可以复用
  - 中-右：为集合与文件的读写，加入两个读写方法
  ![学生管理系统IO版图解](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/%E5%AD%A6%E7%94%9F%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9FIO%E7%89%88%E5%9B%BE%E8%A7%A3.bmp)

- ### 学生类代码
  - 可直接复用

- ### 学生管理类代码
  - 复用增删改查方法，并加入集合到文件的读写两个方法
  - 增删改查：
    - main方法中删去新建ArrayList, 改为定义文件
      - `String fileName = "students.txt";`
    - 参数列表改为传入文件名：
      - `public static void addStudent(String fileName){}`
    - 增删改查方法中先新建ArrayList，后读取文件到集合对象中，下面就一样了
      - `ArrayList<Student> array = new ArrayList<>();`
      - `readData(fileName,array);` 
    - 增删改查方法的最后，array操作之后，将集合对象中的数据写入文件：
      - `writeData(fileName,array);` 
    - 注意：增删改查和main方法需要跟着抛出异常。 
  - 代码示例：
  ```java
  
  //main方法和增删改查略
  
  
  //从文件中读取数据到集合: 'heima001,向问天,30,北京'作为一条对应一个Student对象
  public static void readData(String fileName, ArrayList<Student> array) throws IOException{
  	//创建输入缓冲流对象
	BufferedReader br = new BufferedReader(new FileReader("fileName"));
	String line;
	while((line = br.readLine()) != null){
		String[] datas = line.spit(",");
		Student s = new Student();
		s.setId(datas[0]);
		s.setName(datas[1]);
		s.setAge(datas[2]);
		s.setAddress(datas[3]);
		array.add(s);
	}
	br.close();
  }
  
  //把集合中的数据写入文件：'heima001,向问天,30,北京'作为一条对应一个Student对象
  public static void writerData() throws IOException{
  	//创建输出缓冲流对象
	BufferedWriter bw = new BufferedWriter(new FileWriter(fileName));
	for(int i = 0; i<array.size(); i++){
		Student s = array.get(i);
		StringBuilder sb = new StringBuilder();//需要拼接成’heima001,向问天,30,北京‘，可以用StringBuilder
		sb.append(s.getId()).append(",").append(s.getName()).append(",").append(s.getAge()).append(",").append(s.getAddress();
		
		bw.write(sb.toString());
		bw.newLine();
		bw.flush();
	}
	bw.close();
  }
  
  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Object
- ### 对象
  - 可以通过查阅API进行学习
  - eclipse：
    - ctrl/command + 光标移动到某某XX：打开并查看源码
    - ctrl/command + o: 展示代码结构(类、变量、方法等)，搜索输入可以查找
   
- ### 概述
  - Object类 是类层次结构的根类, 在java.lang包下。
  - 每个类都使用 Object 作为超类。
  - 所有对象（包括数组）都实现这个类的方法
  - 代码示例：
    - `class Demo extends Object{...}//默认继承Object类`

- ### Object类要掌握的功能
  - toString
  - equals 

- ### toString方法
  - eclipse：ctrl/command+XX：查看源码
    - command+toString跳转到其源码
  - `String toString`: 返回对象的字符串表示
    - 输出对比可知：输出对象，默认输出的是`对象.toString()` 
  - toString源码：`return getClass().getName() + "@" + Integer.toHexString(hashCode());`  
    - getClass()：返回运行时类，即字节码文件
    - getName()：返回类名
    - "@"：一个分隔符
    - Integer.toHexString()：返回指定参数的十六进制字符串形式
    - hashCode()：返回该对象的哈希码值(内存地址)
  - 注意：
    - toString的源码对于输出没有意义，一般重写toString方法
    - eclipse提供了快捷重写：source -- Generate toString -- 选择变量 -- 自动生成重写的toString方法 
  - toString方法的使用场景：
    - 一般开发不用，自己写/学习/测试/调试的时候多用 
  - 代码示例：
  	```java
	Fruit f = new Fruit();
	System.out.println(f.toString());//test.demo.Fruit@6ff3c5b5
	System.out.println(f);//test.demo.Fruit@6ff3c5b5 -- 输出对比
  	```
	
	```java
	public class ObjectDemo {
		public static void main(String[] args) {
			Fruit f = new Fruit();
			System.out.println(f.toString());//test.demo.Fruit@6ff3c5b5
			f.name = "橘子";
			f.age = 12;
			System.out.println(f);//test.demo.Fruit@6ff3c5b5
		}
	}

	class Fruit extends Object{
		String name;
		int age;
		@Override
		public String toString() {
			return "Fruit [name=" + name + ", age=" + age + "]";
		}	
	}
	/*
	输出：
	Fruit [name=null, age=0]
	Fruit [name=橘子, age=12]
	*/
	```

- ### equals方法
  - boolean equals(Object 0):
    - 使用==来比较两个对象是否相等，比较的是地址值是否相等
    - 比较地址值没有什么意义，如果要使用，一般需要重写equals方法 
  - 源码：
	  ```java
	  public boolean equals(Object obj) {
		return (this == obj);
	  }
	  ```
  - eclipse提供了快捷重写：
    - source -- Generate HashCode() and equals() -- 选择变量 -- 自动生成重写的两个方法 
  - 自动生成的代码：
  	```java
	@Override
	public boolean equals(Object obj) {
		if (this == obj) //判断是否是本身：提高效率
			return true;
		if (obj == null) //判断是否为空：方法可以调用，那么this本身一定不是null，提高效率
			return false;
		if (getClass() != obj.getClass()) //判断类型是否不同，不同则一定不相等：提高健壮性，避免下一行向下转型抛出异常
			return false;
		
		Fruit other = (Fruit) obj; //向下转型
		
		if (age != other.age)
			return false;
		if (name == null) {
			if (other.name != null) //一个为null，一个不为null
				return false;
		} else if (!name.equals(other.name)) //基本判断
			return false;
		return true;//以上情况都没有时，返回true
	}	  
  	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## System
- ### eclipse快捷键
  - 方法抽取：
    - 将方法抽取为一个独立的方法 
  - 方法抽取快捷键：
    - 右键 -- refactor -- extract method(这里会展示快捷键组合提示)
    - windows: alt+shift+M
    - Mac: option+command+M
  - 抽取步骤：
    - 选中想要抽取的代码
    - 抽取操作(以上三种任选其一)
    - 抽取为独立方法 

- ### System类概述 
  - 概述：
    - System：包含一些有用的类字段和方法；不能被实例化。
      - 类字段：静态所修饰的成员变量，属于所有的对象，因此称为类字段。
      - 不能实例化：构造方法是私有的；
        - 不能实例化的类：抽象类；构造私有的工具类。 
      - 成员变量和成员方法静态修饰：static，直接用类名调用。 
    - System类提供的设施中有：
      - 标准输入、标准输出和错误输出流；
      - 对外部定义的属性和环境变量的访问；
      - 加载文件和库的方法；
      - 快速复制数组的一部分的实用方法。 
  - System类要掌握的功能
    - arraycopy
    - exit
    - currentTimeMillis
 
- ### arraycopy
  - static void	arraycopy(Object src, int srcPos, Object dest, int destPos, int length) 
    - 从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束。
    - Object src: 源数组
    - int srcPos: 源数组的起始索引位置
    - Object dest: 目标数组
    - int destPos: 目标数组的位置
    - int length: 指定接收的元素个数
  - 使用注意：
    - 长度length：注意在源数组和目标数组都会存在越界问题
    - 目标数组中，没有存放源数组复制到的新元素的位置，还是默认值
      - 比如int[]中，仍是默认值0
    - length灵活，不一定要复制完源数组中从索引值开始以后的所有元素，可以只复制部分
  - 代码示例：
  	```java
	private static void method() {
			int[] src = {1,2,3,4,5};
			int[] dest = new int[5];
	//		System.arraycopy(src, 0, dest, 0, 5);//12345
	//		System.arraycopy(src, 2, dest, 0, 3);//34500
	//		System.arraycopy(src, 2, dest, 2, 5);//Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException
	//		System.arraycopy(src, 2, dest, 2, 3);//00345
	//		System.arraycopy(src, 2, dest, 2, 1);//00300
			System.arraycopy(src, 2, dest, 4, 3);//Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException

			for(int i=0; i<dest.length;i++) {
				System.out.print(dest[i]);
			}
		}  
  	```
  
- ### currentTimeMillis
  - static long	currentTimeMillis() 
    - 返回以毫秒为单位的当前时间。
      - 1000 毫秒 = 1秒 
      - 返回的是相对时间
      - 即：当前时间与协调世界时 1970 年 1 月 1 日午夜之间的时间差（以毫秒为单位测量）
    - 示例：
      - 1970-1-1 00:00:00：返回0
      - 1970-1-1 00:00:01：返回1000
      - 1970-1-1 00:01:00：返回1000 * 60
      - 1970-1-1 01:00:00：返回1000 * 60 * 60
    - 注意: 
      - 当返回值的时间单位是毫秒时，值的粒度取决于底层操作系统，并且粒度可能更大。例如，许多操作系统以几十毫秒为单位测量时间。
    - 应用场景：
      - 可以在开始和结束分别求时间点，并相减得出程序的运行时间(单位：毫秒) 
    - 代码示例：
    	
	```java
	long start = System.currentTimeMillis();
		for (int i = 0; i < 1000000; i++) {
			System.out.println(i);
		}
		long end = System.currentTimeMillis();
		System.out.println(end-start);    
   	/* 输出：
	...
	999998
	999999
	1845
	*/	
	```
    
- ### exit
  - static void	exit(int status) 
    - 终止当前正在运行的 Java 虚拟机
    - 参数用作状态码；根据惯例，非 0 的状态码表示异常终止。
    - 终止代码：`System.exit(0);`
    - 代码示例：
    ```java
	for (int i = 0; i < 1000; i++) {
		System.out.println(i);
		if(i==100)
			System.exit(0);//当i==100时，终止虚拟机
	}  
	/* 输出：
	...
	97
	98
	99
	100
	*/
    ```

- ### gc
  - static void	gc():
    - 运行垃圾回收器 
    - 调用 gc 方法暗示着 Java 虚拟机做了一些努力来回收未用对象，以便能够快速地重用这些对象当前占用的内存。
    - 当控制权从方法调用中返回时，虚拟机已经尽最大努力从所有丢弃的对象中回收了空间。
      - "尽最大努力"：意味着不一定会全部回收。 
    - 系统会自动调用。 
  - Object中的 protected void finalize(): 
    - 当垃圾回收器确定不存在对该对象的更多引用时，由对象的垃圾回收器调用此方法。
    - 可以重写并加入一些首尾的工作。
  - 代码示例：
	```java
	public class SystemDemo {
		public static void main(String[] args) {
			new Demomo();
			System.gc();//多次执行后，输出："我被回收了"
		}
	}

	class Demomo{//默认继承并重写Object的finalize方法
		@Override
		protected void finalize() throws Throwable {
			// TODO Auto-generated method stub
			System.out.println("我被回收了");
		}
	}	
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Date
- ### 类 Date 概述
  - 表示特定的瞬间，精确到毫秒。
  - 可以通过方法来设定自己所表示的时间，可以表示任意时间。
  - util包和sql包(util的子类)下都有同名Date类，现在主要看util下的
    - 注意导包不要导错。 

- ### Date类的构造方法
  - 空构造 Date():
    - 创建的是一个表示当前系统时间的Date对象。
    - toLocaleString方法：返回系统时区格式相匹配的方法，但是过时了
    - 代码示例：
    ```java
	import java.util.Date;

	public class DateDemo {
		public static void main(String[] args) {
			Date d = new Date();
			System.out.println(d);//Fri May 13 18:43:35 CST 2022
			System.out.println(d.toLocaleString());//2022年5月13日 下午6:44:02
		}
	}    
    ```
  - 有参构造Date(long date)：参数为毫秒值的构造方法
    - 根据“指定时间”创建Date对象 
    - 基本时间仍然是：1970-1-1 00:00:00 + 时区差
    - 参数：在基本时间基础上添加的毫秒数之后的date值
    - 代码示例：    
    ```java
	import java.util.Date;
	public class DateDemo {
		public static void main(String[] args) {
			Date d2 = new Date(1000 * 60 * 60 * 24);//基本时间+1秒*1分*1小时*1天
			System.out.println(d2.toLocaleString());//1970年1月2日 上午8:00:00 - 8点是东八区快8小时
		}
	}    
    ```
 
- ### Date类要掌握的功能
  - 毫秒到日期的转换
    - void setTime(long time); 
      - 使用给定毫秒时间值设置现有 Date 对象 
    - 设置date，返回值是void，参数是long。
    - 毫秒值到date值的其他方法：Date(long date)：参考上面的带参构造方法
  - 日期到毫秒的转换
    - long getTime();
    - 获取值，返回值是long，参数是void
  - 代码示例：
  	```java
	import java.util.Date;
	public class DateDemo {
		public static void main(String[] args) {
			Date d = new Date();
			d.setTime(1000 * 60 * 60);
			System.out.println(d.toLocaleString());
			System.out.println(d.getTime());
		}
	}  
  	```


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## DateFormat
- ### DateFormat概述
  - DateFormat类是对日期进行格式化的类 
  - 位于java.text包下：
    - 这个包下大部分是格式化相关的类
  - DateFormat: 抽象类
    - 抽象类的使用：通过子类调用 / 通过静态方法调用 
    - 直接已知子类：SampleDateFormat:
      - SampleDateFormat：以与语言环境有关的方式来格式化和解析日期的具体类，允许进行格式化(日期->文本)、解析(文本->日期)和规范化。

- ### DateFormat要掌握的功能
  - 从日期到字符串的转换：格式化
    - Date to String
      - eg. 想要"2049年8月26日"而不是"2049-8-26"这种格式
    - String format(Date date) 
  - 从字符串到日期的转换：解析
    - String to Date
      - eg. 想要"2049年8月26日"的后一天 
    - Date parse(String sourse)
  - 构造方法：
    - SimpleDateFormat(): 使用默认的模式进行对象的构建
      - 示例：`SimpleDateFormat sdf = new SimpleDateFormat();` 
    - SimpleDateFormat(Sting pattern): 使用指定的模式进行对象的构建
      - 示例：`SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");`
  - 指定模式：
    - API规定的模式字母（所有其他字符 'A' 到 'Z' 和 'a' 到 'z' 都被保留）
      - 详见API SampleDateFormat文档 
    - 常用：
      - 年 月 日 时:分:秒 -- yyyy年MM月dd日 HH:mm:ss 
  - 注意：
    - 需要导入相应的包 
    - 解析的字符串，模式必须和构建对象的模式一样；
    - 否则会报错：java.text.ParseException 
  - PS: parse |pa:z| 解析
  - 代码示例：
  	```java
	import java.text.ParseException;
	import java.text.SimpleDateFormat;
	import java.util.Date;
	
	//class...
	public static void main(String[] args) throws ParseException {//抛出异常：sdf.parse()
		//使用默认模式进行对象的构建
		SimpleDateFormat sdf = new SimpleDateFormat();
		Date d = new Date();//创建日期对象
		
		//格式化：把日期对象转换成字符串
		String s = sdf.format(d);
		System.out.println(s);//2022/5/16 下午6:24
		
		//解析：把字符串转换成日期对象
		Date date = sdf.parse("2022/5/16 下午6:24");
		System.out.println(date.toLocaleString());//2022年5月16日 下午6:24:00
		
		//Date date2 = sdf.parse("2020年2月28日");//Exception in thread "main" java.text.ParseException: Unparseable date: "2020年2月28日"
		
	}  
  	```
	
	```java
	public static void main(String[] args) throws ParseException {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");//指定模式的构造方法
		Date d = new Date();
		
		String s = sdf.format(d);//格式化
		System.out.println(s);//2022年05月16日 18:44:45
		
		Date date = sdf.parse("2088年05月16日 18:44:45");//解析
		System.out.println(date.toLocaleString());//2088年5月16日 下午6:44:45 (修改传入的日期，则输出结果也相应地改变)
		
	}	
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->


## Calendar
- ### Calendar类概述
  - 日历类，用于替代Date类的使用。
  - 它里面提供了很多功能来单独获取日历的某个数据。

- ### Calendar类的使用
  - util包下 `import java.util.Calendar;`
  - 抽象类，但是提供方法用于获取子类对象
  - 创建对象:
    - static Calendar getInstance():
      - 使用默认时区和语言环境获得一个日历 
      - 静态，直接类名调用
    - 代码示例：
      - `Calendar c = Calendar.getInstance();` 
  - 获取 
    - int get(int field): 返回指定日历字段的值
      - field: 给定的日历字段，即已经定义好的字符，可以由字段名调用
      - 注意：
        - MONTH: 在格里高利历和罗马儒略历中一年中的第一个月是 JANUARY，它为 0 -- 因此需要在获取值的基础上+1才是想要获取到的值
    - 示例：
      - public static final int YEAR = 1
      - `System.out.println(Calendar.YEAR);//输出：1` 
    - 代码示例：
    ```java
	import java.util.Calendar;
	public class CalendarDemo {
		public static void main(String[] args) {
			Calendar c = Calendar.getInstance();
			//System.out.println(Calendar.YEAR);//1

			int year = c.get(Calendar.YEAR);
			int month = c.get(Calendar.MONTH) + 1;//此处注意MONTH的起始值是0，实际月应+1
			int day = c.get(Calendar.DAY_OF_MONTH);
			System.out.println(year + "年" + month + "月" + day + "日");//2022年5月16日
			//注意：year等变量是int类型，syso语句直接用加号+连接会数值相加
		}
	}    
    ```
  - 修改
    - void set(int field, int value):
      - 把指定字段field修改为指定的值 
    - 示例：
    ```java
	c.set(Calendar.YEAR, 1999);
	int year = c.get(Calendar.YEAR); 
	syso(year);//输出：1999
    ```
  - 添加
    - void add(int field, int value):
      - 在指定字段上加上指定的值
    - 示例：
    ```java
	c.add(Calendar.MONTH, -3);//可以是负数(时间倒流)，和可以超过12(自动累加到第二年)
	int month = c.get(Calendar.MONTH)+1;
	syso(month);//2022年2月17日
    ```
     
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




##


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->

### END
