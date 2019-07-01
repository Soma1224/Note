# SpringMVC



![mvc](.\picture\%5CUsers%5Clenovo%5CDesktop%5Cmvc.png)



## SpringMVC分析

### 创建一个简单的SpringMVC项目

![1541323989348](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541323989348.png)





### springMVC配置文件名字的问题

web.xml                                             部署描述符

springmvc-servlet.xml                    springmvc的配置文件





默认情况下是用dispatcherServlet的名字当作命名空间

[servletName(==这里是前端控制器DispatcherServlet的名字==)]-servlet.xml(WEB-INF)之下寻找

[servletName(==这里是前端控制器DispatcherServlet的名字==)]-servlet=namespace

如果非要使用自己喜欢的名字的话，可以在web.xml中配置namespace

![1541420966532](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541420966532.png)

```xml
<init-param>
  <param-name>namespace</param-name>
  <param-value>mvc</param-value>
</init-param>
```

配置完之后，springMVC配置文件名字就可以写成==mvc.xml==

- 默认的规则要求在WEB-INF下，但是maven项目的标准应该在resources下面，如何解决这个问题？

重新指定上下文的配置文件的位置即可

![1541421552240](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541421552240.png)

```xml
<init-param>
  <!--上下文配置文件的指定-->
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:springmvc.xml</param-value>
</init-param>
```

这种情况下是在类路径下去寻找是springmvc.xml这个配置文件，推荐使用（位置自己指定，名字自己指定）



### 视图解析器

springmvc支持多种视图技术

- jsp
- freemaker（模板技术）

内部的资源视图解析器

- 视图前缀
  - /jsp/它是我们的请求响应的资源的路径配置             例如viewName(视图名称)：girl
- 后缀
  - .jsp  此时我们的前缀+视图名称+后缀  =  /jsp/girl.jsp

![1541422071327](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541422071327.png)

物理视图由逻辑视图转换而来

物理视图是webapp/jsp/girl.jsp



逻辑视图是

- prefix
- logicViewName
- suffix



故物理视图 = prefix + logicViewName + suffix（由dispatcherServlet完成从物理视图到逻辑视图的转换）



## 注解开发模式

基于实现接口的方式已经是过去式了，现在采用注解开发

基本注释

- @Controller
- @RequestMapping

![1541424637747](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541424637747.png)

划红线的是官网spring用谷歌浏览器搜索xmlns:context得到的结果

![1541424665753](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541424665753.png)



开发步骤：

1. 配置一下基础扫描包，这样注解才会生效
2. 在指定的类上面添加@controller注解
3. 添加@RequestMapping（不同requesthandler处理的HandlerMapping）



当我们写上@Controller之后，就把它标记为一个spring的控制器组件，此时handlermapping会去扫描这个controller是否与之匹配，如果匹配就把工作交给它

匹配地规则是：

具体的匹配就是通过请求的路径进行匹配的

@RequestMapping（URL）

就是通过这个URL路径进行匹配的

![1541490540561](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541490540561.png)



==@RequestMapping可以写在方法上，也可以写在类上（推荐二者结合的方式）==

![1541494177235](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541494177235.png)









这种jsp里面需要foreach的东西需要在pom.xml中引入jstl的依赖

![1541494070167](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541494070167.png)









具体的开发步骤：

![1541494029949](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541494029949.png)



转发和重定向

- 转发到页面
- 重定向到页面
- 转发到另外一个控制器



![1541504174508](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541504174508.png)



重定向的话需要标识符前缀==redirect/==来表示这个方法属于重定向问题

![1541504185105](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541504185105.png)



==转发到另外一个控制器==



![1541504844063](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541504844063.png)



![1541504995957](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541504995957.png)





### 关于springmvc访问web元素

- request
- session
- application

可以通过模拟对象完成操作，也可以使用原生的ServletAPI完成，直接在方法里面入参即可。



![1541506616753](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541506616753.png)



![1541506645249](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541506645249.png)



### 注解详解

#### ==@RequestMapping==

- value写的是路径，写的是数组的形式，可以匹配多个路径
- path是value的别名，作用一样

![1541507716815](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541507716815.png)

![1541507728030](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541507728030.png)

- method

![1541508075932](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541508075932.png)

![1541508056351](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541508056351.png)



在form表里的action怎么写？如果向项目部署的名称被修改了怎么办？

答：利用servlet的生命周期的特点来完成上下文初始化的工作，这个类的触发的生命周期是非常早的，仅次于容器tomcat和dispatcherServlet

![1541510127772](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541510127772.png)



![1541510169499](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541510169499.png)



![1541510231113](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541510231113.png)



由于form是post和m1是get不是对应的，所以form请求无效



- param         可以去指定参数，你还可以去限定这个参数的特征，必须等于某个值，不等于某个值的话，就会访问不到，报错：bad Request
- header    能够影响浏览器的行为
- consumer   媒体类型，可以限定必须为application/json;charset=UTF-8
- produces     产生的响应类型



#### 关于请求风格

springmvc主持ant风格

