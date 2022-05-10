# Java面向对象

### 目录


<!--GFM-TOC -->
* [面向对象思想概述](#面向对象思想概述): 面向过程与面向对象，面向对象思想的3个特点
* [类与对象](#类与对象): 认识，类与对象的关系，类的定义和使用，内存图解
* [成员变量和局部变量的区别](#成员变量和局部变量的区别): 类中位置不同，内层中位置不同，生命周期不同，初始化值不同
* [私有](#私有): 引入私有，private关键字，private最常见应用
* [封装](#封装): 封装的概述，面向对象三大特征之一，封装的原则，封装的好处
* [this关键字](#this关键字): 成员变量和局部变量同名时辨析，this关键字引入的必要性，含义和使用
* [构造方法](#构造方法): 作用，格式，无参构造带参构造，调用，注意事项
* [标准类的代码编写与测试](#标准类的代码编写与测试): 以Student类为例展示
* [类名作为形式参数和返回值](#类名作为形式参数和返回值): 类合理联想到对象实体
* [static关键字](#static关键字): static概述, 特点, 静态/非静态相互调用, 优缺点, 应用场景与Math类, static自定义工具类
* [代码块](#代码块): 代码块概述, 局部代码块, 构造代码块, 静态代码块, 涉及代码块执行顺序的面试题分析
* [继承](#继承): 概述, 特点, 继承的成员变量和成员方法, 方法的重写, 注解`@`, 继承中的构造方法, super, 继承的优缺点
* [抽象类](#抽象类): abstract关键字, 抽象类概述, 特点, 成员特点, 抽象类的细节问答, 抽象类在API中的应用
* [接口](#接口): 概述, 成员特点, 接口与类的关系, 接口思想与API, 接口的优点, 接口与抽象类的关系, 运动员案例示例
* [匿名对象](#匿名对象): 匿名对象概述, 应用场景, 问题
* []():
* []()
* []()

<!--GFM-TOC -->



## 面向对象思想概述
- ### 面向过程开发
  - 面向着具体的每一个步骤和过程，把每一个步骤和过程完成，然后由这些功能方法相互调用，完成需求。
  - 面向过程的思想：强调的是每一个功能的步骤，“执行者”。
  - 面向过程的代表语言：C语言

- ### 面向对象思想
  - 把步骤和功能在进行封装，封装时根据不同的功能，进行不同的封装，功能类似的封装在一起。
  - 这样结构就清晰了很多。用的时候，找到对应的类就可以了。
  - 这就是面向对象的思想。
  - 面向对象思想：强调的是对象，然后由对象去调用功能，”指挥者“。

- ### 面向对象思想特点：3个（思考习惯，简单化，角色转换）
  - 更符合思考习惯的思想；
  - 将复杂的事情简单化；
  - 从执行者变成了指挥者，角色发生了转换。
  - 面向对象思想举例：买电脑，洗衣服。
    - 面向过程的买电脑：
      - 我要买电脑 -- 要明确买电脑的意义 -- 上网查对应参数信息 -- 去中关村买电脑 -- 讨价还价 -- 搬回电脑。
    - 面对对象的买电脑：
      - 我要买电脑 -- 班长去给我买电脑 -- 买回电脑。
      - 使用"班长"做了整个买电脑的过程细节。
    - 面向过程的洗衣服：
      - 脱衣服 -- 找盆 -- 放洗衣粉 -- 放水 -- 浸泡 -- 搓洗 -- 拧干 -- 晾衣服。
    - 面向对象的洗衣服：
      - 脱衣服 -- 打开全自动洗衣机 -- 放入衣服 -- 按按钮 -- 晾衣服。 
  - 注：面试时问到"对面向对象的理解"：三个特点，并具体举例。

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 类与对象
- ### 分析 
  - 学习编程语言，就是为了模拟现实世界的事物，实现信息化。
  - 如何表示一个现实世界事物呢：属性和行为。
    - 属性：就是该事物的描述信息；
    - 行为：就是该事物能够做什么；
    - 举例：学生事物
  - 类：
    - 我们学习的Java语言最基本单位是类；
    - 所以，我们就应该把事物用一个类来体现。

- ### 类和对象的关系
  - 类：用于描述现实世界的事物，是一组相关的属性和行为的集合。
  - 对象：是该类事物的具体体现。
  - 类与对象：类相当于抽象概述，对象相当于类对应的具体实物。
  - 举例：
    - 类：学生；对象：班长(学生中具体的一员)
    - 类：动物；对象：老虎。 

- ### 类的定义与使用
  - 概述：用于描述现实世界的事物，是一组相关的属性和行为的集合。
    - 属性：事物的描述信息
    - 行为：事物能做什么
  - Java中用class描述事物：
    - 成员变量：就是事物的属性(和以前定义变量是一样的)
      - 位置不同：在类中，方法外。
      - 初始化值：不需要给初始化。
    - 成员方法：就是事物的行为(和以前定义方法是一样的)。
      - 不同：把static去掉。
  - 定义类：其实就是定义类的成员(成员变量和成员方法)
  - eclipse中定义类：
    - project中的包中的类：一个类对应一个Java文件，相当于一个Java文件包含一个特定类
    - 举例：`Student.java`中仅放’学生类‘的成员变量和成员方法，而main方法需要新建一个`StudentDemo.java`的文件
  - 类的使用：
    - 学生类(讲解)
      - 如何定义：白话解释如下
        - 使用一个类，就是使用该类的成员(成员变量、成员方法)；
        - 要想使用一个类的成员，就必须先拥有该类的对象
        - 如何拥有一个类的对象呢？创建对象即可。
      - 如何使用：创建对象 `类名 对象名 = new 类名();`
      - 如何访问：
        - 成员变量：
          - 先赋值后使用：`对象名.成员变量a=xxxx;`; `对象名.成员变量b=xxxx;`
	  - `对象名.成员变量` -- 先赋值后使用(因为定义中并没有初始化,直接用是默认值)
	- 成员方法：
	  - `对象名.成员方法(...)` 
	  - 按方法的参数列表，传入小括号相应的值，或为空。
  - 手机类练习-代码示例
	
	```java	
	/*	Phone.java:
	 *	手机类：
	 * 		成员变量：品牌，价格，颜色...
	 * 		成员方法：打电话，发短信...
	 */
	public class Phone {
		//品牌
		String brand;
		//价格
		int price;
		//颜色
		String color;
	
		//打电话
		public void call(String name) {
			System.out.println("给"+name+"打电话");
		}
		
		//发短信
		public void sendMessage() {
			System.out.println("群发短信");
		}
	}
	```

	```java
	/*
	 * PhoneDemo.java:
	 * 手机类的测试类
		*/
	public class PhoneDemo {
		public static void main(String[] args) {
			//创建对象
			Phone p = new Phone();
			
			//输出成员变量值
			System.out.println("品牌："+p.brand);//null
			System.out.println("价格："+p.price);//0
			System.out.println("颜色："+p.color);//null
			System.out.println("------------");
			
			//给成员变量赋值
			p.brand = "锤子";
			p.price = 2999;
			p.color = "棕色";
			
			//再次输出成员变量值
			System.out.println("品牌："+p.brand);//锤子
			System.out.println("价格："+p.price);//2999
			System.out.println("颜色："+p.color);//棕色
			System.out.println("------------");
			
			//调用成员方法
			p.call("林青霞");
			p.sendMessage();
		}
	}
	```

- ### 对象内存图解
  - 一个对象的内存图
    - 顺序是：先有方法区的内容，之后main方法入栈，有new动作时，对象进入堆
    ![一个对象的内存图](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/class/%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.bmp)
  - 方法公用的内存图: 重点是对方法区方法的共用
    ![方法公用的内存图](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/class/%E6%96%B9%E6%B3%95%E5%85%B1%E7%94%A8%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.bmp)
  - 两个引用指向同一个对象的内存图
    ![两个引用指向同一个对象的内存图](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/class/%E4%B8%A4%E4%B8%AA%E5%BC%95%E7%94%A8%E6%8C%87%E5%90%91%E5%90%8C%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.bmp)
  - 注：
    - class和成员变量、成员方法在方法区，公用。
    - 成员方法有一个地址值，当堆中的对象调用时，按照地址找到该方法。

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 成员变量和局部变量的区别
- ### 在类中的位置不同 
  - 成员变量：类中方法外
  - 局部变量：方法内或者方法声明上（形式参数）

- ### 在内存中的位置不同
  - 成员变量：堆内存
  - 局部变量：栈内存

- ### 生命周期不同
  - 成员变量：随着对象的存在而存在，随着对象的消失而消失
  - 局部变量：随着方法的调用而存在，随着方法的调用完毕而消失

- ### 初始化值不同
  - 成员变量：有默认的初始化值
  - 局部变量：没有默认的初始化值，必须先定义，赋值，才能使用(否则报错)

- ### 参考代码
  ```java
  public class Variable{
  	int x; //成员变量
	public void show(){
		int y = 0; //局部变量
		syso(x);
		syso(y);
	}
  }
  ```
  
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 私有 
- ### 成员变量安全问题
  - 通过对象直接访问成员变量，存在数据安全问题。
  - 能不能不让外界直接访问成员变量：能。私有化。 

- ### private关键字
  - 是一个权限修饰符。
  - 可以修饰成员(成员变量和成员方法)
  - 被private修饰的成员只在本类中才能访问。

- ### private最常见的应用：
  - 把成员变量用private修饰，提供对应的getXxx()/setXxx()的公共方法(public)，用于获取和设置。
    - 这样可以在赋值时设置一些特定的约束条件，进行判断，保证安全。
  - 一个标准的案例的使用
	```Java
	//相应类中定义：
	private int age;
	public void setAge(int a){ //对传进来的参数进行判断
		if(age <0 || age >200)
			syso("数据有误");
		else
			age = a;
	}
	public void getAge(){
		return age;
	}
	
	//引用：
	//s.setAge(28); 
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 封装
- ### 封装概述
  - 是面向对象三大特征之一
  - 是面向对象编程语言对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界无法直接操作和修改。就像刚才说的年龄。

- ### 封装原则：
  - 将不需要对外提供的内容都隐藏起来。
  - 把属性隐藏，提供公共方法对其访问。
    - 成员变量private，提供对应的getXxx()/setXxx()方法

- ### 好处：
  - 通过方法来控制成员变量的操作，提高了代码的安全性
  - 把代码用方法进行封装，提高了代码的复用性

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## this关键字
- ### this:代表所在类的对象引用
  - 起名需要做到见名知意
  - 但这容易重名，造成不确定性。

- ### 同名辨析
  - 就近原则：成员变量与局部变量同名，且局部范围内同时出现成员变量和局部变量时，就近原则选取其指向。
  - 示例：
	```java
	//错误示范：
	private int age;
	public void setAge(int age){
		age = age; //这里第一个age默认为就近的参数age，而不是外部的成员变量age。
			   //因此最终并不能将传入的值赋值给成员变量，而是做了一个无用功(本身赋值给本身)，成员变量依然是默认初始化值。
	}
	```

	```java
	//正确示范：使用this关键字进行区分
	private int age;
	public void setAge(int age){
		this.age = age; //这里第一个age代表所在类的对象引用，即指向成员变量。
				//第二个age就近原则，指向传入的参数。
			        //因此最终能将传入的值赋值给成员变量。
	}
	```

- ### this的含义：
  - 方法被哪个对象(某个抽象的类对应的具体的对象实体)调用，this就代表那个对象(即对应的是类)

- ### 使用场景--this
  - 局部变量隐藏成员变量 (区分上述的同名情况)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 构造方法
- ### 构造方法作用
  - 给对象的数据进行初始化
  - #### 成员变量赋值：setXxx()方法；带参构造方法。

- ### 构造方法格式
  - 位置：类中
  - 方法名：方法名与类名相同
  - 返回值：没有返回值类型，连void都没有；没有具体的返回值
  - 分类：无参构造，带参构造
  - 示例：`public Student(){}`

- ### 构造方法调用
  - 通过new关键字调用
  - 格式：`类名 对象名 = new 构造方法(...);`
  - 示例：`Student s = new Student();` -- 同new对象的格式。

- ### 构造方法注意事项
  - 如果不提供构造方法，系统会给出默认的无参构造方法；
  - 如果提供了构造方法，系统将不再提供默认的无参构造方法；
    - 此时如果想使用无参构造方法，需要自己提供。
  - 建议：自己给出无参构造方法，避免报错。
  - 构造方法可以重载的
    - `public Student(){} //无参构造方法，创建时用 Student s = new Student();`
    - `public Student(String name)(this.name=name;) //带参构造方法,创建时直接传入对应的参数 Student s = new Student("林青霞");`
    - `public Student(String name, int age){this.age=age;} //带参构造方法，创建时同传入对应的参数 Student s = new Student("linda",28);`
  - 注意：
    - 这种直接的初始化也是可以接受的，因为只要是方法中，就可以对传入的参数设置相应的判断，以保证安全性。

- ### 代码示例
	```java
	public class Student {
		private String name;
		private int age;
		
		public Student() {}
		
		public Student(String name) {
			this.name = name;
		}
		
		public Student(int age) {
			this.age = age;
		}
		
		public Student(String name,int age) {
			this.name = name;
			this.age = age;
		}

		public void show() {
			System.out.println(name+"---"+age);
		}
	}

	public class StudentDemo {
		public static void main(String[] args) {
			//如何调用构造方法呢?
			//通过new关键字调用
			//格式：类名 对象名 = new 构造方法(...);
			Student s = new Student();
			s.show();
			
			//public Student(String name)
			Student s2 = new Student("林青霞");
			s2.show();
			
			//public Student(int age)
			Student s3 = new Student(28);
			s3.show();
			
			//public Student(String name,int age)
			Student s4 = new Student("林青霞",28);
			s4.show();
		}
	}
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 标准类的代码编写与测试
- ### 类
  - 成员变量
  - 构造方法
    - 无参构造方法
    - 带参构造方法
  - 成员方法
    - getXxx()
    - setXxx()

- ### 给成员变量赋值的方式
  - 无参构造方法+setXxx()
  - 带参构造方法

- ### 代码示例
	```java
	public class Student {
		//成员变量
		private String name;
		private int age;
		
		//构造方法
		public Student() {}
		
		public Student(String name,int age) {
			this.name = name;
			this.age = age;
		}
		
		//成员方法
		public void setName(String name) {
			this.name = name;
		}
		
		public String getName() {
			return name;
		}
		
		public void setAge(int age) {
			this.age = age;
		}
		
		public int getAge() {
			return age;
		}
	}
	```

	```java
	public class StudentDemo {
		public static void main(String[] args) {
			//无参+setXxx()
			Student s = new  Student();
			s.setName("林青霞");
			s.setAge(28);
			System.out.println(s.getName()+"---"+s.getAge());
			
			//带参构造
			Student s2 = new Student("林青霞",28);
			System.out.println(s2.getName()+"---"+s2.getAge());
		}
	}
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 类名作为形式参数和返回值
- ### 类名作为形式参数案例
  - 要的其实是该类的对象：类合理联想到对象实体
  - 代码示例：
	```Java
	//需求： 调用Teacher的test方法
	//类名作为形式参数：其实这里需要的是该类对象。
	public class Test {
		public static void main(String[] args) {
			Teacher t = new Teacher();
			Student s = new Student();
			t.test(s);
		}
	}

	public class Teacher {
		public void test(Student s) { //类名作为形式参数
			s.study();
		}
	}

	public class Student {
		public void study() {
			System.out.println("好好学习,天天向上");
		}
	}
	```

- ### 类名作为返回值案例
  - 如果返回值是类名，返回的其实是该类的对象：类合理联想到对象实体
  - 代码示例：
	```Java
	//需求： 通过Teacher得到Student对象，然后调用Student类的方法
	//如果方法的返回值是类名：其实返回的是该类的对象
	public class Test {
		public static void main(String[] args) {
			Teacher t = new Teacher();
			Student s = t.getStudent();
			s.study();
		}
	}

	public class Teacher {	
		public Student getStudent() { //类名作为返回值
			Student s = new Student();
			return s;
		}
	}

	public class Student {
		public void study() {
			System.out.println("好好学习,天天向上");
		}
	}
	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## static关键字
- ### 静态static关键字概述
  - 关键字，修饰符，用于修饰成员变量和成员方法
  - 代码示例：
	  ```java
	  class Person{
		String name;
		int age;
		static Sting graduateFrom;//毕业院校
		public void speak(){
			System.out.println(name + age + graduateFrom);
		}
	  }
	  ```
  
- ### 静态static的特点：
  - 被所有对象所共享；
    - 若当一个变量是static而开局没有初始化, 则当第一个对象进行了定义，后面的对象的该变量默认值都是第一个对象定义好的值，进行了共享。
  - 可以使用类名调用；
    - 代码示例：
      - `Person.graduateFrom = "传智学院";`，则后面所有对象的默认graduateFrom参数都是此处定义好的
  - 静态的加载优先于对象，是随着类的加载而加载的。
    - 随着该类的字节码文件的加载而加载。 
  
- ### 静态/非静态的相互调用 
  - 静态方法：静态只能访问静态(成员变量和成员方法)
    - 理解为：静态加载时，非静态的成员挂靠在对象，还没有生成呢，不存在的东西不能使用。
    - 可以调用静态的成员变量；
    - 可以调用静态的成员方法；
    - 不可以调用非静态成员变量；
    - 不可以调用非静态成员方法。
  - 非静态方法：既可访问静态，又可访问非静态
    - 理解为：静态先于非静态加载，有非静态时一定有静态在了，可以用没有冲突。
    - 可以调用静态的成员变量；
    - 可以调用静态的成员方法；
    - 可以调用非静态的成员变量；
    - 可以调用非静态的成员方法。
  - 静态方法中不可以定义this, super关键字
    - 理解为：静态加载时还没有对象
  - 代码示例：
	  ```java
	  public class StaticDemo{
		public static void main(String[] args){
			Student.graduateFrom = "传智学院";
			Student.study();
			//输出：传智学院(回车) sleep
		}
	  }

	  class Person{
	  	String name;
		int age;
		static String graduateFrom;//毕业院校
		
		public static void study(){//静态的成员方法：调用测试区
			System.out.println(graduateFrom);//静态方法可以调用静态的成员变量
			sleep();//静态方法可以调用静态的成员方法
			
			//syso(name);//报错：静态方法不能调用非静态的成员变量
			//eat();//报错：静态方法不能调用非静态的成员方法
		}
		public static void sleep(){//静态的成员方法
			System.out.println("sleep");
			//this.xx：空白，召唤不出任何东西。//非静态中不能使用this关键字
		}
		public void eat(){//非静态的成员方法
			System.out.println("eat");
			System.out.println(graduateFrom);//非静态方法可以调用静态的成员变量
			sleep();//非静态方法可以调用静态的成员方法
			//非静态：调用非静态成员变量和方法是之前一直在做的事，可以调用。
		}
	  }
	  ```

- ### 静态的优缺点：
  - 优点：
    - 对对象的共享数据提供单独空间的存储，节省空间，没有必要每一个对象都存储一份
    - 可以直接被类名调用,不用在堆内存创建对象
  - 缺点：
    - 访问出现局限性。（静态虽好，但只能访问静态）
 
- ### 静态的应用场景
  - Math类的使用：典型应用
  - Math:
    - 查阅API进行学习
    - 包含基本的数学运算方法
    - lang包下：不用导包
    - Math的所有方法都是static静态的
    - Java没有提供构造方法：直接通过类名调用，和对象无关
    - 常用方法示例：
      - static double PI: `syso(Math.PI);//直接类名Math调用，输出π的值`
      - static double max(double a, double b): min()同，求最值
        - `syso((Math.max(3,4));//返回值：4`
      - static double abs(double a): 
        - 求绝对值，返回double类型，但一般不新增小数点；注意求绝对值方法有4中数据类型的重载
	- `syso((Math.abs(-10));//返回值：10`
      - static double ceil(double a): 
        - 天花板，向上取整，返回double类型, 会补一个小数点位 (不涉及四舍五入)
	- `syso((Math.ceil(-1.23));//返回值: -1.0`
      - static double floor(double a): 
        - 地板，向下取整，返回double类型, 会补一个小数点位 (不涉及四舍五入)
	- `syso((Math.floor(-1.23));//返回值: -2.0`
      - static long round(double a): 
        - 四舍五入，返回long类型
	- `syso((Math.round(1.23));//返回值：1`
	- `syso((Math.round(1.83));//返回值：2`
	- `syso((Math.round(-1.23));//返回值：-1`
	- `syso((Math.round(-1.83));//返回值：-2`
      - static double pow(double a, double b):
        - a的b次幂
        - `syso((Math.pow(2,3));//返回值：2^3=8.0`
      - static double random(): 
        - 返回一个带正号、介于0.0-1.0之间的double值随机数
        - `syso((Math.random());//返回值: 0.34674326810933...`

- ### 静态自定义工具类
  - 将不需要new对象的方法定义为静态后直接调用
  - 代码示例：
	  ```java
	  //MyArrays.java
	  public class MyArrays{
		private MyArrays(){}//不需要创建对象，私有构造函数

		//求最大值：返回数据中的最大元素 <设定为自然数最值>
		public static int getMax(int[] arr){
			int max = 0;//参照物
			for(int i = 0; i<arr.length; i++){
				if(arr[] > max)
					max = arr[];
			}
			return max;
		}

		//返回数组中指定参数的索引
		public static int getIndex(int[] arr, int a){
			for(int i=0; i<arr.length; i++){
				if(arr[i] == a)
					return i;
			}
			return -1;
		}
	  }
	  ```
	  
	  ```java
	  //MyArrayDemo.java
	  public class MyArrayDemo{
	  	public static void main(String[] args){
			int[] arr = {3,5,8,10,2};
			int max = MyArray.getMax(arr);//类名调用获取最值方法
			syso(max);
			int index = MyArray.getIndex(arr,8);//类名调用获取索引值方法
			syso(index);
		}
	  }
	  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 代码块
- ### 代码块概述：
  - 在代码中，用{}括起来的代码被称为代码块
  
- ### 分类：
  - 局部代码块
    - 在方法中出现，控制变量生命周期(作用域)
    - 好处：及早释放，提高内存利用率
    - 代码示例：
	    ```java
	    //写在main函数中的局部代码块
	    public static void main(String[] args){
		{int num = 10;}
		System.out.println(num);//代码块中的num生命周期已结束，此处syso语句中已经读取不到num
	    }

	    ```
  - 构造代码块
    - 在<类中方法外>出现，抽取<构造方法>中的共性
    - 执行：每次创建对象都会执行，并且在构造方法前执行。
    - 代码示例：
	    ```Java
	    public Teacher{
	    	String name;
		int age;
		{System.out.println("我爱Java");}
		public Teacher(){
			syso("我是无参空构造");
		}
		public Teacher(String name, int age){
			syso("我是带参构造");
			this.name = name;
			this.age = age;
		}
	    }

	    ```
	    ```Java
	    //调用输出：
	    public static void main(String[] args){
	    	Teacher t1 = new Teacher();
		Teacher t2 = new Teacher("小张老师",18);
	    }
	    /*
	    输出：<构造代码块先于构造方法执行>
	    我爱Java
	    我是无参空构造
	    我爱Java
	    我是带参构造
	    */    
	    ```
  - 静态代码块
    - 在<类中方法外>出现，并加上static修饰；
    - 用于给类进行初始化，在加载的时候就执行，并且只执行一次。
    - 一般用于加载驱动
    - 代码示例：
	    ```java
	    public class BlockDemo {
		public static void main(String[] args) {
			Teacher t1 = new Teacher();
			Teacher t2 = new Teacher("小张老师",18);
		}
	    }

	    class Teacher{
		String name;
		int age;
		static{//静态代码块
			System.out.println("我的静态代码块");
		}

		{//构造代码块
			System.out.println("我是构造代码块");
		}

		public Teacher() {
			System.out.println("我是无参空构造");
		}
		public Teacher(String name, int age) {
			System.out.println("我是带参构造");
		}

	    }
	    /*
	    输出：
		我的静态代码块
		我是构造代码块
		我是无参空构造
		我是构造代码块
		我是带参构造
	    */
	    ```
  - 静态代码块和构造代码块的执行顺序：
    - 静态代码块>构造代码块>构造函数内代码
    - 静态代码块只执行一次
    - 构造代码块：构造一次对象(new一次对象)，执行一次
  - 同步代码块(多线程讲)

- ### 代码块面试题
  - 考查代码块的执行顺序
    - 开始执行主函数，需要先加载BlockTest, 于是先执行BlockTest的静态代码块
    - 然后执行主函数
    - 之后执行`Coder c1 = new Coder();`
      - 用到Coder类：Coder类第一次被加载，先加载Coder的静态代码块
      - `Coder c1 = new Coder();`: 先加载Coder的构造代码块，后加载无参构造
      - `Coder c2 = new Coder();`: 先加载Coder的构造代码块，后加载无参构造
    - 注意：
      - 静态代码块只在第一次加载该类的时候用到，因此Coder类的静态代码块只执行了一次。 
      - 没有用到主函数所在的BlockTest的《构造代码块》和《无参构造》，是因为没有创建BlockTest的对象。
  - 代码示例：
	```java
	public class BlockTest {
		static {
			System.out.println("BlockTest静态代码块执行了");
		}
		{
			System.out.println("BlockTest构造代码块执行了");
		}
		public BlockTest() {
			System.out.println("BlockTest无参空构造执行了");
		}
		public static void main(String[] args) {
			System.out.println("BlockTest的主函数执行了！");
			Coder c1 = new Coder();
			Coder c2 = new Coder();
		}
	}

	class Coder{
		static{
			System.out.println("Coder静态代码块执行");
		}
		{
			System.out.println("Coder构造代码块执行");
		}
		public Coder(){
			System.out.println("Coder无参空构造执行");
		}

	}
	```
  - 代码结果：
  	```
	BlockTest静态代码块执行了
	BlockTest的主函数执行了！
	Coder静态代码块执行
	Coder构造代码块执行
	Coder无参空构造执行
	Coder构造代码块执行
	Coder无参空构造执行
 	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 继承
- ### 继承概述
  - 多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要继承那个类即可。
  - 子类可以直接访问父类中的<非私有>的属性和行为。
  - 通过 extends 关键字让类与类之间产生继承关系。
    - `class SubDemo extends Demo{}`

- ### 继承的特点：
  - Java只支持单继承，不支持多继承：一个儿子只能有一个亲爹
    - 一个类只能有一个父类，不可以有多个父类。
    - class SubDemo extends Demo{} //ok
    - class SubDemo extends Demo1,Demo2...//error
  - Java支持多层继承(继承体系)：一个儿子可以有一个亲爹，一个亲爷爷
    - class A{}
    - class B extends A{}
    - class C extends B{}
 
- ### 继承中的成员变量
  - 继承中的成员变量
    - 子类只能获取父类的<非私有>成员
    - 子父类中成员变量的名字不一致时：所调用的变量子类没有，父类有时，获取父类的成员变量 <向上追溯>
    - 子父类中成员变量的名字是一致时：所调用的变量子类有，父类也有时，获取子类的成员变量 <就近原则>
  - 就近原则：谁离我近就优先用谁
    - 如果有局部变量：优先使用局部变量；
    - 如果没有局部变量，有子类的成员变量：优先使用子类的成员变量；
    - 如果没有局部变量，也没有子类的成员变量，而有父类的成员变量：优先使用父类的成员变量；
    - 都没有：报错！
  - super(): 
    - 可以获取父类的成员变量和成员方法，用法与this相似
  - 代码示例：
  	```java
	public class ExtendsDemo {
		public static void main(String[] args) {
			Kid k = new Kid();
			k.show();
		}	
	}

	class Dad{
		String name = "父类";
	}

	class Kid extends Dad{
		String name = "子类";
		public void show() {
			String name = "局部变量";
			System.out.println(name);
			System.out.println(this.name);
			System.out.println(super.name);
		}
	}
	/*
	输出为：
	局部变量
	子类
	父类
	*/
  	```

- ### 继承中的成员方法
  - 继承中成员方法的特点
    - 调用子类中没有的方法：调用父类的方法
    - 调用子类中也有的方法：调用子类的
    - 注：也类似于就近原则，但稍有区别。 
  - 方法的重写：
    - 当子类出现和父类一模一样的函数时，当子类对象调用该函数，会运行子类函数的内容。如同父类的函数被覆盖一样。
    - 其他名称：重写、覆盖、复写。
  
- ### 方法的重写
  - 重写override与重载overlord
    - 重写：
      - 子父类中
      - 子类的方法和父类的完全一样
      - 子类重写了父类的方法(覆盖)
      - 当子类重写了父类的方法之后，使用子类对象调用的就是子类的方法
    - 重载：
      - 在一个类中
      - 有多个重名的方法
      - 其参数不同(参数个数、参数类型、参数顺序), 方法名相同
      - 与返回值无关
  - 方法重写的应用场景：
    - 当子类需要父类的功能，而父类方法不能完全满足子类使用时，可以复写父类中的方法
    - 这样，即沿袭了父类的功能，又定义了子类特有的内容
    - 并且可以在子类的方法中使用super() 调用父类的方法
      - 当子类重写的方法仍然想用到父类的方法时，可以用super()调用，而不是复制代码
      - 复制代码会在后期的修改维护时造成同步性问题，不建议复制代码。 
  - 方法重写的注意事项：
    - 覆盖时，子类方法权限一定要 <大于等于> 父类方法权限
      - 权限修饰符：public > 默认 > protected > private 
    - 父类中的私有方法可不可以被覆盖 (私有的方法外面根本看不到)
    - 使用注解`@override`: 帮助保证重写的正确性 
      - `@override`的位置：在想要重写的方法前，比如子类的某个想要重写父类的方法前
      - 写了override注解但参数列表不同时：
        - 会报错，重写失败：参数列表不同不算重写
        - 代码示例：`(父)public void call(){}`与`(子)public void call(Sting name){}`的不同
      - 写了override注解但访问不到想要重写的父类方法时：
        - 会报错，重写失败：访问不到父类的目标方法，不算重写
        - 代码示例：`(父)private void call(){}`与`(子)public void call(){}`的不同
      - 没写override注解但访问不到想要重写的父类方法时：
        - 不报错，重写失败，相当于子类定义了与父类无关的新方法，但你自己不知道重写失败了
        - 代码示例：`(父)private void call(){}`与`(子)public void call(){}`的不同
  - 代码示例：
  	```Java
	public class ExtendsDemo2 {
		public static void main(String[] args) {
			NewPhone np = new NewPhone();
			np.call();
		}
	}

	class Phone{
		public void call() {
			System.out.println("打电话");
		}
	}
	class NewPhone extends Phone{
		@Override
		public void call() {
			System.out.println("录音");
			super.call();
		}

	}  
 	```
  
- ### 继承中的构造方法
  - 在有子父类继承关系的类中，创建子类的对象，调用子类的构造方法
    - `super();`: 写在子类构造方法的第一行，可用于调用父类的构造方法 
  - 继承中构造方法的执行顺序
    - 对子类对象进行初始化时，父类的构造函数也会运行：因为子类的构造函数默认第一行有一条隐式的语句`super();`  
    - 如果子类构造方法的第一行代码没有调用父类的构造方法：会默认调用父类的<无参构造>
    - 如果子类构造方法的第一行代码调用了父类或本身的构造方法：则不会执行默认的`super();`
      - this(); this(参数); super(参数); 都会覆盖默认的super();
    - 注：肯定会执行父类的构造，因为要先给父类的成员进行初始化，子类可能会用到
  - 代码示例：
    - `new Kid()`:调用子类无参
    - 子类无参第一行`this(2);`: 调用子类带参
    - 子类带参：第一行没有调用子父类构造方法，默认调用父类无参`super()`
      - 父类无参执行;
      - 子类带参执行；
    - 回到子类无参：子类无参执行。
	```java
	public class ExtendsDemo {
		public static void main(String[] args) {
			Kid k = new Kid();
		}	
	}

	class Dad{
		String name = "父类";
		public Dad() {
			System.out.println("我的父类无参构造");
		}
		public Dad(int n) {
			System.out.println("我是父类带参构造");
		}
	}

	class Kid extends Dad{
		String name = "子类";
		public Kid() {
			this(2);
			System.out.println("我是子类无参构造");
		}
		public Kid(int n) {
			//super();
			System.out.println("我是子类带参构造");
		}
	}
	/*
	我的父类无参构造
	我是子类带参构造
	我是子类无参构造
	*/
	```

- ### super关键字
  - super关键字
    - super代表当前子类对象父类的引用
    - 当子父类出现同名成员时，可以用super进行区分
    - 子类要调用父类构造函数时，可以使用super语句 
  - super和this的区别
    - this：当前对象的引用(谁调用就代表谁)
      - 调用子类的成员变量和成员方法: 例如`this.age=50;`，`this.show();`等
      - 在子类构造方法的第一行调用子类的其他构造方法: `this(2);`
    - super：当前对象的父类的引用。
      - 调用父类的成员变量和成员方法: 例如`super.num=10`，`super.method();`等
      - 在子类构造方法的第一行调用父类的构造方法: `super();`
  - 注意点：`syso(this.num);`
    - 当局部变量和子类都没有num变量时，输出的是父类里(如果有)的num变量的值 
 
- ### 继承的优缺点：
  - 优点
    - 提高了代码的复用性
    - 提高了代码的可维护性
  - 缺点：
    - 类的耦合性增强了
  - 开发的原则：高内聚低耦合
    - 内聚：就是自己完成某件事情的能力
    - 耦合：类与类的关系
 
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 抽象类
- ### abstract关键字
  - 抽象：是从多个事物中将共性的，本质的内容抽取出来。
    - 例：狼和狗共性都是犬科，犬科就是抽象出来的概念。 
  - abstract：用于修饰抽象类和抽象方法

- ### 抽象类概述
  - 抽象方法：
    - 不同类的方法是相似的，但是具体内容又不太一样时，只能抽取他的声明 (例如同样的动物，cat和dog吃东西的内容是不一样的) 
      - 抽取声明：只没有方法体，只有第一行的各种修饰符、返回值、方法名等声明。 
    - 没有方法体的方法，该方法的具体实现由子类完成，该方法称为抽象方法
    - 格式：
      - 抽象方法：方法名前、修饰符后加abstract关键字，方法名后没有方法体{}，而是以分号结尾。
      - 抽象类：类名前加abstract关键字
    - 代码示例：`public abstract void eat();`
  - 抽象类：
    - 包含抽象方法的类就是抽象类 
    - 注：有抽象方法的类必须是抽象类
  - 注意：
    - 当一个类继承了抽象类，要么需要重写抽象类的所有抽象方法，要么需要这个类也是抽象类
    - 抽象类中的非抽象方法：子类可以不重写
  - 代码示例：
	```java 
	abstract class Animal{//抽象类：含有抽象方法和非抽象方法
		public abstract void eat();//抽象方法
		public void run() {}//非抽象方法，子类可以不重写
	}

	class Cat extends Animal{//抽象类的子类重写父类的抽象方法
		@Override
		public void eat() {
			// TODO Auto-generated method stub
			System.out.println("猫吃鱼");
		}	
	}

	abstract class Dog extends Animal{//抽象类的子类也是抽象类，不用重写抽象方法

	}    
	```

- ### 抽象类的特点
  - 抽象方法一定在抽象类中, 抽象方法和抽象类都必须被abstract关键字修饰
  - 抽象类中可以有抽象方法也可以有非抽象方法
  - 抽象类和一般类没有太大的不同，抽象类和类的关系也是继承
  - 抽象类不可以用new创建对象(不能实例化)：因为调用抽象方法没意义
  - 一个类继承了抽象类，要么需要重写抽象类的所有抽象方法，要么需要这个类也是抽象类
  - 抽象类中的抽象方法要被使用：
    - 必须由子类复写其<所有>的抽象方法后，建立子类对象调用；如果子类只覆盖了部分的抽象方法，那么该子类还是一个抽象类。
  - 抽象类中可以不定义抽象方法：
    - 应用场景是：不让该类建立对象时，可以加abstract
 
- ### 抽象类的成员特点
  - 成员变量	
    - 可以有变量
    - 可以有常量
  - 构造方法
    - 可以有构造方法: 对成员变量进行初始化
  - 成员方法	
    - 可以有抽象方法
    - 可以有非抽象方法
  - final关键字：修饰类、成员变量、成员方法
    - 常量：可以用final定义变量的方法进行定义 `final int n = 10;` 
  - 代码示例：
  	```java 
	abstract class Animal{//抽象类：含有抽象方法和非抽象方法
		String name = "动物";//成员变量
		final int num = 123;//常量
		public Animal() {
			System.out.println("我是父类构造方法");
		}
		public abstract void eat();//抽象方法
		public void run() {}//非抽象方法
	}  
	
	class Cat extends Animal{//抽象类的子类重写父类的抽象方法
		//略
	}
	```

- ### 抽象类的细节问答
  - 抽象关键字abstract不可以和哪些关键字共存？
    - final; private 
  - 抽象类中是否有构造函数？
    - 可 
  - 抽象类中可不可以没有抽象方法？
    - 可以，当不想让某个类实例化的时候，可以用abstract修饰
    - 其他方法：用private修饰后的类或方法也不会被调用。 

- ### 抽象类在Java API中的应用
  - 以Writer类为例
  - `public abstract class Writer extends Object ..`
    - 已知子类：BufferedWriter,FileWriter, PrintWriter, ....
    - 若干抽象方法
  - 定义抽象类和抽象方法的意义：
    - 规范化，规定了一系列方法的参数列表和返回值等。    

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 接口
- ### 接口的概述
  - 引入的必要性：
    - Java语言的继承是单一继承，一个子类只能有一个父类
    - 为了处理继承单一的局限性，Java语言为我们提供了一种机制，即接口。 
  - 接口interface：
    - 一种比抽象类还抽象的类，接口里所有的方法全是抽象方法
    - 接口只包含常量和方法的定义,而没有变量和方法的方法体
  - 接口和类的关系是实现 `implements` 
    - 帮助抽象类中的抽象方法实现为具体的方法 
    - 一个类实现一个接口，必须实现该接口的所有方法 
  - 接口的格式：`interface 接口名{}` -- 类似于类的定义

- ### 接口的成员特点
  - 接口只包含常量和抽象方法,而没有变量和方法的方法体
    - 只有常量没有变量：接口体中并没有一行操作代码，因此变量的值是需要一开始就初始化好的、且全程不改变的量，就是常量了。
  - 修饰符：
    - 接口中的成员的修饰符都是固定的 
    - 接口中的所有成员都是public的：便于被其他方法实现。
  - 成员方法：public abstract
    - 默认 且 只能 是这两个修饰符 
    - 默认修饰符，可以省略不写，但是建议写上更明确。
  - 成员常量：public static final
    - 默认 且 只能 是这三个修饰符，可省略
    - 是全局变量
    - final：常量
    - static：可以用类名调用 `Animal.num;`
  - 注意：
    - 接口不能创建对象 <不能实例化> 

- ### 接口与类的各种关系
  - 类与类
    - 继承关系
    - 单一继承，多层继承 
  - 类与接口
    - 实现关系
    - 多实现
    - 代码示例：`class Demo implements InterA, InterB{...}` 
  - 接口与接口
    - 继承关系
    - 多继承（不存在重复方法的不确定性）
    - 不是实现关系，因为实现需要把抽象方法具象化，而接口都是抽象方法，不能具象。 
  - “单继承与多实现”
    - 单继承：
      - 多个父类，可能父类中有方法名相同、方法内容不同的非抽象方法，此时JVM无法判断是哪个父类的方法，就存在了不确定性和安全隐患。
    - 多实现：
      - 接口中的方法都是抽象的，即使有方法名相同的情况，因为没有方法体，也并不冲突，甚至可以一次性实现同名的多个抽象方法。
  - 接口和多实现的好处：
    - 一个类继承另一个类的同时可以实现多个接口，扩展了功能
    - 接口的出现：打破了单继承的局限性
  - 代码示例：
  	```java
	interface InterA {
		public abstract void method();	//相同方法
	}

	interface InterB extends InterA {
		public abstract void method(); //相同方法
	}

	interface InterC extends InterA, InterB {//接口与接口的多继承

	}

	/*
	interface InterD implements InterA {//报错：Syntax error on token "implements", extends expected	
	}
	*/

	class Demo implements InterA, InterB{//实现两个接口中的相同方法，只需要一次重写即可
		@Override
		public void method() {
			// TODO Auto-generated method stub

		}
	}  
  	```

- ### 接口的思想
  - 以集合类：Collection类为例，说明接口的思想在Java API中的广泛应用

- ### 接口的优点
  - 接口中的成员都是public的：
    - 对外提供规则/规范。
    - 类比USB接口
  - 类与接口的关系是实现：多实现
    - 打破了单一继承的局限性。
  - 接口的出现降低耦合性：
    - 实现了模块化开发,定义好规则,每个人实现自己的模块,大大提高了开发效率。
    - (不需要因为每个人的开发进度不同而相互等待)

- ### 接口与抽象类的区别
  - 共性：
    - 都是不断抽取出来的抽象的概念
  - 区别1：与类的关系
    - 类与接口：实现关系，多实现，一个类可以实现多个接口
    - 类与抽象类：继承关系，单一继承，多层继承。
  - 区别2：成员变量
    - 抽象类：可以有成员变量，也可以有常量
    - 接口：只能有常量，以带有'public static final'修饰的变量的形式定义
  - 区别3：成员方法
    - 抽象类：可以有抽象方法，也可以有非抽象方法
    - 接口：只能有抽象方法，且方法有默认修饰符'public abstract'
  - 区别4：构造方法
    - 抽象类：有构造方法
    - 接口：没有构造方法 (只有常量没有变量，也不需要初始化什么)

- ### 运动员案例
  - 图示：
  ![运动员案例分析](https://github.com/anliux/JAVALearning/blob/master/images/01-java-base/class/%E8%BF%90%E5%8A%A8%E5%91%98%E6%A1%88%E4%BE%8B%E5%88%86%E6%9E%90.png)
  - 代码示例：
  	```java
	/* 	
	 * 	篮球运动员和教练
		乒乓球运动员和教练
		现在篮球运动员和教练要出国访问,需要学习英语
		请根据你所学的知识,分析出来哪些是类,哪些是抽象类,哪些是接口
	 */

	public class AbstractTest {
		public static void main(String[] args) {
			//篮球运动员
			BasketBallPlayer bbp = new BasketBallPlayer();
			bbp.name = "姚明";
			bbp.age = 20;
			bbp.gender = "男";
			bbp.eat(); //吃饭
			bbp.study(); //学扣篮
			bbp.speak(); //姚明说英语		

			//乒乓球教练
			PingpangCoach ppc = new PingpangCoach(); 
			//变量初始化略
			ppc.teach(); //教抽球
			//ppc.speak();//未定义此方法
		}	
	}

	//人
	class Person{
		String name;//姓名
		int age;//年龄
		String gender;//性别

		public Person() {//无参构造
		}

		public Person(String name, int age, String gender) {//带参构造
			this.name = name;
			this.age = age;
			this.gender = gender;
		}

		public void eat() {
			System.out.println("吃饭");
		}
		public void sleep() {
			System.out.println("睡觉");
		}	
	}

	//运动员
	abstract class Player extends Person{
		public abstract void study();
	}

	//教练
	abstract class Coach extends Person{
		public abstract void teach();
	}

	//学英语
	interface speakEnglish{
		public abstract void speak();
	} 

	//篮球运动员
	 class BasketBallPlayer extends Player implements speakEnglish {
		@Override
		public void study() {
			System.out.println("学扣篮");
		}

		@Override
		public void speak() {
			System.out.println(name+"说英语");
		}	
	}

	//篮球教练
	class BasketBallCoach extends Coach implements speakEnglish {
		@Override
		public void teach() {
			System.out.println("教扣篮");
		}

		@Override
		public void speak() {
			System.out.println(name+"说英语");
		}	
	}

	//乒乓球运动员
	class PingpangPlayer extends Player{
		@Override
		public void study() {
			System.out.println("学抽球");
		}	
	}

	//乒乓球教练
	class PingpangCoach extends Coach{
		@Override
		public void teach() {
			// TODO Auto-generated method stub
			System.out.println("教抽球");
		}	
	}  
  	```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 匿名对象
- ### 概述
  - 匿名对象：没有名字的对象，是对象的简化形式
  - 匿名对象是没有变量引用的
  - 代码示例：
	  ```Java
	  Student s = new Student();
	  s.study();
	  ```
	  vs.
	  `new Student().study();`
  
- ### 匿名对象的应用场景
  - 当对对象的方法仅进行一次调用时
    - 代码示例：若干次的`s.study();`时，匿名`new Student().study();`则重复创建多次对象
  - 匿名对象可以作为实际参数进行传递，但无法在传参前做其他事情
    - 代码示例：`method(new Student());`  
    - 此时不能对对象的变量进行修改，仅能通过构造在new时传入参数赋值
    ```java
    Student s = new Student();
    s.name = "张三";
    s.age = 18;
    method(s); //此时直接匿名创建对象，不能修改变量值
    ```

- ### 匿名对象的问题
  - 调用属性：
    - 匿名对象可以调用成员变量并赋值，但是赋值并没有意义。 
  - 代码示例：
	  ```Java
	  new Student().age = 18;
	  syso(new Student().age);//无关新对象，仍然是Student()对象的age默认值
	  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->





## final

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 多态















<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 包














<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 修饰符













<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 内部类











<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
