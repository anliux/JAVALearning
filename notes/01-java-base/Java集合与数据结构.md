# Java集合与数据结构


### 目录

<!--GFM-TOC -->
* [ArrayList](#arraylist): 集合类, ArrayList, 构造方法, 添加方法, 增删改查方法, 集合遍历
* [集合类](#集合类): 集合类的体系结构, Collection常用功能, 迭代器与并发修改异常, 泛型, foreach循环
* [常见数据结构](#常见数据结构): 数组, 链表, 栈和队列的简单图解
* [List](#list):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
* [](#):
<!--GFM-TOC -->



## ArrayList
- ### 备注
  - 此部分在“Java常用API”系列中首次出现，这里直接复制并简化了相关内容。
  - 详见：[Java常用API: 集合类与ArrayList](https://github.com/anliux/JAVALearning/blob/master/notes/01-java-base/Java%E5%B8%B8%E7%94%A8API.md#%E9%9B%86%E5%90%88%E7%B1%BB%E4%B8%8Earraylist)

- ### 集合类概述
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
    - java.util包下
    - 接口，不能实例化 -- 用子类创建(多态)
    - 示例：`Collection c = new ArrayList();//多态,父类引用指向子类对象`

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
  - 迭代器：`Iterator<E> iterator()`
    - 下一小节详述 

- ### 迭代器与并发修改异常
  - 集合的遍历方式：
    - 法1：toArray() 把集合转为数组，然后以数组的方式遍历
      - 局限性：不是所有集合都与索引相关
    - 法2：`Iterator<E> iterator()`: 
      - 返回一个迭代器对象，通过迭代器对象来迭代集合
      - 后面还有一个foreach循环方法 
  - 迭代器：
    - `Iterator<E> iterator()`: 
      - 注意区别前后两个迭代器 
        - iterator(): 是Collection类的一个方法
        - Iterator接口：是一个接口
      - Collection对象的这个iterator()方法的作用就是返回一个迭代器对象，因此可以通过此方法获取迭代器对象。
    - Iterator接口：
      - 用于遍历集合
      - 有三种方法：hasNext(), next(), remove()
    - 获取迭代器方法：
      - 由Collection对象的iterator()方法获取
      - 代码示例：`Iterator it = c.iterator();` 
    - `E next()`方法：
      - 返回下一个元素
      - 没有下一个元素时报错：
        - 抛出异常：Exception in thread "main" java.util.NoSuchElementException
      - 代码示例：`syso(it.next());//返回获取到的元素，或者报错`
    - `boolean hasNext()`: 
      - 判断是否有下一个元素可以获取，有则返回true，否则false
    - 代码示例：
    ```java
      import java.util.ArrayList;
      import java.util.Collection;
      import java.util.Iterator;

      public class IteratorDemo {
        public static void main(String[] args) {
          Collection c = new ArrayList();
          c.add("hello");
          c.add("world");
          c.add("java");

          Iterator it = c.iterator();
          while(it.hasNext()) {
            System.out.println(it.next());
          }
          System.out.println(it.next());//java.util.NoSuchElementException
        }
      }  
    ```
  - 并发修改异常
    - 并发修改异常：
      - ConcurrentModificationException 
    - 异常分析：
      - 迭代器是依赖于集合的，相当于集合的一个副本；
      - 当迭代器操作时，如果发现和集合不一样，会抛出异常。 
      - 迭代中途给集合添加元素触发了“不一样”
    - 异常代码示例：
    ```java
      import java.util.ArrayList;
      import java.util.Collection;
      import java.util.Iterator;

      public class IteratorDemo {
        public static void main(String[] args) {
          Collection c = new ArrayList();
          c.add("hello");
          c.add("world");
          c.add("java");

          Iterator it = c.iterator();
          while(it.hasNext()) {
            String s = (String)it.next();
            if(s.equals("java"))
              c.add("android");//java.util.ConcurrentModificationException
          }
        }
      }
   
    ```
    - 使用ListIterator解决
      - 让迭代器去添加或修改，会同步到集合中，这样就不会触发并发修改异常
      - 在Iterator接口中没有发现add相关方法，找Iterator的子接口ListIterator中找到add()方法
      - ListIterator创建：`ListIterator<E>	listIterator()`
        - 返回此列表元素的列表迭代器（按适当顺序）。
      - 综上：
        - 创建集合部分，用List代替Collection；
        - 创建迭代器部分，用list.listIterator()方法；
        - 添加元素部分：用ListIterator迭代器的add()方法
    - 改进后的代码示例：
    ```java
        import java.util.ArrayList;
        import java.util.List;
        import java.util.ListIterator;

        public class IteratorDemo {
          public static void main(String[] args) {
            //Collection c = new ArrayList();
            List c = new ArrayList();//也可以ArrayList代替List
            c.add("hello");
            c.add("world");
            c.add("java");

            //Iterator it = c.iterator();
            ListIterator lit = c.listIterator();
            while(lit.hasNext()) {
              String s = (String)lit.next();
              if(s.equals("java"))
                //c.add("android");//java.util.ConcurrentModificationException
                lit.add("android");//不要用集合添加，而是使用迭代器添加，迭代器会同步到集合
            }

            System.out.println(c);//[hello, world, java, android]
          }
        }      
    ```

- ### 泛型
  - 泛型概述：
    - 引入：
      - 集合可以存储任意类型的数据
      - 当存储了不同类型的数据，就有可能在转换的时候发生类型转换异常 ClassCastException
      - java为了解决这个问题，就引入了一种机制，即泛型。 
    - 概述：
      - 一种广泛的类型
      - 把明确数据类型的工作提前到了编译时期
      - 借鉴了数组的特点
    - 好处：
      - 避免了数据类型转换异常的发生；
      - 减少了编辑器里的黄色警告标识；
      - 简化了代码的书写
  - 泛型使用：
    - 查阅API/Ctrl查看源码，当看到类或接口有`<E>`，就可以使用泛型。 
    - 可以标明泛型而没有写，编辑器会给黄色警告线
    - 注意：`<E>`中的E在实际代码中需要替换为具体的对象类型
    - 示例：
      - `Collection<Student> c = new ArrayList<Student>();//声明集合c总存储的对象类型为Student`
      - `Iterator<Student> it = c.iterator();`
  - 代码示例：

- ### foreach循环
  - foreach:
    - 增强for循环，一般用于遍历集合或数组
  - 格式：
    - 每次循环，将 (冒号后的)集合或数组对象中的一个元素 放入 (冒号前的)定义为元素类型的变量中，并在循环中使用取出的变量 
  ```java
  for(元素的类型  变量 : 集合或者数组对象){
    可以直接使用变量;
  }
  ```
  - 注意：
    - 增强for循环提供了一种新的遍历集合的方法。
    - 增强for循环中不能修改集合，否则会出现并发修改异常。
    - 增强for循环底层是迭代器循环(上一条的原因)
      - Collection 的父接口 Iterator：
      - 其中有一条说明：`public interface Iterable<T>`
        - 实现这个接口允许对象成为 "foreach" 语句的目标。 
  - 代码示例：
  ```java
    import java.util.ArrayList;
    import java.util.Collection;
    import java.util.List;
    import java.util.ListIterator;

    public class IteratorDemo {
      public static void main(String[] args) {
        Collection<String> c = new ArrayList<String>();
        c.add("hello");
        c.add("world");
        c.add("java");

        for (String string : c) {
          System.out.println(string);
        }
      }
    }

  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 常见数据结构
- ### 数组
  - 特点：查找快，增删慢 
  - ![常见数据结构（数组）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E6%95%B0%E7%BB%84%EF%BC%89.bmp) 

- ### 链表
  - ![常见数据结构（链表）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E9%93%BE%E8%A1%A8%EF%BC%89.bmp) 

- ### 栈和队列
  - ![常见数据结构（栈和队列）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E6%A0%88%26%E9%98%9F%E5%88%97%EF%BC%89.bmp) 


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