- ？                         任意字符，斜杠除外，例如$/m3?$
- $*$                           0到任意个字符都可以，不能含有斜杠，例如$/m3*$
- $**$                         支持任意层路径，要写成$/m3/**$，这样才可以体现出来





#### @GetMapping，@PostMapping

- @GetMapping              相当于把requestMapping里面的method指定为get
- @PostMapping             同理





#### 对于非get和post的请求的支持

对于非get和post的请求的支持，例如：delete和put请求，需要添加一个过滤器来额外处理

- 过滤器
- 返回的不再是页面而是数据

```xml
<!--注册一个支持所有http请求的过滤器-->
<filter>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

- 表单提交里面还要添加一个隐藏的参数



#### 关于静态资源访问的问题

由于我们的servlet设置了URL匹配方式为/ ，所以，它将静态资源也当作一个后台的请求，比如

```xml
http://localhost:8080/abc/static/css/index.css
```

它尝试去匹配一个static/css/index.css的controller里面的RequestMapping的组合，因为没有，所以报了404，解决方式：

让springmvc单独处理，将这些交给容器默认的servlet处理，不让DispatcherServlet处理

- 解决方式1（最为推荐）

```xml
<!--默认的servlet处理者-->
<mvc:default-servlet-handler/>
<!--但是只加上它一个的话相当于全部交给它处理了,所以要加上后面的这句话-->
<mvc:annotation-driven/>
```

- 解决方式2

通过映射关系描述，一一对应编写规则

```xml
<mvc:resources mapping="/static/css/*" location="static/css/"/>
```

- 解决方式3

自行在web.xml定义映射规则



#### @PathVariable

restful风格

![1541671892720](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541671892720.png)



#### @Responsebody

==用于返回数据==，一般情况下返回的是JSON格式



#### @ModelAttribute

==使用方式一：==

```java
@Controller
@RequestMapping("/user2")
public class UserController2 {

    //就是在controller里面的任意一个处理具体方法之前都会执行
    @ModelAttribute
    public User init()
    {
        System.out.println("init......");
        User u=new User();
        u.setName("王菲");
        return u;
    }

    @RequestMapping("/login")
    public String login(Model model)
    {
        System.out.println(model.containsAttribute("u"));
        System.out.println(model.containsAttribute("user"));
        System.out.println(model.containsAttribute("sdfsf"));

        return "msg";
    }
}
```

如果某些对象在每次请求中从头到尾都要存在的话，就适合这么使用



==使用方式二：==

```java
//就是在controller里面的任意一个处理具体方法之前都会执行
@ModelAttribute
public void init(Model model)
{
    System.out.println("init......");
    User user=new User();
    user.setName("王菲");
    model.addAttribute("user",user);
}
```

返回值是void的写法，和方式一类似，方式一和方式二的login方法无论你jsp里面输入的是什么都会返回“王菲”

```java
@RequestMapping("/login")
public String login(Model model)
{
    System.out.println(model.containsAttribute("u"));
    System.out.println(model.containsAttribute("user"));
    System.out.println(model.containsAttribute("sdfsf"));

    return "msg";
}
```





==**使用方式三：**==

这种方式的话把@ModelAttribute加在参数前面，这样jsp里面输入是什么，显示的就是什么，如果jsp里面什么都不输入的话，显示的就是”王菲“

```java
@Controller
@RequestMapping("/user2")
public class UserController2 {

    //就是在controller里面的任意一个处理具体方法之前都会执行
    @ModelAttribute
    public void init(Model model)
    {
        System.out.println("init......");
        User user=new User();
        user.setName("王菲");
        model.addAttribute("user",user);
    }

    

    @RequestMapping("/login")
    public String login(@ModelAttribute User user)
    {
        System.out.println(user.getName()+user.getPassword());
        return "msg";
    }
}
```



#### @SessionAttributes

**==原理：==**

　默认情况下Spring MVC将模型中的数据存储到request域中。当一个请求结束后，数据就失效了。如果要跨页面使用。那么需要使用到session。而@SessionAttributes注解就可以使得模型中的数据存储一份到session域中。











#### @SessionAttribute

要求当前这次访问中的会话中间必须要有这个对象

**==原理：==**



#### @CookieValue

**==原理：==**







### 关于post请求中文乱码问题的解决

我们添加了一个过滤器即可，SpringMvc提供了一个很好的字符编码过滤器，注册即可

```xml
<filter>
  <filter-name>characterEncodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <!--指定字符编码-->
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
  <init-param>
    <param-name>forceRequestEncoding</param-name>
    <param-value>true</param-value>
  </init-param>
</filter>
```



### 关于form表单提交数据的方式

==**方式一：通过属性名字进行绑定**==

通过属性的名称进行绑定，可以完成数据的传递，页面当中表单元素的name值要和后台的形参名字保持一致

如果有多个形参，按名字绑定即可

![1541768553827](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541768553827.png)



![1541768580098](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541768580098.png)



==**方式二：利用@RequestParam**==

jsp页面不变

后台改变如下

![1541769007820](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541769007820.png)



==**方式三：直接使用pojo形式进行传递**==

jsp页面不变

后台改变如下

适合于参数很多的情况

```java
@Controller
@RequestMapping("/user")
public class UserController {


    @PutMapping("/put")
    @ResponseBody
    public String put(User user)
    {
        System.out.println(user.getName()+" "+user.getPassword());

        return "ok";

    }

}
```



### 关于form表单提交日期格式数据处理的问题

- 处理日期（没有时间）

```java
package com.david.controller;

import com.david.pojo.User;
import org.springframework.beans.propertyeditors.CustomDateEditor;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.WebDataBinder;
import org.springframework.web.bind.annotation.*;


import java.text.SimpleDateFormat;
import java.util.Date;

@Controller
@RequestMapping("/user")
public class UserController {


    @InitBinder("user")
    public void init(WebDataBinder binder)
    {
        //这里指定什么格式，前台就只能传递格式
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
        dateFormat.setLenient(false);
        binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));

    }

    @PutMapping("/put")
    @ResponseBody
    public String put(@ModelAttribute("user") User user)
    {
        System.out.println(user.getName()+" "+user.getPassword());

        System.out.println(user.getBirth());
        return "ok";

    }

}
```



```java
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <form action="${david}/user/put" method="post">
            <input type="hidden" name="_method" value="put">
            <input type="text" name="name"><br>
            <input type="password" name="password"><br>
            <input type="Date" name="birth"><br>
            <input type="submit" value="提交">
        </form>
        
    </body>
</html>
```

注意User类中的Date类型的变量名称要和put.jsp中的变量名称一致，另外注意patten的写法，必须这么写，不能写成yyyy/MM/dd

![1541915079092](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541915079092.png)

![1541915103528](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541915103528.png)

- 没有指定以下名称，根据数据类型也可以匹配成功（红色框内地内容可以删除，所能达到地效果也是一致的）

![1541915312900](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541915312900.png)



- 处理日期加上时间（在原有代码上改变两处即可）

![1541915542208](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541915542208.png)



![1541915563176](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541915563176.png)





## Json数据交互

### 额外依赖

```xml
    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.3</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.9.3</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-annotations</artifactId>
      <version>2.9.3</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/net.sf.json-lib/json-lib -->
    <dependency>
      <groupId>net.sf.json-lib</groupId>
      <artifactId>json-lib</artifactId>
      <version>2.4</version>
      <classifier>jdk15</classifier>
    </dependency>


    <!--添加处理json为javabean-->
    <!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-core-asl -->
    <dependency>
      <groupId>org.codehaus.jackson</groupId>
      <artifactId>jackson-core-asl</artifactId>
      <version>1.9.2</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-mapper-asl -->
    <dependency>
      <groupId>org.codehaus.jackson</groupId>
      <artifactId>jackson-mapper-asl</artifactId>
      <version>1.9.2</version>
    </dependency>

```

另外记得添加

```xml
<!--激活springmvc的消息转换功能-->
<mvc:annotation-driven></mvc:annotation-driven>
```



### @RestController

==@RestController=@Controller+@Responsebody==





### JSON数据返回前台如何解析

#### JSON后台返回

1.返回POJO

```java
@RequestMapping("/m1")
@ResponseBody//这个注解将知道现在返回的不是视图，它会将这个数据转换为Json格式
public User m1()
{
    User u=new User();
    u.setName("许晴");
    u.setPassword("123");
    return u;
}
```



2.返回map

```java
@RequestMapping("/m2")
@ResponseBody
public Map<String,Object> m2()
{
    Map<String,Object> map=new HashMap<>();
    map.put("name","徐倾向");
    map.put("age",29);
    return map;
}
```



3.返回数组

```java
@RequestMapping("/m3")
@ResponseBody
public User[] m3()
{
    User u=new User();
    u.setName("开玩笑");
    u.setPassword("123");

    User u2=new User();
    u2.setName("不开玩笑");
    u2.setPassword("321");

    return new User[]{u,u2};

}
```



4.返回list

```java
@RequestMapping("/m4")
@ResponseBody
public List<User> m4()
{
    List<User> list=new ArrayList<>();
    User u=new User();
    u.setName("开玩笑");
    u.setPassword("123");

    User u2=new User();
    u2.setName("不开玩笑");
    u2.setPassword("321");

    list.add(u);
    list.add(u2);
    return list;

}
```









#### JSON前台如何解析

1.引入jquery

![1542028646261](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542028646261.png)

2.编写json.jsp（解析返回的User，Map，数组，List，List<Map<String,User>>）

```xml
$(function () {
    $('#b1').click(function () {
        $.ajax({
            url:'${david}/json/m1',
            type:'post',
            success:function (data) {
                alert(data.name);
                alert(data.password);
            }
        })
    })

    $('#b2').click(function () {
        $.ajax({
            url:'${david}/json/m2',
            type:'post',
            success:function (data) {
                alert(data.name);
                alert(data.age);
            }
        })
    })

    $('#b3').click(function () {
        $.ajax({
            url:'${david}/json/m3',
            type:'post',
            success:function (data) {
                for (var i=0;i<data.length;i++)
                {
                    alert(data[i].name);
                    alert(data[i].password);
                }
            }
        })
    })

    $('#b4').click(function () {
        $.ajax({
            url:'${david}/json/m4',
            type:'post',
            success:function (data) {
                for (var i=0;i<data.length;i++)
                {
                    alert(data[i].name);
                    alert(data[i].password);
                }
            }
        })
    })

		$('#b5').click(function () {
				$.ajax({
					url:'${david}/json/m5',
					type:'post',
					success:function (data) {
							for (var i=0;i<data.length;i++)
              {
                  alert(data[i].u1.name);
                  alert(data[i].u1.password);
                  alert(data[i].u2.name);
                  alert(data[i].u2.password);
               }
            }
        })
    })	
})
```











### JSON数据如何使用Ajax提交到后台，后台如何解析

1.先指定内容格式

```js
contentType:"application/json;charset-utf-8"
```

- 前台写法

```js
<script>
    $(function () {
        $('#b1').click(function () {

            var obj={
              'name':'叶问',
              'password':'怕老婆啊'
            };

            $.ajax({
                url:'${david}/json2/add',
                type:'post',
                contentType:'application/json;charset-utf-8',
                data:JSON.stringify(obj),
                success:function (data) {

                }
            })

        })
    })

</script>
```



- 后台写法

```java
@Controller
@RequestMapping("/json2")
public class JsonController2 {

    //前台如何提交一个User回来
    @RequestMapping("/add")
    //User user入参只能处理表单提交的数据
    public String add(@RequestBody User user)
    {
        System.out.println(user.getName()+user.getPassword());
        return "msg";

    }


}
```

User user入参只能处理form表单提交数据的问题

一定要加上@RequestBody，否则无法解析



### 关于form提交数据和Ajax自定义提交JSON数据的区别

form：

![1542075496333](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542075496333.png)



Ajax：

![1542074518705](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1542074518705.png)



对于form表单提交数据来说，contentType是属于`ContentType:application/x-www-form-urlencoded`

对于ajax发送JSON数据来说contentType是属于`ContentType:application/json`



发送POJO

前台

```js
$('#b1').click(function () {

    var obj={
      'name':'叶问',
      'password':'怕老婆啊'
    };

    $.ajax({
        url:'${david}/json2/add',
        type:'post',
        contentType:'application/json;charset-utf-8',
        data:JSON.stringify(obj),
        success:function (data) {

        }
    })

})
```

后台

```java
//前台如何提交一个User回来
@RequestMapping("/add")
//User user入参只能处理表单提交的数据
@ResponseBody
public String add(@RequestBody User user)
{
    System.out.println(user.getName()+user.getPassword());
    return "msg";

}
```



发送一组POJO到后台

前台

```js
 $('#b2').click(function () {

        var obj={
            'name':'叶问',
            'password':'怕老婆啊'
        };
        var obj2={
            'name':'师傅',
            'password':'123456'
        };

        var arr=new Array();
        arr.push(obj);
        arr.push(obj2);


        $.ajax({
            url:'${david}/json2/addList',
            type:'post',
            contentType:'application/json;charset-utf-8',
            data:JSON.stringify(arr),
            success:function (data) {
                alert(data.code);
            }
        })

    })
})
```





后台

```java
RequestMapping("/addList")
//User user入参只能处理表单提交的数据
@ResponseBody
public Map<String,Integer> addList(@RequestBody List<User> list)
{
    Map<String,Integer> map=new HashMap<>();
    System.out.println(list);
    map.put("code",2000);
    return map;
}
```





## 关于项目如何实时的保存到电脑中的方式

1.clean一下

![1542071213173](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542071213173.png)



2.复制（Ctrl+C）到指定的文件夹并且命名

![1542071361863](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542071361863.png)





## xml数据交互

对于很多第三方开发，还是会采用xml进行数据交互，例如微信

1.添加额外的依赖

```xml
<!--xml额外数据处理-->
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.dataformat/jackson-dataformat-xml -->
<dependency>
  <groupId>com.fasterxml.jackson.dataformat</groupId>
  <artifactId>jackson-dataformat-xml</artifactId>
  <version>2.9.3</version>
</dependency>
```

2.方法返回数据类型定义

```java
@Controller
@RequestMapping("/xml")
public class XMLController
{
    @RequestMapping(value = "/m1",produces = {MediaType.APPLICATION_XML_VALUE})
    @ResponseBody
    public User m1()
    {
        //将数据转化为xml的格式
        User u=new User();
        u.setName("张三");
        u.setPassword("1243");
        return u;
    }
}
```

3.网页显示如下：

![%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542178714653](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1542178714653.png)





如果我想实现如下效果可以吗？

```xml
<user name="张三">
		<password>1243</password>
  	<birth></birth>
</user>
```

也就是我不把name当作子标签，把name当作属性



## 文件上传

### apache上传组件方案

1.添加依赖

```xml
<!--apache文件上传组件-->
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
<dependency>
  <groupId>commons-fileupload</groupId>
  <artifactId>commons-fileupload</artifactId>
  <version>1.3.3</version>
</dependency>
```



2.在springmvc中要注册一个文件上传解析器

```xml
<!--注册文件上传解析器
    id必须是multipartResolver，源代码已经写死了
-->
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <!--定义一个最大文件传输的大小，单位是bytes-->
    <property name="maxUploadSize" value="1024*1024"></property>
    <property name="defaultEncoding" value="UTF-8"></property>
    <!--单个文件最大上传大小-->
    <property name="maxUploadSizePerFile" value="2000000"></property>
</bean>
```



3.准备一个上传的页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <form action="${david}/file/upload" method="post" enctype="multipart/form-data">
            文件：<input type="file" name="file"><br>
            <input type="submit" value="提交">


        </form>
        
    </body>
</html>
```



4.后台处理程序

```java
@Controller
@RequestMapping("/file")
public class FileController {

    private static String uploadPath="D:"+ File.separator;

    //入参就可以代表上传的文件
    @RequestMapping("/upload")
    public String upload(@RequestParam("file")MultipartFile multipartFile, Model model)
    {
        //传到那里去 传什么东西 传的细节
        if (multipartFile!=null&&!multipartFile.isEmpty())
        {
            //获取原始的文件名称
            String originalFilename = multipartFile.getOriginalFilename();

            //截取原文件的文件名称前缀，不带后缀
            String fileNamePrefix=originalFilename.substring(0,originalFilename.lastIndexOf("."));

            //加工处理文件名，文件名称+时间戳
            String newFileNamePrefix=fileNamePrefix+new Date().getTime();

            //得到新的文件名
            String newFileName=newFileNamePrefix+originalFilename.substring(originalFilename.lastIndexOf("."));

            //构建文件对象
            File file =new File(uploadPath+newFileName);

            //上传
            try {
                multipartFile.transferTo(file);
                model.addAttribute("fileName",newFileName);

            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return "uploadSuc";
    }

}
```



如果需要上传多个文件的话需要修改的部分就是：

前台：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <%--多个文件上传--%>
            <form action="${david}/file/upload2" method="post" enctype="multipart/form-data">
                文件：<input type="file" name="file"><br>
                文件：<input type="file" name="file"><br>
                文件：<input type="file" name="file"><br>
                文件：<input type="file" name="file"><br>
                文件：<input type="file" name="file"><br>
                文件：<input type="file" name="file"><br>
                <input type="submit" value="提交">


            </form>

    </body>
</html>
```







后台：

```java
@RequestMapping("/upload2")
public String upload2(@RequestParam("file")MultipartFile[] multipartFiles, Model model)
{

    List<String> fileNames=new ArrayList<>();
    //传到那里去 传什么东西 传的细节
    if (multipartFiles!=null&&multipartFiles.length>0)
    {
        for (MultipartFile multipartFile:multipartFiles)
        {
            //获取原始的文件名称
            String originalFilename = multipartFile.getOriginalFilename();

            //截取原文件的文件名称前缀，不带后缀
            String fileNamePrefix=originalFilename.substring(0,originalFilename.lastIndexOf("."));

            //加工处理文件名，文件名称+时间戳
            String newFileNamePrefix=fileNamePrefix+new Date().getTime();

            //得到新的文件名
            String newFileName=newFileNamePrefix+originalFilename.substring(originalFilename.lastIndexOf("."));

            //构建文件对象
            File file =new File(uploadPath+newFileName);

            //上传
            try {
                multipartFile.transferTo(file);
                fileNames.add(newFileName);

            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }
    model.addAttribute("fileNames",fileNames);
    return "uploadSuc2";
}
```





## 文件下载

```java
@Controller
@RequestMapping("/download")
public class DownloadController {

    //定义一个文件下载目录
    private static String parentPath="D:"+File.separator;

    @RequestMapping("/down")
    public String down(HttpServletResponse response)
    {
        //通过输出留写到客户端，浏览器
        //1.获取文件下载名
        String fileName="毒液.mp4";

        //2.构建一个文件对象
        Path path = Paths.get(parentPath,fileName);

        //3.判断它是否存在
        if (Files.exists(path))
        {
            //存在即下载
            //通过response设定它的响应类型
            //4.获取文件的后缀
            String fileSuffix=fileName.substring(fileName.lastIndexOf(".")+1);

            //5.设置contentType，只有指定它才能去下载
            response.setContentType("application/"+fileSuffix);

            //6.添加头信息
            try {
                response.addHeader("Content-Disposition","attachment;filename="+new String(fileName.getBytes("UTF-8"),"ISO8859-1"));
            } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
            }

            //7.通过path写出去
            try {
                Files.copy(path,response.getOutputStream());
            } catch (IOException e) {
                e.printStackTrace();
            }


        }
        return "msg";
    }


}
```





## 拦截器

拦截器类似于过滤器，它将在我们的请求之前先进行检查，拦截器有权决定，接下来是否继续，拦截器还有个功能：对于我们的请求进行加工

拦截器可以设计多个



定义了三个非常重要的方法

- 前置处理
- 后置处理
- 完成处理



### 方法拦截器

通过拦截器实现方法耗时的统计和警告



- 拦截器的配置



```xml
 <mvc:interceptor>
     <!--
				"/*"的写法只能拦截/name的方法，也就是只能拦截一层，不能拦截多层
        "/**/*"能拦截任意层的URL都可以拦截
     -->
     <mvc:mapping path="/**/*"/>
     <bean class="com.david.interceptors.MethodTimerInterceptor">

     </bean>
