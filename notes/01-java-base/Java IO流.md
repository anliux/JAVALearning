# Java IO流


### 目录

<!--GFM-TOC -->
* [IO流基础](#IO流基础): 
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
- ### 字符缓冲流
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
  - 用缓冲流复制文件
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



## IO流应用
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

- ### 集合数据的读取
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

- ### 判断功能
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

- ### 获取功能
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

- ### 修改名字功能
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
  - 题目：
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
