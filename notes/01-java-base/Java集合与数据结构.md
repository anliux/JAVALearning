# Java集合与数据结构


### 目录

<!--GFM-TOC -->
* [ArrayList](#arraylist): 
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



## ArrayList
- ### 备注
  - 此部分在“Java常用API”系列中首次出现，这里直接复制并简化了相关内容。
  - 详见：[Java常用API: 集合类与ArrayList](https://github.com/anliux/JAVALearning/blob/master/notes/01-java-base/Java%E5%B8%B8%E7%94%A8API.md#%E9%9B%86%E5%90%88%E7%B1%BB%E4%B8%8Earraylist)

- ### 集合类
  - 引入
    - 面向对象语言对事物的描述是通过对象体现的; 为了方便对多个对象进行操作，必须把这多个对象进行存储。
    - 而要想存储多个对象，就不能是一个基本的变量，而应该是一个容器类型的变量。
    - 已经学过的，有哪些是容器类型的呢? 数组和StringBuilder
      - StringBuilder的结果是一个字符串，不一定满足我们的要求，
      - 所以我们只能选择数组，这就是对象数组。
    - 对象数组的弊端：不能适应变化的需求，因为数组的长度是固定的
    - 因此：为了适应变化的需求，Java就提供了 <集合类> 供我们使用。
  - 集合类的特点：
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

- ### 集合遍历
  - 用for循环 + size()方法 + get()方法
  - 注：常规的做法是，输出时，先将get获取到的元素存储在变量中，然后输出变量。

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 集合类
- ### 集合类的体系结构
  - 体系结构:
    - 怎么学习？
      - 从最顶层开始学习，因为最顶层包含了所有的共性。 
    - 怎么使用？
      - 使用最底层，因为最底层就是具体的实现。
  - 集合的体系结构：
    - 由于不同的数据结构(数据的组织、存储方式)，所以Java为我们提供了不同的集合。
    - 不同的集合功能相似，不断向上提取，将共性抽取出来，就是集合体系结构的原因。 
  - ArrayList --> List --> Collection 
    - Collection: 最顶层 

- ### Collection常用功能
  - Collection: 
    - 接口，不能实例化 -- 用子类创建(多态)
    - 示例：`Collection c = new ArrayList();//多态,父类引用指向子类对象`
    - java.util包下
  - boolean add(E e)：添加元素e，返回是否添加成功
    - ArrayList: 允许重复，返回值恒为true
    - 示例：`c.add("hello");`
      - 可以直接输出；可赋值给Boolean类型的变量 
  - void clear(): 清空集合
    - 会清空集合中所有元素，慎用
    - 示例：`c.clear();`
  - boolean contains(Object o): 判断集合中是否包含指定元素
    - 示例：`syso(c.contains("hello"));//true`
  - boolean isEmpty()：判断集合是否为空
    - 示例：`syso(c.isEmpty());//false`
    - 注：`c.clear();` 后会判空为true
  - boolean remove(Object o): 删除元素，返回删除成功与否
    - 示例：`syso(c.remove("Java"));//删除没有的元素，返回false`
  - int size(): 返回集合中的元素个数
    - 求集合对象的个数或长度： 注意与 数组length属性 和  String的length()方法区分。
    - 示例：`syso(c.size());`  
  - Object toArray(): 将集合转换为Object类型的数组
    - Object类型：任意类型的父类型，确保涵盖所有类型的元素。
    - 使用场景：用数组思路遍历集合时可以先转为数组类型
    - 示例：`Object[] objs = c.toArray();//转为Object类型的数组后遍历` 
  - Interator<E> interator(): 迭代器
    - 下一小节详述
  
- ### 迭代器与并发修改异常
  - 集合的遍历方式：
    - 法1：toArray() 把集合转为数组，然后以数组的方式遍历
      - 局限性：不是所有集合都与索引相关
    - 法2：interator(): 返回一个迭代器对象，通过迭代器对象来迭代集合 
  - 迭代器：
  


  
  
  
  
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 泛型

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->





## 常见数据结构

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




## List





<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Map


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




## Set


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
