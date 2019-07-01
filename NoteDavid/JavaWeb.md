

# JavaWeb

## 动态网页技术

- servelt/jsp
- asp
- php

## servlet简介

servlet是单实例的（init和destroy方法），天然支持多线程（service方法）

## 数据传入和解析问题

- form表单可以传递数据，以name为准，后台通过请求getParameter或者getParameterValues获取
- url直接拼接参数传递

单个数据

```java
http://localhost:8080/abc/get/param?girl=fei
```

多个数据

```java
http://localhost:8080/abc/get/param?girl=fei&girl2=hanxue
```

## Spring

添加依赖，一般只要引入context的话，其余都会成功引入

```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>5.0.8.RELEASE</version>
</dependency>
```

applicationContext.xml配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--将对象的创建交给spring容器，在这个配置文件里面去声明我要什么对象
        class：写java的全限定类名，它是通过全类名然后使用反射的技术创建的
        id：ID就是给这个对象在整个应用程序上下文当中取个名字以方便区分
    -->
    <bean class="com.david.pojo.Girl" id="girl">

    </bean>
    
</beans>
```

pojo

```java
package com.david.pojo;

public class Girl {

    private String name;
    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }
}
```

测试：

```java
package com.david;

import com.david.pojo.Girl;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;



public class TestSpring {
    @Test
    public void m1()
    {
        //获取上下文对象，spring里声明对象都需要通过上下文获取
        ApplicationContext ctx=new ClassPathXmlApplicationContext("applicationContext.xml");

        //通过这个对象获取我们的gril
        Girl g=(Girl)ctx.getBean("girl");
        System.out.println(g);

    }
}
```

### 普通编写 VS spring方式

​       普通的获取对象方式，所有对象的依赖，类之间的依赖关系都是在java代码里面维护的，很难维护，有替换方案的话也是比较困难的

​	spring对象的产生全部是在配置文件里面完成的，易于管理

### 值的注入

- setter注入（最常用）
  - 必须其字段有对应的setter方法才可以完成，例如name setNamre
  - 通过properties子节点完成注入
- 构造注入



#### 注意两种报错的方式：

- 必须要有对应的set方法
- 默认是通过无参构造器完成对象的创建的（类中一定要有无参构造器，如果写了有参构造器，要手动加上无参构造器）

### bean元素探讨

#### 属性探讨

- abstract 该bean无法被实例化
- parent：指定它的父bean是谁，将会继承父bean的所有内容
- destroy-method：指定这个bean最后确实被销毁的时候一定要执行的方法，适用于清理性工作
  - 容器close会触发
  - refresh时会触发
  - 过时的destroy方法也会触发
- init-method：指定bean的初始化方法
- name：别名，与id有所区别，id只能是唯一的，而name可以是多个，彼此分割可以用：空格或者是逗号
- scope：指定范围
  - singleton：单例，==spring上下文==当中，只有一个实例（注意不是整个项目的上下文）
  - prototype：原型，要一个就新给一个
- lazy-init：
  - ==默认情况下，所有的bean都是容器初始化完毕就立刻注入的==
  - true的话spring不会一上来就直接初始化bean
- depends-on：依赖的bean，使用情况：如果某一个bean的使用严重依赖另外一个的话，就可以配置该参数，==初始化的时候会有先后关系==

#### 对于非字面值可以描述的值的注入问题

### spring当中各种值的注入

- 数组

```xml
<property name="friends">
    <array>
        <value>刘德华</value>
        <value>郭富城</value>
        <value>黎明</value>
        <value>张学友</value>
    </array>
</property>
```



- List

  普通值

```xml
<property name="nums">
    <list>
        <value>8</value>
        <value>7</value>
    </list>
</property>
```

​       类

```xml
<property name="cats">
    <list>
        <!--内部bean无法被外部引用，所以无需ID-->
        <bean class="com.david.pojo.Cat">
            <property name="leg" value="2"/>
            <property name="skin" value="蓝色"/>
        </bean>
        <bean class="com.david.pojo.Cat">
            <property name="leg" value="4"/>
            <property name="skin" value="青色"/>
        </bean>
    </list>
</property>
```

- Set

```xml
<property name="pigs">
    <set>
        <bean class="com.david.pojo.Pig">
            <property name="name" value="佩奇"/>
            <property name="sleep" value="88"/>
            <property name="kw" value="香辣"/>

        </bean>
        <bean class="com.david.pojo.Pig">
            <property name="name" value="小宝"/>
            <property name="sleep" value="99"/>
            <property name="kw" value="酱香"/>

        </bean>
    </set>
</property>
```



- Map

```xml
<property name="users">
    <map>
        <entry key="user1">
            <bean class="com.david.pojo.User">
                <property name="name" value="韩雪"/>
                <property name="address" value="梧桐村"/>
            </bean>
        </entry>
        <entry key="user2">
            <bean class="com.david.pojo.User">
                <property name="name" value="凌青霞"/>
                <property name="address" value="台湾"/>
            </bean>
        </entry>
    </map>
