# Java集合与数据结构


### 目录

<!--GFM-TOC -->
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
* [](#)
<!--GFM-TOC -->



## 集合类与ArrayList
- ### 备注
  - 此部分在“Java常用API”系列中首次出现，这里直接复制并简化了相关内容。
  - 详见：[Java常用API: 集合类与ArrayList](https://github.com/anliux/JAVALearning/blob/master/notes/01-java-base/Java%E5%B8%B8%E7%94%A8API.md#%E9%9B%86%E5%90%88%E7%B1%BB%E4%B8%8Earraylist)

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





## 


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




## 


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->








### END
