# Java异常处理


### 目录

<!--GFM-TOC -->
* [Java异常](#java异常):
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

- ### 异常的处理方式
  - 两种：
    - 捕获
    - 抛出  
  - 捕获
    - 关键语句：`throw...catch`，同if-else的语句组合
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
  - 抛出：
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

- ### 处理多个异常
  - 可以使用多个try-catch组合
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
  - 可以使用一个try和多个catch 
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
  - 多个try-catch的执行顺序：
    - 多个catch之间的异常可以有子父类异常共存；
    - 平级异常之间没有顺序关系，可以任意放在前后；
    - 如果有子父类同时在，父类异常必须放在子类的后面
      - 否则父类后面的代码永远执行不到，java不允许这样的语句存在。  

- ### Throwable的常用方法
  - Throwable 类: 
    - Java 语言中所有错误或异常的超类。
    - 只有当对象是此类（或其子类之一）的实例时，才能通过 Java 虚拟机或者 Java throw 语句抛出。
    - 类似地，只有此类或其子类之一才可以是 catch 子句中的参数类型。
    - 简单来说，当有异常发生的时候，并且收集到某‘Exception e’中时，就可以通过e调用其方法
  - `String	getMessage()`:
    - 获取异常原因
    - 示例：
      - `catch(ArithmeticException e) { System.out.println(e.getMessage());/// by zero }`
  - `String	toString()`:
    - 获取异常的类型和原因
    - 示例：
      - `System.out.println(e.toString());//java.lang.ArithmeticException: / by zero` 
  - `void	printStackTrace()`:
    - 打印异常的类型、原因和位置
    - 自带打印，没有返回值，可以直接调用，会自动输出 
    - 示例：
      - `e.printStackTrace();`
  - 与JVM自动抛出异常的区别：
    - 手动调用后，是可控的输出，不会终止程序，异常语句后的语句也会正常运行。 
    - 例如：下方示例代码的try-catch代码块后的hello语句也会正常执行。
  - 代码示例：
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
  - eclipse快速生成try-catch代码：
    - 选中语句 -- 右键 -- surroundwith - try/catch block
    - 自动填充`e.printStackTrace();`，可以手动修改catch传入的异常类型

- ### finally
  - 

- ### 异常的分类

- ### 自定义异常


- ### 递归



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
