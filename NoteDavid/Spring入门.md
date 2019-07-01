# Spring入门

## Spring的IOC的底层实现的原理：

![1543973727294](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543973727294.png)

一开始是接口和实现类之间的耦合关系通过工厂模式进行解决，耦合就是如果想切换接口的实现类的话，需要修改程序的源码

虽然改为接口和工厂类的设计模式了，解除了接口和实现类的耦合，但是接口和工厂类之间的耦合并没有解除，这里的耦合是指如果想切换接口的实现类的话，需要修改工厂的源代码

最终是==工厂+反射+配置文件==的方式完成最终的解耦。



![1543977363336](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543977363336.png)



# Spring Bean管理：

## 三种实例化Bean的方式：

![1543978431129](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543978431129.png)

## Bean的配置：

![1543979400687](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543979400687.png)

区别就是：id是不可以包含有特殊字符的，但是name是可以包含特殊字符的。



![1543979549344](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543979549344.png)

singleton是默认的，其余需要配置scope属性



![1543990444502](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543990444502.png)





## XML方式注入：

![1544082323559](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544082323559.png)



![1544154275077](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544154275077.png)



![1544154292853](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544154292853.png)



![1544099492785](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544099492785.png)



![1544099514968](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544099514968.png)



![1544146077717](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544146077717.png)



## 注解方式注入：

![1544148001229](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544148001229.png)



![1544148057317](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544148057317.png)



![1544148187494](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544148187494.png)

## 关于普通类型和对象类型的注入总结：

- 普通类型                                                                         @Value
- 对象类型                                                                        
  - @Autowired+@Qualifier
  - @Resource                          这个注入式@Autowired+@Qualifier的结合形式





 ![1544148535451](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544148535451.png)



![1544152902983](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544152902983.png)



## XML和注解方式的整合：

- **XML只管理类的注入**

- **属性注入通过注解的方式注入**



## 明确属性注入和包扫描注解的开启方式：

这种方式是包扫描的方式，**类注入和类中的属性注入都可以使用**

```xml
<context:component-scan base-package="com.imooc"/>
```



**这种方式只是开启了属性注入**

```xml
<context:annotation-config/>
```



总结：包扫描的方式包含了属性输入这种方式



# Spring的AOP技术：

![1544184297386](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544184297386.png)



如果在UserDao里面在保存用户（Save方法）里面增加管理员权限的话，传统的方法就是**纵向继承**，也就是继承一个base类，实现里面的checkPrivilege()方法。



![1544184863280](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544184863280.png)



AOP采用了**横向抽取机制**取代了传统的纵向继承。



![1544185302740](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544185302740.png)



![1544185461965](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544185461965.png)



![1544185551701](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544185551701.png)



![1544186306823](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544186306823.png)



![1544186458324](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544186458324.png)



## AOP的底层实现一：JDK的动态代理

==JDK的动态代理只能对**实现了接口的类**实现动态代理==

案例：demo1可见

## AOP的底层实现二：CGLIB的动态代理

如果有个类没有实现接口的话，JDK的动态代理就会无效，那么就需要新的代理

![1544187685156](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544187685156.png)



案例：demo2可见



## Spring代理知识点的总结：

![1544188475717](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544188475717.png)



![1544188553350](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544188553350.png)



## SpringAOP的通知类型介绍：

![1544407649865](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544407649865.png)



![1544407717581](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544407717581.png)



## SpringAOP的切面类型：

![1544407859740](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544407859740.png)



## SpringAOP的一般切面Advisor的案例：

![1544408640804](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544408640804.png)



![1544410402300](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544410402300.png)



## SpringAOP的带有切入点的切面案例：

![1544410494456](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544410494456.png)



## SpringAOP自动代理：

![1544411960913](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544411960913.png)



### BeanNameAutoProxyCreator举例：

对所有以dao结尾的bean的所有方法使用代理

缺点是：必须对所有指定类的所有方法进行代理，如果先对某些类里面的某些方法进行代理的话，只能用下面的。

### DefaultAdvisorAutoProxyCreator举例：





# Spring的AspectJ实现AOP

## AspectJ简介：

![1544424684988](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544424684988.png)



