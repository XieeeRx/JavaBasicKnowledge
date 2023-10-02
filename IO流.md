# IO流

### 什么是IO流？
I/O(Input/Output)流是Java中用于**处理输入和输出**的机制。用于与外部资源（如文件、网络连接、键盘、屏幕等）进行**数据交换**的重要工具。IO流用于读取数据从外部资源到程序中（输入流）或将程序中的数据写入外部资源（输出流）。

### IO流的分类有哪些？
- 按照数据的流向
  - **输入流：读数据**
  - **输出流：写数据**
- 按照数据类型分
  - **字节流：字节输出流、字节输入流**
    - 用于处理二进制数据，类名以`InputStream`和`OutputStream`结尾，它们都是对应字节输入流和输出流的所有类的超类，其子类名称都是以其父类作为子类名的后缀。比如FileOutputStream文件输出流用于将数据写入File。
  - **字符流：字符输入流、字符输出流**
    - 用于处理文本数据，类名以`Reader`和`Writer`结尾

### 字节流的基本概念有哪些？
- <p style="font-size:20px;font-weight:bold;color:black">使用字节输出流写数据的步骤：</p>

  1. **创建字节输出流**
   - 调用系统功能创建了文件
   - 创建字节输出流对象
   - 让字节输出流对象指向文件
  2. **调用字节输出流对象的写数据方法**
  3. **释放资源**
   - 关闭此文件输出流
   - 释放与此流相关联的任何系统资源
    ```Java{.line-numbers}
    public class FileOutputStreamDemo01{
        public static void main(String[] args) throws IOException{
            // 创建字节输出流对象
            // FileOutputStream(String name)，创建文件输出流以指定的名称写入文件
            FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
            /*
                做了三件事情：
                A.调用系统功能创建了文件
                B.创建了字节输出流对象
                C.让字节输出流对象指向创建好的文件
            */

           // void write(int b)：将指定的字节写入此文件输出流
           fos.write(97);
           fos.write(57);
           fos.write(55);

           // 最后都要释放资源
           // void close(); 关闭此文件输出流并释放与此流相关联的任何系统资源
           fos.close();
        }
    }
    ```

- <p style="font-size:20px;font-weight:bold;color:black">字节流写数据的3种方式：</p>
 | 方法名 | 说明 |
 | ---- | ---- |
 |void write(int b)|将指定的字节写入此文件输出流<br>一次写一个字节数据|
 |void write(btye[] b)|将b.length字节从指定的字节数组写入此文件输出流<br>一次写一个字节数组数据|
 |void write(byte[] b, int off, int len)|将len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流<br>一次写一个字节数组的部分数据|
 > **两种构造方法：**
 > **FileOutputStream(String name):** 创建文件输出流以指定的名称写入文件
 > **FileOutputStram(File file):** 创建文件输出流以写入由指定的File对象表示的文件
 ```Java{.line-numbers}
    public class FileOutputStreamDemo02{
        public static void main(String[] args){
            // 第一种构造方法
            // FileOutputStream(String name):创建文件输出流以指定的名称写入文件
            FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
            // 以上的构造方法的底层方法其实如下：
            FileOutputStream fos = new FileOutputStream(new File("myByteStream\\fos.txt"));
            // 将一个字符串路径封装为一个File

            // 第二种构造方法
            // FileOutputStram(File file):创建文件输出流以写入由指定的File对象表示的文件
            File file = new File("myByteStream\\fos.txt");
            FileOutputStream fos2 = new FileOutputStream(file);
            // 简洁写法如下：
            FileOutputStream fos2 = new FileOutputStream(new File("myByteStream\\fos.txt"));
            // 说到底还是第一种构造方法简单一点

            // 写数据的三种方式
            // 第一种 void write(int b)将指定的字节写入此文件输出流
            fos.write(97);
            fos.write(98);
            fos.write(99);
            fos.write(100);
            fos.write(101);
            // fos.txt文件输出abcde

            // 第二种 void write(btye[] b)将b.length字节从指定的字节数组写入此文件输出流
            byte[] bys = {97, 98, 99, 100, 101};
            fos.write(bys);
            // 另一种写法，可以根据字符串得到数据
            byte[] bys = "abcde".getBytes();
            fos.write(bys);
            // fos.txt文件输出abcde

            // 第三种 void write(byte[] b, int off, int len)将len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流
            byte[] bys = "abcde".getBytes();
            fos.wirte(bys,1,3);

            // 释放资源
            fos.close();
        }
    }
 ```

