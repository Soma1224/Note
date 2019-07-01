# Socket网络编程

## 第2章 Socket网络编程快速入门

### 2-1 什么是网络？

#### 7层网络模型

![1545877842555](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545877842555.png)

![7层网络](.\picture\7层网络.jpg)



![1545878417364](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545878417364.png)



### 2-2 Socket与TCP、UDP

![1545879581515](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879581515.png)

![1545879689562](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879689562.png)

![1545879705676](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879705676.png)



![1545879839371](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879839371.png)

![1545879962979](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879962979.png)

**TCP传输只有两种状态：成功和失败**

![1545879990354](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545879990354.png)





![1545880019788](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545880019788.png)





![1545880238631](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545880238631.png)



### 2-3 报文、协议、Mac地址

![1545984595622](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545984595622.png)



![1545984699602](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545984699602.png)



![1545984742158](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545984742158.png)



![1545984836261](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545984836261.png)



### 2-4 IP、端口、远程服务器

![1545985052364](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985052364.png)



![1545985089242](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985089242.png)



![1545985159972](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985159972.png)



![1545985224492](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985224492.png)



![1545985272606](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985272606.png)



![1545985345011](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985345011.png)



![1545985383298](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985383298.png)



![1545985456700](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985456700.png)

本地电脑有多个IP的情况下，因为一个ip对应的端口总数为65536个，本地电脑端口的连接远远超过65536个



![1545985599668](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985599668.png)



![1545985691834](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985691834.png)

一般的，一个局域网会为该局域网中的电脑分配一个IP地址的，所以每台电脑的IP地址时对应局域网的IP地址，不是互联网的IP地址。所以不同局域网之间的电脑是不能直接连接的



![1545985747180](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545985747180.png)



![1545986017539](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545986017539.png)

qq服务器类比图，该服务器的IP是固定好的。



![1545986094370](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545986094370.png)

192.168.1.112一定是电脑的局域网IP地址

110.90.45.6是外网服务器IP地址

假设访问百度，输入的是：www.baidu.com，是域名DNS，经过域名服务器的53号端口去查询DNS所对应的IP和端口号

HTTP和HTTPS都是基于TCP的封装





## Socket UDP快速入门

### 3-1 UDP是什么

UDP是一种基于报文的协议，TCP是基于链接的协议

![1545986701567](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545986701567.png)

![1545986786284](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545986786284.png)

![1545986877860](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545986877860.png)

UDP一次传输最大包的大小为65507byte

![1545987033726](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545987033726.png)

### 3-2 UDP核心API讲解

![1545987392384](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545987392384.png)

![1545987501877](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1545987501877.png)



![1546044151080](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546044151080.png)

![1546044415915](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546044415915.png)

![1546044460285](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546044460285.png)



![1546044526710](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546044526710.png)

![1546045692708](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546045692708.png)





![1546045731254](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546045731254.png)

### 3-3 UDP单播、广播、多播-1

![1546046069581](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546046069581.png)



![1546046279308](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546046279308.png)



一般家庭的网络都是C类地址



### 3-4 UDP单播、广播、多播-2

![1546046463925](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546046463925.png)

#### **根据IP地址和子网掩码求 网络地址和广播地址？**

- 将IP地址和子网掩码换算为二进制，子网掩码连续全1的是==网络地址==，后面的0是==主机地址==
- **IP地址和子网掩码进行与运算，结果是网络地址**（即主机号全0是网络地址）
- 将运算结果中的网络地址不变，**主机地址变为1，结果就是广播地址**
- 地址范围就是含在本网段内的所有主机



网络地址+1即为第一个主机地址，广播地址-1即为最后一个主机地址， 
由此可以看出地址范围是： 网络地址+1 至 广播地址-1

- 主机的数量=2^二进制位数的主机-2

减2是因为主机不包括网络地址和广播地址



**示例** 
一个主机的IP地址是202.112.14.137，掩码是255.255.255.224，要求计算这个主机所在网络的网络地址和广播地址

