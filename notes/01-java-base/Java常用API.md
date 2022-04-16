# Java常用API

### 目录


<!--GFM-TOC -->
* [API概述](#api概述): API概述，Scanner获取字符串
* [String类](#string类): String概述, 构造方法(4种)及对比, 判断功能(4种), 获取功能(5种), 转换功能(3种), 其他功能(2种), 相关典型问题
* [StringBuilder](#stringbuilder): 
* [对象数组的练习](#对象数组的练习): eclipse自动生成构造函数、get/set方法
* [集合类与ArrayList](#集合类与arraylist):
* [ArrayList案例分析](#arraylist案例分析): 
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
	```
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
	```
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
	```
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
    - `public E get(int index)` -- 返回指定索引处的元素
    - get方法不改变原有集合
  - 集合长度：
    - `public int size()` -- 返回集合中的元素的个数
  - 删除元素：
    - `public boolean remove(Object o)` -- 删除指定的元素，并返回删除是否成功（布尔型）
    - `public E remove(int index)` -- 删除指定索引处的元素，并返回被删除的元素
  - 修改元素：
    - `public E set(int index, E element)` -- 修改指定索引处的元素，返回被修改的元素（原来的元素）


- ### 增删改查的代码演示
	```
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
			System.out.println("set:"+array.set(1, "android"));//set:java

			System.out.println("array:"+array);//array:[hello, android, world]

		}
	}

	```

- ### 集合遍历
  - 用for循环 + size方法 + get方法
  - 注：常规的做法是，输出时，先将get获取到的元素存储在变量中，然后输出变量。

- ### 集合遍历的代码演示
	```
	package com.itcast01;

	import java.util.ArrayList;

	public class ArrayListDemo3 {
		public static void main(String[] args) {
			//新建集合
			ArrayList<String> array = new ArrayList<String>();
			array.add("hello");
			array.add("world");
			array.add("java");
			for(int i = 0; i < array.size(); i++) {
				//System.out.println(array.get(i));
				String s = array.get(i);
				System.out.println(s);
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
    - size，get，startswith，
  - 代码：
  	```
	package com.itcast01;

	import java.util.ArrayList;

	public class ArrayListTest {
		public static void main(String[] args) {
			String[] strArray = {"张三丰","宋远桥", "张无忌","殷梨亭","张翠山","莫声谷"};
			ArrayList<String> array = new ArrayList<String>();
			for(int i = 0; i < strArray.length; i++) {
				array.add(strArray[i]);
			}
			System.out.println(array);
			for(int j = 0; j < array.size(); j++) {
				String s = array.get(j);
				if(s.startsWith("张"))
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
    - ArrayList<Student>
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
   ```
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

   ```
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

- ### 学生管理系统

	


	
	
	
	
	
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->
	
	








<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->





##

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




##

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




##


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->


##


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




##


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->


### END
