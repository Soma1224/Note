# 深入理解java虚拟机笔记

## java可视化监控工具jconsole

- 在配置好jdk环境变量的前提下，cmd输入jconsole即可使用~
- 具体文件位置是在：C:\Program Files\Java\jdk1.8.0_172\bin\jconsole.exe

## 并发与并行

- 并行：扔垃圾和扫垃圾各干各的
- 并发：扔垃圾和扫垃圾同时干

## 垃圾收集算法

### 标记-清除算法

### 复制算法

### 标记-整理算法

### 分代收集算法



## 垃圾收集器

### Serial

### ParNew

### Parallel Scavenge

### Serial Old

### Parallel Old

### CMS

### GI

- 由于运用标记-清除算法，所以是老年代垃圾收集器















## 内存分配与回收策略

### 对象优先在Eden中分配

垃圾收集器的选用是根据jdk所处的环境决定的

如果是server的话，默认指定的是ParNew；如果是client的话，默认指定的是Serial

如何看是server还是client？

![Snipaste_2018-10-11_14-58-08](E:\Typora文件\图片\Snipaste_2018-10-11_14-58-08.png)



- 本次配置的是：

```java
-verbose:gc -XX:+PrintGCDetails -XX:+UseSerialGC -Xms20M -Xmx20M -Xmn10M 
-XX:SurvivorRatio=8
```

- 堆内存的分配是：

![Snipaste_2018-10-11_16-19-40](E:\Typora文件\图片\Snipaste_2018-10-11_16-19-40.png)

运行的程序是：

```java
public static void main(String[] args) {
    byte[] b1=new byte[2*1024*1024];
    byte[] b2=new byte[2*1024*1024];
    byte[] b3=new byte[2*1024*1024];
    byte[] b4=new byte[4*1024*1024];
    System.gc();
}
```

- 划红色线的是发生在新生代的Minor GC：方括号内是新生代内存从6M到几乎没有，方括号外是堆内存从6M变为4M，此处注意这些数字是相对于此次垃圾回收的瞬间内存变化情况来说的。

![Snipaste_2018-10-11_16-02-06](E:\Typora文件\图片\Snipaste_2018-10-11_16-02-06.png)

- 对于参数的解释：

![Snipaste_2018-10-11_15-18-07](E:\Typora文件\图片\Snipaste_2018-10-11_15-18-07.png)

### 大对象直接进入老年代

参数：-XX:PretenureSizeThreshold

现在可以直接写6M，7M了

### 长期存活的对象将进入老年代中

对象在新生代的Eden出生经过Minor GC的复制算法进入到survivor中

### 空间分配担保







### 逃逸分析和栈上分配

#### 栈上分配

> 栈上分配是java虚拟机提供的一种优化技术，基本思想是对于那些线程私有的对象（指的是不可能被其他线程访问的对象），可以将它们打散分配在栈上，而不是分配在堆上。分配在栈上的好处是可以在函数调用结束后自行销毁，而不需要垃圾回收器的介入，从而提供系统的性能。



#### 线程逃逸

> 我们把指向刚分配出来的Test实例的引用赋值到了一个静态变量或者可以被其他线程访问的实例字段上时，就可能导致别的线程可以感知到这个新对象的存在，所以这种动作也叫做“发布”（publish）或者叫做“线程逃逸”（thread escaping）。











