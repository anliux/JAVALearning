# Java异常处理


### 目录

<!--GFM-TOC -->
* [Java异常](#java异常): 异常概述, 异常的体系结构, JVM处理异常的方式
* [异常的处理方式](#异常的处理方式): 捕获(try-catch), 抛出(方法名后throws)
* [处理多个异常](#处理多个异常): 多个try-catch组合, 一个try多个catch, 多个catch的执行顺序
* [Throwable的常用方法](#throwable的常用方法): Throwable概述, getMessage(), toString(), printStackTrace(), 与JVM自动抛出异常的区别, eclipse生成try-catch
* [finally](#finally): finally概述, finally格式, IO流中使用异常捕获的正确方法
* [异常的分类](#异常的分类): 编译时异常, 运行时异常
* [自定义异常](#自定义异常): throw和throws, 查看源码学习定义一个异常的格式, 自定义一个MyException异常
* [递归](#递归): 
<!--GFM-TOC -->



## Java异常
- ### 异常概述
  - 引入：
    - 在写代码时，经常出现一些小问题。为了方便我们处理这些问题，Java提供了异常机制 
  - 概述： 
    - 异常，即不正常，在写代码时出现的编译或运行时的异常。
  - 异常内容：
    - 包含了错误的类型、原因和位置。   

- ### 异常的体系结构
  - 最顶层：Throwable 
    - Error: 出现的不能处理的严重问题
    - Exception: 可以处理的问题 
  - 类比：电脑
    - 系统中毒：重装系统就可以了
    - 主板坏了：换一台新电脑 

- ### JVM处理异常的方式
  - 如果出现异常我们没有处理，则JVM会帮我们处理
  - JVM会把异常的类型、原因、位置显示在命令行，并且终止程序
  - 异常后的代码不会执行

### 异常的处理方式
- ### 两种：
  - 捕获
  - 抛出  

- ### 捕获
  - 关键语句：
    - `throw...catch`，同if-else的语句组合
  - 语句格式：
    ```java
      throw{
        语句1;
        可能出问题的代码;
        语句2;
      }catch(异常类名XxxException 自定义异常名){
        处理异常语句;
      }
    ```
  - try..catch语句的执行顺序：
    - 如果发生异常：
      - 则异常语句下面的代码不执行，直接跳入catch语句中，catch语句结束后，整个try-catch结束。
    - 如果没有发生异常：
      - try语句执行结束后，try..catch直接结束，不再执行catch语句。
    - 代码示例：
    ```java
      public class ThrowsDemo {
        public static void main(String[] args) {
          try {
            System.out.println(1);
            System.out.println(10/0);
            System.out.println(2);
          }catch(ArithmeticException ae) {//注意catch参数
            System.out.println(3);
          }
          //输出：1 3
        }
      }    
    ```

- ### 抛出：
  - 场景：
    - 当我们不想处理异常，或者没有能力处理时，可以选择抛出异常，谁调用方法谁处理异常
  - 使用关键字throws在方法的声明处抛出异常
    - 注意：抛出的异常可以是异常的父类异常 
  - 代码示例：
    ```java
      import java.io.FileWriter;
      import java.io.IOException;

      public class ThrowsDemo {
        public static void main(String[] args) throws IOException {//此处也可以抛出父类异常: Exception
          //method();
          function();
        }

        public static void function() throws IOException{
          FileWriter fw = new FileWriter("a.txt");
        }
      }  
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 处理多个异常
- ### 可以使用多个try-catch组合
  - 针对可能异常的代码，分别catch异常
  - 存在try的代码重复
  - 代码示例：
    ```java
        public class ExceptionDemo {
          public static void main(String[] args) {
            try {
              String s = null;
              System.out.println(s.length());//java.lang.NullPointerException
            }catch(NullPointerException e) {
              System.out.println("空指针异常了");
            }

            try {
              int[] arr = new int[5];
              System.out.println(arr[8]);//java.lang.ArrayIndexOutOfBoundsException
            }catch(ArrayIndexOutOfBoundsException e) {
              System.out.println("数组越界异常了");
            }
            /* 输出：
             * 空指针异常了
             * 数组越界异常了			
             * */	
          }
        }    
    ```

- ### 可以使用一个try和多个catch 
  - 类似于if-else语句，catch直接跟在catch后面即可
    - 如果一段代码有多个异常，只能捕获最开始出现的异常，然后就通过catch退出了
  - 最后可以添加一个所有异常的父类异常，相当于'if-else if'里的else
  - 代码示例：
    ```java
        public class ExceptionDemo {
          public static void main(String[] args) {
            try {
              //String s = null;
              //System.out.println(s.length());//java.lang.NullPointerException

              //int[] arr = new int[5];
              //System.out.println(arr[8]);//java.lang.ArrayIndexOutOfBoundsException

              System.out.println(10/0);//出现异常了

            }catch(NullPointerException e) {
              System.out.println("空指针异常了");
            }catch(ArrayIndexOutOfBoundsException e) {
              System.out.println("数组越界异常了");
            }catch(Exception e) {
              System.out.println("出现异常了");
            }	
          }
        }    
    ```
  
- ### 多个catch的执行顺序：
  - 多个catch之间的异常可以有子父类异常共存；
  - 平级异常之间没有顺序关系，可以任意放在前后；
  - 如果有子父类同时在，父类异常必须放在子类的后面
    - 否则父类后面的代码永远执行不到，java不允许这样的语句存在。  

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Throwable的常用方法
- ### Throwable类:
  - Java 语言中所有错误或异常的超类。
  - 只有当对象是此类（或其子类之一）的实例时，才能通过 Java 虚拟机或者 Java throw 语句抛出。
  - 类似地，只有此类或其子类之一才可以是 catch 子句中的参数类型。
  - 简单来说，当有异常发生的时候，并且收集到某‘Exception e’中时，就可以通过e调用其方法

- ### `String	getMessage()`:
  - 获取异常原因
  - 示例：
    - `catch(ArithmeticException e) { System.out.println(e.getMessage());/// by zero }`

- ### `String	toString()`:
  - 获取异常的类型和原因
  - 示例：
    - `System.out.println(e.toString());//java.lang.ArithmeticException: / by zero` 
  
- ### `void	printStackTrace()`:
  - 打印异常的类型、原因和位置
  - 自带打印，没有返回值，可以直接调用，会自动输出 
  - 示例：
    - `e.printStackTrace();`
  
- ### 与JVM自动抛出异常的区别：
  - 手动调用后，是可控的输出，不会终止程序，异常语句后的语句也会正常运行。 
  - 例如：下方示例代码的try-catch代码块后的hello语句也会正常执行。
  
- ### 代码示例：
    ```java
      public class ExceptionDemo {
        public static void main(String[] args) {
          try {
            System.out.println(10/0);//出现异常了

          }catch(ArithmeticException e) {
            System.out.println(e.getMessage());/// by zero
            System.out.println(e.toString());//java.lang.ArithmeticException: / by zero
            e.printStackTrace();
            /*
             * java.lang.ArithmeticException: / by zero
             * 		at test.demo.ExceptionDemo.main(ExceptionDemo.java:6)
             * */
          }	
          syso("hello");//hello
        }
      }  
    ```
  
- ### eclipse快速生成try-catch代码：
  - 选中语句 -- 右键 -- surroundwith - try/catch block
  - 自动填充`e.printStackTrace();`，可以手动修改catch传入的异常类型

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## finally
- ### finally概述：
  - try-catch-finally组合使用，finally用于释放资源等收尾工作
  - 无论try-catch语句如何执行，finally的代码都一定会执行。
  
- ### finally格式：
    ```java
    try{
      有可能出问题的代码;
    }catch(异常对象 异常名){
      处理异常;
    }finally{
      释放资源;
      清理垃圾;
    }    
    ```
  
- ### IO流中使用异常捕获的正确方法
  - 思路：
    - `FileWriter fw = new FileWriter("exception.txt");`: 
      -  两种异常处理方式，之前IO流部分选抛出异常，这次选try-catch环绕，自动生成try-catch代码块
    - `fw.close();`: 
      - 如果写在try部分，中途有异常语句(比如'10除以0')，后面不执行，则不刷新，则异常前的write()也无法写入内容
      - 要保证close()执行，则把这条语句放在finally里
    - `FileWriter fw = new FileWriter("exception.txt");`: 定义FileWriter对象
      - 如果定义在try代码块，则finally的fw.close()会有问题，看不到fw对象
      - 所以需要在try-catch代码块外先定义好: `FileWriter fw;`
    - `fw.close()`: 
      - 此时finally部分的close代码仍然需要处理异常，继续选try-catch处理
      - 根据错误提示，fw初始化为null：`FileWriter fw = null;`
      - 注意：开始写入才需要close，如果在fw创建IO对象/写入语句执行之前就有异常，则抛出相应的异常 (参考如下代码)  
        - finally部分的fw看不到try部分的fw做了什么，可能在任何位置异常中断，因此需要在代码块外赋初值null
  - 代码示例： 
    ```java
          import java.io.FileWriter;
          import java.io.IOException;

          public class ExceptionDemo {
            public static void main(String[] args) {
              FileWriter fw = null;////finally的fw看不到try部分的任何操作，需要有初始化值
              try {
                System.out.println(10/0);//此句异常：抛出异常，没有生成"exception.txt"文件
                fw = new FileWriter("exception.txt");
                fw.write("hello");
                fw.write("java");
                //System.out.println(10/0);//此句异常：中断刷新后，仍然写入了hellojava
                fw.write("world");

              } catch (IOException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
              } finally {
                try {//close: 放在finally中保证执行此句代码，由此衍生出另一个try-catch代码块
                  if(fw != null)//不加这条判断，会抛出空指针异常
                    fw.close();//加上这条判断：java.lang.ArithmeticException
                } catch (IOException e) {
                  // TODO Auto-generated catch block
                  e.printStackTrace();
                }
              }		
            }
          }
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 异常的分类
- ### 运行时异常
  - RuntimeException的子类就是运行时异常
  - 在编译时期可以自由选择处理或不处理
  - 举例：数组越界异常、空指针异常、数学运算异常(除以0)等都是运行时异常，编译阶段并不会报错。

- ### 编译时异常
  - Exception的子类，且非RuntimeException的子类
  - 在编译时期就必须处理
  - 举例: IOException

- ### 在方法名处throws异常 
  - 如果是编译时异常，必须抛出；
  - 如果是运行时异常，可以不抛出。 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 自定义异常
- ### throw和throws:
  - throws: 处理异常的一种方式，把异常抛出，由调用者来处理
    - 示例：`public static void main(String[] args) throws IOException` 
  - throw: 制造异常的方式，同时结束方法
    - 示例：`throw new MyException("考试成绩不符合要求");`
  - 注意：
    - 如果抛出(throw)的是编译时异常，则必须在方法声明处抛出(throws)   
  
- ### 查看异常的源码学习如何自定义一个异常
  - 异常的父类：
    - 按照异常分类定义，运行时异常继承RuntimeException，编译时异常继承Exception
  - 关键点：
    - 写一个无参构造继承父类，一个带参构造(传入String类型)继承父类
  - eclipse可以自动生成构造：
    - 只选取无参和带String参两种构造即可
  
- ### 自定义一个MyException异常，并在main方法中调用的代码示例：
    ```java
    //MyException.java

    public class MyException extends RuntimeException{

      public MyException() {
        super();
        // TODO Auto-generated constructor stub
      }

      public MyException(String message) {
        super(message);
        // TODO Auto-generated constructor stub
      }
    }  
    ```
    
    ```java
    //ExceptionDemo.java
    
    public class ExceptionDemo {
      public static void main(String[] args) {
          try {
            checkScore(110);
          } catch (Exception e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
          }
      }

      public static void checkScore(int score) {
        if(score>100 || score<0) {
          throw new MyException("考试成绩不符合要求");
        }
        System.out.println("考试成绩符合要求");
      }
    }    
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 递归
- ### 递归概述
  - 引入：
    - 把大问题拆成很多小问题，然后把小问题拆成更多的小小问题；
    - 当把更多小小问题解决了，小问题也解决了；
    - 随着小问题的解决，大问题也随之解决了。
  - 概述
    - 在方法本身不断地调用方法自己 
  - 注意：
    - 递归一定要有出口，否则内存溢出；
    - 递归次数不宜过多，否则内存溢出。  
    - 代码示例：
    ```java
    public void show(int n){
      if(){//出口
        return;
      }
      show(n-1);//微调
    }
    ```
  
  
- ### 求5的阶乘
  - 思路：
    - 5! = 5 * 4!
    - 4! = 4 * 3!
    - ..
    - 2! = 2 * 1!;
    - 1! = 1; 这里是出口 
  - 代码示例：
  ```java
      public class RecurrenceDemo {
        public static void main(String[] args) {
          int result = jC(5);
          System.out.println(result);//120
        }

        public static int jC(int n) {
          if(n == 1) {//出口
            return 1;
          }else {
            return n * jC(n-1);
          }
        }
      }    
  ```
  - 图解：
  ![递归求5的阶乘图解](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/method/%E9%80%92%E5%BD%92%E6%B1%825%E7%9A%84%E9%98%B6%E4%B9%98%E5%9B%BE%E8%A7%A3.bmp)

- ###


- ###



<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->





<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->






<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->






<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->




### END
