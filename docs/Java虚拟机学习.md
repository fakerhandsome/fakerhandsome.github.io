---
id: JVM与JAVA体系结构
title: JVM与JAVA体系结构
---
## Java虚拟机学习01
### 1. JAVA 虚拟机特点

+ 内存动态分配
+ 垃圾收集机制
虚拟机划分:
+ 系统虚拟机 (VMware Visual Box)
+ 程序虚拟机 (JVM)

>虚拟机就是一台虚拟的计算机，用来执行一系列虚拟计算机指令
>        系统虚拟机是对物理计算机的仿真，提供了可运行完整操作系统的软件平台
>        程序虚拟机专门为执行单个计算机程序而设计
---
### 2. Java虚拟机作用
```java
Java虚拟机就是二进制字节码的运行环境，负责装载字节码到内部，解释/编译为对应平台上的机器指令执行。
特点
+ 一次编译，到处运行
+ 自动内存管理
+ 自动垃圾回收功能
```
### 3. JVM的整体结构
采用解释器和即时编译器并存的架构。

<img src="https://cdn.jsdelivr.net/gh/fakermama/ImgHosting/fakermama-PIC/Snipaste_2021-04-20_23-27-38.png" style="zoom:50%;" />

### 4. JVM的生命周期
#### 1. 虚拟机的启动

Java虚拟机的启动是由于引导类加载器(bootstrap class loader)创建一个初始类initial class来完成的，这个类是由虚拟机指定实现的

#### 2. 虚拟机的执行

一个运行中的Java虚拟机有着一个清晰的任务，执行Java程序，程序开始执行时它执行，程序结束时它停止。
执行一个所谓的Java程序的时候，真真正正在执行的是一个叫做Java虚拟机的进程。
`jps`-->打印当前执行的进程，用来查看虚拟机的执行进程(直接输入`jps`查看)

#### 3. 虚拟机的退出
有如下几种情况
+ 程序正常执行结束
+ 程序在执行过程中遇到了异常或错误而异常终止
+ 由于操作系统出现错误而导致Java虚拟机进程终止
+ 某线程调用Runtime类或System类的exit方法，或Runtime类的halt方法，并且Java安全管理器也允许这次exit或halt操作
+ JNI(Java本地接口)规范描述了JNI Invocation API来加载或卸载Java虚拟机。
### 5. Java代码执行流程
Java源码(.java文件)通过Java编译器生成JVM字节码文件，进入Java虚拟机通过类加载器对字节码文件的加载，字节码校验器(翻译字节码)，JIT编译器(编译执行)

### 6. JVM的架构模型
Java编译器输入的指令流是基于栈的指令集架构(还有一种是基于寄存器的指令集架构)
+ 基于栈式架构的特点
   + 设计实现简单
   + 使用零地址指令方式分配
   + 可移植性好，跨平台
+ 基于寄存器架构的特点
   + 完全依赖硬件，可移植性差
   + 性能优秀，执行高效
   + 寄存器架构的指令集不是以零地址指令为主
```java
逻辑运算的时候，第一步生成常量iconst,第二步保存到索引位istore，第三步加载iload，第四步进行添加运算iadd，第五步保存结果istore,最后才是返回结果
反编译命令
javap -v class文件名(进入编译运行后生成的class文件路径)
public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=4, args_size=1
         0: iconst_2  //常量
         1: istore_1  // 保存
         2: iconst_3
         3: istore_2
         4: iload_1   //加载
         5: iload_2
         6: iadd   //逻辑加法运算
         7: istore_3
         8: return
      LineNumberTable:
        line 5: 0
        line 6: 2
        line 7: 4
        line 8: 8
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       9     0  args   [Ljava/lang/String;
            2       7     1     i   I
```
### 7. JVM发展历程
1. `SunClassic` VM
2. Exact VM
3. `HotSpot` VM(Sun公司第三个虚拟机)
>目前市场`HotSpot`占有绝对的市场地位，JDK6或者8默认的虚拟机都是`HotSpot`，(热点代码探测技术)，通过计数器找到最具编译价值代码，触发即时编译或栈上替换，通过编译器和解释器协同合作，在最优化的程序响应时间或最佳执行性能中取得平衡。

