# Mybatis

## Mybatis参数问题

### 单个基本数据类型

如果仅仅是一个简单的单值传入，那么#{}中写什么都可以~





### 多个基本数据类型入参问题

- mybatis把参数定义为arg0，arg1.......或者是param1，param2.....

```java
select * from girl where name=#{arg0} and flower=#{agr1}
select * from girl where name=#{param1} and flower=#{param2}
```

故推荐使用

```java
Girl queryByNameFlower(@Param("name") String name,@Param("flower") String flower);
```



### 单个JavaBean

- 默认通过javabean里面的属性的名称去引用，通过getter方法去获取这些值，所以只能用属性名称



### Map

```java
Girl queryByMap(Map<String,Object> map);
```

按照这种方式封装，就是按照键的名称进行取值



### 多个JavaBean

```java
Girl queryByAB(@Param("a")A a,@Param("b")B b);
```









## 日志log4j

- 在Mybatis官方网站上查看日志配置

## 缓存（cache）

- 一级缓存是Session级别的（只有在同一个会话中才有效），二级缓存是SessionFactory级别的
- 如果开启了二级缓存，先去二级缓存中尝试命中，如果无法命中，尝试去一级缓存中命中，还不命中，再去数据库中查询，默认的一级缓存是开启的
- 缓存失效方式一：如果查询之后进行了增删改查的行为，会导致缓存失效



