</mvc:interceptor>
```



- 后台代码

```java
package com.david.interceptors;


import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.logging.Logger;

/**
 * 方法耗时统计的拦截器
 */


public class MethodTimerInterceptor implements HandlerInterceptor {

    //日志
    private static final Logger LOGGER=Logger.getLogger(String.valueOf(MethodTimerInterceptor.class));

    //前置功能  开始到结束，两个点减法
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //1.定义开始时间
        long start=System.currentTimeMillis();
        //2.将其存到请求域中
        request.setAttribute("start",start);
        //记录请求日志
        LOGGER.info(request.getRequestURI()+"，请求到达");
        //返回true，才会去找下一个拦截器，如果没有下一个拦截器，则去controller
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        //取出start
        long start=(long)request.getAttribute("start");
        //得到end
        long end=System.currentTimeMillis();
        //3.记录一下耗时
        long spendTime=end-start;

        if (spendTime>=1000)
        {
            LOGGER.warning("方法耗时严重，请及时处理，耗时："+spendTime+"毫秒");

        }else
        {
            LOGGER.info("方法耗时："+spendTime+"毫秒，速度正常");

        }


    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}
```





### 会话拦截器

- 拦截器配置

```xml
<mvc:interceptor>
    <!--
        只想拦截User下面的所有URL
        还需要开放登陆权限

    -->
    <mvc:mapping path="/user/**/*"/>
    <!--排除登陆的URL-->
    <mvc:exclude-mapping path="/user/login"/>
    <bean class="com.david.interceptors.SessionIntercepter">

    </bean>
