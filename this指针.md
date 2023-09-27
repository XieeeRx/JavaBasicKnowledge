# this关键字

### this关键字有什么作用？

首先我们先来看个`Student`类
```Java{.line-numbers}
public class Student{
    // 全局变量name
    private String name;
    // 全局变量name
    public String getName(){
        return name;
    }
    // 局部变量name
    public void setName(String name){
        this.name = name;
    }
}
```

可以看到这里在第3行声明全局变量`name`，而后在第9行声明了局部变量`name`。两个变量都是同名，但实际上不相同。**如何区分这两个变量呢？那就是用this关键字了。`this.name`这里指代的是全局变量`name`。在等号=的右边是局部变量`name`。** 这里是将局部变量赋给了全局变量。OK我们可以总结如下：

1. **this关键字修饰的变量用于指代全局变量（也叫成员变量）**
 - 方法的形参如果与全局变量同名，不带this修饰的变量是形参，而不是全局变量。
 - 方法的形参没有与全局变量同名，不带this修饰的变量指的就是成员变量。

2. **什么时候使用this呢？**
 - 解决局部变量隐藏全局变量的时候可用。

3. **this：代表所在类的对象引用**
 - 方法被哪个对象调用，this就代表哪个对象。