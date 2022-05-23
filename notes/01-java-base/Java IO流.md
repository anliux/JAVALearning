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
  - 这里选取关键内容整理保留
 
- ### IO流概述和分类
  - 引入：类似ArrayList的集合类，存储数据的有效范围仅为该代码运行期间，在内存中临时存储，再次打开时输入的数据已丢失。而IO流技术可以永久存储。
  - 概述：IO流用来处理设备之间的传输问题，包括文件复制、上传/下载文件等。
  - IO流分类：
    - 输出流 (写数据)：FileWriter
    - 输入流 (读数据)：FileReader
  - 图示：
  ![IO流的作用及分类](https://raw.githubusercontent.com/anliux/JAVALearning/master/images/01-java-base/io/IO%E6%B5%81%E7%9A%84%E4%BD%9C%E7%94%A8%E5%8F%8A%E5%88%86%E7%B1%BB.bmp)

- ### FileWriter概述  
  - 输出流写数据，通过阅读API学习
  - java.io包下：因此需要导包 `import java.io.FileWriter;`
  - 输出流写数据的步骤：
    - 1. 创建输出流对象；<创建文件时需要调用系统资源>
    - 2. 调用输出流对象的写数据的方法，并flush刷新缓冲区；
    - 3. 释放资源。<即通知系统释放和该文件相关的资源，因为创建输出流对象是调用系统资源创建的>

- ### FileWriter的构造方法和成员方法
  - 构造方法：
    - `FileWriter(String fileName)`: 传递一个文件名称 <或路径+文件名>
  - 成员方法：
    - `void write(String str)`: 写入数据
    - `void flush()`: 刷新缓冲区
      - 数据不会直接写到文件，而是写到了内存缓冲区，flush刷新后显示 
    - `void close()`: 释放调用的系统资源
  - 创建输出流对象做了哪些事情：`FileWriter fw = new FileWriter("d:\\a.txt")`
    - 1. 调用系统资源创建了一个文件；(没有路径所指文件时会自动创建)
    - 2. 创建输出流对象；
    - 3. 把输出流对象指向该文件。
  - 写数据方法的路径问题：
    - 相对路径：相对当前项目而言，在项目的根目录下(注意是"项目")
      - 示例：`FileWriter fw = new FileWriter("a.txt")//不加盘符的文件名;` 
    - eclipse中显示相对路径的文件：
      - 选中项目project -- 右键 -- refresh，即可在项目下出现相应的文件(a.txt)
    - 绝对路径：指明盘符的具体路径
      - 示例：`FileWriter fw = new FileWriter("d:\\a.txt");//加了盘符位置的文件名`
      - 注意：mac中路径为'/users/xx/...'
  - close()和flush()方法：
    - flush(): 刷新缓冲区；之后流对象还可以继续使用。
    - close(): 先刷新缓冲区，后通知系统释放资源；之后流对象不可以再使用了。
      - close()做两步，因此即使write()之后没有flush(), close()的时候也会自动刷新。
      - 写入内容较少时，可以省略flush().
  - 代码示例：(注意导包和导抛出异常)
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
    - 上一次的读取会被下一次替换，当下一次读取不够全部提黄上一次读取时，上一次的读取会遗留在存储字符数组中
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
	  
- ### 字符缓冲流
  - BufferedWriter:
    - 将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组、字符串的高效写入
    - 代码示例：`BufferedWriter bw = new BufferedWriter(new FileWriter("bw.txt"));`
    - 调用使用同FileWriter()
  - BufferedReader:
    - 从字符输入流中读取文本，缓冲各个字符，从而提供单个字符、数组、行的高效读取
    - 代码示例：`BufferedReader br = new BufferedReader(new FileReader("br.txt"));`
      - 仍然分为读取单个字符和读取字符数组两种方式。
  - 导包：`import java.io.BufferedWriter/BufferedReader;`
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
    - 此处涉及异常抛出注意点：当所调用的方法抛出了异常时，所调用的方法也需要抛出异常，即main方法也需要加`throws IOException`

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



##


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