</mvc:interceptor>
```



- 后台代码

```java
package com.david.interceptors;

import com.david.pojo.User;
import org.springframework.web.servlet.HandlerInterceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.logging.Logger;

/**
 * 会话拦截器
 */

public class SessionIntercepter implements HandlerInterceptor {


    private static final Logger LOGGER=Logger.getLogger(String.valueOf(MethodTimerInterceptor.class));
    //检查当前会话是否有User，有放行，没有就不放行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {


        Object user=request.getSession().getAttribute("SESSION_USER");
        if (user==null)
        {
            LOGGER.warning("您不具备权限，请先登陆");
        }

        if (user instanceof User)
        {
            //再去数据库里面查询他的身份是否正确


            //如果有这个人的话，那么就把他的密码置为null，只取得他的名字
            User u=(User)user;
            u.setPassword(null);
            request.getSession().setAttribute("SESSION_USER",u);


            LOGGER.info(u.getName()+"正在处于工作状态，可以执行操作");

            return true;

        }else{
            LOGGER.warning("请不要搞事，请先登陆");
            return false;
        }


    }
}
```





### 拦截器执行顺序问题

如果有n个拦截器，并且都能拦截到某个URL的的时候，执行的顺序问题

在springmvc中拦截器定义的顺序是有关系的，配置在前面的拦截器优先拦截，按照顺序来。



### 拦截器与过滤器的比较

#### 相似

都有优先处理请求的权利，可以决定是否将请求转移到实际处理的控制器处，都可以对请求或者会话当中的数据进行加工。

#### 不同

- 拦截器可以做前置处理，后置处理，完成后处理，控制的跟家详细一些，而过滤器只是负责前面的过滤行为而已。
- 过滤器相对于拦截器优先执行，因为过滤器是servlet规范里面的组件，而拦截器是框架自己额外添加的一个组件



## SSM整合开发

spring和springmvc是天然集成的，所以只需要解决mybatis和spring整合的问题，中间项目mybatis-spring项目进行整合，重点整合mabatis和spring的两个东西

- 由spring容器管理mybatis这个mapper
- 由spring利用申明事务（AOP）进行事务的综合管理



### 添加依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.david</groupId>
  <artifactId>springMVCDemo1</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <name>springMVCDemo1 Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring.version>5.0.8.RELEASE</spring.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <!--spring的依赖start-->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.0.8.RELEASE</version>
    </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-context-support -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context-support</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-beans -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-beans</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-web -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-web</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-aop</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-aspects -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-aspects</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-jdbc</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>

      <!--利用它处理事务问题-->
      <!-- https://mvnrepository.com/artifact/org.springframework/spring-tx -->
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-tx</artifactId>
          <version>5.0.8.RELEASE</version>
      </dependency>
      <!--spring的依赖end-->



      <!--添加json数据依赖start-->
      <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
      <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.9.3</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-core -->
      <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-core</artifactId>
          <version>2.9.3</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-annotations -->
      <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-annotations</artifactId>
          <version>2.9.3</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/net.sf.json-lib/json-lib -->
      <dependency>
          <groupId>net.sf.json-lib</groupId>
          <artifactId>json-lib</artifactId>
          <version>2.4</version>
          <classifier>jdk15</classifier>
      </dependency>


      <!--添加处理json为javabean-->
      <!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-core-asl -->
      <dependency>
          <groupId>org.codehaus.jackson</groupId>
          <artifactId>jackson-core-asl</artifactId>
          <version>1.9.2</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/org.codehaus.jackson/jackson-mapper-asl -->
      <dependency>
          <groupId>org.codehaus.jackson</groupId>
          <artifactId>jackson-mapper-asl</artifactId>
          <version>1.9.2</version>
      </dependency>
      <!--添加json数据依赖end-->


      <!--文件上传依赖start-->
      <!--apache文件上传组件-->
      <!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->
      <dependency>
          <groupId>commons-fileupload</groupId>
          <artifactId>commons-fileupload</artifactId>
          <version>1.3.1</version>
      </dependency>
      <!--文件上传依赖end-->

      <!--持久层依赖start-->
      <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
      <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
          <version>3.4.1</version>
      </dependency>
      <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>5.1.38</version>
      </dependency>
      <!--持久层依赖end-->

      <!--日志依赖start-->
      <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-api -->
      <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-api</artifactId>
          <version>1.7.12</version>
      </dependency>
      <!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-log4j12 -->
      <dependency>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-log4j12</artifactId>
          <version>1.7.12</version>
      </dependency>
      <!--日志-->
      <dependency>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
          <version>1.2.17</version>
      </dependency>
      <!--日志依赖end-->


      <!--数据源的引入，池化技术-->
      <!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
      <dependency>
          <groupId>com.mchange</groupId>
          <artifactId>c3p0</artifactId>
          <version>0.9.2.1</version>
      </dependency>

      <!--mybatis和spring整合所需要的依赖-->
      <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
      <dependency>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis-spring</artifactId>
          <version>1.3.0</version>
      </dependency>

      <!--servlet jsp jstl等依赖start-->
      <!--jstl依赖-->
      <!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>jstl</artifactId>
          <version>1.2</version>
      </dependency>

      <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
      <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>javax.servlet-api</artifactId>
          <version>4.0.1</version>
          <scope>provided</scope>
      </dependency>

      <dependency>
          <groupId>javax.servlet.jsp</groupId>
          <artifactId>javax.servlet.jsp-api</artifactId>
          <version>2.3.1</version>
          <scope>provided</scope>
      </dependency>
      <!--servlet jsp jstl等依赖end-->

      <!--处理时间格式-->
      <!-- https://mvnrepository.com/artifact/joda-time/joda-time -->
      <dependency>
          <groupId>joda-time</groupId>
          <artifactId>joda-time</artifactId>
          <version>2.9.9</version>
      </dependency>

      <!--mybatis分页依赖-->
      <!-- https://mvnrepository.com/artifact/com.github.pagehelper/pagehelper -->
      <dependency>
          <groupId>com.github.pagehelper</groupId>
          <artifactId>pagehelper</artifactId>
          <version>5.1.2</version>
      </dependency>

      <!--apache用于MD5加密-->
      <!-- https://mvnrepository.com/artifact/commons-codec/commons-codec -->
      <dependency>
          <groupId>commons-codec</groupId>
          <artifactId>commons-codec</artifactId>
          <version>1.10</version>
      </dependency>








  </dependencies>

  <build>
    <finalName>springMVCDemo1</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.0.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.7.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.20.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```



