# 类的拓展

## 接口
1、接口是一种约定，它声明了它拥有哪些能力，但自身无法实现，需要其他类来实现，其他类必须遵守这个约定，否则就会出错。

2、在java中使用**interface**关键字来表示接口。接口可以定义方法和变量，   
* 声明方法：  
    1、实现接口的类必须实现这个方法；
* 声明变量：
    1、方法的修饰符可以写可以不写，如果不写则默认为**public adstract**;变量的修饰也是可写可不写，若不写则默认为**public static final**；

3、接口是可以多继承的，一个接口可以同时继承多个其他接口:
```java 
public interface Test extends Test1, Test2{
    // 内部代码省略
}
```

4、类可以同时继承类并且实现接口：

``` java 
// 需要注意的是必须先继承在实现接口
public class Test extends Test1 implements Test2 {
    // 内部代码省略
}
```

5、也可以对接口使用**instanceof**关键字，用来判断一个对象是否实现一个接口

## 抽象类
1、抽象类是指抽象的类，表示一种抽象的概念，给开发人员一组需要需要实现的功能标准。

2、抽象方法：一种只有子类知道如何实现的方法叫做抽象方法。

3、**abstract**关键字：
* 定义类：
```java 
public abstract class abstractTestClass {
    ....
}
```

* 定义方法：
``` java 
public abstract void test(){
    ....
}
```

4、抽象类的特点：
 * 继承抽象类之后，必须实现抽象类中的抽象方法，否则子类必须定义为抽象类；

 * 抽象类不能创建对象，只能通过引用来访问该类的具体子类；

 * 抽象类可以定义具体方法和实例变量；

5、与接口比较：**接口是特殊的抽象类**
* 抽象类中可以有具体方法和实例变量，而接口中只有抽象方法和常量（接口中的方法默认修饰符为 public adstract，变量为public static final）

* 抽象类可以继承并且实现接口，但接口只能继承接口

6、接口与抽象类是配合使用的，而不是替代关系，例如：List接口和AbstractList类，List接口里声明了这个接口能使用的方法，而对应的抽象类中给出了默认实现。

## 内部类
> 内部类是指在类内部创建的类。

### 特点
1、内部类可以设置为private修饰符，阻止外部的访问，提供很好的封装性。

2、内部类可以访问外部类（外部方法）的变量、参数和方法。

3、每个内部类在编译后都会生成一个独立的class文件。

4、内部类是通过在编译时在外部类中生成能访问本类私有成员的方法来使得能够访问外部类的私有成员变量。

### java中提供的内部类
> 主要有4种类型：静态内部类、成员内部类、方法内部类、匿名内部类。

**静态内部类**：
``` java 
public class Outer {
    private int a = 1;

    private static String value = "outer class value";

    public static class InnerClass {
        public void innerMethod(){
            // 可以直接调用外部类的静态成员
            System.out.println("value:" + value);
            // 不可以调用外部类的非静态成员
            // System.out.println("a value:" + a);
        }
    }

    public void test(){
        InnerClass innerClass = new InnerClass();
        innerClass.innerMethod();
    }

}
```
1、静态内部类与普通类相同，只是多了static关键字。所以静态内部类是可以创建成员变量和方法、静态方法和变量、构造方法。

2、静态内部类不可以访问外部类的成员变量和方法，只能访问外部类的静态成员和方法。公有直接访问，私有通过外部类提供访问方法访问。

3、外部类可以直接调用内部类，就像上面代码中test()方法中写的那样。

4、静态内部类的访问范围是根据访问修饰来决定的，public最广所有类都可以访问，而private则是只能在关联的外部类中访问。

**成员内部类**
``` java 
public class Outer {
    private int a = 100;

    private void test(){
        System.out.println("outer class private method");
    }

    public class InnerClass {
        public void show(){
            System.out.println("a value:" + a);
            // 没有与外部类重名的方法时的写法
            test();
            // 遇到与外部类重名的方法时的写法
            Outer.this.test();
        }
    }

    public testInnerClass() {
        Outer outer = new Outer();
        Outer.InnerClass inner = outer.new InnerClass();
        inner.show();
    }

}
```

1、成员内部类可以访问外部类的静态变量和方法，外部类的实例变量和方法。

2、成员内部类和静态内部类一样，都可以在外部类访问，只不过成员内部类是要通过外部类对象来创建对象，然后才进行访问。

3、成员内部类访问外部类私有实例变量时，是通过外部类创建访问方法的方式来实现的。

4、静态内部类的访问范围是根据访问修饰来决定的，public最广所有类都可以访问，而private则是只能在关联的外部类中访问。

**方法内部类**
``` java 
public class Outer {
    private int a = 100;

    public void test(final int params) {
        final String str = "method params";
        class Inner{
            public void innerMethod() {
                System.out.
            }
        }
    }
}
```

