---
id: Java的三大特性
title: day01学习
---

## 一 反馈摘要

```html
All these will be part of the blog post summary.
Even this.
```




## 二 知识概要

- 面向对象复习
- 继承
- 抽象类
- 模板设计模式

## 三 课程内容

###  01 类定义及对象的创建

#### 学习目标

能够定义类并创建对象

#### 内容讲解

#### 【1】类的定义格式

关键字：**class**

```java
修饰符 class 类名{
  成员变量
  成员方法
  构造方法
  代码块
  内部类
}
```

例如：

定义一个学生类，包含属性姓名，年龄

```java
public class Student{
  String name;
  int age;
}
```





#### 【2】创建对象

关键字：**new**

```java
类名 对象名  = new 类名(参数);
```

例如：

创建学生对象，给姓名和年龄设置值，并使用对象访问成员属性值。

```java
Student stu = new Student();
stu.name="Mike";
stu.age=18;

System.out.println(stu.name);
System.out.println(stu.age);
```



#### 内容小结

1. 类定义的关键字？

   class

2. 对象定义的关键字？

   new 



###  02 封装

#### 学习目标

- 理解关键字private
- 能够使用private对类中成员进行封装

#### 内容讲解



#### 【1】private关键字

private关键字的含义就是私有。可以用来对成员进行封装



#### 【2】封装的操作步骤

- 第一步：先把成变量使用private封装

- 第二步：提供getter、setter方法



举例：

定义一个学生类，含有属性姓名，年龄。对姓名和年龄进行封装，并提供可访问的getter、setter方法

```java
public class Demo01 {
    public static void main(String[] args) {
        Student stu = new Student();
        //借助setter方法给属性设置值
        stu.setName("前进");
        stu.setAge(16);

        //借助getter方法获取属性值
        System.out.println(stu.getName()+":"+stu.getAge());


    }
}
//定义一个学生类，含有属性姓名，年龄。对姓名和年龄进行封装，并提供可访问的getter、setter方法
class Student{
    private String name;
    private int age;

    //并提供可访问的getter、setter方法
    //name 的get方法
    public String getName(){
        return name;
    }

    //name的set方法
    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```



#### 内容小结

1. 封装使用什么关键字？

   private

2. 封装的步骤？

   1. 使用private关键字封装属性
   2. 提供getter、setter方法进行访问





###  03 构造器（Constructor）

#### 学习目标

- 能够定义并使用类的构造器

#### 内容讲解

#### 【1】构造器的定义及其作用

格式：

```java
修饰符 类名 (形参){
   给成员变量初始化值
}
```

特点：

1. 没有返回值（即使void也不用写）
2. 方法名一定是和当前类的类名一样
3. 构造方法支持重载（同名不同参）

作用：

- 结合关键字new创建对象，也可以同时给成员变量赋值。

  
  
  ```
  目前可以给成员变量赋值的四种方式：
  1.直接赋值（没有封装）
  2.通过setter方法
  3.通过构造器
  4.反射（后面学习）
  ```
  
  

#### 【2】代码实践

定义一个学生类，含有属性姓名，年龄。

1. 对姓名和年龄进行封装，并提供可访问的getter、setter方法
2. 同时提供无参构造方法，满参构造方法。

```java
package _02构造器;

public class Demo01 {
    public static void main(String[] args) {
        //无参构造方法创建对象
        Student stu1 = new Student();
        System.out.println(stu1.getName() + "::" + stu1.getAge());
        stu1.setName("钱进");
        stu1.setAge(20);
        System.out.println(stu1.getName() + "::" + stu1.getAge());

        //有参构造方法
        Student stu2 = new Student("昌老师",18);
        System.out.println(stu2.getName() + "::" + stu2.getAge());
        
    }
}

class Student {
    private String name;
    private int age;

    //定义构造器
    //无参
    public Student() {

    }

    //满参
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }


    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```



思考：使用满参构造方法创建对象有什么好处？

可以一次性给多个属性赋值



#### 内容小结

构造方法特点？

- 没有返回值
- 方法名和类名相同
- 构造方法可以重载

构造方法有什么作用？

