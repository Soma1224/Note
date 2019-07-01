



# Spring入门

注入的方式（@Autowired）：

- 方法参数注入
- 字段注入
- setter方法注入
- 普通方法注入
- 构造器注入









# Spring Boot微信点餐系统

![1542963629169](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542963629169.png)







![1542963710939](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542963710939.png)







![1542963974579](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542963974579.png)







![1542964051006](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542964051006.png)









![1542964102435](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542964102435.png)





![1542964183371](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542964183371.png)





![1542965011365](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542965011365.png)





![1542965088213](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542965088213.png)



## 开发环境搭建

要保证虚拟机和本机的ip能够ping的上，即处于同一个网段



- 在虚拟机上新建数据库，选择mb4的目的是能够保存微信的表情

![1543309178396](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543309178396.png)



## 日志的选择

![1543310371785](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543310371785.png)

![1543310412042](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543310412042.png)





这里选择Logback



## 日志的使用

首先要引入

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>
```

其次需要安装lombok插件

![1543318174038](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543318174038.png)







- Logback的配置

![1543317443814](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543317443814.png)

application.yml进行的是简单的配置，而logback-spring.xml开源进行一些复杂的配置



application.yml如下：

```yml
logging:
  pattern:
    console: "%d - %msg%n"
#  path: /var/log/tomcat/
  file: /var/log/tomcat/sell.log
  level:
    com.imooc.LoggerTest: debug
```





比如有一下需求：

![1543317608578](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543317608578.png)

logback-spring.xml如下：

```yml
<?xml version="1.0" encoding="UTF-8" ?>

<configuration>

    <!--控制台的输出-->
    <appender name="consoleLog" class="ch.qos.logback.core.ConsoleAppender">
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>
                %d - %msg%n
            </pattern>
        </layout>
    </appender>

    <!--配置输出的INFO文件-->
    <!--因为要每天都生成日志文件，所以要滚动输出-->
    <appender name="fileInfoLog" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!--
            为了不让info这边输出error的日志的话，如果还是使用过滤器只想过滤info资源的话，
            error也会被输出出来，因为error的级别比info高，所以要用到LevelFilter
        -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>DENY</onMatch>
            <onMismatch>ACCEPT</onMismatch>
        </filter>
        <encoder>
            <pattern>
                %msg%n
            </pattern>
        </encoder>
        <!--滚动策略-->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--路径-->
            <fileNamePattern>E:\Java-Develop/var/log/tomcat/sell/info.%d.log</fileNamePattern>
        </rollingPolicy>
    </appender>


    <!--配置输出的ERROR文件-->
    <appender name="fileErrorLog" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!--根据范围来配置，error只希望输出error级别的日志-->
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <level>ERROR</level>
        </filter>
        <encoder>
            <pattern>
                %msg%n
            </pattern>
        </encoder>
        <!--滚动策略-->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--路径-->
            <fileNamePattern>E:\Java-Develop/var/log/tomcat/sell/error.%d.log</fileNamePattern>
        </rollingPolicy>
    </appender>

    <root level="info">
        <appender-ref ref="consoleLog" />
        <appender-ref ref="fileInfoLog" />
        <appender-ref ref="fileErrorLog" />
    </root>

</configuration>
```



日志的级别：

![1543319423926](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543319423926.png)

如果还是使用过滤器只想过滤info资源的话，error也会被输出出来，因为error的级别比info高，所以要用到LevelFilter



## 买家类目

安装或lomok插件并引入依赖后，就可以进行买家类目的单元测试



**买家类目类：**

```java
package com.david.dataobject;

import lombok.Data;
import org.hibernate.annotations.DynamicUpdate;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import java.util.Date;

/**
 * 类目
 * Created by 廖师兄
 * 2017-05-07 14:30
 */
@Entity
//这个注解是使mysql里面的属性自动增长的
@DynamicUpdate
//lombok中的getter,setter和tostring方法的补充（即类中已经不需要写了）
@Data
public class ProductCategory {

    /** 类目id. */
    @Id
    @GeneratedValue
    private Integer categoryId;

    /** 类目名字. */
    private String categoryName;

    /** 类目编号. */
    private Integer categoryType;

    private Date createTime;

    private Date updateTime;

    public ProductCategory() {
    }

    public ProductCategory(String categoryName, Integer categoryType) {
        this.categoryName = categoryName;
        this.categoryType = categoryType;
    }


}
```



**买家类目类执行方法接口：**

```java
package com.david.repository;

import com.david.dataobject.ProductCategory;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.List;

/**
 * Created by 廖师兄
 * 2017-05-07 14:35
 */
public interface ProductCategoryRepository extends JpaRepository<ProductCategory, Integer> {

    List<ProductCategory> findByCategoryTypeIn(List<Integer> categoryTypeList);
}
```



**单元测试类：**

```java
package com.david.repository;

import com.david.dataobject.ProductCategory;
import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import java.util.Arrays;
import java.util.List;


@RunWith(SpringRunner.class)
@SpringBootTest
public class ProductCategoryRepositoryTest {