</property>
```



==如果其对应的是简单的字面值，就直接写就可以了，如果是一个其他的类，那么使用内部bean的方式去完成，内部bean无法被外部引用，所以无需ID==



### 自动注入

- byType：按照数据类型注入

==byType是根据类型进行注入的属性，此时在上下文当中搜索Pig这种bean，找到有且仅有一个的情况下，将会注入成功，如果一个都没有，则不注入，如果不止一个，将会有异常，所以只能一个primary属性为true==

```xml
<bean class="com.david.pojo.User" id="user" autowire="byType">
    <property name="name" value="陈慧琳"/>
    <property name="address" value="香港"/>
</bean>

<bean class="com.david.pojo.Pig" primary="true">
    <property name="name" value="大宝"/>
</bean>


<bean class="com.david.pojo.Pig" primary="false">
    <property name="name" value="举大宝"/>
</bean>
```

- byName：==按照bean对应的pojo里面的属性的名字进行匹配，bean标签里面id和name都可以==

```xml
<bean class="com.david.pojo.User" id="user" autowire="byName">
    <property name="name" value="陈慧琳"/>
    <property name="address" value="香港"/>
</bean>

<!--也就是说private Pig pig中的pig叫什么，这里就和name或者id进行匹配-->

<bean class="com.david.pojo.Pig" name="pig">
    <property name="name" value="大宝"/>
</bean>
```

- constructor

带有两个参数的构造函数

```java
public User(String name, Pig pig) {
    this.name = name;
    this.pig = pig;
}
```



```xml
<bean class="com.david.pojo.User" autowire="constructor" id="user">
    <constructor-arg name="name" value="韩红"/>
</bean>



<bean class="com.david.pojo.Pig" name="pig1">
    <property name="name" value="大宝"/>
</bean>


<bean class="com.david.pojo.Pig" id="pig2">
    <property name="name" value="举大宝"/>
</bean>
```

此时是报错的，因为没有一个名字叫pig

==首先按照类型去匹配，如果匹配到了一个，而且这个类型是唯一的，那么直接注入，不止一个的情况下按照构造器里面属性的名字进行匹配，例如上面就是找pig的这个名字，进行注入，如果一个都找不到，注入失败==

- default
- no

### 零碎的知识点

- 如何引入外部properties文件

```xml
<context:property-placholder location="classpath:database.properties"/>
```

- 如何通过表达式引用外部properties的键值

```xml
<property name="driver" value="${driver}"/>
<property name="url" value="${url}"/>
<property name="user" value="${user}"/>
<property name="password" value="${password}"/>
```



- 从一个配置文件引入多个spring文件

```xml
<import resources="classpath:spring/spring-*.xml"/>
```



- 配置扫描包

```xml
<!--激活注解
	扫描包是扫描包以及子包所有
-->
<context:component-scan base-package-"com.david.Service">
    <!--这个包下面的repository这种注解不扫描-->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Repository"/>
</context:component-scan>
```



### springAOP

面向切面编程

#### XML版本的实现过程

- 额外添加的依赖

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjrt -->
<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjrt</artifactId>
  <version>1.9.1</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjweaver</artifactId>
  <version>1.9.1</version>
</dependency>
```



- 配置文件

```xml
    <!--aop是基于代理完成的，所以我们要激活我们的自动代理-->
    <aop:aspectj-autoproxy/>
    
    <!--注册一个切面-->
    <bean class="com.david.advice.BeforeAdvice" id="beforeAdvice">

    </bean>

    <bean class="com.david.Service.ProviderService1" id="providerService1">

    </bean>

    <bean class="com.david.advice.AfterAdvice" id="afterAdvice">

    </bean>

    <!--配置我们的切入点-->
    <aop:config>
        <aop:aspect id="beforeAspect" ref="beforeAdvice">
            <!--aop:before表明是前置通知
                method表明它使用beforeAdvice的哪个方法来切
                pointcut：切入点 表明需要切什么包下的什么类的什么方法
                Service.*.*(..)
                第一个*表示service下的任意的类
                第二个*表示任何的方法名
                (..)表示任意参数
            -->
            <aop:before method="methodBefore" pointcut="execution(* com.david.Service.*.*(..))"></aop:before>
        </aop:aspect>

        <aop:aspect id="afterAspect" ref="afterAdvice">
            <!--
                execution(* com.david.Service.*.*(..)) 切无参
                execution(* com.david.Service.*.*(java.lang.String)) 切参数为一个且为String类型的方法
                execution(* com.david.Service.*.*(java.lang.String,int)) 切参数为一个且为String类型和int类型的方法
            -->
            <aop:after method="after" pointcut="execution(* com.david.Service.*.*(java.lang.String,int))"></aop:after>
        </aop:aspect>
    </aop:config>
    
</beans>
```







![Snipaste_2018-10-15_18-30-23](F:\Typora文件\Typora文件 公司电脑\图片\Snipaste_2018-10-15_18-30-23.png)







#### 注解版的实现过程



com下的任何子包（无论多少层）下的任何类的任何方法都可以切到

```java
execution(* com..*.*.*(..))
```

在com包及其子包（无论多少层）下面的任何类的任何方法都可以切到

```java
execution(* com.*.*.*(..))
```



### springMVC

#### 简介

何谓mvc？

model          模型

view              视图

controller     控制器



是一种设计模式

好处

- 结构清晰
- 更好维护

坏处

- 更加复杂





























