- 创建对象并且可以初始化对象中属性的值











###  04 this关键字

#### 学习目标

- 理解this关键字的含义
- 能够使用this关键字解决局部变量和成员变量冲突问题

#### 内容讲解

#### 【1】this的含义

- this就是指当前类型的对象
- this一般出现在构造器，实例方法中
  - 如果在构造器中，this就是当前new的对象。
  - 如果出现在实例方法，this就是调用该方法的对象。



#### 【2】作用

this关键字就是为了解决局部变量和成员变量名字冲突的调用问题。

格式：

```
this.成员变量
```

例如：

```java
//构造方法
public Student(String name,int age){
  this.name=name;
  this.age = age;
}


//setter
public void setName(String name){
  this.name = name;
}
```





#### 内容小结

- this关键字含义？

  this就是当前类的对象：

  - this在构造方法：当前new的对象
  - this在实例方法：谁调用该方法，this就是谁

- this关键字有什么作用？

  可以解决局部变量和成员变量冲突问题




###  05 匿名对象

#### 学习目标

- 能够定义类的匿名对象
- 能够使用匿名对象

#### 内容讲解

#### 【1】什么是匿名对象

- 有名对象：有对象名表示的对象

  ```java
  Student stu = new Student();
  
  Scanner sc = new Scanner(System.in);
  ```

- 匿名对象：没有对象名表示的对象

  ```java
  new Student();
  
  new Scanner(System.in);
  ```



#### 【2】匿名对象使用特点

匿名对象可以直接调用对象成员，但是只能使用一次。有名对象可以怎么用，匿名对象也可以怎么用。

- 直接使用匿名对象调用方法
- 直接当做一个参数传给方法
- 直接当做返回值进行传递



#### 【3】代码演示

```java
package _03匿名对象;
public class Demo01 {
    public static void main(String[] args) {
        //有名对象
        Student stu = new Student("钱进");
        //匿名对象
        new Student("文星");
        //- 直接使用匿名对象调用方法
        new Student("文星").study();

        //- 直接当做一个参数传给方法
        showStudent(stu);//对象名传入方法
        showStudent(new Student("李鹏程"));//匿名对象

        //- 直接当做返回值进行传递
        getStudent().study();
        Student stu2 = getStudent();//相当于将方法中的匿名对象赋值给stu2

        //以上三种方式都体现了匿名对象的一次性使用特点
    }

    public static void showStudent(Student stu) {
        stu.study();
    }

    public static Student getStudent() {
        return new Student("王超");
    }
}

class Student{
    String name;

    public Student(String name) {
        this.name = name;
    }

    public void study() {
        System.out.println(name+"正在认真的学习java！！");
    }
}
```



#### 内容小结

1. 什么是匿名对象？

   没有对象名的对象，匿名对象

2. 匿名对象怎么用？

   - 直接调用方法使用
   - 当做参数直接传递
   - 当做方法的返回值传递





###  06 继承认识

#### 学习目标

- 理解继承的思想

- 能够使用关键字extends书写继承的代码

- 能够知道继承的好处

  

#### 内容讲解

#### 【1】继承思想概述

面向对象的特性：封装，继承，多态

设计类的过程中就可以去使用继承，可以提高代码的复用性。