### 指定整个程序上下文信息

```xml
<!--指定整个程序上下文信息-->
<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:spring/applicationContext.xml</param-value>
</context-param>
```



### 字符编码以及全HTTP请求支持的过滤器添加

```xml
<filter>
  <filter-name>characterEncodingFilter</filter-name>
  <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  <!--指定字符编码-->
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
  <init-param>
    <param-name>forceRequestEncoding</param-name>
    <param-value>true</param-value>
    <init-param>
      <param-name>forceResponseEncoding</param-name>
      <param-value>true</param-value>
    </init-param>
  </init-param>
</filter>

<filter-mapping>
  <filter-name>characterEncodingFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>

<!--注册一个支持所有http请求的过滤器-->
<filter>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```



### DispatcherServlet注册

```xml
<!--注册一个前端控制器

DispatcherServlet

-->

<servlet>
  <!--这里的名字是有讲究的，如果我们不去修改spring默认文件的默认位置，那么springMVC
      它会web-inf下面找一个叫做springmvc-servlet.xml的文件
  -->
  <servlet-name>springmvc</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

</servlet>

<servlet-mapping>
  <servlet-name>springmvc</servlet-name>
  <!--这里统一写成/-->
  <url-pattern>/</url-pattern>
</servlet-mapping>
```



