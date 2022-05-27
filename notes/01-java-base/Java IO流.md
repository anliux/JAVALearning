# Java IO流


### 目录

<!--GFM-TOC -->
* [IO流基础](#io流基础): 关联其他文件的备注, IO流概述和分类
* [FileWriter](#filewriter): FileWriter概述, 构造方法和成员方法, FileWriter写数据的方法, FileWriter写数据的换行, 追加写入
* [FileReader](#filereader): FileReader概述, FileReader读数据的方法, IO流案例之复制文本文件
* [字符缓冲流](#字符缓冲流): 字符缓冲流概述, 字符缓冲流的特殊功能：newLine()和readLine(), 字符缓冲流复制文件
* [字符流读写应用](#字符流读写应用): 复制文本文件的5种方法, 集合数据的读写应用
* [File类](#file类): File类概述, File类的构造方法, File类的创建/删除/判断/获取/修改功能, File的方法应用
* [IO流分类](#io流分类): 
* [输入输出流](#输入输出流): 
* [打印流](#打印流): 
* [对象操作流](#对象操作流): 
<!--GFM-TOC -->



## IO流基础
- ### 备注：
  - 本部分首次出现是在：[Java常用API: IO流](https://github.com/anliux/JAVALearning/blob/master/notes/01-java-base/Java%E5%B8%B8%E7%94%A8API.md#io%E6%B5%81)
  - 这里选取关键内容整理保留，并进行了新的标题划分
 
- ### IO流概述和分类
  - 引入：
    - 类似ArrayList的集合类，存储数据的有效范围仅为该代码运行期间，在内存中临时存储，再次打开时输入的数据已丢失。而IO流技术可以永久存储。
  - 概述：
    - IO流用来处理设备之间的传输问题，包括文件复制、上传/下载文件等。
  - IO流分类：
    - 输出流 (写数据)：FileWriter
    - 输入流 (读数据)：FileReader
    - 注：输入输出说的是Java程序本位下的输入输出，输入相当于读到Java程序，输出相当于从Java程序写数据到别的地方
  - 图示：
  ![IO流的作用及分类](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/IO%E6%B5%81%E7%9A%84%E4%BD%9C%E7%94%A8%E5%8F%8A%E5%88%86%E7%B1%BB.bmp)

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## FileWriter
- ### FileWriter概述
  - 输出流写数据，通过阅读API学习
  - java.io包下：
    - 需要导包 `import java.io.FileWriter;`
  - 输出流写数据的步骤：
    - 创建输出流对象；<创建文件时需要调用系统资源>
    - 调用输出流对象的写数据的方法，并flush刷新缓冲区；
    - 释放资源。<即通知系统释放和该文件相关的资源，因为创建输出流对象是调用系统资源创建的>

- ### FileWriter的构造方法和成员方法
  - 构造方法：
    - `FileWriter(String fileName)`: 传递一个文件名称 <或路径+文件名>
  - 成员方法：
    - `void write(String str)`: 写入数据
    - `void flush()`: 刷新缓冲区
      - 数据不会直接写到文件，而是写到了内存缓冲区，flush刷新后显示 
    - `void close()`: 释放调用的系统资源，写入数据不多时自带flush()步骤。
  - 创建输出流对象做了哪些事情：`FileWriter fw = new FileWriter("d:\\a.txt")`
    - 调用系统资源创建了一个文件；(没有路径所指文件时会自动创建)
    - 创建输出流对象；
    - 把输出流对象指向该文件。
  - 写数据方法的路径问题：
    - 相对路径：相对当前项目而言，在项目的根目录下(注意是"项目")
      - 示例：`FileWriter fw = new FileWriter("a.txt")//不加盘符的文件名;` 
    - eclipse中显示相对路径的文件：
      - 选中项目project -- 右键 -- refresh，即可在项目下出现相应的文件(a.txt)
      - 注意：右键的是项目名，不是包名或者Java程序名
    - 绝对路径：指明盘符的具体路径
      - 示例：`FileWriter fw = new FileWriter("d:\\a.txt");//加了盘符位置的文件名`
      - 注意：mac中路径为'/users/xx/...'
  - close()和flush()方法：
    - flush(): 刷新缓冲区；之后流对象还可以继续使用。
    - close(): 先刷新缓冲区，后通知系统释放资源；之后流对象不可以再使用了。
      - close()做两步，因此即使write()之后没有flush(), close()的时候也会自动刷新。
      - 写入内容较少时，可以省略flush().
  - 代码示例：(注意导包和抛出异常)
	  ```Java
	  import java.io.FileWriter;
	  import java.io.IOException;
	  public class FileWriterDemo{
		public static void main(String[] args) throws IOException {
			//创建输出流对象
			FileWriter fw = new FileWriter("d:\\a.txt");//没有该文件时会自动创建，使用绝对路径
				//如果不带盘符地址，默认为所写入的文件在代码项目所在路径下的相对路径
			//调用数据流对象的写数据方法
			fw.write("IO流你好");//写一个字符串数据
			fw.flush();//数据没有直接写到文件，而是写到了内存缓冲区，刷新缓冲区后才会显示
			fw.write("javaee");
			fw.flush();
			fw.close();//释放资源，否则fw会一直占用中
			//fw.write("123"); //close()之后再写数据会报错
			
		}
	  }
	  ```

- ### FileWriter写数据的方法
  - `void write(String str)`: 
    - 写入一个字符串数据
    - 代码示例：`fw.write("abcde");  fw.close(); //写入"abcde"; 此处写入较少可省略flush()` 
  - `void write(String str, int index, int lens)`:
    - 写入一个字符串中的一部分数据，即从索引值index开始，长度为lens的子串
    - 代码示例：`fw.write("abcde", 1, 3);  fw.close(); //可写入"bcd"`  
  - `void write(int ch)`:
    - 写入一个字符数据
    - 为int类型的好处是：既可以写char类型的数据，也可以写char对应的int类型的值，比如'a'和97均可
    - 代码示例：`fw.write('a');`和`fw.write(97);`均可写入字符'a' 
  - `void write(char[] chs)`: 
    - 写入一个字符数组数据
    - 代码示例：`char[] chs = {'a','b','c','d','e'}; fw.write(chs);//写入的数据在文件中的形式是"abcde"不带引号`
  - `void write(char[] chs, int index, int lens)`: 
    - 写入一个字符数组的一部分数据
    - 代码示例：`char[] chs = {'a','b','c','d','e'}; fw.write(chs,2,3);//写入的数据在文件中的形式是"cde"不带引号`

- ### FileWriter写数据的换行
  - 用换行符可以实现换行
    - 代码示例：for循环中：`fw.write(x); fw.write("\r\n");`
  - 不同系统识别的换行符不同：
    - Windows: `\r\n` 
    - linux: `\n`
    - mac: `\r`
    - 注意：如果在Windows用`\n`写入，则自带的记事本打开无法识别，显得的仍然是没有换行的；而用编辑器打开可以识别。
  - 缓冲流有特殊的换行方法
    - BufferedWriter: `void newLine()` -- 可根据系统自动匹配换行符，详见缓冲流的特殊功能部分。
    - 代码示例：`bw.newLine();//取代bw.write("\r\n")；`

- ### FileWriter写数据的追加写入
  - 构造方法：`FileWriter(Sting str, Boolean append)`
    - append默认为false，当需要追加时，可以在第二个参数位置写true
    - 这时再运行，会将新的内容追加到文件中
  - 代码示例：
    - `FileWriter fw = new FileWriter("c.txt",true); //默认为false，写为true时表示追加写入`
    - `fw.write("xxxxxx");//这时会追加新的xxxx内容写入到文件` 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## FileReader
- ### FileReader概述
  - 输入流写数据，通过阅读API学习
  - java.io包下：因此需要导包 `import java.io.FileReader;`
  - 构造方法：`FileReader(String filename)` -- 传递文件名称
    - 注意：仍然需要导包和抛出异常
  - 输入流写数据的步骤：
    - 创建输入流对象;
    - 调用输入流对象的读数据方法;
    - 释放资源.
  
- ### FileReader读数据的方法：
  - `int read()`: 
    - 一次读取一个字符，且存储类型为int，即字符对应的int值
      - 可通过(char)强转为char类型
    - 再次使用本方法时：自动读取下一个字符 <不需要像写数据一样声明追加>
    - 当没有可读取数据时，返回-1 <可作为读取循环结束的判断条件>
    - 空格、回车等也可以读取到，不需要在输出语句(syso)里加`ln` 
      - 例如：读取某个.java文件，可以在控制台输出带格式的代码 
    - 循环时while语句的妙用：
      - `while((ch = fr.read()) != -1){...}`
      - 做了三步：read()读数据; 读取到的结果赋值给ch; 判断ch的值是否为-1
    - `void close()`: 读取结束后记得关闭释放资源
      - 代码示例：`fr.close();`
    - 读数据常见异常：
      - `java.io.FileNotFoundException: fr.txt (系统找不到指定文件)` 
    - 代码示例：
	 ```Java
	  import java.io.fileNotFoundException;
	  import java.io.FileReader;
	  import java.io.IOException;
	  public class FileReaderDemo{
		public static void main(String[] args) throws IOException{
			FileReader fr = new FileReader("fr.txt");//创建输入流对象; fr.txt内容为："abc"
			/*
			int ch = fr.read();//调用输入流对象的读取方法
			System.out.println(ch);//97
			System.out.println((char)ch);//a
			*/
			int ch;
			while((ch = fr.read()) != -1){//这条语句做了三个步骤
				System.out.print();
			}
			fr.close();//释放资源
			
		}
	  }
	 ```
  - `int read(char[] cbuf)`
    - 一次读取一个字符数组的数据，返回<实际>读取的字符个数
    - 步骤仍然是：创建对象；调用读数据方法；释放资源。
    - `char[] chs = new char[1024];`
      - 自定义字符数组，相当于读取到自定义数组中，数组长度为每次读取的字符个数
      - 通常，数组长度定义为1024或1024的整数倍：因为MB,GB等的换算是1024
    - 读取为空时，返回-1 <可作为循环结束的条件>
    - 会读取回车 `\r\n`，占用2个长度
    - 上一次的读取会被下一次替换，当下一次读取不够全部替换上一次读取时，上一次的读取会遗留在存储字符数组中
      - 详见下方图解 
    - 输入推荐用`System.out.println(new String(chs,0,len));`
    - 代码示例：
	```java 
	//创建输入流对象
	FileReader fr = new FileReader("a.txt");
	char[] chs = new char[1024];
	int len;
	while((len = fr.read(chs)) != -1){
	System.out.print(new String(chs,0,len));//注意syso不要写ln，读取了回车等格式符
	}
	fr.close();    
	```
  - FileReader两种读数据方法对比图解
  ![FileReader读数据的两种方式图解](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/FileReader%E8%AF%BB%E6%95%B0%E6%8D%AE%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F%E5%9B%BE%E8%A7%A3.bmp)

- ### IO流案例：复制文本文件
  - 题目：
    - 文件复制：将相同项目下的a.java中的内容复制到b.java文件中
  - 文件复制的套路：
    - 数据源：a.java -- 读数据 -- FileReader
    - 目的地：b.java -- 写数据 -- FileWriter
  - 注意点：
    - 同时有读写时，close()先关哪个都可，推荐先关write.
  - '一次读取一个字符'的代码示例：
	```java 
	  FileReader fr = new FileReader("a.java");//同项目下，用相对路径即可。下同。
	  FileWriter fw = new FileWriter("b.java");
	  //一次读取一个字符的定义方法
	  int ch;//定义返回值flag
	  while((ch = fr.read()) != -1){//参考按单个字符读取的循环
		fw.write(ch);
	  }
	  fw.close();
	  fr.close();
	```
  - '一次读取一个字符数组'的代码示例：
	```java 
	  FileReader fr = new FileReader("a.java");//同项目下，用相对路径即可。下同。
	  FileWriter fw = new FileWriter("b.java");
	  //一次读取一个字符数组的定义方法
	  char[] chs = new char[1024];//定义读取的字符数组
	  int len;//定义返回值flag
	  while((len = fr.read(chs)) != -1){//参考按单个字符读取的循环
		fw.write(chs,0,len);
	  }
	  fw.close();
	  fr.close();
	```	  

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 字符缓冲流
- ### 字符缓冲流概述
  - BufferedWriter:
    - 将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组、字符串的高效写入
      - 注意参数：传入一个new的输出流对象
    - 代码示例：`BufferedWriter bw = new BufferedWriter(new FileWriter("bw.txt"));`
    - 调用使用同FileWriter()
  - BufferedReader:
    - 从字符输入流中读取文本，缓冲各个字符，从而提供单个字符、数组、行的高效读取
      - 注意参数：传入一个new的输入流对象 
    - 代码示例：`BufferedReader br = new BufferedReader(new FileReader("br.txt"));`
      - 仍然分为读取单个字符和读取字符数组两种方式。
  - 导包：
    - `import java.io.BufferedWriter/BufferedReader;`
  
- ### 用缓冲流复制文件
    - 注意：记得开始导包和抛出异常
    - 数据源：a.java -- 读数据 -- FileReader -- 高效读数据 -- BufferedReader
    - 目的地：b.java -- 写数据 -- FileWriter -- 高效写数据 -- BufferedWriter
    - 代码示例：
	```java
	import java.io.* 
	...
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new FileReader("a.java"));
		BufferedWriter bw = new BufferedWriter(new FileWriter("b.java"));
		/*
		//一次读写一个字符
		int ch;
		while((ch = br.read()) != -1){
			bw.write((char)ch);
		}
		*/
		//一次读取一个字符数组
		char[] chs = new char[1024];
		int len;
		while((len = br.read(chs)) != -1){
			bw.write(chs,0,len);//不要忘记参数，防止写入未覆盖的遗留数据
		}
	}
	```

- ### 字符缓冲流的特殊功能
  - 字符缓冲流：
    - 包含缓冲输入/输出流：BufferedWriter 和 BufferedReader
    - 创建缓冲流对象：构造方法参数为对应的基本输入/输出流对象，而不是直接传入文件。 
    - 代码示例：`BufferedReader br = new BufferedReader(new FileReader("br.txt"));`
  - BufferedWriter:
    - `void newLine()`: 写一个换行符，这个换行符由系统决定 
      - 不需要再判断系统换行符，取代之前的`fw.write("\r\n");`
    - 代码示例: `bw.newLine();`
  - BufferedReader:
    - `String readLine()`: 一次读取一行数据，但不读取换行符 (但读取空格)
      - 返回值是字符串格式
      - 读取空格：所以不用担心格式会乱，只需要加上换行即可
      - 读取为空时返回null，可以作为循环结束的判断语句
    - 代码示例：
	```java 
	    BufferedReader br = new BufferedReader(new FileReader("br.txt"));
	    String line;
	    while((line = br.readLine()) != null){//这里同时做了三步，同上 (读取、赋值、判断)
		System.out.println();//readLine()不读取换行符，因此syso语句需要加上`ln`
	    }
	    br.close();
	```
  - 导包注意点：
    - 用字符缓冲流时，BufferedWriter/BufferedReader和FileWriter/FileReader都需要导入
    - 当然还有IO流异常 IOException 
  - 使用字符缓冲流的特殊方法复制文本文件
    - 代码示例：
    ```java
    public class CopyFileDemo{
	public static void main(String[] args) throws IOException{
		//创建缓冲流对象
		BufferedReader br = new BufferedReader(new FileReader("a.txt"));
		BufferedWriter bw = new BufferedWriter(new FileWriter("b.txt"));
		String line;
		while((line = br.readLine()) != null){
			bw.write(line);
			bw.newLine()
			bw.flush();
		}
		bw.close();
		br.close()
	}
    }
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 字符流读写应用
- ### 复制文本文件的5种方法
  - 基本流一次读写一个字符
  - 基本流一次读写一个字符数组
  - 缓冲流一次读写一个字符
    - 注意：缓冲流也可以用基本流的方法`br.read()`进行读取
  - 缓冲流一次读写一个字符数组
  - 缓冲流一次读写一个字符串 <推荐，重点掌握>
    - 用缓冲流的特殊方法进行读写 
    - `br.readLine()` and `bw.newLine()`.
  - 注：
    - 写代码时可以将读写的文件名和五种方法单独定义，提高复用性
    - 此处涉及异常抛出注意点：
      - 当所调用的方法抛出了异常时，所调用的方法也需要抛出异常，即main方法也需要加`throws IOException`

- ### 集合数据的读写应用
  - IO流：将集合中的数据写入文本文件
    - 题目：
      - 把ArrayList集合中的字符串数据存储到文本文件，每一个字符串元素作为文件中的一行数据 
    - 步骤：
      - 创建集合对象
      - 往集合中添加元素
      - 创建输出缓冲流对象
      - 遍历集合，得到每一个字符串元素，然后把该字符串元素作为数据写入到文本文件
      - 释放资源
    - 代码示例：
    ```java
    import java.io.*; //(ctrl+shift+o大法好)
    import java.util.ArrayList;

    public class ArrayListToFile{
	public static void main(String[] args) throws IOException{
		ArrayList<String> array = new ArrayList<>();
		array.add("hello");
		array.add("Java");
		array.add("world");
		BufferedWriter bw = new BufferedWriter(new FileWriter("a.txt"));
		for(int i=0;i<array.size();i++){
			String s = array.get(i);
			bw.write(s);
			bw.newLine();
			bw.flush();
		}
		bw.close();
	}
    }
    //运行，并刷新项目
    ```
  - IO流：将文本文件中的数据读取并存入集合中
    - 题目：
      - 文本文件中读取数据到ArrayList中，并遍历集合；每一行数据作为一个字符串元素。
    - 步骤：
      - 创建输入缓冲流对象；
      - 创建集合对象；
      - 去读数据，每次读取一行数据，把该行数据作为一个元素存储到集合中；
      - 释放资源；
      - 遍历集合.
    - 代码示例：
    ```java
    import java.io.*; //(ctrl+shift+o大法好)
    import java.util.ArrayList;

    public class ArrayListToFile{
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new FileReader("a.txt"));
		ArrayList<String> array = new ArrayList<>();
		String line;
		while((line = br.readLine()) != null){
			array.add(line);
		}
		br.close();
		for(int i=0;i<array.size();i++){
			String s = array.get(i);
			System.out.println(s);
		}
	}
    }
    //运行，并刷新项目
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## File类
- ### File类概述
  - 文件和目录路径名的抽象表示形式。
    - 目录：即路径 
  - File类的实例是不可变的。
    - 也就是说，一旦创建，File 对象表示的抽象路径名将永不改变 
  - 位置：java.io包
  - 注意不同系统的路径表示不同：
    - Windows：与注释相反方向的斜杠分割路径 "D:\abc\file.txt"
    - mac: 与注释相同方向的斜杠分割路径 "/users/abc/.."

- ### File的构造方法
  - 背景：
    - 在D盘下创建文件夹a, 并在文件夹a中创建文件b.txt
    - 路径：`D:\\a\\b.txt`
  - `File(String pathname)`:
    - 将指定的路径名转换成一个File对象
    - 示例：`File f = new File("D:\\a\\b.txt");` 
    - 注：
      - 如果删掉b.txt文件再运行，没有新建b.txt文件
      - 因此：本条语句只是创建了一个File对象指向特定路径而已，没有做其他事
  - `File(String parent, String child)`:
    - 根据指定的父路径和文件路径创建File对象
    - 父路径和文件路径的划分：
      - 父`D:\\a`, 文件路径`b.txt`: 可
      - 父`D:\\`, 文件路径`a\\b.txt`: 可
    - 示例: `File f = new File("D:\\a, "b.txt");` 或 `File f = new File("D:\\, "a\\b.txt");` 
  - `File(File parent, String child)`:
    - 根据指定的父路径对象和文件路径创建File对象
    - 与上一条的区别：父路径是File对象
    - 示例：
      - 先创建：`File parent = new File("D:\\a"); File f = new File(parent, "b.txt");`
      - 匿名调用：`File f = new File(new File("D:\\a"), "b.txt");`  

- ### File的创建功能
  - 绝对路径和相对路径：
    - 绝对路径：
      - 固定不可变的路径，以盘符开头 
    - 相对路径：  
      - 相对于某个参照物的路径，不以盘符开头
      - 在eclipse中，相对路径是指相对于当前项目的根目录 
  - 创建功能的返回值：
    - 如果是void，则一定会创建成功；
    - 如果是boolean，则不一定会创建成功，某些条件下会创建失败。 
  - 注：按需抛出异常并导异常包：
    - `..main() throws IOException{..}` 
  - `boolean createNewFile()`:
    - 创建文件的功能
    - 返回值为boolean类型：
      - 当指定文件不存在时：创建文件并返回true, 选中eclipse中的项目名刷新后会在根目录下显示新建的文件
      - 当指定文件已存在时：返回false 
    - 示例：`File f = new File("a.txt"); syso(f.createNewFile());//true, 再次运行为false`
  - `boolean mkdir()`:
    - 创建文件夹的功能
    - 返回值boolean型：
      - 指定文件夹不存在时创建并返回true，否则，若文件夹已存在时返回false
    - 示例：`File f = new File("b"); syso(f.mkdir());//结果：返回true, 且在项目根目录下新建b文件夹` 
  - `boolean mkdirs()`:
    - 创建多层文件夹的功能 
    - 创建指定文件夹，当文件夹所在的目录不存在，则顺道一块创建了 
      - mkdir没有的功能，没有上层文件时返回false
      - 注：mac系统路径格式问题(路径是另一个方向的斜杠)：
        - 没有上层文件时创建名为路径名的单层文件夹(eg. 'c\d\e')，mkdirs()返回的也是这个
    - 示例：
      - `File f = new File("c\\d\\e"); syso(f.mkdirs());//创建多层文件夹。而使用f.mkdir()返回false (指没有c\\d文件夹时)`
      - mac系统：路径是另一个方向的斜杠 `File f = new File("c//d//e");`，两个方法的返回结果同wins系统
    - 注：mkdirs()可以覆盖mkdir()方法，即可以用mkdirs() 替代mkdir()方法
  - 创建的是文件还是文件夹，关键看使用的方法是哪个
    - 代码：`File f = new File("c.txt"); syso(f.mkdir());`    
    - 看似创建的是c.txt文件，但是调用的是mkdir的方法，因此结果是生成一个名为“c.txt”的文件夹
    - 注意：不要被new的部分迷惑，关键看调用的方法是要创建什么

- ### File的删除功能
  - `boolean delete()`:
    - 当指定的文件或文件夹存在时，删除该文件或文件夹，并返回true; 否则返回false
    - 注意：
      - 创建文件或文件夹有多个不同方法，但删除只有这一种；
      - 删除文件夹：
        - 当文件夹下没有其他文件或文件夹时，才能被删除 (系统删除的时候也是这样，先删除里面的内容，再删文件夹)
        - 也因此，delete没办法删除多层文件夹，类似`c\\d\\e`
      - 用此方法删除的文件或文件夹不走回收站，直接删除。  
    - 示例：
      - 删除文件：`File f = new File("a.txt"); syso(f.delete());//删除文件a.txt 成功返回true`
      - 删除空文件夹：`File f = new File("b"); syso(f.delete());//删除文件夹b 成功返回true`
      - 删除多层文件夹的里层文件夹：`File f = new File("c//d//e"); syso(f.delete());//删除位于最里层的文件夹e`

- ### File的判断功能
  - `boolean exists()`:
    - 判断文件或文件夹是否存在，存在时返回true，否则返回false
    - 示例：`File f = new File("a.txt"); syso(f.exists);//文件存在，返回true`
  - `boolean isAbsolute()`:
    - 判断File对象指向的路径是否是绝对路径，是则true，不是则false
      - 注：不管判断的路径是否存在，只看格式是否是绝对路径 
    - 示例1：`File f = new File("f.txt"); syso(f.isAbsolute);//相对路径，返回false`
    - 示例2：`File f = new File("/users/a.txt"); syso(f.isAbsolute);//绝对路径，返回true` 
  - `boolean isDirectory()`:
    - 判断File对象指向的路径是否存在且是文件夹，是返回true，不是返回false
    - 注：和isAbsolute()的区别：这里明确说明需要”存在“且”是“。
    - 示例：`File f = new File("c//d"); syso(f.isDirectory());//是文件夹，返回true`
  - `boolean isFile()`:
    - 判断File对象指向的路径是否存在且是文件，是返回true，不是返回false
    - 注：和isAbsolute()的区别：这里明确说明需要”存在“且”是“。同isDirectory()
    - 示例：`File f = new File("a.txt"); syso(f.isFile());//是文件夹，返回true`
  - `boolean isHidden()`:
    - 判断File对象指向的路径(文件或文件夹)是否有隐藏属性，是则返回true，否则返回false
    - 不同系统关于 隐藏 的具体定义不同:
      - 在 UNIX 系统上，如果文件名以句点字符 ('.') 开头，则认为该文件被隐藏。
      - 在 Windows 系统上，如果在文件系统中文件被标记为隐藏，则认为该文件被隐藏。 
    - 示例：`File f = new File("a.txt"); syso(f.isHidden());//被标记了隐藏，则为true，否则为false`

- ### File的获取功能
  - `File getAbsoluteFile()`:
    - 以File对象的形式返回当前File对象所指向的绝对路径, 等同于`new File(this.getAbsolutePath())`。
      - 相当于把路径打包为File对象返回了 
    - 方法后加句点`.`，可以调用File的若干方法 
    - 注意：不管传入对象使用的是绝对路径还是相对路径，输出的都是绝对路径
    - 示例：`File f = new File("a.txt"); syso(f.getAbsoluteFile());//Users/x...u/eclipse/eclipse-workspace/Demo/a.txt`
  - `String getAbsolutePath()`:
    - 返回File对象所指向的绝对路径
    - 方法后加句点`.`，只可以调用String的若干方法 
    - 注意：不管传入对象使用的是绝对路径还是相对路径，输出的都是绝对路径，同getAbsoluteFile();
    - 示例：`File f = new File("a.txt"); syso(f.getAbsolutePath());//Users/x...u/eclipse/eclipse-workspace/Demo/a.txt`
  - `String getParent()`和`File getParentFile()`：
    - `String getParent()`:
      - 返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回 null。
    - `File getParentFile()`:
      - 返回此抽象路径名父目录的抽象路径名；如果此路径名没有指定父目录，则返回 null。
    - Patent需要提前指定，否则为null
    - 注意：当父路径不存在，但定义过时，也会返回定义的父路径
    - 代码示例：
    ```java
	import java.io.File;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException {
			//先创建父路径，后求父路径
			File parent = new File("b//c");
			File f = new File(parent, "f.txt");
			if(!parent.exists()) {
				parent.mkdirs();//不知道是几层路径，直接用这个方法
			}
			System.out.println(f.createNewFile());//true
			System.out.println(f.getParent());//b/c
			System.out.println(f.getParentFile());//b/c

			//父路径不存在时：
			File f2 = new File(new File("d//e"), "f2.txt");
			System.out.println(f2.getParent());//d/e
			System.out.println(f2.getParentFile());//d/e
		}
	}    
    ```
  - `String getName()`:
    - 获取文件或文件夹的名称
    - 示例1：`File f = new File("b//c//a.txt"); syso(f.getName());//a.txt`
    - 示例2：`File f = new File("b//c"); syso(f.getName());//c`
  - `String getPath()`:
    - 返回创建File对象时所给的路径
      - 即创建时是绝对路径则返回绝对，是相对路径则返回相对，是文件夹则返回文件夹名 
    - 示例：`File f = new File("b//c"); syso(f.getPath());//b/c`  
  - `long lastModified()`:
    - 以毫秒值的形式返回最后修改时间，与右键查看文件属性所得的最后修改时间一致
    - 代码示例：
    ```java
	import java.io.File;
	import java.io.IOException;
	import java.sql.Date;

	public class FileDemo {
		public static void main(String[] args) throws IOException {
			File f = new File("a.txt");
			System.out.println(f.lastModified());//1653365294140

			Date d = new Date(1653365294140L);//Date的有参构造：输入long类型数据，加L
			System.out.println(d.toLocaleString());//2022年5月24日 下午12:08:14，参考a.txt文件可知这个时间正是最后修改时间
		}
	}    
    ```
  - `long length()`:
    - 返回文件的字节数，与右键查看文件属性所得的文件byte大小一致 
      - 不存在的文件或文件夹的大小返回：0 
    - 注意：只能查看文件的字节数，用此方法查看文件夹为0
      - 此条：mac系统并不是，文件夹也会返回2的N次幂大小，即使是空文件夹也会返回
    - 示例1：`File f = new File("a.txt"); syso(f.length());//查看属性是13 bytes，输出为13`
    - 示例2：`File f = new File("c//d//a.txt"); syso(f.length())//长路径名返回的也是最里层的文件或文件名的大小：13`
  - `String[] list()`
    - 返回当前路径下所有的文件和文件夹的名称
    - 注意：只有指向文件夹的File对象才可以调用此方法，文件调用返回空指针异常。
    - 示例：
    ```java
	public class FileDemo {
		public static void main(String[] args) throws IOException {
			File f = new File("b");
			String [] s = f.list();
			System.out.println(s);//[Ljava.lang.String;@d716361
			for(int i = 0; i<s.length; i++) {
				System.out.println(s[i]);//输出f.txt和c, 分别为b目录下的两个文件和文件夹
			}	
		}
	}    
    ```
  - `File[] listFiles()`:
    - 以File的形式返回当前路径下所有的文件和文件夹的绝对路径
    - 注：同样，只有指向文件夹的File对象才可以调用此方法，文件调用返回空指针异常。
    - 与list()方法的区别：返回值类型不同，返回值为File()类型，可以调用File相关方法
    - 示例：`File f = new File("b"); File[] files = f.listFiles();`
  - `static File[] listRoots()`:
    - 列出可用的文件系统根，即返回所有盘符
    - 静态：可以直接用类名调用`File.listRoots();`
    - 注意：
      - Windows系统：一般返回几个盘符目录 `C:\\` and `D:\\`
      - mac系统：一般返回`/` 
    - 示例：
    ```java
	File[] roots = File.listRoots();
	for (File root : roots) {
		System.out.println(root);
	}    
    ```

- ### File的修改名字功能
  - `boolean renameTo(File dest)`:
    - 修改文件的名字
    - 有两个参数，因此需要至少两个File
    - 注意：不能修改为重名的文件
    - 示例：
    ```java
	File f = new File("a.txt");
	File f2 = new File("m.txt");
	System.out.println(f.renameTo(f2));//true
    ```	

- ### File的方法应用
  - 题目1：
    - 输出指定目录下的所有Java文件名 (包含子目录) 
  - 思路： 
    - 先考虑不包含子目录的所有Java文件，之后考虑通过递归处理子目录下的文件判断
    - listFile()获取所有文件和文件夹，遍历并判断是否是以".java"结尾的Java文件
    - 之后处理一些细节，完善逻辑，增加鲁棒性等，详见代码注释
  - 注意：包名中的句点 `.` 分隔符也是文件夹分级分隔符，路径中用斜杠分割
  - 代码示例：
    ```java
	import java.io.File;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException {
			File f = new File("src//test//StudentArray");
			method(f);		
		}
		public static void method(File file) {
			if(file.isDirectory()) {//如果传入的是文件而不是文件名，程序也不会异常抛出终止，增加健壮性
				File[] files = file.listFiles();//以File的形式返回当前路径下所有的文件和文件夹的绝对路径
				for (File f : files) {//遍历并判断
					if(f.isFile()) {
						if(f.getName().endsWith(".java")) {//获取字符串并判断是否是Java文件
							System.out.println(f.getName());//如果符合，输出
						}
					}else {//不是文件，就是文件夹，或者加个if判断
						method(f);//如果是文件夹，递归调用method方法，以获取子目录下的Java文件
					}
				}
			}
		}
	}    
    ```
  - 题目2：
    - 删除指定的目录（包含子目录）
  - 思路：
    - 先删除所有的子文件和子文件夹，然后删除自己
    - 删除子文件和子文件夹：先获取listFile(), 之后遍历，判断
      - 如果是文件，直接删除；
      - 如果是文件夹，递归调用method()方法，继续查看是否有文件和子目录 
    - 删除自己：简单，直接delete()即可
  - 注意：不要随意删文件!!!
  - 代码示例:
  ```java
	import java.io.File;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException {
			File f = new File("b");
			System.out.println(f.exists());
			method(f);		
		}
		public static void method(File file) {
			if(file.isDirectory()) {
				//干掉自己的所有子文件和子目录
				//先获取所有子文件和子目录
				File[] files = file.listFiles();
				for (File f: files) {
					if(f.isFile()) {//判断是否是文件
						System.out.println(f.getName());//可视化此删除操作,非必要
						f.delete();
					}else if(f.isDirectory()) {//如果是文件夹，递归调用
						method(f);
					}
				}		
				//干掉自己这个目录
				file.delete();
			}
		}
	}  
  ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## IO流分类
- ### 根据流向分：
  - 输入流：
    - 读取数据
    - FileReader -- 父类Reader 
  - 输出流：
    - 写出数据
    - FileWriter -- 父类Writer 

- ### 根据数据类型分：
  - 字节流：
    - 字节输入流：
      - 读取数据：Inputstream 
    - 字节输出流： 
      - 写出数据：OutputStream 
      - 注意：字符流直接写入文件，不存缓冲区，因此可以不flush()
  - 字符流： 
    - 字符输入流：
      - 读取数据：Reader 
    - 字符输出流： 
      - 写出数据：Writer 
  - 区别：
    - 比如汉字，如果按字节读取，会很慢，需要多次才能读一个，这时就需要字符流
    - 但是有些数据就必须按字节读取，比如读取图片数据等
    - 综上：字符流能做的字节流都能做，但是字节流能做的字符流不一定能做。 

- ### 字节流对象
  - 字节输入流FileInputStream的构造方法：
    - 两种：`FileInputStream(File file)`和`FileInputStream(String name)`  
    - `FileInputStream(String name)`的底层：
      - `this(name != null ? new File(name) : null);`: 同File构造方法，先判断路径下文件是否存在，不存在则先创建File()对象
  - 题目：使用字节流复制文本文件
    - 思路:
      - 创建字节输入/输出流对象；
      - 两种读写方法：1. 一次读写一个字节；2. 一次读写一个字节数组；
      - 释放资源。 
    - 代码示例：
    ```java
	import java.io.File;
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//复制测试.png
			//创建字节流对象
			FileInputStream fis = new FileInputStream("Student.java");
			FileOutputStream fos = new FileOutputStream("c//Student_copy.java");

			//一次读取一个字节
			/*
			int by;
			while((by = fis.read()) != -1) {
				fos.write(by);
			}*/

			//一次复制一个字节数组
			int len;//用于存储读到的字符个数
			byte[] bys = new byte[1024];
			while((len = fis.read(bys)) != -1) {
				fos.write(bys, 0, len);
			}

			//释放资源
			fis.close();
			fos.close();

			System.out.println(new File("c//Student_copy.java").exists());//true	
		}
	}    
    ```
- ### 分别用字符流和字节流复制图片文件
  - 字符类复制：
    - 复制文件成功，但是会打不开，字符流复制图像文件的过程中丢失了部分字节导致图像文件打不开了
    - 代码示例：
    ```java
	import java.io.File;
	import java.io.FileReader;
	import java.io.FileWriter;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException {
			//复制测试.png
			//创建字符流对象
			FileReader fr = new FileReader("复制测试.png");
			FileWriter fw = new FileWriter("c//复制测试.png");

			//一次复制一个字符数组
			int len;//用于存储读到的字符个数
			char[] chs = new char[1024];
			while((len = fr.read(chs)) != -1) {
				fw.write(chs, 0, len);
				fw.flush();
			}

			//释放资源
			fw.close();
			fr.close();

			System.out.println(new File("c//复制测试.png").exists());//测试是否创建成功：true
		}
	}  
    ```
  - 字节流复制
    - 图像文件复制成功，且可以顺利打开
    - 代码示例： 
    ```java
	import java.io.File;
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.IOException;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//复制测试.png
			//创建字节流对象
			FileInputStream fis = new FileInputStream("复制测试.png");
			FileOutputStream fos = new FileOutputStream("c//复制测试.png");

			//一次复制一个字符数组
			int len;//用于存储读到的字符个数
			byte[] bys = new byte[1024];
			while((len = fis.read(bys)) != -1) {
				fos.write(bys, 0, len);
			}

			//释放资源
			fis.close();
			fos.close();

			System.out.println(new File("c//复制测试.png").exists());//true
		}
	}  
    ```
  - 小结：
    - 二进制文件只能使用字节流进行复制
      - 根据表将字节转换为字符，中间会丢失部分字节，对于二进制文件来说这种复制的文件会打不开 
      - 二进制文件：指使用Windows自带记事本打开是乱码的文件 
    - 文本文件的复制：
      - 既可以使用字符流，也可以使用字节流
    - 如果不确定使用字符流还是字节流：
      - 使用字符流 

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 输入输出流
- ### 标准输入输出流概述
  - System类的三个静态成员变量：
    - err, in, out, 重点看后两个 
    - 静态：直接用类名调用
  - 标准输入流：`public static final InputStream in`
    - 字节输入流，用来读取键盘录入的数据
    - 引用类型`InputStream`: 类似于`public static final int a;`，int是基本数据类型
    - 静态：直接用类名调用
      - `System.in;` 或赋值给特定变量`InputStream is = System.in;`
    - 常见应用：读取键盘录入的数据
      - 示例：`Scanner sc = new Scanner(System.in);`  
  - 标准输出流：`public static final PrintStream out` 
    - 字节输出流，将数据输出到命令行
    - 示例：`System.out.println();`


- ### OutputStreamWriter
  - 题目：读取指定文件，并输出到命令行
    - 数据源：指定路径下的Java文件 BufferedReader
    - 目的地：命令行 System.out 
  - 标准输出流的局限性：
    - 由于标准输出流是字节输出流，只能输出字节或者字节数组，但是读取到的是字符串时，想进行输出还需要转换成字节数组，麻烦
    - 代码示例：注意读取的是String, 写入的是字节流byte，需要转换
    ```java
	import java.io.BufferedReader;
	import java.io.FileReader;
	import java.io.IOException;
	import java.io.OutputStream;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//题目：读取指定文件，并输出到命令行
			//创建输入流对象
			BufferedReader br = new BufferedReader(new FileReader("Student.java"));
			//创建输出流对象
			OutputStream os = System.out;

			String line;//用于存储读取到的数据
			while((line = br.readLine()) != null) {//readLine()是String, 写入字节流需要转换为字节
				os.write(line.getBytes());//String换行为字节，下同
				os.write("\r\n".getBytes());
			}

			//释放资源
			os.close();
			br.close();		
		}
	}    
    ```
  - 转换流：OutputStreamWriter：
    - 要想通过标准输出流输出字符串，把标准输出流转换成一种字符输出流即可，即OutputStreamWriter  
    - OutputStreamWriter：
      - 父类Writer，子类FileWriter, 是字符流通向字节流的桥梁，会把字符输出流转换成字节输出流
      - 构造方法为传入OutputStream对象
    - 为了获得最高效率，可考虑将 OutputStreamWriter 包装到 BufferedWriter 中，以避免频繁调用转换器。例如：
      - `Writer out = new BufferedWriter(new OutputStreamWriter(System.out));//多态`
    - 改进代码示例：
    ```java
	import java.io.BufferedReader;
	import java.io.BufferedWriter;
	import java.io.FileReader;
	import java.io.IOException;
	import java.io.OutputStreamWriter;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//题目：读取指定文件，并输出到命令行
			//创建输入流对象
			BufferedReader br = new BufferedReader(new FileReader("Student.java"));
			//创建输出流对象: 转换流改进 + 缓冲流
			//OutputStream os = System.out;
			//Writer w = new OutputStreamWriter(System.in);
			BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

			String line;//用于存储读取到的数据
			while((line = br.readLine()) != null) {//转换流改进
				bw.write(line);
				bw.newLine();
			}

			//释放资源
			bw.close();
			br.close();		
		}
	}    
    ```

- ### InputStreamReader
  - 题目：读取键盘录入的数据，并输出到指定路径的文件中
    - 数据源：读取键盘录入的数据 System.in
    - 目的地：指定路径的文件中 FileWriter 
  - 标准输入流的局限性：
    - 标准输入流是字节输入流，写入需要的是字符输出流(FileWriter只能输入String或字符数组)，这中间需要转换，麻烦
    - 代码示例：
    ```java
	import java.io.FileWriter;
	import java.io.IOException;
	import java.io.InputStream;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//题目：读取键盘录入的数据，并输出到指定路径的文件中
			//创建输入流对象
			InputStream is = System.in;
			//创建输出流对象
			FileWriter fw = new FileWriter("a.txt");

			//读写数据
			byte[] bys = new byte[1024];
			int len;
			while((len = is.read(bys)) != -1) {
				fw.write(new String(bys,0,len));//write需要传入String或字符数组，先把byte[]转为String
				fw.flush();
			}

			//释放资源
			fw.close();
			is.close();		
		}
	}    
    ```
  - 转换流：InputStreamReader
    - 需要把字节输入流转换成字符输入流，InputStreamReader
    - OutputStreamWriter：
      - 父类Reader，子类FileReader, 是字节流通向字符流的桥梁, 会把字节输入流转换成字符输入流
      - 构造方法为传入InputStream对象
    - 为了达到最高效率，可要考虑在 BufferedReader 内包装 InputStreamReader。例如：
      - `BufferedReader in = new BufferedReader(new InputStreamReader(System.in));`
    - 改进的代码示例：
    ```java
	import java.io.FileWriter;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.Reader;

	public class FileDemo {
		public static void main(String[] args) throws IOException{
			//题目：读取键盘录入的数据，并输出到指定路径的文件中
			//创建输入流对象
			//InputStream is = System.in;
			Reader r = new InputStreamReader(System.in);//使用转换流
			//创建输出流对象
			FileWriter fw = new FileWriter("a.txt");

			//读写数据
			char[] chs = new char[1024];//修改为char数据
			int len;
			while((len = r.read(chs)) != -1) {
				fw.write(chs,0,len);//直接读取不需要转换了
				fw.flush();
			}

			//释放资源
			fw.close();
			r.close();		
		}
	}    
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 打印流
- ### 打印流概述：
  - 打印流只有输出流：
    - 分为 字符打印流PrintWriter 和字节打印流PrintStream  
  - PrintWriter:
    - 父类：Writer 
    - 向文本输出流打印对象的格式化表示形式。此类实现在 PrintStream 中的所有 print 方法 
    - `println()`: 可以自动换行，不受不同系统的换行符的限制
    - 不能输出字节，可以输出其他任意类型
    - 通过某些配置，可以实现自动刷新 （只有在调用 println、printf 或 format 的其中一个方法时才可能完成此操作）
    - 也是包装类，不具备写出功能
    - 此类中的方法不会抛出 I/O 异常，尽管其某些构造方法可能抛出异常
    - 也可以把字节输出流转换成字符输出流
  - PrintStream
    - 父类：FilterOutputStream; 父类的父类：OutputStream
    - PrintStream 打印的所有字符都使用平台的默认字符编码转换为字节
    - PrintStream 为其他输出流添加了功能，使它们能够方便地打印各种数据值表示形式
  - 代码示例：
	```java
	import java.io.IOException;
	import java.io.PrintWriter;

		public class PrintWriterDemo {
		public static void main(String[] args) throws IOException {
			//创建打印流对象
			PrintWriter pw = new PrintWriter("b.txt");

			//写出数据
			pw.write("hello world ");
			pw.write("java");

			//释放资源
			pw.close();
		}
	}  
  	```

- ### 打印流特有功能
  - 自动换行
    - 使用PrintWriter的方法println()实现自动换行
    - 代码示例：
    ```java
	//创建打印流对象
	PrintWriter pw = new PrintWriter("b.txt");
	//写出数据
	pw.println("hello world ");
	pw.println("java");
	//释放资源
	pw.close();    
    ```
  - 自动刷新
    - 构造函数部分：`PrintWriter(Writer out, boolean autoFlush)` 
      - autoFlush传入是否自动刷新的boolean类型参数
      - 注意前半部分传入的是Writer类型 
      - 另有：`PrintWriter(OutputStream out, boolean autoFlush)`
      - 只有在调用 println、printf 或 format 的其中一个方法时才进行自动刷新
    - 注意：
      - 创建FileWriter的对象时传入的boolean参数：是否追加
      - 创建打印流对象时传入的boolean参数：是否自动刷新 
    - 代码示例：
    ```java
	import java.io.FileWriter;
	import java.io.IOException;
	import java.io.PrintWriter;

	public class PrintWriterDemo {
		public static void main(String[] args) throws IOException {
			//创建打印流对象
			PrintWriter pw = new PrintWriter(new FileWriter("b.txt"), true);

			//写出数据
			pw.println("hello world ");
			pw.println("java");

			//释放资源: 注释掉以后仍然可以刷新到文件中
			//pw.close();
		}
	}        
    ```


- ### 使用打印流复制文本文件
  - 数据源：Student.java BufferedReader
  - 目的地：c//d//Student.java PrintWriter
  - 打印流的优势：
    - 省了两个步骤：换行和刷新，正是打印流的特有功能 
  - 代码示例：
    ```java
	import java.io.BufferedReader;
	import java.io.FileReader;
	import java.io.FileWriter;
	import java.io.IOException;
	import java.io.PrintWriter;

	public class PrintWriterDemo {
		public static void main(String[] args) throws IOException {
			//创建输入流对象
			BufferedReader br = new BufferedReader(new FileReader("Student.java"));
			//创建输出流对象
			PrintWriter pw = new PrintWriter(new FileWriter("c//d//Student.java"), true);//开启自动刷新

			String line;//用于存储读取到的每行数据
			while((line = br.readLine()) != null) {
				pw.println(line);//省去换行和刷新
			}
			//释放资源
			pw.close();
			br.close();
		}
	}    
    ```

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 对象操作流
- ### 对象操作流概述
  - 对象操作流：可以用于读写任意类型的对象 
  - ObjectOutputStream:
    - writeObject
    - ObjectOutputStream(OutputStream out)
  - ObjectInputStream:
    - readObject
    - ObjectInputStream(InputStream in)
  - 注意：
    - 使用对象输出流写出对象，只能使用对象输入流来读取对象
    - 只能支持java.io.Serializable接口的对象写入流中  

- ### 使用对象操作流读写数据
  - 使用对象输出流写数据
    - 步骤：
      - 预备一个Student.java代码 
      - 创建对象输出流对象 
      - 创建学生对象
      - 写出学生对象
      - 释放资源
    - 注意点：
      - Student.java: 为了输出需要重写toString方法；针对序列化异常需要实现此异常接口，并重写方法
        - PS：虽然序列化异常的接口是空的，不需要额外重写什么方法
      - 打开a.txt发现乱码多：
        - 因为是需要对象输入流去读取的，不是人去读取  
    - 代码示例：
    ```java
	//Student.java
	public class Student implements Serializable{...}
    ```
    
    ```java
    	//bjectStreamDemo.java
	import java.io.FileOutputStream;
	import java.io.IOException;
	import java.io.ObjectOutputStream;

	public class ObjectStreamDemo {
		public static void main(String[] args) throws IOException {
			//创建对象输出流的对象
			ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("a.txt"));

			//创建学生对象
			Student s = new Student("zhangsan",18);
			Student s2 = new Student("lisi",19);
			//写出学生对象
			oos.writeObject(s);
			oos.writeObject(s2);

			//释放资源
			oos.close();
		}
	}    
    ```
  - 使用对象输入流读数据
    - 步骤：
      - 创建对象输入流的对象
      - 读取对象
      - 释放资源 
    - 注意点：
      - 如果上一步写入的文件不太对，例如第一次运行时莫名其妙跑序列化异常，可以重新生成一下a.txt文件
      - 首次遇到 EOFException 异常，用try-catch处理
    - 代码示例：
    ```java
	public static void main(String[] args) throws IOException, ClassNotFoundException {
			//创建对象输入流的对象
			ObjectInputStream ois = new ObjectInputStream(new FileInputStream("a.txt"));

			//读取对象
			try {
				while(true) {
					Object obj = ois.readObject();
					System.out.println(obj);
				}
			}catch(EOFException e) {
				System.out.println("读到文件末尾了");
			}

			//释放资源
			ois.close();
			/*
			 * Student [name=zhangsan, age=18]
			   Student [name=lisi, age=19]
			   读到文件末尾了
			 * */
		}    
    ```
  - 遇到的异常： 
    - `Exception in thread "main" java.io.NotSerializableException: test.demo.Student`
      - NotSerializableException: 当实例需要具有序列化接口时，抛出此异常。序列化运行时或实例的类会抛出此异常。参数应该为类的名称。
      - ObjectOutputStream: 只能将支持 java.io.Serializable 接口的对象(Student.java)写入流中
      - Serializable: 
        - 源码：`public interface Serializable {}`
        - 序列化，是一个标识窗口，只能起标识作用，没有方法；
        - 当一个类的对象需要IO流进行读写时，这个类必须实现该接口
    - `Exception in thread "main" java.io.EOFException`
      - 当输入过程中意外到达文件或流的末尾时，抛出此异常：手动循环到末尾时会直接抛出异常
      - 不能解决的异常，需要try-catch来处理
      - 其他许多输入操作返回一个特殊值表示到达流的末尾，而不是抛出异常：可以作为循环终止的判定条件
  - 这里涉及到的序列化与反序列化问题
    - 参考：[java对象的序列化和反序列化详细解释](https://blog.csdn.net/qq_43842093/article/details/118763937)
    - 代码示例：
    ```java
	import java.io.*;

	public class ObjectStreamTest {
		public static void main(String[] args) throws IOException, ClassNotFoundException {
		ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(new File("b.txt")));
		oos.writeObject(new Student("d",1));//序列化Student对象,写入文件
		ObjectInputStream ois = new ObjectInputStream(new FileInputStream(new File("b.txt")));
	       /* System.out.println(ois.readObject());*/
		Student stu = (Student) (ois.readObject());//将Student对象加载到Java程序中,反序列化
		System.out.println(stu);
		ois.close();
		oos.close();
	    }
	}    
    ```

- ### 解决对象输入流读取对象异常的问题
  - 针对`EOFException 异常`, 用try-catch解决显得有点被动
  - 考虑提前算好加入的对象个数，可以将对象存到ArrayList中，之后遍历集合即可，避免程序读着读着就挂了
    - 写入时：先添加到集合中，然后直接写入集合对象即可
    - 读取时：先向下转型转为集合类，然后遍历集合即可
  - 代码示例：
	```java
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.IOException;
	import java.io.ObjectInputStream;
	import java.io.ObjectOutputStream;
	import java.util.ArrayList;

	public class ObjectStreamDemo {
		public static void main(String[] args) throws IOException, ClassNotFoundException {
			//创建对象输出流的对象
			ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("b.txt"));
			//写入创建集合，并写入学生对象
			ArrayList<Student> list = new ArrayList<Student>(); 
			list.add(new Student("zhangsan",80));
			list.add(new Student("lisi",60));
			oos.writeObject(list);

			//创建对象输入流的对象
			ObjectInputStream ois = new ObjectInputStream(new FileInputStream("b.txt"));

			//读取对象
			Object obj = ois.readObject();
			//System.out.println(obj);//[Student [name=zhangsan, age=80], Student [name=lisi, age=60]]

			//向下转型：获取具体的子类对象
			ArrayList<Student> list2 = (ArrayList<Student>) obj;
			for (Student student : list2){
				System.out.println(student);
			}
			/*
			 * Student [name=zhangsan, age=80]
			 * Student [name=lisi, age=60]
			 * */

			//释放资源
			oos.close();
			ois.close();
		}
	}  
	```

- ### 序列化中的serialVersionUID号
  - 参考：[java对象的序列化和反序列化详细解释](https://blog.csdn.net/qq_43842093/article/details/118763937)
  - serialVersionUID是序列化前后的唯一标识符
    - 中间发生了变化会导致对不上暗号，造成反序列化失败 
  - 默认如果没有人为显式定义过serialVersionUID，那编译器会为它自动声明一个
    - 例如根据该类的各方面信息自动地为它生成一个默认的serialVersionUID
    - 当序列化前后对类进行了修改，如增删了成员变量，会导致默认序列号的变化，导致对不上暗号
  - 为了serialVersionUID的确定性，凡是implements Serializable的类，建议人为显式地为它声明一个serialVersionUID明确值
    - 对类加实现`implements Serializable`之后eclipse会产生黄色感叹号，可以生成序列号
    - 两种，一种是默认序列号，一种是生成一个序列号，建议用生成序列号
      - 默认：`private static final long serialVersionUID = 1L;` 
      - 生成：`private static final long serialVersionUID = 7578031297319648676L;`

<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## Properties
- ### Properties概述
  - 集合：
    - Collections: 单列集合
    - Map: 双列集合 
    - Properties：实现了Map集合
  - Properties：可以与IO流结合使用
  - Properties：实现了Map接口，父类是Hashtable
    - Hashtable小番外：
      - t应该大写，误写为小写了，但是版本太高了，将错就错使用小写沿用至今...
    - Hashtable和HashMap:
      - Hashtable是同步的，安全性高，效率低；
      - HashMap是非同步的，安全性低，效率高
  - Properties类：属性列表
    - 表示了一个持久的属性集。(不是临时写入，程序结束就消失那种，而是较持久地写入了文件或什么中)
    - Properties 可保存在流中或从流中加载。
    - 属性列表中每个键及其对应值都是一个字符串。
  
- ### Properties的构造方法和简单应用
  - Properties的构造方法：
    - Properties() 和 Properties(Properties defaults) 
    - 一般用空构造即可
  - 简单应用：创建并遍历
    - 步骤：
      - 创建属性列表对象
      - 添加映射关系
      - 遍历属性列表
    - 注：Properties也有相关的特有方法，不过用Map继承的方法也足够用了
    - 代码示例：
    ```java
	import java.util.Map;
	import java.util.Properties;
	import java.util.Set;

	public class PropertiesDemo {
		public static void main(String[] args) {
			//创建属性列表对象
			Properties prop = new Properties();

		    //添加映射关系: 使用Map的赋值方法
			prop.put("ID001", "zhangsan");
			prop.put("ID002", "lisi");
			prop.put("ID003", "wangwu");

			//遍历属性列表
			//方法1：获取所有的key, 通过key获取value
			Set<Object> keys = prop.keySet();//注意：Properties是String, 但现在使用Set的方法，泛型需要是Object类，下同
			for (Object key : keys) {//同理，泛型需要是Object类
				Object value = prop.get(key);
				System.out.println(key + "---" + value);
			}
			//方法2：获取所有的映射关系对象
			Set<Map.Entry<Object, Object>> entrys = prop.entrySet();
			for (Map.Entry<Object, Object> entry : entrys) {
				Object key = entry.getKey();
				Object value = entry.getValue();
				System.out.println(key + "---" + value);
			}
		}
	}    
    ```

- ### Properties与IO流结合的功能
  -  



<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



## 编码表
- ### 编码表概述


- ### Java中字符串的编码





- ### 字符流中的编码


<!--GFM-TOC -->
* ### [返回目录](#目录)
<!--GFM-TOC -->



### END
