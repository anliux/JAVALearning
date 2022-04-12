# Java常用API

### 目录


<!--GFM-TOC -->
* [API概述](#api概述): API概述，Scanner获取字符串
* [String类](#string类): 
* [StringBuilder](#stringbuilder)
* []()
* []()
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
      - `String s1 = new String(“hello”);`
    - 直接赋值创建字符串对象
      - `String s2 = "hello";`
      - `String s3 = "hello";`
  - `==`:
    - 基本数据类型：比较的是基本数据类型的值是否相等。
    - 引用数据类型：比较的是引用数据类型的地址值是否相等。
  - 比较结果：`s1==s2:false;` `s1==s3:false;` `s2==s3:true;`
    - s1: new存入堆内存中地址值为001并开辟空间，而这个空间里存的不是"hello", 而是这个字符串在方法区的常量池中的地址值002
      - 字符串的内容("hello")是存储在方法区的常量池中的，为了方便字符串的重复使用。
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
      - 大小写转换是字符串String的方法，不能用charAt()截取。
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
    - 主函数调用：`String str = reverse(s);`

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## StringBuilder
- ### StringBuilder类概述
  - 字符串缓冲区，可变字符串。
  - 字符串拼接的弊端
    - 每次拼接，都会构建一个新的String对象，既耗时，又浪费空间。
    - 图解：
    ![String拼接浪费空间](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/api/String%E6%8B%BC%E6%8E%A5%E6%B5%AA%E8%B4%B9%E7%A9%BA%E9%97%B4.bmp)
    - 而StringBuilder就可以解决这个问题。

- ### StringBuilder和String的区别?
  - String: 内容固定，不可变。
  - StringBuilder：可变字符串。
  
- ### StringBuilder构造方法：
  - 无参构造：`public StringBuilder()`
    - 构造一个不带任何字符的字符串生成器，其初始容量为 16 个字符。

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
    - 代码示例：
      - `sb.append("hello"); sb.append(true); sb.append(100); //输出：hellotrue100`
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



## 待续。。。





### END