### spring启动监听器配置

```xml
<listener>
  <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```





### spring核心配置文件的编写

核心配置文件用于引入其他配置文件

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!--引入spring和其他整合的配置文件-->

    <import resource="classpath:spring/spring-*.xml" />

</beans>
```



### spring-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:cache="http://www.springframework.org/schema/cache"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:jdbc="http://www.springframework.org/schema/jdbc"
       xmlns:jee="http://www.springframework.org/schema/jee"
       xmlns:lang="http://www.springframework.org/schema/lang"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:task="http://www.springframework.org/schema/task"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee.xsd
      http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
      http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
      http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd
      http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc.xsd
      http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd
      http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task.xsd
      http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang.xsd
      http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd ">




    <!--启动注释
        排除了servlet的注释

    -->

    <context:component-scan base-package="com.david">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Service"/>

    </context:component-scan>

    <!--配置一个视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>

    <!--加上MVC驱动-->
    <mvc:annotation-driven>
        <!--配置消息转化器以及支持JSON的使用-->
        <mvc:message-converters>
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>application/json:charset=UTF-8</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>

    <!--配置请求映射的适配器-->
    <bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
        <property name="messageConverters">
            <list>
                <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                    <property name="supportedMediaTypes">
                        <list>
                            <value>text/html:charset=UTF-8</value>
                            <value>application/json:charset=UTF-8</value>
                        </list>
                    </property>
                </bean>
                <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                    <property name="supportedMediaTypes">
                        <list>
                            <value>text/html:charset=UTF-8</value>
                            <value>application/json:charset=UTF-8</value>
                        </list>
                    </property>

                </bean>
            </list>
        </property>
    </bean>


    <!--文件上传 id必须去名multipartResolver,注册我们的文件上传解析器-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!--最大上传文件的大小,单位byte-->
        <property name="maxUploadSize" value="54000000"/>
        <property name="defaultEncoding" value="UTF-8"/>
    </bean>

    <!--静态资源处理-->
    <mvc:default-servlet-handler/>







</beans>
```