==根据子网掩码可以分割网络号+主机号==

`255.255.255.224` 转二进制：

> 11111111 11111111 11111111 11100000

网络号有27位，主机号有5位

网络地址就是：把IP地址转成二进制和子网掩码进行**与运算**

11001010 01110000 00001110 10001001

IP地址&子网掩码



> 11001010 01110000 00001110 10001001
>
> 11111111 11111111 11111111 11100000
>
> \------------------------------------------------------------------
>
> 11001010 01110000 00001110 10000000

**即：202.112.14.128**



==计算广播地址==

广播地址：网络地址的主机位全部变成1 ，10011111 即159 即：202.112.14.159



==主机数：==
$$
2^5-2=30
$$



![1546049934522](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546049934522.png)

结论：两台主机在不同的网段里面，所以不能进行通讯。





## Socket TCP快速入门

### 4-1 TCP是什么、能做什么

![1546407114932](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546407114932.png)



![1546407235278](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546407235278.png)



![1546410971412](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546410971412.png)



![1546411036868](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546411036868.png)



### 4-2 TCP核心API讲解

![1546413774346](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546413774346.png)



当服务器端调用accept方法后，会进入一个阻塞状态，直到一个客户端到达为止。

![1546416684503](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546416684503.png)

![1546416872415](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546416872415.png)



![1546416924038](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546416924038.png)

- 默认状态下，电脑中的任意进程都能创建一个socket连接。
- 一个进程仅仅是使用了TCP完成进程之间的交互，进程是无法管理到TCP底层的东西的，例如TCP的三次握手，四次挥手，TCP的数据校验机制等



![1546417180750](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546417180750.png)

### 4-3 TCP连接可靠性-三次握手、四次挥手

==位码（TCP标志位）==

- SYN(synchronous建立联机)
- ACK(acknowledgement 确认)
- PSH(push传送) 
- FIN(finish结束)
- RST(reset重置)
- URG(urgent紧急)







![1546417855494](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546417855494.png)

- 随机数的出现就是保证连接的可靠性，没有进行错误的回送，连接是一一对应的。

![1546418010077](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546418010077.png)



![1546418136573](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546418136573.png)



### 4-4 TCP传输可靠性-排序、丢弃、重发

![1546428471997](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546428471997.png)





## 第5章 UDP辅助TCP实现点对点传输案例

- UDP可以作为广播的发送、搜索、基于报文的传输
- TCP是基于连接上的传输，一定能确保数据完整地送达



**如何把TCP和UDP结合起来使用？**

如果你知道服务器地ip地址和端口的话，可以通过TCP建立和服务器的连接，但是在一个局域网当中你不知道服务器的ip地址，仅仅知道服务器的公共的UDP的端口，在这种情况下，你如何实现TCP的连接呢？



答：如果要实现TCP的连接，由于TCP的连接是点对点的连接，那么一定要知道TCP服务器的ip地址和端口，如何知道TCP服务器的ip地址和端口呢？可以在客户端发起一个UDP的广播，广播的接收者服务器在接收到这个广播后，会回送给客户端TCP服务器的ip地址和端口号，这样就知道了TCP服务器的ip地址，就可以进行TCP连接了。



![1546519334230](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546519334230.png)





![1546519404970](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546519404970.png)

**要实现服务器端和客户端的接收和发送信息互不干扰**

参考代码：==SocketDemo-L5-TCP-Channel==



![1546763366886](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1546763366886.png)

**所述例子实现了服务器端和客户端的收发并行的功能，但是并不是完全意义上的收发并行独立，Client的发送是因为有一个键盘输入的线程，把键盘输入的线程阻塞在Client端，在键盘上输出的文字充当了输出的线程。Server端首先是一个键盘输入的线程，然后键盘的线程会被转到每个客户端的线程池上面去，然后由客户端的每个单线程池发送出去。**

