# Java多线程


### 目录

<!--GFM-TOC -->
* [多线程概述](#多线程概述): 进程和线程, 单线程和多线程, Thread类, 主方法是单线程
* [多线程的实现方式](#多线程的实现方式): Thread的常用方法(getName,setName,Thread(Runnable target),Thread.currentThread()), 继承Thread类构建线程, 实现Runnable接口构建线程, 两种方法对比
* [多线程模拟火车站售票与同步代码块](#多线程模拟火车站售票与同步代码块): 分析, Ticket类和主函数代码示例, 线程中加入sleep(), 同步代码块, 同步方法
* [线程的生命周期](#线程的生命周期): 生命周期, 线程的生命周期, 图解
<!--GFM-TOC -->



## 多线程概述
- ### 进程和线程：
  - 进程：当前正在运行的程序，一个应用程序在内存中的执行区域
    - 参考任务管理器中展示的多个进程 
  - 线程：进程中的一个执行控制单元，执行路径 
    - 运行程序是通过进程中的线程来执行的，线程依赖于进程 
    - 例如：一个公司接了一个活，这个活是由公司里的程序员来做的

- ### 单线程和多线程：
  - 一个进程可以有一个线程(单线程), 也可以有多个线程(多线程) 
  - 单线程：安全性高，但效率低
  - 多线程：安全性低，但效率高 
  - 举例：只刷牙肯定不会出问题，但是占用时间; 边刷牙边看手机，手机可能会掉水池里
 
- ### 多线程案例： 
  - 360中的多个线程同时执行：边体检边杀毒
  - 迅雷中的多个下载任务同时执行 

- ### Thread类
  - 位于java.lang包下，可以直接使用
  - 实现了Runnable接口
  - 线程：是程序中的执行线程。Java 虚拟机允许应用程序并发地运行多个执行线程。
  - 每个线程都有一个优先级，高优先级线程的执行优先于低优先级线程。每个线程都可以或不可以标记为一个守护程序。当某个线程中运行的代码创建一个新 Thread 对象时，该新线程的初始优先级被设定为创建线程的优先级，并且当且仅当创建线程是守护线程时，新线程才是守护程序。

- ### 主方法
  - 主方法的单线程和多线程两种方法的探讨图示
    - 如果是单线程的：
    ![主方法是单线程的](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/thread/%E4%B8%BB%E6%96%B9%E6%B3%95%E6%98%AF%E5%8D%95%E7%BA%BF%E7%A8%8B%E7%9A%84.bmp)
    - 如果是多线程的：
    ![主方法是多线程的](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/thread/%E4%B8%BB%E6%96%B9%E6%B3%95%E6%98%AF%E5%A4%9A%E7%BA%BF%E7%A8%8B%E7%9A%84.bmp) 
  - 结论
    - 主方法是单线程
    - 但是主方法中可以定义多个线程，以此来实现多线程 
 
<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 多线程的实现方式
- Thread的常用方法 
  - `String	getName()`: 
    - 返回该线程的名称。 
  - `void	setName(String name)`: 
    - 改变线程名称，使之与参数 name 相同。
  - 传入Runnable对象的构造方法：`Thread(Runnable target)` 
    - 分配新的 Thread 对象
    - 可以用在实现Runnable的多线程中
  - `static Thread currentThread()`: 
    - 返回对当前正在执行的线程对象的引用。
    - 静态可以直接类名调用，可以用在实现Runnable的多线程中
    - 注意：想要调用类名仍然需要使用getName()方法
    - 调用类名示例：`Thread.currentThread().getName()` -- 链式编程

- ### 方式1：继承Thread类
  - 将类声明为 Thread 的子类。该子类应重写 Thread 类的 run 方法。接下来可以分配并启动该子类的实例
    - 四个要点
    - 1. 将类声明为 Thread 的子类：继承Thread类
    - 2. 该子类应重写 Thread 类的 run 方法：重写run()方法
    - 3. 分配：创建该子类的实例 new
    - 4. 启动该子类的实例：start()方法
  - 创建MyThread类并定义
    - 两个要点：继承Thread方法；重新run()方法
    - 代码示例：
    ```java
        //MyThread.java
        public class MyThread extends Thread{
          @Override
          public void run() {//这里可以输入run后用alt+/自动填充
            for (int i = 0; i < 100; i++) {
              System.out.println(getName() + ": " + i);
            }
          }
        }     
    ```
  - 在main方法中创建并使用MyThread对象  
    - 两个要点：创建子类对象；启动子类示例
    - 代码示例：
    ```java
        //ThreadDemo.java
        public class ThreadDemo {
          public static void main(String[] args) {
            //创建线程实例
            MyThread mt = new MyThread();
            //修改线程名字
            mt.setName("张三");
            //启动线程
            mt.start(); 
            
            MyThread mt2 = new MyThread();//创建线程示例
            mt2.setName("李四");
            mt2.start();//启动线程
          }
        }         
    ```
  - 多线程资源分配：
    - 每次运行，两个线程的启动先后是不一样的：
      - 随机性
    - CPU执行程序(线程)的随机性：
      - CPU在多个线程之间快速切换
      - 感觉不到程序卡顿，实际是CPU在快速切换，同时仍然是只执行某一个线程 
    - 多线程的高效性：
      - 虽然是同时只能执行一个，但多线程的情况下，抢到执行权的概率就高了，效率相对也变高了 

- ### 方式2：实现Runnable接口
  - 声明实现 Runnable 接口的类。该类然后实现 run 方法。然后可以分配该类的实例，在创建 Thread 时作为一个参数来传递并启动。
    - 定义线程类，并实现Runnable接口
    - 线程类：实现 run 方法
    - 创建线程类实例
    - 创建 Thread 时，该实例作为一个参数来传递并启动：`new Thread(p).start();`
      - 创建Thread和启动start可以分两步，也可以写在一起 
  - 创建MyThread类并定义
    - 两个要点：继承Thread方法；重新run()方法
    - 代码示例：
     ```java
      public class MyThread implements Runnable{
        @Override
        public void run() {//这里可以输入run后用alt+/自动填充
          for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName()+ ": " + i);//getName()不可用了
          }
        }
      }    
     ```
  - 在main方法中创建并使用MyThread对象  
    - 两个要点：创建子类对象；启动子类示例
    - 两种方法：
      - 分别创建两个MyThread实例和两个Thread实例
      - 共用同一个MyThead实例，分别传入两个Thread实例中
        - 弊端：如果MyThread带参构造，new时传入参数，并在run()中进行了输出等使用，则结果会不同
    - 代码示例：
     ```java
        //分别创建两个MyThread实例和两个Thread实例
        public class ThreadDemo {
          public static void main(String[] args) {
            //创建线程实例
            MyThread mt = new MyThread();//new时可以传入不同的参数
            Thread t = new Thread(mt);
            t.setName("老王");
            t.start();

            //创建另一个线程实例
            MyThread mt2 = new MyThread();//new时可以传入不同的参数
            Thread t2 = new Thread(mt2);
            t2.start();
          }
        } 
        
        //共用一个MyThread实例，分别传入两个Thread实例中
        public class ThreadDemo {
          public static void main(String[] args) {
            //创建线程实例
            MyThread mt = new MyThread();//共用：new时传入的参数相同
            Thread t = new Thread(mt);
            t.setName("老王");
            t.start();

            //创建另一个线程实例
            Thread t2 = new Thread(mt);
            t2.start();
          }
        }        
     ```

- ### 两种方式的区别：
  - 第一种是继承，而第二种是实现。
  - 鉴于Java的单一继承规则，如果用第一种方式，则不能再继承其他父类，而用第二种，不影响其他父类的继承
  - 推荐使用第二种：实现的方式 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 多线程模拟火车站售票与同步代码块
- ### 分析：
  - 需要火车票的总数量，并且每售出一张，数量减一
  - 需要判定：当火车票数量小于1时，停止售票
  - 需要使用多线程模拟多个售票窗口
  - 当火车票售完以后，火车票并不会关门，仍然开着

- ### Ticket类
  - 注意点：
    - 优先选实现Runnable的方法
    - 设置票数变量tickets，且调用时使用同一个TicketThread对象实例，以保证是同一个票数对象在变化
    - tickets--：放在循环里，节约写代码的空间
  - 代码示例： 
    ```java
      public class TicketThread implements Runnable{
        int tickets = 100;

        @Override
        public void run() {
          while(true) {//火车站不会因为票卖光而关闭: 程序需要手动终止
            if(tickets > 0 ) {
              System.out.println(Thread.currentThread().getName() + ":" + tickets--);
            }
          }
        }
      }  
    ```

- ### 主函数
  - 步骤：
    - 创建同一个Ticket线程实例：保证票数变化的是同一个票数
    - 创建三个线程，传入同一个Ticket线程对象，并分别重命名线程的名字
    - 启动线程
    - 卖票结束后需要手动终止程序 (这个设定危，一定一定要记得终止程序!!!!)
  - 代码示例：
    ```java
      public class ThreadDemo {
        public static void main(String[] args) {
          //创建线程实例
          TicketThread tt = new TicketThread();

          Thread t1 = new Thread(tt);
          t1.setName("窗口1");
          Thread t2 = new Thread(tt);
          t2.setName("窗口2");
          Thread t3 = new Thread(tt);
          t3.setName("窗口3");

          //启动线程对象
          t1.start();
          t2.start();
          t3.start();
        }
      }  
    ```

- ### 线程中加入sleep()
  - `static void sleep(long millis)`:
    - 在指定的毫秒数内让当前正在执行的线程休眠（暂停执行）
    - 此操作受到系统计时器和调度程序精度和准确性的影响。
  - 加到代码中会需要try-catch捕获异常(上面没有抛出，下面捕获即可)
  - 加入sleep()的问题：
    - 结果会出问题，比如售出相同票编号多于一次，或售出0甚至负数编号的票 
  - 代码示例：
    ```java
      //TicketThread.java
      public class TicketThread implements Runnable{
        int tickets = 100;

        @Override
        public void run() {
          while(true) {//火车站不会因为票卖光而关闭: 程序需要手动终止
            if(tickets > 0 ) {
              try {
                Thread.sleep(100);//参数单位是毫秒
              } catch (InterruptedException e) {
                e.printStackTrace();
              }
              System.out.println(Thread.currentThread().getName() + ":" + tickets--);
            }
          }
        }
      }  
    ```
  - 加入sleep()后出现问题的原因分析：
    - 三个售票窗口t1, t2, t3
    - 假设只剩下1张票，则仍然符合'if(tickets>0){}'的判断，可以进入if代码块中，即会执行里面的sleep()和syso()语句
      - t1: 过来发现有票，进入if代码块，然后sleep()了
      - t2: 也过来，发现有票，进入if代码块，然后sleep()了
      - 这时t1：sleep结束，执行下一句syso语句，ticket=0;
      - 这时t2: sleep结束，执行下一句syso语句，ticket=-1;
      - 如果在t1和t2 sleep时，t3也进入了if代码块，则会出现ticket=-2的情况  

- ### 同步代码块
  - 问题出现的原因分析：
    - 有多个线程；
    - 有被多个线程所共享的数据；
    - 多个线程并发地访问共享的数据。
  - 举例说明：火车上的厕所
    - 当有人在使用时，就会把门锁上，标识变红，其他人就进不去了；
    - 使用完毕，打开锁，标识变绿，这时其他人才能使用
    - 如果里面的人一直锁着门，标识一直是红色，别人无法使用，直到锁打开
  - Synchronized: 
    - 同步(锁)，可以修饰代码块和方法，被修饰的代码块和方法一旦被某个县城访问，则直接锁住，其他的线程将无法访问
  - 同步代码块： 
    - 注意：锁对象需要被所有的线程所共享(否则如果有线程不认识，就难办了) 
    ```java
      Synchronized(锁对象){
        //coding...
      }
    ```
  - 用同步改进后的TickedThread类：
    - 首先要创建一个被所有线程所共享的锁，并传入同步代码块中
    - 把需要锁起来的代码放在同步代码块中
    - 注：加了同步以后明显能感觉到运行变慢了，这是同步的缺点
     ```java
        public class TicketThread implements Runnable{
          int tickets = 100;
          Object obj = new Object();//放在这里，可以被所有线程所共享，可以作为锁

          @Override
          public void run() {
            while(true) {//火车站不会因为票卖光而关闭: 程序需要手动终止
              synchronized (obj) {
                if(tickets > 0 ) {
                  try {
                    Thread.sleep(100);
                  } catch (InterruptedException e) {
                    e.printStackTrace();
                  }//参数单位是毫秒
                  System.out.println(Thread.currentThread().getName() + ":" + tickets--);
                }
              }
            }
          }
        }  
     ```
  - 同步与非同步的优缺点：
    - 同步：安全性高，效率低
    - 非同步：效率高，安全性低

- ### 同步方法
  - 同步方法的几种方式：
    - 方式1：
      - 将有问题的代码封装进一个方法中，然后在同步代码块中调用此方法
      - 代码示例：
        ```java
        synchronized (obj) {
          method();
        }
        ...
        private void method(){
          //这里放所有有同步问题的代码
        }
        ```
    - 方式2：
      - 与方式1类似的思路，如果调用时不放在同步代码块中，则使用同步代码块把抽出的方法中的代码都用同步代码块封装
      - 代码示例：
        ```java
        method();//调用时不放在同步代码块中
        ...
        private void method(){
          synchronized (obj) {
            //这里放所有有同步问题的代码
          }          
        }
        ```
    - 方式3： 
      - 使用Synchronized来修饰方法
      - 代码示例：
        ```java
        method();//调用时不放在同步代码块中
        ...
        private Synchronized void method(){//同步修饰符修饰此方法
            //这里放所有有同步问题的代码       
        }
        ```
    - 方式4：
      - 静态同步方法，也是可以的，同步修饰符放在void之前，否则报错
      - 代码示例：
        ```java
        method();//调用时不放在同步代码块中
        ...
        private static Synchronized void method(){//同步修饰符修饰此方法
            //这里放所有有同步问题的代码 
            //注意：此静态方法内的成员方法，也需要用静态修饰，比如外面的`static int tickets=100;`
        }
        ```   
  - 同步方法：
    - 使用关键字Synchronized修饰的方法
    - 一旦被某一个线程访问，则整个方法全部锁住，其他线程无法访问 
  - 注意：
    - 同步方法也需要有锁对象，与同步代码块必须要一个锁对象类似 
    - 非静态同步方法的锁对象：this
    - 静态同步方法的锁对象：当前类的字节码对象
      - 静态方法随着类的加载而加载，没有this 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 线程的生命周期
- ### 生命周期：
  - 指一个对象的生老病死 

- ### 线程的生命周期：
  - 新建 -- 就绪 -- 运行 -- 死亡，中间可能经历等待
  - 新建：创建线程对象
    - 两种方法，继承和实现
    - 根据需要，如果需要继承其他父类，则只能选择实现的方式 
  - 就绪：
    - 在新建和运行之间的一个阶段
    - 具备了执行条件，没有具备执行权利 
  - 运行：
    - 具备了执行条件，同时具备了执行权利 
  - 死亡：
    - 线程对象变成了垃圾  
  - 等待：
    - 介于就绪和运行之间的一个阶段
    - 需要锁对象调用：wait()等待，notify()唤醒
    - 运行过程中，调用了wait()则进入等待阶段
    - 等待过程中，如果调用了notify()则进入

- ### 图解：
  ![线程的生命周期](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/thread/%E7%BA%BF%E7%A8%8B%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.bmp)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