- <p style="font-size:20px;font-weight:bold;color:black">字节流写数据的两种小技巧：</p>
 1. **实现字节流数据换行**
   - 写完数据后，加换行符
    - windows：\r\n
    - linux:\n
    - mac:\r
 2. **字节流数据实现追加写入**
   - 使用构造方法public FileOutputStream(String name, boolean append)
   - 创建文件输出流以指定的名称写入文件。如果第二个参数为true，则字节将写入文件的末尾而不是开头。

- <p style="font-size:20px;font-weight:bold;color:black">字节流写数据加异常处理：</p>
 **finally**：在异常处理时提供finally块来执行所有清楚操作。比如说IO流中的释放资源。特点：被finally控制的语句一定会执行，除非JVM退出。
 ```{.line-numbers}
 try{
    可能出现异常的代码;
 }catch(异常类名 变量名){
    异常的处理代码;
 }finally{
    执行所有清除操作;
 }
 ```

- <p style="font-size:20px;font-weight:bold;color:black">字节流读数据（一次读一个字节数据）：</p>
 需求：把文件中的内容读取出来在控制台输出
 **FileInputStream：**从文件系统中的文件获取输入字节
 - FileInputStream(String name):通过打开与实际文件的连接来创建一个FileInputStream，该文件由文件系统中的路径名name命名
 > 使用字节输入流读数据的步骤：
 > ① 创建字节输入流对象
 > ② 调用字节输入流对象的读数据方法
 > ③ 释放资源
 ```Java{.line-numbers}
 public class FileInputStreamDemo01{
    public static void main(String[] args) throws IOException{
        // 创建字节输入流对象
        // FileInputStream(String name)
        FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");

        // 调用字节输入流对象的读数据方法
        // int read(): 从该输入流读取一个字节的数据
        int by = fis.read();
        System.out.println(by);
        System.out.println((char)by);
        // 多读取如果达到文件的末尾，则会读出 -1
        // 使用循环
        int by;
        while((by = fis.read()) != -1){
            System.out.print((char)by);
        }

        // 释放资源
        fis.close();
    }
 }
 ```

- <p style="font-size:20px;font-weight:bold;color:black">字节流读数据（一次读一个字节数据）：</p>
 > 使用字节输入流读数据的步骤：
 > ① 创建字节输入流对象
 > ② 调用字节输入流对象的读数据方法
 > ③ 释放资源
 ```Java{.line-numbers}
 public class FileInputStreamDemo02{
    public static void main(String[] args) throws IOException{
        // 创建字节输入流对象
        FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");

        // 调用字节输入流对象的读数据方法
        // int read(byte[] b): 从该输入流读取最多b.length个字节的数据到一个字节数组
        byte[] bys = new byte[5];

        // 读取数据
        byte[] bys = new byte[1024]; // 1024及其整数倍
        int len;
        while((len = fis.read(bys)) != -1){
            System.out.print(new String(bys, 0, len));
        }

        // 释放资源
        fis.close();
    }
 }
 ```

### 案例: 复制文本文件
需求：把"E:\\itcast\\文本.txt" 复制到模块目录下的 "课本.txt"

分析：
 - 复制文本文件，其实就是把文本文件的内容从一个文件中读取出来（数据源），然后写入到另一个文件中（目的地）。
 - 数据源：E:\\itcast\\文本.txt --- 读数据 --- InputStream --- FileInputStream
 - 目的地：myByteStream\\课本.txt --- 写数据 --- OutputStream --- FileOutputStream

