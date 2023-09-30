# static关键字

### 什么是static关键字？
是状态修饰符的一种，一种是final(最终态)，一种是static(静态)。
static关键字是静态的意思，可以修饰成员方法、成员变量。

首先我们来看一下代码：
```Java{.line-numbers} 
+++++ 学生类 +++++
public class Student{

    public String name; // 姓名
    public int age; // 年龄
    public String university; // 学校

    public void show(){
        System.out.println(name + "," + age + "," + university);
    }
}
```
```Java{.line-numbers} 
+++++ 学生测试类 +++++
public class StaticDemo{

    public static void main(String[] args){
        Student s1 = new Student();
        s1.name = "张三";
        s1.age = 21;
        s1.university = "哥谭大学";
        s1.show();

        Student s2 = new Student();
        s2.name = "李四";
        s2.age = 22;
        s2.university = "哥谭大学";
        s2.show();
    }
}
```
此时我们运行**学生测试类**，会发现输出：
> 张三，21，哥谭大学
> 李四，22，哥谭大学

但是我们这样写就太麻烦了，每次新建一个对象的时候都要定义对象相关的值，如果多个对象的值有部分是相同的呢？比如同学们都是来自哥谭的人才，每次新增一个同学我就要写一行`sx.university = "哥谭大学"`，显然很麻烦。因此我们在**学生类**中直接使用static。
```Java{.line-numbers} 
+++++ 学生类 +++++
public class Student{

    public String name; // 姓名
    public int age; // 年龄
    public static String university; // 学校 加了static关键字

    public void show(){
        System.out.println(name + "," + age + "," + university);
    }
}
```
然后在**学生测试类**修改如下：
```Java{.line-numbers} 
+++++ 学生测试类 +++++
public class StaticDemo{

    public static void main(String[] args){

        // 用静态修饰的成员可以用类名访问，写起来不冗杂
        Student.university = "哥谭大学";

        Student s1 = new Student();
        s1.name = "张三";
        s1.age = 21;
        // 将对象成员赋值注释掉，这里是通过对象名访问，写起来比较冗杂
        // s1.university = "哥谭大学";
        s1.show();

        Student s2 = new Student();
        s2.name = "李四";
        s2.age = 22;
        // 将对象成员赋值注释掉
        // s2.university = "哥谭大学";
        s2.show();
    }
}
```
通过运行**学生测试类**输出以下结果：
> 张三，21，哥谭大学
> 李四，22，哥谭大学

是不是对比之下简便了很多，其实就是归功于**static共用**的特性。

### 那static修饰的特点是啥？
- 被类的所有**对象共享**
  - 这也是我们判断是否使用静态关键字的条件
- 可以通过类名调用，也可以通过对象名调用
  - **推荐使用类名调用**
- 静态的成员方法只能访问静态的成员变量和静态的成员方法，非静态的成员方法能够访问非静态的成员变量和方法，也能够访问静态的成员变量和方法。