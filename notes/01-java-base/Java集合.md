# Java集合

### 目录


<!--GFM-TOC -->
* [对象数组的练习](#对象数组的练习)
* [为什么出现集合类](#为什么出现集合类)
* [ArrayList](#arraylist)
* [ArrayList案例分析](#arraylist案例分析)
* []()
* []()
* []()
* []()
* []()
* []()
* []()
<!--GFM-TOC -->



## 对象数组的练习
- ### 题目
  - 创建一个学生数组，存储三个学生对象并遍历

- ### 步骤分析
  - 定义学生类
  - 创建学生数组
  - 创建学生对象
  - 把学生对象作为元素赋值给学生数组
  - 遍历学生数组

- ### 定义学生类的代码
  - 自动生成构成函数和getset方法
	A：自动生成构成方法：
		代码区域右键 -- Source -- Generate Constructors from Superclass.. ： 无参构造函数
		代码区域右键 -- Source -- Generate Constructors using Fields...: 带参构造函数
	B：自动生成get、set方法：
		代码区域右键 -- Source -- Generate Getters and Setters.. -- select all
  - 代码：
```
package com.itcast;

public class Student {
	private String name;
	private int age;
	public Student() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Student(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	
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


- ### 学生类演示代码
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
		}
	}
}


```


- ### 对象数组的内存图
  - 图示：
    ![对象数组的内存图]()



## 为什么出现集合类
- ### 概述
  - 我们学习的是面向对象语言，而面向对象语言对事物的描述是通过对象体现的；
  - 为了方便对多个对象进行操作，我们就必须把这多个对象进行存储。
  - 而要想存储多个对象，就不能是一个基本的变量，而应该是一个容器类型的变量。
  - 在我们目前所学过的知识里面，有哪些是容器类型的呢?数组和StringBuilder。
    - StringBuilder的结果是一个字符串，不一定满足我们的要求，
    - 所以我们只能选择数组，这就是对象数组。
  - 而对象数组又不能适应变化的需求，因为数组的长度是固定的，
  - 这个时候，为了适应变化的需求，Java就提供了集合类供我们使用。

- ### 集合类的特点：
  - 长度可变。



## ArrayList
- ### ArrayList概述
  - 最常用的集合

- ### 通过阅读API学习
  - java.util包下：因此需要导包
  - ArrayList<E>：大小可变数组的实现。
  - <E>：一种特殊的数据类型，泛型。
    - 在出现E的地方，使用引用数据类型替换即可。
    - 举例：ArrayList<String>, ArrayList<Student>

- ### 构造方法
  - 无参：ArrayList()

- ### 添加元素
  - public boolean add(E e)
    - 添加元素，E根据定义的类型确定，用的多
  - public void add(int index, E element)
    - 在指定索引处添加元素，用的不多


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
    - public E get(int index) -- 返回指定索引处的元素
    - get方法不改变原有集合
  - 集合长度：
    - public int size() -- 返回集合中的元素的个数
  - 删除元素：
    - public boolean remove(Object o) -- 删除指定的元素，并返回删除是否成功（布尔型）
    - public E remove(int index) -- 删除指定索引处的元素，并返回被删除的元素
  - 修改元素：
    - public E set(int index, E element) -- 修改指定索引处的元素，返回被修改的元素（原来的元素）


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



## 学生管理系统








### END