思路：
 - 根据数据源创建字节输入流对象
 - 根据目的地创建字节输出流对象
 - 读写数据，复制文本文件（一次读取一个字节，一次写入一个字节）
 - 释放资源

代码如下：
```Java{.line-numbers}
public class CopyTxtDemo{
    public static void main(String[] args) throws IOException{
        // 根据数据源创建字节输入流对象
        FileInputStream fis = new FileInputStream("E:\\itcast\\文本.txt");

        // 根据目的地创建字节输出流对象
        FileOutputStream fos = new FileOutputStream("myByteStream\\课本.txt");

        // 读写数据，复制文本文件（一次读取一个字节，一次写入一个字节）
        int by;
        while((by = fis.read()) != -1){
            fos.write(by);
        }

        // 释放资源
        fos.close();
        fis.close();
    }
}
```

### 案例: 复制图片
需求：把"E:\\itcast\\mn.jpg" 复制到模块目录下的 "mn.jpg"

思路：
 - 根据数据源创建字节输入流对象
 - 根据目的地创建字节输出流对象
 - 读写数据，复制图片（一次读取一个字节，一次写入一个字节）
 - 释放资源

代码如下：
```Java{.line-numbers}
public class CopyJpgDemo{
    public static void main(String[] args) throws IOException{
        // 根据数据源创建字节输入流对象
        FileInputStream fis = new FileInputStream("E:\\itcast\\mn.jpg");

        // 根据目的地创建字节输出流对象
        FileOutputStream fos = new FileOutputStream("myByteStream\\mn.jpg");

        // 读写数据，复制图片（一次读取一个字节，一次写入一个字节）
        byte[] bys = new byte[1024];
        int len;
        while((len = fis.read(bys)) != -1){
            fos.write(bys, 0, len);
        }

        // 释放资源
        fos.close();
        fis.close();
    }
}
```

### 什么是字节缓冲流？
 字节缓冲流：
 - BufferOutputStream: 该类实现缓冲输出流。通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用。
 - BufferedInputStream：创建BufferedInputStream将创建一个内部缓冲区数组。当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次很多字节。
 
 构造方法：
 - 字节缓冲输出流：BufferedOutputStream(OutputStream out)
 - 字节缓冲输入流：BufferedInputStream(InputStream in)

 **字节缓冲流仅仅提供缓冲区，而真正的读写数据还得依靠基本的字节流对象进行操作**

 ```Java{.line-numbers}
 public class BufferStreamDemo{
    public static void main(String[] args) throws IOException{
        // 字节缓冲输出流：BufferedOutputStream(OutputStream out)
        FileOutputStream fos = new FileOutputStream("myByteStream\\bos.txt");
        BufferedOutputStream bos = new BufferedOutputStream(fos);
        // 两个合并起来写法如下：
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\bos.txt"));
        // 写数据
        bos.write("hello\r\n".getBytes());
        bos.write("world\r\n".getBytes());
        // 释放资源
        bos.close();

        // 字节缓冲输入流：BufferedInputStream(InputStream in)
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("myByteStream\\bos.txt"));
        // 一次读取一个字节数据
        int by;
        while((by = bis.read()) != -1){
            System.out.print((char)by);
        }
        // 一次读取一个字节数组数据
        byte[] bys = new byte[1024];
        int len;
        while((len = bis.read(bys)) != -1){
            System.out.print(new String(bys,0,len));
        }
        // 释放资源
        bos.close();
    }
 }
 ```

### 案例: 复制视频
需求：把"E:\\itcast\\字节流复制图片.avi" 复制到模块目录下的 "字节流复制图片.avi"

思路：
 - 根据数据源创建字节输入流对象
 - 根据目的地创建字节输出流对象
 - 读写数据，复制视频
 - 释放资源

四种方式实现复制视频，并记录每种方式复制视频的时间
1. 基本字节流一次读写一个字节
2. 基本字节流一次读写一个字节数组
3. 字节缓冲流一次读写一个字节
4. 字节缓冲流一次读写一个字节数组