### spring-mybatis.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">




    <context:component-scan base-package="com.david.mapper">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>

    </context:component-scan>



    <!--引入属性文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--1 注入一个数据源-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <!--数据库连接四大金刚-->
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="user" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>

        <!--如果有需要,请把所有的属性加到properties文件中去-->
        <!--c3p0连接池私有属性-->
        <property name="maxPoolSize" value="30"/>
        <property name="minPoolSize" value="10"/>
        <!--关闭连接后不自动commit-->
        <property name="autoCommitOnClose" value="false"/>
        <!--获取连接超时时间-->
        <property name="checkoutTimeout" value="100000"/>
        <!--获取连接失败重试次数-->
        <property name="acquireRetryAttempts" value="2"/>

    </bean>


    <!--最重要的一步,如何整合mybatis-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--引入com/sz/mapper所有xml文件-->
        <!--这就要求所有的mapper文件必须在com/david/mapper/之下-->
        <property name="mapperLocations" value="classpath:com/david/mapper/*.xml"/>
        <!--配置mybatis一些配置 比如settings-->
        <property name="configuration">
            <bean class="org.apache.ibatis.session.Configuration">
                <!--其他mybatis的配置也就是mybatis.cfg.xml的相关配置都会转移到这里来-->
                <!--数据库的下划线风格转换为驼峰风格-->
                <property name="mapUnderscoreToCamelCase" value="true"/>
                <!--日志-->
                <property name="logImpl" value="org.apache.ibatis.logging.log4j.Log4jImpl"/>
            </bean>
        </property>

        <!--插件的配置-->
        <property name="plugins">
            <array>
                <!--分页插件的配置 拦截器实现分页功能-->
                <bean class="com.github.pagehelper.PageInterceptor">
                    <property name="properties">
                        <value>
                            helperDialect=mysql
                            reasonable=true
                            supportMethodsArgument=true
                            params=count=countSql
                            autoRuntimeDialect=true
                        </value>
                    </property>
                </bean>
            </array>
        </property>
    </bean>


    <!--持久层的接口-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.david.mapper"/>
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactoryBean"/>

    </bean>



    <!--事务的配置-->

    <bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">
        <!--这个事务管理要使用和上面的是同一个数据源-->
        <property name="dataSource" ref="dataSource"/>
    </bean>


    <tx:advice id="transactionAdvice" transaction-manager="transactionManager">
        <!--事务处理的相关性及其它的传播性-->
        <tx:attributes>
            <!--相关操作只读-->
            <tx:method name="get*" read-only="true"/>
            <tx:method name="query*" read-only="true"/>
            <tx:method name="list*" read-only="true"/>
            <tx:method name="select*" read-only="true"/>
            <!--如果出现了异常，事务要回滚-->
            <tx:method name="delete*" propagation="REQUIRED" rollback-for="Exception" />
            <tx:method name="update*" propagation="REQUIRED" rollback-for="Exception" />
            <tx:method name="insert*" propagation="REQUIRED" rollback-for="Exception" />
            <tx:method name="add*" propagation="REQUIRED" rollback-for="Exception" />
        </tx:attributes>
    </tx:advice>



    <!--使用aop对事务管理的范围进行织入,需要明确几个点
        1.对哪些地方需要进行事务的管理execution书写,明确边界
        2.使用什么策略去管理,我们使用了tx:advice全部写于其中,在我们的aop的advisor当中只需要去引用这个即可



    -->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(public  * com.david.service..*.*(..))"/>
        <aop:advisor advice-ref="transactionAdvice" pointcut-ref="txPointCut"/>


    </aop:config>


    <!--采用注解进行事务配置,请在Service的实现类上面加上@Transanctional注解-->
    <tx:annotation-driven transaction-manager="transactionManager"/>