## AspectJ的通知类型介绍：

![1544426201025](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544426201025.png)



## AspectJ的注解开发AOP：切入点表达式的定义

![1544426493418](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544426493418.png)

execution括号里面的第一个*号表示的是任意的返回值



### @Before前置通知

![1544427354384](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544427354384.png)



### @AfterReturning后置通知

![1544427635216](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544427635216.png)



### @Around 环绕通知

![1544428009921](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544428009921.png)



### @AfterThrowing 异常抛出通知

![1544428104727](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544428104727.png)



### @After 最终通知

![1544435850779](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544435850779.png)



## 通过@Pointcut为切点命名

![1544439997695](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544439997695.png)



# JDBC Template

![1544441378500](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544441378500.png)



![1544441439020](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544441439020.png)



![1544441540894](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544441540894.png)



![1544441801156](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544441801156.png)



## update和batchUpdate：

![1544442671458](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544442671458.png)

Update方法中的int返回值代表的是影响的行数，注意此处的重载

另外调用批量增删改操作在商城项目中是很常见的



![1544445254336](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544445254336.png)

## 优缺点分析：

![1544446711711](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544446711711.png)





# 事务处理

## 事务的概念：

![1544447857026](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544447857026.png)

## 事务的特性：

![1544448071237](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544448071237.png)

- 一致性必须在原子性的基础上才能进行，比如下了一个订单，订单数量为苹果1个，在库存那张表里面苹果数量减少了2个，虽然两条sql语句都符合原子性，但是不符合一致性
- 由于隔离性的存在数据库里面都会设置隔离级别

## Mysql事务处理：

### Mysql基本语句：

![1544492229215](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544492229215.png)



### 并发问题：

![1544492706533](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544492706533.png)

脏读解决方式：==只能读取永久性的数据，不能读取内存中的数据==



![1544492736443](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544492736443.png)



不可重复读解决方式：==锁行==



![1544492766662](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544492766662.png)

幻读解决方式：==锁表（锁行是解决不了的，因为两个事务操作的不是同一行）==



### 事务隔离级别：

![1544493242682](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544493242682.png)



## JDBC事务处理：

### 基本语句：

![1544497351101](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544497351101.png)

JDBC是基于一个Connection对象的多个sql语句才能封装成一个事务，不同的Connection对象不能封装成一个事务。



```java
connection.setAutoCommit(false);
Statement statement = connection.createStatement();
statement.execute("insert into orders values('100002','100001',2,2499,now(),null,null,'刘备','1330000000','成都','待发货')");
statement.execute("update products set stck=stock-2 where id='100001'");
statement.close();
connection.commit();
```

上面的代码中这个connection中把==setAutoCommit的属性变为false==之后，后面不管有多少个sql语句都是一个事务了，直到有==connection.commit();==的出现才能把这个事务结束。



![1544529336842](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544529336842.png)



## Spring事务处理：

### 基本概念：

![1544529636318](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544529636318.png)

紫色的是接口，蓝色的是实现类

接口：

- PlatformTransactionManager（事务管理器）
- TransactionDefinition（事务定义）          用户要求Spring开启一个什么特点什么属性的一个事务
- TransactionStatus（事务状态）

实现类：

DataSourceTransactionManager：使用JDBC、JDBC Template、Mybatis

HibernateTransactionManager：Hibernate框架

JpaTransactionManager：Jpa模式



![1544530270037](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544530270037.png)

![1544530283809](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544530283809.png)



```java
public void a(){
    //begin
    //步骤
    b();
    //commit
}
public void b(){
    //步骤
}
```

Spring事务传播行为就是在一个方法中调用另外一个方法的事情



### Spring的编程式事务处理的两种方式：

![1544531936874](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544531936874.png)



### Spring的声明式事务处理的四种方式：

![1544532567865](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544532567865.png)



![1544532651600](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1544532651600.png)

- 第一种是基于拦截器
- 第二种是简化拦截器
- 第三种是把就简化拦截器中的每次都要为一个bean对象设置一个TransactionProxyFactoryBean的方式修改成简化的方式

后面两种方式才是开发中比较常用的，最流行的就是第四种方式。