代码如下：
```Java{.line-numbers}
public class CopyJpgDemo{
    public static void main(String[] args) throws IOException{
        // 记录开始时间
        long startTime = System.currentTimeMillis();

        // 复制视频
        method1();
        method2();
        method3();
        method4();

        // 记录结束时间
        long endTime = System.currentTimeMillis();
        System.out.println("共耗时：" + (endTime - starttime) + "毫秒");

    }

    // 基本字节流一次读写一个字节
    public static void method1() throws IOException{
        FileInputStream fis = new FileInputStream("E:\\itcast\\字节流复制图片.avi");
        FileOutputStream fos = new FileOutputStream("myByteStream\\字节流复制图片.avi");

        int by;
        while((by = fis.read()) != -1){
            fos.write(by);
        }

        fos.close();
        fis.close();
    }

    // 基本字节流一次读写一个字节数组
    public static void method2() throws IOException{
        FileInputStream fis = new FileInputStream("E:\\itcast\\字节流复制图片.avi");
        FileOutputStream fos = new FileOutputStream("myByteStream\\字节流复制图片.avi");

        byte[] bys = new byte[1024];
        int len;
        while((len = fis.read(bys)) != -1){
            fos.write(bys, 0, len);
        }

        fos.close();
        fis.close();
    }

    // 字节缓冲流一次读写一个字节
    public static void method3() throws IOException{
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("E:\\itcast\\字节流复制图片.avi"));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\字节流复制图片.avi"));

        int by;
        while((by = bis.read()) != -1){
            bos.write(by);
        }

        bos.close();
        bis.close();
    }

    // 字节缓冲流一次读写一个字节数组
    public static void method4() throws IOException{
        BufferedInputStream bis = new BufferedInputStream(new FileInputStream("E:\\itcast\\字节流复制图片.avi"));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\字节流复制图片.avi"));

        byte[] bys = new byte[1024];
        int len;
        while((len = bis.read(bys)) != -1){
            bos.write(bys, 0, len);
        }

        bos.close();
        bis.close();
    }
}
```

### 为什么会出现字符流？
因为字节流操作中文不是特别的方便，所以Java就提供字符流
**字符流 = 字节流 + 编码表**
那用字节流复制文本文件时，文本文件也会有中文，但是没有问题，原因是最终底层操作会自动进行字节拼接成中文，如何识别是中文的呢？
**汉字在存储的时候，无论选择哪种编码存储，第一个字节都是负数**
```Java{.line-numbers}
public class FileInputStreamDemo{
    public static void main(String[] args) throws IOException{
        String s = "中国";
        // 用GBK编码格式
        byte[] bys = s.getBytes("GBK");
        // 用UTF-8编码格式
        byte[] bys = s.getBytes("UTF-8");
        System.out.println(Arrays.toString(bys));
    }
}
```
> 一个汉字存储：
> 如果用的是GBK编码，占用2个字节
> 如果是UTF-8编码，占用3个字节
> 如上代码，使用GBK打印时为[-42,-48,-71,-6],使用UTF-8打印时为[-28,-72,-83,-27,-101,-67]。

### 字符流有哪些基本概念？
字符流抽象基类
- Reader：字符输入流的抽象类
- Writer：字符输出流的抽象类

字符流中和编码解码问题相关的两个类：
- InputStreamReader：是从字节流到字符流的桥梁
- OutputStreamWriter：是从字符流到字节流的桥梁

字符流写数据的5种方式
| 方法名 | 说明 |
 | ---- | ---- |
 |void write(int c)|写一个字符|
 |void write(char[] cbuf)|写入一个字符数组|
 |void write(char[] cbuf, int off, int len)|写入字符数组的一部分|
 |void write(String str)|写一个字符串|
 |void write(String str, int off, int len)|写一个字符串的一部分|

字符流读数据的2种方式
| 方法名 | 说明 |
 | ---- | ---- |
 |int read()|一次读一个字符数据|
 |int read(char[] cbuf)|一次读一个字符数组数据|