    @Autowired
    private ProductCategoryRepository repository;

    @Test
    public void findOneTest()
    {
        ProductCategory productCategory = repository.findOne(1);
        System.out.println(productCategory.toString());
    }

    @Test
    //我们希望测试完后数据库是干净的，是没有我们测试的数据的
    //这个事务在service层里面如果抛出异常的话就回滚，但是在测试类中是完全回滚的
    @Transactional
    public void saveTest()
    {
        ProductCategory productCategory=new ProductCategory();
        productCategory.setCategoryName("女生最爱");
        productCategory.setCategoryType(3);
        ProductCategory result = repository.save(productCategory);
        Assert.assertNotNull(result);
        //Assert.assertNotEquals(null,result);
    }

    @Test
    public void updateTest()
    {
        ProductCategory productCategory=repository.findOne(2);
        productCategory.setCategoryType(10);
        repository.save(productCategory);
    }

    @Test
    public void findByCategoryTypeInTest()
    {
        List<Integer> list= Arrays.asList(2,3,4);
        List<ProductCategory> reult=repository.findByCategoryTypeIn(list);
        Assert.assertNotEquals(0,reult.size());
    }


}
```





## 买家商品：

- 遇到的问题一：

![1543376448741](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543376448741.png)

![1543376466942](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543376466942.png)



- 值得注意的问题一：

值得提醒的一点：数据库的查询不要放到for循环中去查询，这样花费的时间和内存开销都很大。



- 遇到的问题二：

![1543384775198](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543384775198.png)

![1543384790512](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543384790512.png)

反思：linux操作不太熟悉，这里面涉及到的linux操作

![1543384962449](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543384962449.png)

![1543385004296](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543385004296.png)





- **虚拟机前端页面与后端代码联调**

修改nginx的配置

![1543389901090](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543389901090.png)



![1543389965587](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543389965587.png)

重启nginx

![1543390065401](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543390065401.png)



![1543389993468](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543389993468.png)



![1543390022619](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543390022619.png)







## 买家订单:

如果需要查看result里面的内容的话需要在合适的地方添加断点，然后再进行查看

![1543392468293](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543392468293.png)

![1543392446933](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543392446933.png)





## 买家订单-service创建：

关于OrderServiceImpl的话，入参肯定是OrderDTO，service层就是由controller层调用的，controller层不可能把所有OrderDTO参数都传递过来，例如订单的总金额和OrderDetail中的单价（尤其是这个不能从前端传过来，只能去数据库读取）



## 微信特性：











## 卖家订单：











## webSocket消息推送：

1. 引入webSocket的依赖：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```



2. 配置webSocket：

```java
package com.david.config;

import org.springframework.context.annotation.Bean;
import org.springframework.web.socket.server.standard.ServerEndpointExporter;

/**
 * Created by 廖师兄
 * 2017-07-30 23:17
 */
//@Component
public class WebSocketConfig {

    @Bean
    public ServerEndpointExporter serverEndpointExporter() {
        return new ServerEndpointExporter();
    }
}
```











# Spring Boot进阶之web进阶

## 表单验证

提出问题：

我们在遇到女生年龄小于18岁的时候就禁止调用表单，不让它添加进数据库

就需要使用表单验证：**@Valid**



## AOP技术：

AOP：面向且切面编程，将面向对象所创建的庞大的类的体系进行水平的切割，并且把影响了很多类的公共行为封装成一个可重用的模块，将通用的逻辑从业务逻辑中分离出来

![1543829056588](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1543829056588.png)



### 实例操作：

1. 添加依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

2. 创建aspect文件夹下面的HttpAspect类

```java
package com.imooc.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.*;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import org.springframework.web.context.request.RequestContextHolder;
import org.springframework.web.context.request.ServletRequestAttributes;

import javax.servlet.http.HttpServletRequest;

/**
 * Created by 廖师兄
 * 2017-01-15 12:31
 */
@Aspect
@Component
public class HttpAspect {

    private final static Logger logger = LoggerFactory.getLogger(HttpAspect.class);


    @Pointcut("execution(public * com.imooc.controller.GirlController.*(..))")
    public void log() {
    }

    @Before("log()")
    public void doBefore(JoinPoint joinPoint) {
        ServletRequestAttributes attributes = (ServletRequestAttributes) RequestContextHolder.getRequestAttributes();
        HttpServletRequest request = attributes.getRequest();

        //url
        logger.info("url={}", request.getRequestURL());

        //method
        logger.info("method={}", request.getMethod());

        //ip
        logger.info("ip={}", request.getRemoteAddr());

        //类方法
        logger.info("class_method={}", joinPoint.getSignature().getDeclaringTypeName() + "." + joinPoint.getSignature().getName());

        //参数
        logger.info("args={}", joinPoint.getArgs());
    }

    @After("log()")
    public void doAfter() {
        logger.info("222222222222");
    }

    @AfterReturning(returning = "object", pointcut = "log()")
    public void doAfterReturning(Object object) {
        logger.info("response={}", object.toString());
    }

}
```



