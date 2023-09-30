# final关键字

### 什么是final关键字？
是状态修饰符的一种，一种是final(最终态)，一种是static(静态)。
final关键字是最终的意思，可以修饰成员方法、成员变量、类。可以变相理解为二叉树中的最终子结点。一旦被final定义，则不能再更改。

- **修饰成员方法：**
```Java{.line-numbers}
public class Fu{

    public final void method(){ // 成员方法加了final关键字
        System.out.printl("Fu method");
    }
}

public class Son extends Fu{

    @Override
    public void method(){ // 这一行会报错，显示子类不能继承父类 
        System.out.printl("Zi method");
    }
}
```

- **修饰成员变量：**
```Java{.line-numbers}
public class Son extends Fu{

    public final int age = 20; // age由变量变成常量，值不可再变

    public void show(){
        age = 100;  // 因此这一行会报错
        System.out.println(age);
    }
}
```

- **修饰类：**
```Java{.line-numbers}
public final class Fu{ 
// 如果一个类被final修饰，就不能做父类，被子类继承
    public final void method(){
        System.out.printl("Fu method");
    }
}

public class Son extends Fu{ // 这一行会报错

    public void method(){
        System.out.printl("Zi method");
    }
}
```

### 那final修饰的特点是啥？
- 修饰方法：表明该方法是最终方法，**不能被重写**
- 修饰变量：表明该变量是常量，**不能再次被赋值**
- 修饰类：表明该类是最终类，**不能被继承**

### 深层次理解
- 变量是基本类型：final修饰指的是基本类型的**数据值**不能改变
- 变量是引用类型：final修饰指的是引用类型的**地址值**不能改变，但是地址里面的内容是可以发生改变的