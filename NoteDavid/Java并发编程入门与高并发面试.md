# Java并发编程入门与高并发面试

## 第2章 并发基础

### Java内存模型（JMM）

**JMM**

- JMM是一种规范，规范了Java虚拟机和计算机是如何协同工作的
- JMM规定了一个线程==如何==和==何时==可以看到其他线程修改过的共享变量的值，以及在必须时如何同步地访问共享变量。

**堆**

- 可以在运行时动态分配内存大小，生存期也不必事先告诉编译器（因为java的GC会自动进行垃圾回收）

- java中的堆是运行时动态分配内存的，存取速度相对较慢一些

**栈**

- 优点：存取速度比堆要快，仅次于计算机中的寄存器 ，栈的数据是可以共享的
- 缺点：存在栈中的==数据的大小==和==生存期==必须是确定的，缺乏一些灵活性。
- 栈中一般存放一些基本类型的变量，例如：int，double，boolean，char，string，char



![1547084507975](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547084507975.png)

**JMM要求调用栈和本地变量存放在线程栈（Thread Stack）上，对象存放在堆上。**

- 一个本地变量（Local Variable）也可能是一个指向对象（Object）的引用（Reference），对该对象的引用是存放在线程栈（Thread Stack）上的，而对象本身是存放在堆（Heap）上的。

- 一个对象可能包含方法（Method），这些方法可能包含本地变量（Local Variable），这些方法和方法所包含的本地变量都是存放在Thread Stack上的

- 一个对象的成员变量可能会随着对象的自身存放在堆（Heap）上，静态成员变量跟随类的定义一起存放在堆（Heap）上

- 存在堆（Heap）上的对象（Object）可以被持有这个对象的引用的线程（Thread）所访问

- ==如果两个线程调用了同一个对象的同一个方法，他们都会访问这个对象的成员变量，每一个线程都拥有了这个成员变量的私有拷贝。==



  **硬件架构**

  ![1547086234768](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547086234768.png)

  CPU Registers：CPU寄存器

  Cache：高速缓存（因为计算机的主存储设备和处理器的读写速度差太多，Cache作为内存和处理器之间的缓冲，让运算能够快速地进行）

  Main Memory：主存

  CPU读写速度：CPU Registers > Cache > Main Memory

运作原理：CPU想要读取Main Memory中的数据，通常会把Main Memory的部分读取到Cache中，甚至会把Cache的数据读到CPU Registers里面，需要回送给Main Memory的时候，通过CPU Registers ——> Cache ——> Main Memory的刷新过程。



**JMM和硬件架构**

![1547086705481](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547086705481.png)



可以看到硬件架构没有区分线程、栈和堆



**线程和主内存之间的抽象关系：**

![1547087646255](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547087646255.png)



- 本地内存：JMM的抽象概念，不是真实存在的，它涵盖了：缓存、缓冲区、寄存器、其他硬件和编译器的优化



**Java内存模型同步的八种操作**

![1547117408914](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117408914.png)

![1547117424090](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117424090.png)



**Java内存模型同步规则**

![1547117471927](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117471927.png)

![1547117501848](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117501848.png)

![1547117524664](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117524664.png)

![1547117548762](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117548762.png)

**同步操作与规则**



![1547117192438](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547117192438.png)



### 并发的优势和风险

![1547118231282](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547118231282.png)



## 第3章 项目准备

**用代码进行并发模拟**

- CountDownLatch    ==可以阻塞一个线程，并且能够保证该线程在满足特定条件下能够继续执行，比较适合线程执行完后再进行其他的处理==

![1547171783256](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547171783256.png)

- Semaphore     ==可以阻塞进程，并且控制同一时间请求的并发量，适合控制同时并发的线程数==

![1547172221585](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547172221585.png)

CountDownLatch和Semaphore一般会配合线程池来使用



**并发模拟工具**

- PostMan：Http请求模拟工具
- Apache Bench：Apache附带的工具，测试网站性能
- JMeter：Apache组织开发的压力测试工具



## 第4章 线程安全性

- **线程安全性**

![1547185099816](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547185099816.png)



![1547196242195](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1547196242195.png)



- **CAS(CompareAndSwap)**



- **AtomicLong**



- **LongAdder**

**优点：**        将热点数据分离，比如它可以将AtomicLong的内部核心数据value分离成一个数组，每个线程访问时，通过hash等算法预测到其中一个数字进行计数，而最终的计数结果是这个数组的所有元素的求和和累加。其中热点数据value会被分割成多个单元的scale，每个scale独自维护内部的值，当前value值由所有的scale累计合成，这样的话热点就进行了有效的分离并提高了并行度，LongAdder相当于在AtomicLong的基础上将单点的更新压力分散到各个结点上，在低并发的时候，通过对base的直接更新，可以很好地保证和AtomicLong的性能基本保持一致，而在高并发的时候通过分散提高了性能。

**缺点：**        LongAdder在统计的时候如果有并发更新，可能导致统计的数据有误差。