![ImgHosting](https://cdn.jsdelivr.net/gh/fakermama/ImgHosting/fakermama-PIC/image-20201028103456573.png) 



#### 【2】继承的格

Java中如何完成类型的继承：需要借助关键字，extends，implements

今日讲extends，类继承类使用 extends。

例如：已知Fu，Zi类，Zi类继承了Fu类。

```java
class Fu{
  成员
}

class Zi extends Fu{
  
}

```

父类也可以称为基类，超类

子类也可以称为扩展类

注意：继承只支持单继承。即一个子类只能存在一个直接父类。



#### 内容小结

- 继承的好处？

  可以提高代码的复用性

- 继承使用的关键字？

  extends

- 格式

  ```java
  class A{}
  class B extends A{}
  ```
  
  



###  07 继承入门案例

#### 学习目标

- 能够使用继承思想定义类



#### 内容讲解

#### 【需求】

学校要开发一个系统，用户有学生，老师，班主任等角色，以继承的思想定义以下类型：

1. 学生类
   属性:姓名,年龄
   行为:吃饭,睡觉
2. 老师类
   属性:姓名,年龄，薪水
   行为:吃饭,睡觉，教书
3. 班主任
   属性:姓名,年龄，薪水
   行为:吃饭,睡觉，管理



#### 【分析】

如果不用继承的思想定义类，发现有属性：姓名，年龄。行为：吃饭，睡觉，会重复定义。

使用继承的思想定义类：

- 把共性的属性或者行为抽取到父类中。
- 定义子类继承父类。重复的部分不用定义，特有的需要定义。



#### 【步骤】

1. 定义父类Human，将共性的属性和行为抽取放到该父类中
2. 定义子类，如果有特有的属性和行为单独定义子类
3. 使用子类创建对象



#### 【代码】

```java
package _04继承案例;

public class Demo01 {
    public static void main(String[] args) {
        Student stu1 = new Student();
        stu1.name = "Rose";
        stu1.eat();

        Teacher t1 = new Teacher();
        t1.name = "Jack";//父类
        t1.salary = 1;//本类
        t1.eat();//父类
        t1.teaching();//本类
    }
}

//1. 定义父类Human，将共性的属性和行为抽取放到该父类中
class Human {
    //共同的属性
    String name;
    int age;

    //共同的行为
    public void eat() {
        System.out.println(this.name + "在吃饭饭！！");
    }

    public void sleep() {
        System.out.println(name + "在睡觉觉！！");
    }

}
//2. 定义子类，如果有特有的属性和行为单独定义子类

class Student extends Human {
}

class Teacher extends Human {
    int salary;

    public void teaching() {
        System.out.println(name + "在教Java！！");
    }
}


//3. 使用子类创建对象
```



班主任类在课后完成。



#### 内容小结

如何使用继承思想设计类？

把多个类的共性属性或者行为抽取到父类中。

定义子类继承父类，如果有特殊的属性和行为单独定义在子类中





###  08 继承中成员变量的使用特点

#### 学习目标

- 理解继承中子类访问父类成员变量的特点
- 能够解决方法中变量，成员变量中及其父类中成员变量冲突

#### 内容讲解

#### 【1】继承中成员变量的使用特点

一个类访问成员变量时，先看本类中是否存在，如果本类存在直接访问。如果本类没有找父类，如果父类没有就没有访问报错。



- 子类可以直接使用父类属性的情况：
  - 如果子类和父类相同包，可以直接使用父类的public，protected，package-private（不写权限）修饰的属性
  - 如果子类和父类在不同包，可以直接使用父类的public，protected修饰的属性。
- 如果子类不能直接访问，可以借助getter，setter方法去进行访问
- 如果子类中存在与父类相同的成员变量，就近先使用子类的（会把父类同名成员变量隐藏）。

 





#### 【2】继承中子类方法中局部变量，子类成员变量中，父类成员变量中名字冲突

在子类方法中访问：

| 位置 | 子类方法中局部变量 | 子类成员变量  | 父类成员变量   |
| ---- | ------------------ | ------------- | -------------- |
| 访问 | 直接访问           | this.成员变量 | super.成员变量 |



代码示例：

```java
package _05继承中成员变量的访问特点;

public class Demo01 {
    public static void main(String[] args) {
        Cat c1 = new Cat();
        //访问成员变量，先看本类，再看父类，如果父类中还没有不能访问
        System.out.println("c1.num1 = " + c1.num1);//10
        System.out.println("c1.num2 = " + c1.num2);//20

        //区别变量冲突
        c1.show();
    }
}


class Animal {
    int num1 = 10;
    int num2 = 200;
    int age = 333;//父类的成员变量
}

class Cat extends Animal {
    int num2 = 20;
    int age = 222;//成员变量



    public void show() {
        int age = 111;//局部变量

        System.out.println(age);//111
        System.out.println(this.age);//222
        System.out.println(super.age);//333
    }
}
```



#### 内容小结

继承中子类访问父类成员变量的特点？

- 先看本类，再看父类，如果父类没有访问报错。

- 同包下：子类可以访问父类的public，protected，package-private（不写）修饰的属性
- 不同包：子类只能访问父类的public，protected修饰的属性

如果方法中局部变量，本类成员变量，父类的成员变量名字有冲突？

- 局部变量：直接访问

- 本类成员变量：this.

- 父类的成员变量：super.







###  09 继承中成员方法的使用特点

#### 学习目标

- 理解继承中子类访问父类成员方法的特点

  

#### 内容讲解

#### 【1】方法的访问特点

访问特点和成员变量是一样的。

如果子类中定义声明了与父类一样的方法，优先访问子类的方法。



#### 【2】代码示例

```java
public class Demo01 {
    public static void main(String[] args) {
        //创建子类对象调用方法

        Zi zi = new Zi();
        zi.method1();//来自父类
        zi.method2();//来自本类
        //zi.method3();//没有方法

        zi.method();//优先访问本类

    }
}

class Fu{
    public void method1() {
        System.out.println("父类的方法：method1");
    }

    public void method(){
        System.out.println("来自父类的method");
    }
}

class Zi extends Fu{
    public void method2() {
        System.out.println("子类的方法：method2");
    }
    public void method(){
        System.out.println("来自子类的method");
    }
}
```



#### 内容小结

继承中子类访问父类方法的特点？

先访问本类，本类没有找父类，父类没有报错。

继承中如果子类方法和父类方法相同了，子类对象调用该方法优先访问谁呢？

子类



###  10 方法重写

#### 学习目标

- 能够理解为什么要重写
- 能够覆盖重写父类方法

#### 内容讲解

#### 【1】重写概念

当父类中方法继承到子类后，不满足子类需要的时候，子类就可以对这个方法进行覆盖，重写（Override）。



**如何重写父类中的方法呢？**

**声明不变，重新实现。**

- 方法的声明：`修饰符 返回值类型 方法名 (参数列表)`
- 逻辑的重新实现：方法体的逻辑重写

```java
修饰符 返回值类型 方法名 (参数列表)

{
  方法体的逻辑重写
}

public static void main(String[] args){
  //逻辑
}

```



例如：

```java
class Animal {
  public void eat(){
    System.out.println("吃东西");
  }
}


class Cat extends Animal{
  //重写eat方法
  public void eat(){
    System.out.println("猫吃鱼");
  }
}

```



#### 【2】注解

@Override  ：注解，表示该方法是重写的方法。



IDEA重写方法：

1. 直接写方法名，回车补全
2. 快捷键：Ctrl+O 



**代码实例**

已知一个Animal了含有一个eat方法，要求定义子类重写该方法。

```java

public class Demo01 {
    public static void main(String[] args) {
        Cat c = new Cat();
        c.eat();

        Dog d = new Dog();
        d.eat();

    }
}

/**
 * 父类
 */
class Animal{
    public void eat() {
        System.out.println("动物吃东西~~");
    }
}
/**
 * 子类
 */
class Cat extends Animal{
    public void eat(){
        System.out.println("猫吃鱼！！");
    }
}

class Dog extends Animal{
    @Override
    public void eat() {
        //super.eat();//复用父类的逻辑
        System.out.println("狗吃骨头！");
    }
}
```



执行结果：

```java
猫吃鱼！！
狗吃骨头！
```



#### 【3】注意事项

1. 方法重写是发生在子父类之间的关系。

2. 子类方法覆盖父类方法，必须要保证权限大于等于父类权限。（public >protected > package-private ）

3. 子类方法覆盖父类方法，返回值类型、函数名和参数列表都要一模一样。
   **返回值类型可以不一样**

   **子类继承父类，子类范围更具体更小的，父类范围会更抽象更宽泛。父类型大于子类型。**
   
   ```
   子类方法覆盖（重写）父类方法时，子类方法的返回值类型可以小于父类方法中返回值类型【不考虑基本数据类型】
   ```
   
   

平时重写方法时：声明不变



#### 内容小结

1. 为什么要重写？

   父类的逻辑不满足子类需要，就可以对该方法进行重写

2. 如何重写？

   声明不变，重新实现





###  11 继承中构造方法的使用特点

#### 学习目标

- 能够使用super调用父类构造方法初始父类属性

#### 内容讲解

构造方法是不能从父类继承到子类中的，但是可以在子类中借助super关键字进行访问。



**如何借助super关键字调用父类的构造方法？**

- 格式：

  需要在子类构造方法中**第一句**位置，使用super调用

  ```java
  super() 调用父类的无参构造
  super(参数) 调用父类的有参构造方法
  ```

- 特点：

  super调用构造方法一次只能有一个。

  父类的构造方法，总是在子类构造方法执行前，执行。

  子类的构造方法，一定会先调用父类构造方法，如果没有显式使用super调用，默认会有`super()`



**代码实践**

```java
public class Demo01 {
    public static void main(String[] args) {
        Cat c1 = new Cat();
        showCat(c1);//null:0:null

        Cat c2 = new Cat("橘黄色");
        showCat(c2);//tom:2:橘黄色

        Cat c3 = new Cat("蓝色","蓝猫",3);
        showCat(c3);//蓝猫:3:蓝色


    }

    public static void showCat(Cat c) {
        System.out.println(c.name + ":" + c.age + ":" + c.color);
    }
}

class Animal {
    String name;
    int age;

    public Animal() {
    }

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class Cat extends Animal {
    String color;

    public Cat() {
        super();//调用父类的无参构造方法
    }

    public Cat(String color) {
        //要对父类中name赋值为tom，age赋值为2
        super("tom", 2);//调用的是父类满参构造方法
        this.color = color;
    }

    public Cat(String color, String name, int age) {
        super(name, age);
        this.color = color;
    }
    //IDEA也可以直接生成含有调用父类构造方法的子类构造方法
    public Cat(String name, int age, String color) {
        super(name, age);
        this.color = color;
    }
}

```



打印结果：

```
null:0:null
tom:2:橘黄色
蓝猫:3:蓝色
```



#### 内容小结

如何调用父类的构造方法？

1. 使用关键字：super
2. 位置要求：子类构造方法的第一句
3. 格式：super(参数)





###  12 super和this关键字使用小结

#### 学习目标

- 能够区分super和this的用法
- 能够使用this关键字调用本类中的构造方法

#### 内容讲解

#### 【1】super和this的异同

super和this都是指代的同一个对象，this表示的本类空间，super表示的父类空间。

![ImgHosting](https://cdn.jsdelivr.net/gh/fakermama/ImgHosting/fakermama-PIC/image-20201214152103317.png) 

this和super用法一样：

- 调用成员变量
- 调用成员方法
- 调用构造方法

区别在于，this调用的是本类的成分，super调用父类的成分。



#### 【2】this调用本类构造方法

- 格式：

  位置：必须在本类构造方法的第一句

  ```java
  this(参数) 
  ```

  注意：不能调用自身构造方法

- 特点：

  1. this和super调用构造方法不能共存的
  
- 好处：

  可以提高代码的复用性
  
  

代码实践：

```java
public class Demo01 {
    public static void main(String[] args) {
        Cat c = new Cat();
        System.out.println(c.age + "::" + c.weight);
    }
}


class Animal {
    String name;

    public Animal() {
    }

    public Animal(String name) {
        this.name = name;
    }
}

class Cat extends Animal {
    int age;
    int weight;

    public Cat() {
        //调用了本类的构造方法进行赋值
        this(2, 3);

        // this();//构造方法自身不能调用自身
    }

    public Cat(int age, int weight) {
        super();
        this.age = age;
        this.weight = weight;
    }
    
}

```







#### 内容小结

**super和this分别指的是什么？**

this指的子类空间，super指的是父类空间，是同一个对象

**this如何调用本类其他构造方法？**

位置：第一句

格式：this(参数)



**思考：this为何要调用本类其他构造方法？**

提高代码的复用性





###  

### 13 继承的特点

#### 学习目标

- 能够理解继承的三个特点

#### 内容讲解

继承的特点有三个：

1. 只支持单继承

   ```java
   class A {}
   class B {}
   class C extends A{}
   class D extends A,B{} //不行，错误
   ```

2. 允许一个父类有多个子类

   ```java
   class A{}
   class B extends A{}
   class C extends A{}
   ```

3. 允许类多层继承

   ```java
   class A{}  //如果一个类没有显式的继承一个类，默认会继承Object（上帝类）
   class B extends A{}
   class C extends B{}
   class D extends C{}
   ```

   继承也是具有传递性的，A中的成分不仅会继承给B，也会继承给C，也会继承给D。



#### 内容小结

继承三个特点？

1. 只支持单继承
2. 父类允许有多个子类
3. 类支持多级继承（继承具有传递性）

最终的父类是Object





###  14 抽象类的定义

#### 学习目标

- 理解什么是抽象类，抽象方法
- 能够定义抽象类和抽象方法

#### 内容讲解

#### 【定义】

abstract关键字：表示抽象。



使用关键字abstract修饰的类，称为抽象类。

使用关键字abstract修饰的方法，没有方法体，且以分号结尾的方法，称为抽象方法。



#### 【格式】

```java
//抽象类
修饰符 abstract class 类名{
  //抽象方法
  修饰符 abstract 返回值类型 方法名(参数列表);
}
```

- 在抽象类中，可以没有抽象方法。但是如果一个类中存在抽象方法，该类一定是抽象类。
- 抽象类本质上也是一个类，也可以有普通类中的各种成分（成员变量，成员方法，构造方法）





#### 【使用场景】

抽象类，抽象方法的使用场景。

抽取多个类的父类时，通常就会使用抽象类。如果多个类中有共同的方法，但是逻辑具体不同，此时就可以使用抽象方法。

抽象类就是以父类的角色存在。



#### 【代码实践】

学生：姓名，年龄，吃饭，工作

老师：姓名，年龄，吃饭，工作

班主任：姓名，年龄，吃饭，工作



抽取父类人，描述上面的共同的父类。

分析：

属性：姓名，年龄

行为：吃饭，工作，吃饭大家都一样的，可以使用具体的方法，而工作，因为每个角色的内容不同，可以使用抽象方法。

```java
public abstract class Person {
    //姓名，年龄
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    //吃饭，工作
    public void eat() {
        System.out.println("吃饭");
    }

   //抽象方法特点：需要关键字abstract，没有方法体

    public abstract void work();
}

```





#### 内容小结

**什么叫抽象类，什么叫抽象方法？**

用abstract关键字修饰的类，称为抽象类。

用abstract修饰的方法，称为抽象方法

**抽象的关键字是什么？**

abstract

**什么时候可以使用抽象类，抽象方法？**

抽取父类的时候，就可以使用抽象类。

如果抽取的方法不能确定具体的业务逻辑，该方法就可以使用抽象类。



###  15 抽象类的使用

#### 学习目标

- 能够使用抽象抽象

#### 内容讲解



#### 【1】抽象类的使用方式

1. 抽象类不能直接实例化对象使用。

2. 可以定义子类继承抽象的父类，如果存在抽象方法，要将所有的抽象方法进行重写

   重写抽象方法可以叫做实现（重写）。

3. 如果子类不重写抽象方法，你可将子类也变成抽象类。

![image-20201214163930847](https://cdn.jsdelivr.net/gh/fakermama/ImgHosting/fakermama-PIC/image-20201214163930847.png) 



#### 【2】代码实践

使用上一个知识点的Person抽象类作为父类定义学生类，老师类。



当我们使用一个类继承一个抽象类时，发现报错：

![image-20201028160114179](https://cdn.jsdelivr.net/gh/fakermama/ImgHosting/fakermama-PIC/image-20201028160114179.png) 

```java
类Student必须要么定义成抽象类，要么把来自父类的抽象方法work实现
```



```java
public class Demo01 {
    public static void main(String[] args) {
        //抽象类，不能创建对象
        //Person p1 = new Person("张三",18);

        Student stu = new Student();
        stu.work();

    }
}
//学生：姓名，年龄，吃饭，工作
class Student extends Person{
    @Override
    public void work() {
        System.out.println("学生的本职工作就是学习！！");
    }

    @Override
    public void sleep() {

    }
}


//老师：姓名，年龄，吃饭，工作
//班主任：姓名，年龄，吃饭，工作
```





#### 内容小结

**抽象类怎么使用？**

- 抽象类能创建对象么？不能

- 怎么用？

  需要定义子类去继承抽象的父类，子类要么实现所有的抽象方法，要么把自己变成抽象类。



###  16 抽象类的使用注意事项

#### 学习目标

#### 内容讲解

1. 抽象类**不能创建对象**，如果创建，编译无法通过而报错。只能创建其非抽象子类的对象。

   > 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体，没有意义。

2. 抽象类中，可以有构造器，是供子类创建对象时，初始化父类成员使用的。

   > 理解：子类的构造方法中，有默认的super()，需要访问父类构造方法。

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

   > 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设计。

4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，否则子类也必须定义成抽象类，编译无法通过而报错。 

   > 理解：假设不重写所有抽象方法，则类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有意义。



###  17 抽象类存在的意义

#### 学习目标

- 能够理解抽象类存在的意义

#### 内容讲解

抽象类在抽取父类型的时候可以使用，有一些方法假如具体子类型有不同的逻辑，可以使用抽象方法。



抽象类的子类必须要实现所有的抽象方法。否则要变成抽象类。



对子类有一个约束，子类会根据父类而进行设计，体现一种模板思想。



#### 内容小结

抽象类可以当做父类型，里面定义抽象方法，可以约束子类一定要做一个具体的实现。







###  18 模板设计模式

#### 学习目标

- 理解什么是设计模式
- 能够使用抽象类设计模板模式

#### 内容讲解

**什么是设计模式？**

设计模式体现的是解决一个问题一个需求的一种最佳实践。



模板设计模式：

可以利用抽象类定义一些需要子类完成的一系列功能的模板方法。子类继承抽象类之后，只要实现抽象方法。

而模板方法直接继承到子类，不需要重写。子类调用模板方法的时候，就可以按照模板的逻辑进行执行了。



例如：

我现在需要定义新司机和老司机类，新司机和老司机都有开车功能，开车的步骤都一样，只是驾驶时的姿势有点不同，

`新司机:开门,点火,双手紧握方向盘,刹车,熄火`，

`老司机:开门,点火,右手握方向盘左手抽烟,刹车,熄火`。



使用模板设计模式进行定义相关的类，步骤：

1. 抽取所有的共性方法到抽象类中，如果具体类型的逻辑不同的使用抽象方法定义。
2. 定义模板方法，定义每个子类都必须遵循的一个业务逻辑（流程）。

抽象父类（模板）

```java

abstract class Driver{
    //模板方法：定义具体的办事流程
    public final void driving() {//加上final可以阻断子类重写该方法
        System.out.println("开门");
        System.out.println("点火");
        ziShi();//调用的肯定是子类实现的方法
        System.out.println("刹车");
        System.out.println("熄火");
    }

    public abstract void ziShi();
}

```

测试类及其子类：

```java
package _11模板设计模式;

public class Demo01 {
    public static void main(String[] args) {
        NewDriver d1 = new NewDriver();
        d1.driving();//模板方法调用
        System.out.println("============");
        OldDriver d2 = new OldDriver();
        d2.driving();

    }
}
//新司机
class NewDriver extends Driver{
    @Override
    public void ziShi() {
        System.out.println("双手握紧方向盘");
    }
}
//老司机
class OldDriver extends Driver{
    @Override
    public void ziShi() {
        System.out.println("右手握紧方向盘，左手抽烟！");
    }

}

```



#### 内容小结

**什么时候使用模板设计模式？**

当很多类都有一个流程要执行时，流程都一样。可以使用模板设计模式

**如何设计？**

借助抽象类完成，定义具体的模板方法写流程，流程中不确定的逻辑可以使用抽象方法表示。


> 文章作者：**Miracle Wu**  
> 原文地址：<https://miracled.top>    
> 版权声明：文章采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh) 协议，转载请注明出处。





