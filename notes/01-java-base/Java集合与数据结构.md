# Java集合与数据结构


### 目录

<!--GFM-TOC -->
* [ArrayList](#arraylist): 集合类, ArrayList, 构造方法, 添加方法, 增删改查方法, 集合遍历
* [集合类](#集合类): 集合类的体系结构, Collection常用功能, 迭代器与并发修改异常, 泛型, foreach循环
* [常见数据结构](#常见数据结构): 数组, 链表, 栈和队列的简单图解
* [List](#list): List概述, List的特有功能, List的子类(ArrayList和LinkedList), 源码阅读tips
* [Set](#set): Set接口的特点, HashSet的add()方法以及hashCode()和equals()方法的重写
* [Collections工具类](#collections工具类): Collection和Collections的区别(面试题), Collections的常用方法, 模拟斗地主发牌小题
* [Map](#map): Map接口概述, Map的功能, Map的两种遍历方法, HashMap存储对象并遍历(自定义对象为key时重写两个方法)
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
  - 查找快，增删慢 
  - ![常见数据结构（数组）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E6%95%B0%E7%BB%84%EF%BC%89.bmp) 

- ### 链表
  - 查询快，增删慢 
  - ![常见数据结构（链表）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E9%93%BE%E8%A1%A8%EF%BC%89.bmp) 

- ### 栈和队列
  - 栈：先进后出
  - 队列：先进先出 
  - ![常见数据结构（栈和队列）](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/collections/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%EF%BC%88%E6%A0%88%26%E9%98%9F%E5%88%97%EF%BC%89.bmp) 


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




## List
- ### List概述
  - List接口：
    - 有序的 collection（也称为序列）。
    - 此接口的用户可以对列表中每个元素的插入位置进行精确地控制。
    - 用户可以根据元素的整数索引（在列表中的位置）访问元素，并搜索列表中的元素。
  - List特点：
    - 有序的(存储和读取的顺序是一样的); 
    - 有整数索引；
    - 允许重复。 

- ### List的特有功能
  - 针对Collection父类的特有功能，集中体现为索引值相关的增删改查
  - 创建可用的List对象：
    - 示例：`List list = new ArrayList();` 
  - 注意：
    - 涉及到索引值，需要注意越界异常
      - `java.lang.IndexOutOfBoundsException`
  - `void add(int index, E element)`: 
    - 在指定索引位置添加指定元素
    - 指定索引位置已有元素时，会将已有元素向 索引值+1 的位置移动一位，将新元素放在指定索引位置。
    - 示例：`list.add(1,"hello");`
  - `E get(int index)`:
    - 根据索引返回元素
    - 需要注意越界异常
    - 示例：`System.out.println(list.get(1));`
  - `E remove(int index)`:
    - 删除指定元素并返回
    - 注意越界异常
    - 示例：`System.out.println(list.remove(1));//删除索引1处的元素，并将这个被删除的元素返回`
  - `E set(int index, E element)`:
    - 将指定索引位置的元素替换为新的指定元素，并将原来的元素返回
    - 示例：`System.out.println(list.set(0,"android"));//返回值为原索引0处的元素` 
  - 代码示例：
  ```java
      import java.util.ArrayList;
      import java.util.List;

      public class ListDemo {
        public static void main(String[] args) {
          List list = new ArrayList();

          list.add(0, "hello");
          list.add(0, "java");//将原索引0位置的元素向后移动一位，将新元素放在索引0的位置
          list.add(1, "world");//同上
          System.out.println(list);//[java, world, hello]

          System.out.println(list.get(1));//world
          //System.out.println(list.get(3));//java.lang.IndexOutOfBoundsException

          System.out.println(list.remove(0));//java
          System.out.println(list);//[world, hello]

          System.out.println(list.set(1, "android"));//hello
          System.out.println(list);//[world, android]
        }
      }  
  ```

- ### List的子类
  - ArrayList:
    - 底层是数组结构，查询快，增删慢；
  - LinkedList
    - 底层是链表结构，查询慢，增删快。
  - 如何选择使用不同的集合？
    - 如果查询多，增删少：使用ArrayList
    - 如果查询少，增删多：使用LinkedList
    - 如果不知道使用什么：则使用ArrayList 

- ### LinkedList的特有功能
  - void addFirst(E e): 
    - 将元素添加到索引为0的位置
    - 示例：`list.addFirst("java");` 
  - void addLast(E e): 
    - 将元素添加到索引为size()-1的位置
    - 示例：`list.addLast("android");`  
  - E getFirst():
    - 获取索引为0的元素
    - 示例：`System.out.println(list.getFirst());//java` 
  - E getLast(): 
    - 获取索引为size()-1的元素 
    - 示例：`System.out.println(list.getLast());//android`
  - E removeFirst():
    - 删除索引为0的元素并返回该元素
    - 示例：`System.out.println(list.removeFirst());//java` 
  - E removeLast():
    - 删除索引为size()-1的元素并返回该元素
    - 示例：`System.out.println(list.removeLast());//android` 
  - LinkedList这些功能的作用：
    - 可以模拟栈和队列的特性 
  - 代码示例：
  ```java
      import java.util.LinkedList;

      public class LinkedListDemo {
        public static void main(String[] args) {
          LinkedList list = new LinkedList();

          list.add("hello");
          list.add("world");
          System.out.println(list);//[hello, world]

          list.addFirst("java");
          list.addLast("android");
          System.out.println(list);//[java, hello, world, android]

          System.out.println(list.getFirst());//java
          System.out.println(list.getLast());//android

          System.out.println(list.removeFirst());//java
          System.out.println(list.removeLast());//android
          System.out.println(list);//[hello, world]

        }
      }  
  ```

- ### 番外：由小题目引入源码查阅
  - 题目：
    - 1. 定义一个方法，返回指定列表中指定元素的位置
    - 2. 在1的基础上，定义方法，判断元素是否存在
  - 步骤：
    - 1. 定义index()方法，for循环遍历集合，get获取每个元素，然后equals比较是否与目标相同，并返回相应的Boolean值。
    - 2. 定义contains()方法，调用1的index()获取索引值，然后判断`index >= 0`是否为真，为真则存在，否则不存在     
  - 查阅源码：contains()方法
    - 会发现源码的判断方法，同样是调用索引值的方法，然后判断索引值是否大于等于0 
  - 感悟：
    - java源码也并没有多么高深，是一步一步建立起来的
    - Java源码是代码规范和学习的良好教材，多读多想。

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Set
- ### Set接口的特点
  - 无序：
    - 存储和读取的顺序有可能不一样
  - 不允许重复：
    - 要求元素唯一
  - 没有索引

- ### HashSet的add()方法添加元素
  - HashSet的add()方法判断是否重复的原理：
    - 第一步：使用当前集合中的每一个元素和新添加元素的hash值进行比较
      - 如果hash值不一样，则直接添加新的元素；
      - 如果hash值一样，则比较地址值或使用equals方法进行比较  
    - 第二步：比较地址值或使用equals方法
      - 如果比较结果一样，则认为是重复不添加
    - 所有比较结果都不一样，则添加 
  - 使用HashSet存储自定义对象
    - 以Student为例，每个Student对象的hash值/地址值都不一样，即使姓名+年龄相同，也不会判为重复；
    - 研究add()添加判重复原理之后，可以尝试重写hashCode()和equals()方法 
      - hashCode(): 返回确定值，跳过hash值判断，直接进入equals重写的方法进行姓名/年龄的比较
      - equals()：分别比较成员变量是否相同 
  - hashCode()和equals()方法的优化：
    - 参考eclipse直接生成的这两个方法 
    - hashCode():
      - 以上方法中，有一些对象的成员变量完全不同，仍然进行了equals比较，效率较低；
      - 可以让成员变量不同的对象，他们的hash值也不同，可以减少一部分equals比较，从而提高效率 
      - 示例:`return age + name.hashCode();`
    - equals():
      - 比较是否为同一个对象，提高效率：`if(this == obj) return true;`
      - 比较是否为同一类，因为后面有Object向下转型，提高健壮性：`if(this.getClass() ! = obj.getClass()) return false;` 
  - 代码示例：
    ```java
      @Override
      public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + age;
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        //加入一些额外的计算，在hash值比较阶段筛掉一些对象
        return result;
      }
      
      @Override
      public boolean equals(Object obj) {
        //判断是否为同一对象，提高效率
        if (this == obj)
          return true;
        
        //判断比较对象是否为空，提高效率
        if (obj == null)
          return false;
        
        //判断类型，提高健壮性
        if (getClass() != obj.getClass())
          return false;
        Student other = (Student) obj;//向下转型
        
        //比较成员变量的是否一致
        if (age != other.age)
          return false;
        if (name == null) {
          if (other.name != null)
            return false;
        } else if (!name.equals(other.name))
          return false;
        return true;
      }    
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Collections工具类 
- ### 常见面试题：
  - Collection和Collections有什么区别？
  - Collection:
    - 集合体系的最顶层，包含了集合体系的共性 
  - Collections: 
    - 一个工具类，方法都是用于操作Collection的
    - 工具类不需要创建对象，方法是静态的，直接用类名调用。 

- ### Collections的常见方法
  - `static int binarySearch(List list, T key)`:
    - 使用二分搜索法搜索指定列表，以获得指定对象。
    - 参数只能是List: 数据要求是有序的
      - set是无序的，不行；Collection也不行，可能是set 
    - 注意：
      - 对象需要是List类型
      - 泛型位置不能是int, 而应该是Integer，因为ArrayList存放的是对象元素
    - 代码示例：
    ```java
        import java.util.ArrayList;
        import java.util.Collections;
        import java.util.List;

        public class CollectionsDemo {
          public static void main(String[] args) {
            //二分查找
            List<Integer> list = new ArrayList<Integer>();//Integer，不是int
            list.add(1);//自动装箱
            list.add(2);
            list.add(4);
            list.add(6);
            int index = Collections.binarySearch(list, 4);
            System.out.println(index);//2
          }
        }    
    ```
  - `static void copy(List dest, List src)`: 
    - 将所有元素从一个列表复制到另一个列表，即把原列表中的数据覆盖到目标列表。
    - 目标列表在前，源列表在后，不要搞混!!
    - 注意：目标列表的长度至少等于源列表的长度
      - 新建目标列表的长度为空，可以先添加空串或任意内容到目标列表，使其长度大于源列表。 
    - 代码示例：
    ```java
        public static void main(String[] args) {
          //copy
          List<String> src = new ArrayList<String>();
          src.add("hello");
          src.add("world");
          src.add("java");

          List<String> dest = new ArrayList<String>();
          dest.add("");//为保证目标长度大于源长度，可以添加空串
          dest.add("");
          dest.add("");

          Collections.copy(dest, src);
          System.out.println(dest);//[hello, world, java]
        } 
    ```
  - `static void fill(List list, Object obj) `
    - 使用指定元素替换指定列表中的所有元素。
    - 代码示例：
    ```java
        public static void main(String[] args) {
            List<String> list = new ArrayList<String>();
            list.add("hello");
            list.add("world");
            list.add("java");
            
            System.out.println(list);//[hello, world, java]
            Collections.fill(list, "android");
            System.out.println(list);//[android, android, android]
        }    
    ```
  - `static void reverse(List list)`:
    - 反转指定列表中元素的顺序。
    - 代码示例：`Collections.reverse(list);//反转后的[1，2，3，4]列表变为[4,3,2,1]` 
  - `static void shuffle(List list)`: 
    - 使用默认随机源对指定列表进行置换。
    - "傻否"，随机置换：每次运行后的结果可能都不一样。
    - 代码示例: `Collections.shuffle(list);//随机置换后的结果为任意排列` 
  - `static void sort(List list)`:
    - 根据元素的自然顺序对指定列表按升序进行排序。
    - 注：String类也能排，可能是按首字母对应的int
    - 代码示例：`Collections.sort(list);` 
  - `static void swap(List list, int i, int j)`:
    - 在指定列表的指定位置处交换元素。
    - 代码示例：``Collections.swap(list, 0, 2);
  - 小结：
    - 方法返回值是void:
      - 大概率传入的列表发生了变化 
    - 方法返回值是具体的值，非void:  
      - 大概率传入的列表没有变化，而是从其中取了某个元素等返回了 

- ### 模拟斗地主发牌
  - 步骤：
    - 买牌：创建存放卡牌的box容器，并将54张牌放入box中；
    - 洗牌：调用Collections的洗牌方法shuffle();
    - 发牌：(创建三个玩家集合) 遍历box元素，并将这些牌分给三个玩家。
  - 代码示例：
  ```java
        import java.util.ArrayList;
        import java.util.Collections;

        public class CollectionsTest {
          public static void main(String[] args) {
            //买牌
            String[] arr = {"红桃","方块","黑桃","梅花"};
            String[] arr2 = {"A","2","3","4","5","6","7","8","9","10","J","Q","K"};
            ArrayList<String> box = new ArrayList<String>();
            for(int i = 0; i < arr.length; i++) {
              for(int j = 0; j < arr2.length; j++) {
                box.add(arr[i]+arr2[j]);
              }			
            }
            box.add("大王");
            box.add("小王");

            System.out.println(box);
            System.out.println(box.size());//54

            //洗牌
            Collections.shuffle(box);

            //发牌
            ArrayList<String> player1 = new ArrayList<String>();
            ArrayList<String> player2 = new ArrayList<String>();
            ArrayList<String> player3 = new ArrayList<String>();

            for(int i = 0; i < box.size()-3; i++) {//留三张底牌给地主
              //对取模，余数为0，1，2分别派给三个玩家
              if(i % 3 == 0) {
                player1.add(box.get(i));
              }else if(i % 3 == 1) {
                player2.add(box.get(i));
              }else if(i % 3 == 2) {
                player3.add(box.get(i));
              }
            }

            //看牌
            System.out.println("玩家1"+player1);
            System.out.println("玩家2"+player2);
            System.out.println("玩家3"+player3);
            /*
             * [红桃A, 红桃2, 红桃3, 红桃4, 红桃5, 红桃6, 红桃7, 红桃8, 红桃9, 红桃10, 红桃J, 红桃Q, 红桃K, 方块A, 方块2, 方块3, 方块4, 方块5, 方块6, 方块7, 方块8, 方块9, 方块10, 方块J, 方块Q, 方块K, 黑桃A, 黑桃2, 黑桃3, 黑桃4, 黑桃5, 黑桃6, 黑桃7, 黑桃8, 黑桃9, 黑桃10, 黑桃J, 黑桃Q, 黑桃K, 梅花A, 梅花2, 梅花3, 梅花4, 梅花5, 梅花6, 梅花7, 梅花8, 梅花9, 梅花10, 梅花J, 梅花Q, 梅花K, 大王, 小王]
              54
              玩家1[黑桃Q, 梅花J, 方块4, 梅花9, 梅花7, 黑桃10, 方块7, 红桃6, 红桃9, 梅花3, 方块K, 梅花Q, 黑桃3, 黑桃K, 梅花4, 黑桃7, 方块2]
              玩家2[梅花6, 红桃10, 方块8, 梅花K, 红桃3, 梅花2, 红桃J, 方块A, 红桃8, 方块6, 大王, 黑桃J, 黑桃2, 小王, 红桃7, 黑桃A, 梅花10]
              玩家3[梅花5, 梅花A, 方块5, 方块3, 黑桃5, 黑桃8, 红桃2, 方块J, 黑桃9, 黑桃6, 红桃5, 方块9, 红桃A, 红桃Q, 黑桃4, 方块10, 红桃K] 
             * */
          }  

  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Map
- ### Map接口概述
  - Map:
    - 一种用于存储对应关系的集合 
    - 例如：姓名-学号这样的对应关系
  - `Map<K,V>接口`：
    - Map接口，独立于Collection的另一种集合形式 
    - 将键映射到值的对象。
    - 一个映射不能包含重复的键，每一个键最多只能映射到一个值。
      - 一对一：一个学号对应一个姓名 
  - Map和Collection的区别？
    - Map: 
      - 是一个双列集合，常用于处理有对应关系的集合，key不可以重复
      - 又称为“夫妻对集合”。
    - Collection:
      - 单列集合
      - Collection有不同的子体系，有的允许重复有索引有序，有的不允许重复而且无序
      - 又称为“单身汉集合”

- ### Map的功能
  - Map类型对象：
    - 多态创建：
      - 代码示例：`Map<String,String> map = new HashMap<String,String>();//创建HashMap对象` 
    - 输出Map对象：大括号中存放键值对，且键值对用等号连接。
      - 代码示例：`System.out.println(map);//{IT002=李四, IT001=王五}`
  - 映射功能：
    - `V	put(K key, V value)`：
      - 添加或修改映射关系：
        - 将key值映射到value，如果key存在，则覆盖value，并将原value返回。 
      - 返回值：
        - 添加成功返回null，key重复时覆盖并返回key对应的原value值。
      - 代码示例：
        - 添加成功返回null： `System.out.println(map.put("IT002", "李四"));//null`
        - key值重复返回关联的原value值：`System.out.println(map.put("IT001", "王五"));//张三`
  - 获取功能
    - `V	get(Object key)`:
      - 根据指定的key返回对应的value
      - 代码示例：`System.out.println(map.get("IT001"));//王五`
      - get与remove：返回值看着差不多，但是get只做了获取的动作，remove是删除后获取，对map集合进行了修改
    - `int	size()` 
      - 返回对应关系的个数
      - 代码示例: `System.out.println(map.size());//2`
  - 判断功能
    - `boolean	containsKey(Object key)`:
      - 判断某个key值是否存在 
      - 代码示例：`System.out.println(map.containsKey("IT001"));//true`
    - `boolean	containsValue(Object value)`:
      - 判断某个value值是否存在 
      - 代码示例：`System.out.println(map.containsValue("张三"));//false`
    - 以上两个功能注意：
      - 键值需要与方法对应，如果判key，传入了value值，也是不匹配的；
      - 特别是键值对类型相同时，注意不要混淆
    - `boolean	isEmpty()`:
      - 判断是否有对应关系，即判空
      - 注：清空clear()后的map必为空
      - 代码示例：`map.clear(); System.out.println(map.isEmpty());//true
  - 删除功能
    - `void	clear()`:
      - 清空所有对应关系
      - 代码示例：`map.clear();`
    - `V	remove(Object key)`:   
      - 根据指定的key删除对应关系，并返回key对应的value，如果没有删除成功则返回null
      - 代码示例：`System.out.println(map.remove("IT001"));//null`
  - 获取所有元素的方法
    - `Set<K>	keySet()`:
      - 以Set的形式返回所有的key
        - key值不允许重复，所以用Set装正好
      - 注意：Set的泛型是什么类型，需要看定义的key值是什么类型
      - 代码示例：`Set<String> keys = map.keySet();`
        - 之后可以用foreach遍历此集合：`for (String key : keys) { System.out.println(key); }` 
    - `Collection<V>	values()` 
      - 以Collection的形式返回所有的value值
        - value值允许重复，因此没有使用Set装
      - 查看values()方法的源码发现：底层并不是List, 因此不能强转为List类型  
      - 代码示例：`Collection<String> values = map.values();`
        - 之后可以用foreach遍历此集合：`for (String value : values) { System.out.println(value); }`

- ### Map的遍历
  - 遍历方法1：
    - 思路：
      - 先获取所有的Key，然后遍历所有Key，并根据每个Key值依次获取对应的value值  
    - 涉及方法：
      - map.keySet(); map.get(key);
    - 代码示例：
    ```java
          import java.util.HashMap;
          import java.util.Map;
          import java.util.Set;

          public class MapDemo {
            public static void main(String[] args) {
              Map<String, String> map = new HashMap<String, String>();
              map.put("IT001", "张三");//null
              map.put("IT002", "李四");//null
              map.put("IT003", "王五");//张三

              System.out.println(map);//{IT002=李四, IT001=王五}

              Set<String> keys = map.keySet();//获取所有key值
              for (String key : keys) {//遍历所有key值，并获取对应的value值
                String value = map.get(key);
                System.out.println(key+"---"+value);
              }
            }
          }    
    ```
  - 遍历方法2：
    - 思路：
      -  偏面向对象思想；
      -  通过entrySet()方法获取映射关系，然后通过映射关系里的getKey()和getValue()方法分别获取键值对的值。
    - `Set<Map.Entry<K,V>>	entrySet()`:
      - 返回此映射中包含的映射关系的 Set 视图。
      - 包含getKey()和getValue()方法，可以通过此entry对象调用获取对应的键值对的值。 
    - 优势：
      - 相比两层for循环，效率提升了很多 
    - 代码示例：
    ```java
    //entrySet()相当于结婚证对象，通过结婚证对象来获取丈夫和媳妇
    class 结婚证<K,V>{
      K 丈夫;
      V 媳妇;
    }
    public 结婚证(K 丈夫, V 媳妇){
      this.丈夫 = 丈夫;
      this.媳妇 = 媳妇;
    }
    public K get丈夫(){
      return 丈夫;
    }
    public V get媳妇(){
      return 媳妇;
    }
    ```
    
    ```java
        import java.util.HashMap;
        import java.util.Map;
        import java.util.Set;

        public class MapDemo {
          public static void main(String[] args) {
            Map<String, String> map = new HashMap<String, String>();
            map.put("IT001", "张三");//null
            map.put("IT002", "李四");//null
            map.put("IT003", "王五");//张三

            System.out.println(map);//{IT002=李四, IT001=王五}

            Set<Map.Entry<String, String>> entrys = map.entrySet();
            for (Map.Entry<String, String> entry : entrys) {
              String key = entry.getKey();
              String value = entry.getValue();
              System.out.println(key+"---"+value);
            }
          }
        }    
    ```

- ### HashMap存储对象并遍历
  - 字符串对象作为key
    - 同上一节的Map遍历
    - 包含以上两种遍历方法
  - 自定义对象作为key 
    - 同样包括两种遍历方法
    - 不同点：
      - 以Student为例: `new Student("张三",18);`与`new Student("张三",18);`
      - Key值需要具有唯一性，自定义对象作为key值时，默认的方法不会判定成员变量相同的为重复(new了不同的对象)
      - 解决方法：与之前类似，定义对象的代码中重写hashCode(), equals()方法

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
