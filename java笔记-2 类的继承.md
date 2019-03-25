基类代码：
```java
public Class Base {
    public static int s;

    private int a;

    static {
        System.out.println("基类静态代码块 s:" + s);
        s = 1;
    }

    {
        System.out.println("基类实例代码块 a:" + a);
        a = 1;
    }

    public Base(){
        System.out.println("基类构造函数 a:" + a);
        a = 2;
    }

}
```
子类代码：
```java
public Class Child extends Base{
    public static int s;

    private int a;

    static {
        System.out.println("子类静态代码块 s:" + s);
        s = 10;
    }

    {
        System.out.println("子类实例代码块 a:" + a);
        a = 10;
    }

    public Child(){
        System.out.println("子类构造函数 a:" + a);
        a = 20;
    }

}
```
测试代码：
```java
public static void main(String[] args){
    Child child = new Child();
}
```
##当运行主函数中的代码后会发生什么？
1、首先，程序会将当前类的信息加载进内存。（类加载器）
程序会在内存方法区中开辟一段空间存储类信息。

2、接着，程序会为类中的静态成员变量赋初始默认值（数值型 -- 0 ，对象类型（自定义类型） -- null , char -- ‘\u0000’， 布尔类型 -- true）

3、然后会查找这个类是否有父类，如果有则将父类也加载进内存，在加载父类信息的同时，也会查找这个类是否存在父类，如果存在，则将父类加载进内存。

4、设置父子类关系。

5、执行类初始化代码
>  - 定义静态变量时的初始化赋值语句。
>  - 先执行父类静态代码块，然后执行子类静态代码块。

6、类加载完成后，开始创建对象。
 *  分配内存：将引用对象存储在**栈**中，将对象实际引用的内容存放在**堆**中。

 *  执行所有实例变量初始化赋值语句。

 *  执行实例初始化代码。
 >  执行顺序：
    执行父类初始化代码块，执行父类构造函数。
    执行子类初始化代码，执行子类构造函数