</beans>
```



### db.properties

```xml
jdbc.url=jdbc:mysql://localhost:3306/springMVCDemo1
jdbc.username=root
jdbc.password=93g12d24w
jdbc.driver=com.mysql.jdbc.Driver
```



### log4j.properties

```xml
### 设置###
log4j.rootLogger = INFO,Console,File

### 输出信息到控制抬 ###
log4j.appender.Console = org.apache.log4j.ConsoleAppender
log4j.appender.Console.Target = System.out

log4j.appender.Console.layout = org.apache.log4j.PatternLayout
log4j.appender.Console.layout.ConversionPattern = [%-5p] %d{yyyy-MM-dd HH:mm:ss,SSS} method:%l%n%m%n


### mybatis显示SQL语句的配置
lo4j.logger.com.david.mapper=DEBUG

### 文件大小到达指定尺寸的时候产生一个新的文件
log4j.appender.File=org.apache.log4j.RollingFileAppender

### 指定输出目录，这里会放在Tomcat下
log4j.appender.File.File=D:/log.log

### 定义文件的大小
log4j.appender.File.MaxFileSize=10MB

### 输出DEBUG 级别以上的日志到=E://logs/error.log ###
log4j.appender.File.Threshold = ALL
log4j.appender.File.layout = org.apache.log4j.PatternLayout
log4j.appender.File.layout.ConversionPattern = %-d{yyyy-MM-dd HH:mm:ss}  [ %t:%r ] - [ %p ]  %m%n
```



### spring-context.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:c="http://www.springframework.org/schema/c"
       xmlns:cache="http://www.springframework.org/schema/cache"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:jdbc="http://www.springframework.org/schema/jdbc"
       xmlns:jee="http://www.springframework.org/schema/jee"
       xmlns:lang="http://www.springframework.org/schema/lang"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:task="http://www.springframework.org/schema/task"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee.xsd
      http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd
      http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
      http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd
      http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc.xsd
      http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd
      http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task.xsd
      http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang.xsd
      http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd ">

    <!--做spring的基础配置-->
    <!--1.spring容器注册-->
    <context:annotation-config/>
    <!--2.自动扫描配置-->
    <context:component-scan base-package="com.david.service"/>

    <!--3.激活aop注解方式的代理-->
    <aop:aspectj-autoproxy/>

    <!--消息格式转换-->
    <bean id="conversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
        <property name="registerDefaultFormatters" value="false"/>
        <property name="formatters">
            <set>
                <bean class="org.springframework.format.number.NumberFormatAnnotationFormatterFactory"/>
            </set>
        </property>
        <property name="formatterRegistrars">
            <set>
                <bean class="org.springframework.format.datetime.joda.JodaTimeFormatterRegistrar">
                    <property name="dateFormatter">
                        <bean class="org.springframework.format.datetime.joda.DateTimeFormatterFactoryBean">
                            <property name="pattern" value="yyyyMMdd"/>
                        </bean>
                    </property>
                </bean>
            </set>
        </property>
    </bean>



</beans>
```



