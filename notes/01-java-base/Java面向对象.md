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

	```
	/*java
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



## 待续






##



##



### END


