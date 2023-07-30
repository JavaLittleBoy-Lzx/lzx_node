[TOC]

## 一、SpringMVC介绍

### 1.1、什么是MVC

MVC是一种软件架构思想，将软件按照(Model)模型、(View)视图、(Controller)控制来进行划分

#### 1.1.1、Model

Model：模型层，指的是工程中的JavaBean，作用是用于处理数据

JavaBean分类

​	🐏 实体类Bean：专门用来存储业务数据的，和数据库表的映射类，如：Person、Student、User等。

​	🐐 业务处理Bean：专门用来处理业务逻辑和数据访问的，如：Service、Dao等。

#### 1.1.2、View

View：视图层，指的是和用户进行交互的页面，例如：HTML、JSP、Vue等。

#### 1.1.3、Controller

Controller：控制器层，指的是工程项目中的Servlet，主要作用是用于请求和响应浏览器。

#### 1.1.4、MVC的工作流程

用户通过视图层发送请求给服务器，在服务器的请求中请求被Controller接受，Controller调用相关的Model层处理请求，处理完毕以后将结果返回给Controller层，Controller层根据处理的结果找到对应的View视图层，渲染数据后最终响应给浏览器。

![image-20230721152954476](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721153001.png)

### 1.2、什么是SpringMVC

SpringMVC是Spring的一个后续产品，是Spring的一个子项目

SpringMVC为Spring表述层开发提供一整套完整的结局方案

> 🐖：三层架构分别是：表述层(表示层)、业务逻辑层、数据访问层，表述层表示的是前后端的servlet

### 1.3、SpringMVC的特点是什么

- Spring 家族原生产品，与 IOC 容器等基础设施无缝对接
- 基于原生的Servlet，通过了功能强大的前端控制器DispatcherServlet，对请求和响应进行统一处理
- 表述层各细分领域需要解决的问题全方位覆盖，提供全面解决方案
- 代码清新简洁，大幅度提升开发效率
- 内部组件化程度高，可插拔式组件即插即用，想要什么功能配置相应组件即可
- 性能卓著，尤其适合现代大型、超大型互联网项目要求  

## 二、SpringMVC快速入门

### 2.1、开发环境

#### 2.1.1、创建Maven项目

1. 创建Maven项目模块

![image-20230721154241543](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721154241.png)

![image-20230721154420937](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721154421.png)

![image-20230721155022149](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721155022.png)

2. 添加打包方式

![image-20230721155122831](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721155122.png)

3. 添加依赖

```xml
    <dependencies>
        <!-- SpringMVC -->  
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.3.1</version>
        </dependency>
        <!-- 日志 -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>
        <!-- ServletAPI -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <!-- Spring5和Thymeleaf整合包 -->
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>
    </dependencies>
```

4. 添加web.xml文件(自己添加)

   🐕 在模块的src下的main目录下创建webapp文件夹

![image-20230721155511670](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721155511.png)

  🐅 手动添加web.xml文件

![image-20230721155707150](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721155707.png)

![image-20230721160203116](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721160203.png)

#### 2.1.2、配置web.xml

注册前端控制器DispacherServlet

😎 默认配置方式

此配置文件的作用是：SpringMVC的配置文件默认位于WEB-INF下，默认名称为\<servlet-name>-servlet.xml,例如：以下配置所对应的SpringMVC配置文件位于WEB-INF下，名称为SpringMVC-servlet.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--   配置SpringMVC的前端控制器，对浏览器发送的请求统一进行处理 -->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <!--设置SpringMVC的核心控制器所能处理的请求路径
        / ：匹配的请求可以是/login或者.html或.js或.css的请求路径
        但是/ 不能匹配.jsp请求路径的请求
        -->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

🤗 拓展配置方式

![image-20230721172945949](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721172946.png)

> 😈 
>
>  \<url-pattern>/\</url-pattern>的/和/*的区别：
>
> /能够匹配的请求是/login或者是.html/.js或.css方式的请求路径，但是‘/’不能访问.jsp请求路径的请求
>
> 原因是：这样做可以避免在访问.jsp也页面的时候，该请求被DispatcherServlet处理，导致页面不能访问的情况
>
> ‘/*’则能够匹配到所有的请求，例如在使用过滤器时，需要对所有的请求进行过滤则需要使用‘/\*’

#### 2.1.3、创建请求控制器

```java
package com.springmvc.controller;

import org.springframework.stereotype.Controller;

@Controller //标注为控制器
public class TestController {
}
```

### 2.2、创建SpringMVC配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!--自动扫描包 -->
    <context:component-scan base-package="com.springmvc.controller"></context:component-scan>
    <!-- 设置Thymeleaf视图解析器 -->
    <bean id="viewResolver"
          class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
        <property name="order" value="1"/>
        <property name="characterEncoding" value="UTF-8"/>
        <property name="templateEngine">
            <bean class="org.thymeleaf.spring5.SpringTemplateEngine">
                <property name="templateResolver">
                    <bean class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
                        <!-- 视图前缀 -->
                        <property name="prefix" value="/WEB-INF/templates/"/>
                        <!-- 视图后缀 -->
                        <property name="suffix" value=".html"/>
                        <property name="templateMode" value="HTML5"/>
                        <property name="characterEncoding" value="UTF-8" />
                    </bean>
                </property>
            </bean>
        </property>
    </bean>
    <!-- 处理静态资源,例如html css jpg js等
       若只设置该标签,则只能访问静态资源,其他请求则无法访问
       此时则必须设置    <mvc:annotation-driven/>解决问题
       -->
    <mvc:default-servlet-handler/>

    <!-- 开启mvc注解驱动 -->
    <mvc:annotation-driven>
        <mvc:message-converters>
        <!-- 处理相应中文乱码问题 -->
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="defaultCharset" value="UTF-8"/>
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/html</value>
                        <value>application/json</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

### 2.3、测试案例HelloWord

#### 2.3.1、实现对首页的访问

```java
package com.springmvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

/**
 * @ClassName TestController
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/21 17:25:06
 * @Version 1.0
 **/
@Controller //标注为控制器
public class TestController {
    //创建处理请求的方法
    @RequestMapping("/") //@RequestMapping注解的value属性可以通过请求地址匹配请求，/表示的是当前工程的上下文路径
    //localhost:8080/springMVC/
    public String index() {
        return "index";
    }
}
```

#### 2.3.2、通过点击跳转到指定页面

在主页index.html中设置超链接

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
<h1>首页</h1>
<a th:href="@{/hello}">HelloWord</a><br/>
</body>
</html>
```

```java
@RequestMapping("/hello")
public String HelloWord() {
    return "target";
}
```

### 2.4、总结

浏览器通过发送请求，若请求地址符合utl-pattern标签中的地址，则该请求会被DispatcherServlet所拦截处理，前端控制器会读取SpringMVC中的核心组件，通过扫描组件找到控制器。将路径和控制器的value属性值进行匹配，若匹配成功，则该方法就是处理此请求的方法，处理请求的方法需要返回一个字符串类型的制图名称，该视图名称会被视图解析器解析，加上前缀和后缀组成视图路径，通过Thymeleaf对视图渲染，最终发到视图所对应的页面。

## 三、@RequestMapping注解

### 3.1、@RequestMapping注解功能

😀 从注解名称上我们可以看到，@RequestMapping注解的作用就是将请求和处理请求的控制器方法关联
起来，建立映射关系。SpringMVC 接收到指定的请求，就会来找到在映射关系中对应的控制器方法来处理这个请求。  

### 3.2、@RequestMapping注解位置

@RequestMapping标识一个类：设置映射请求路径的初始信息

@RequestMapping标识一个方法:设置映射请求路径的具体信息

### 3.3、@RequestMapping注解属性

#### 3.3.1、value属性

- @RequestMapping注解的value属性通过请求的请求地址匹配请求映射
- @RequestMapping注解的value属性是一个字符串类型的数组，表示该请求映射能够匹配多个请求地址所对应的请求
- @RequestMapping注解的value属性必须设置，至少通过请求地址匹配请求映射

```java
  //可以接受多个请求
    @RequestMapping(value = {"/testRequestMapping","/test"})
    public String testRequestMapping() {
        return "success";
    }
```

```html
<a th:href="@{/testRequestMapping}">测试@RequestMapping的value属性--
    >/testRequestMapping</a><br>
<a th:href="@{/test}">测试@RequestMapping的value属性-->/test</a><br>
```

#### 3.3.2、method属性

- @RequestMapping注解的method属性通过请求的请求方式（get或post）匹配请求映射
- @RequestMapping注解的method属性是一个RequestMethod类型的数组，表示该请求映射可匹配多种请求方式请求
- 若当前请求的请求地址满足请求映射的value属性，但是请求方式不满足method属性，则浏览器报错405：Request method 'POST' not supported  

```html
<a th:href="@{/test}">测试@RequestMapping的value属性-->/test</a><br>
<form th:action="@{/test}" method="post">
    <input type="submit">
</form>
```

> 🐽：对于处理指定请求方式的控制方法，SpringMVC提供了@RequestMapping的派生注解
>
> 处理get请求的映射-->@GetMapping
>
> 处理post请求的映射-->@PostMapping
>
> 处理put请求的映射-->@PutMapping
>
> 处理delete请求的映射-->@DeleteMapping 
>
> 但是目前浏览器只支持get和post，若在form表单提交时，为method设置了其他请求方式的字符串（put或delete），则按照默认的请求方式get处理。
>
> 若要发送put和delete请求，则需要通过spring提供的过滤器HiddenHttpMethodFilter，在
> RESTful部分会讲到  

#### 3.3.3、params属性

#### 3.3.4、headers属性

### 3.4、SpringMVC路径

#### 3.4.1、支持ant风格的路径

- ？：表示任意的单个字符
- *：表示任意的0个或多个字符
- \*\*：表示任意的一层或多层目录
- 注意：在使用\*\*时，只能使用/\*\*/xxx的方式  

#### 3.4.2、支持路径中有占位符(重点)

SpringMVC中的占位符常用于RESTful风格中，若请求的路径中携带数据参数的话，可以在@RequestMapping注解中通过占位符{xxx}来表示传输的数据，再通过@PathVariable注解来将数据作为形参传给下方法

```html
<a th:href="@{/testRest/1/admin}">测试路径中的占位符-->/testRest</a><br>
```

```java
//占位符
@RequestMapping("/testRest/{id}/{username}")
public String testRest(@PathVariable String username, @PathVariable String id) {
    System.out.println("id:" + id + "username:" + username);
    return "success";
}
```

> 😱@PathVariable的值若和{xxx}占位符中的不一致的话需要在@PathVariable("xxx")添加属性值否则会报错

![image-20230721194201472](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230721194202.png)

## 四、SpringMVC获取请求参数

### 4.1、通过ServletAPI获取

通过HttpServletRequest来获取，HttpServletRequest将请求封装为一个对象，可以通过getParameter获取参数

```java
    @RequestMapping("/testParam")
    public String testParam(HttpServletRequest request) {
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        System.out.println("username = " + username + " password = " + password);
        return "success";
    }
```

### 4.2、通过控制器方法形参获取请求参数

```java
  @RequestMapping("/testParam")
    public String testParam(String username,String password) {
        System.out.println("username = " + username + " password = " + password);
        return "success";
    }
```

> 😁 这里通过控制方法的形参来获取请求参数，和上述的@PathVariable注解有区别，若形参和请求参数名称相同的话，这里和@PathVariable注解唯一的区别就在于，请求路径中的{xxx}占位符和形参前添加@PathVariable，即@PathVariable注解中可以不添加属性值。

### 4.3、@RequestParam

### 4.4、@RequestHeader

### 4.5、@CookieValue

### 4.6、通过POJO获取请求参数

```html
<form th:action="@{/testpojo}" method="post">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    性别：<input type="radio" name="sex" value="男">男<input type="radio" name="sex" value="女">女<br>
    年龄：<input type="text" name="age"><br>
    邮箱：<input type="text" name="email"><br>
    <input type="submit">
</form>
```

```java
package com.springmvc.entity;

/**
 * @ClassName User
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/21 20:13:24
 * @Version 1.0
 **/
public class User {
    private Integer id;
    private String username;
    private String password;
    private Integer age;
    private String sex;
    private String email;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", age=" + age +
                ", sex='" + sex + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
}
```

```java
@RequestMapping("/testpojo")
public String testPOJO(User user) {
    System.out.println("user = " + user);
    return "success";
}
```

### 4.7、解决获取请求参数乱码问题

解决获取请求参数的乱码问题，可以使用SpringMVC提供的编码过滤器CharacterEncodingFilter，但是必须在web.xml中进行注册。

```xml
<!--配置springMVC的编码过滤器-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

> 😯 SpringMVC中处理编码的过滤器一定要配置在其他过滤器之前，否则无效

## 五、域对象共享数据

### 5.1、使用Servlet API向request域对象共享数据

### 5.2、使用ModelAndView向request域对象共享数据

### 5.3、使用Model向request域对象共享数据

### 5.4、使用Map向request域对象共享数据

### 5.5、使用ModelMap向request域对象共享数据

### 5.6、ModelMap、Model、Map关系

### 5.7、向session域共享数据

### 5.8、向application域共享数据

## 六、SpringMVC的视图

SpringMVC视图是View接口，作用是渲染数据，将模型Model中的数据展示给用户，SpringMVC的视图种类有很多，默认有转发视图和重定向视图。

👻 若使用视图技术为Thymeleaf，在SpringMVC的配置文件中配置了Thymeleaf的视图解析器，由此经过视图解析器之后得到的是ThymeleafView。

### 6.1、ThymeleafView视图

当控制器方法中所设置的视图没有任何前缀名称的话，此视图的名称会被SpringMVC的配置文件中配置的视图解析器解析，视图名称拼接视图前缀和试图后缀所得到的最终路径，会通过转发的方式实现跳转。

![image-20230722081332155](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722081339.png)

### 6.2、转发视图

SpringMVC默认的转发视图为InternalResourceView，当控制器中的视图以“forward:”为前缀的时候，创建InternalResourceView视图解析器，SpringMVC不会在配置文件中设置视图解析器进行解析，而是会将前缀"forward:"去掉，剩余部分作为最终路径通过转发的方式实现跳转。

```JAVA
  @RequestMapping("/testForward")
    public String testForward() {
        return "forward:/testHello";
    }
    @RequestMapping("/testHello")
    public String testHello() {
        return "success";
    }
```

> 😸 上述转发视图中的路径为转发地址，不是视图地址，即：在testForward()方法中return的"forward:/testHello"中的/testHello是转发的地址。

### 6.3、重定向

SpringMVC默认的重定向视图为RedirectView，方式同转发一致

```java
    @RequestMapping("/testRedirect")
    public String testRedirect() {
        return "redirect:/testHello";
    }
    @RequestMapping("/testHello")
    public String testHello() {
        return "success";
    }
```

#### 转发和重定向的区别

🐯 转发跳转截图

![image-20230722093037569](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722093037.png)

😾 重定向跳转截图

![image-20230722093624482](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722093624.png)

> 🐱‍🏍 上述两者最大的区别在于：转发是一次请求一次响应，在服务器之间实现跳转，故此地址栏中的地址不会发生变化，简单点说就是请求的地址不会因为是转发而发生变化，但是页面会变化，这样的好处在于不会丢失数据；而重定向则是两次请求两次响应，故此地址栏中的地址会发生变化。具体如下图：

![image-20230722100415008](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722100415.png)

![image-20230722101755082](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722101755.png)

### 6.4、视图控制器 View-controller

在控制器方法中，仅仅是为了页面跳转，只需要设置视图名称即可，处理器方法使用view-controller标签进行表示。

```xml
<!--
path：设置处理的请求地址
view-name：设置请求地址所对应的视图名称
-->
<mvc:view-controller path="/testView" view-name="success"></mvc:view-controller>
```

> 当SpringMVC中设置了任何一个view-controller时，其余控制器的请求映射则全部失效，此时需要在SpringMVC的核心配置文件设置开启mvc的注解驱动标签

## 七、RESTful

### 7.1、RESTful简介

REST:Representational State Transfer,表现层资源状态转移

> 😱 资源
> 资源是一种看待服务器的方式，即，将服务器看作是由很多离散的资源组成。每个资源是服务器上一个
> 可命名的抽象概念。因为资源是一个抽象的概念，所以它不仅仅能代表服务器文件系统中的一个文件、
> 数据库中的一张表等等具体的东西，可以将资源设计的要多抽象有多抽象，只要想象力允许而且客户端
> 应用开发者能够理解。与面向对象设计类似，资源是以名词为核心来组织的，首先关注的是名词。一个
> 资源可以由一个或多个URI来标识。URI既是资源的名称，也是资源在Web上的地址。对某个资源感兴
> 趣的客户端应用，可以通过资源的URI与其进行交互。  

>😁 资源的表述
>资源的表述是一段对于资源在某个特定时刻的状态的描述。可以在客户端-服务器端之间转移（交
>换）。资源的表述可以有多种格式，例如HTML/XML/JSON/纯文本/图片/视频/音频等等。资源的表述格
>式可以通过协商机制来确定。请求-响应方向的表述通常使用不同的格式。

> 😕 状态转移
> 状态转移说的是：在客户端和服务器端之间转移（transfer）代表资源状态的表述。通过转移和操作资
> 源的表述，来间接实现操作资源的目的。

### 7.2、RESTful实现

RESTful和传方式的URL地址不同

|     请求方式     |   操作   |     传统方式      |       RESTful       |
| :--------------: | :------: | :---------------: | :-----------------: |
|  GET(获取资源)   | 查询操作 | getUserById？id=1 |  user/1-->get请求   |
|  PUT(更新资源)   | 更新操作 |    updateUser     |   user-->put请求    |
|  POST(新建资源)  | 保存操作 |     saveUser      |   user-->post请求   |
| DELETE(删除资源) | 删除操作 | deleteUser？id=1  | user/1-->delete请求 |

### 7.3、HiddenHttpMethodFilter

浏览器只支持get和post请求，SpringMVC会通过Hi扽HTTPMethodFilter将”post转为“”delete“和”put“请求。

HiddenHttpMethodFilter 处理put和delete请求的条件 ：

1. 当前请求的请求方式必须为post 
2. 当前请求必须传输请求参数_method 

满足以上条件，HiddenHttpMethodFilter 过滤器就会将当前请求的请求方式转换为请求参数\_method的值，因此请求参数_method的值才是最终的请求方式.

在web.xml中注册HiddenHttpMethodFilter

```xml
 <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

> 🐒 在web.xml中注册时，必须先注册CharacterEncodingFilter，再注册HiddenHttpMethodFilter
> 原因：在 CharacterEncodingFilter 中通过 request.setCharacterEncoding(encoding) 方法设置字
> 符集的 request.setCharacterEncoding(encoding) 方法要求前面不能有任何获取请求参数的操作   

### 7.4、RESTful案例

#### 7.4.1、准备工作

```java
package com.springmvc.entity;

/**
 * @ClassName Employee
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/22 10:58:49
 * @Version 1.0
 **/
public class Employee {
    private Integer id;
    private String lastName;
    private String email;
    //1 male, 0 female
    private Integer gender;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Integer getGender() {
        return gender;
    }

    public void setGender(Integer gender) {
        this.gender = gender;
    }

    public Employee(Integer id, String lastName, String email, Integer gender) {
        this.id = id;
        this.lastName = lastName;
        this.email = email;
        this.gender = gender;
    }

    public Employee() {
    }
}
```

```java
package com.springmvc.dao;

import com.springmvc.entity.Employee;
import org.springframework.stereotype.Repository;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

@Repository
public class EmployeeDao {

    private static Map<Integer, Employee> employees = null;
    static{
        employees = new HashMap<Integer, Employee>();
        employees.put(1001, new Employee(1001, "E-AA", "aa@163.com", 1));
        employees.put(1002, new Employee(1002, "E-BB", "bb@163.com", 1));
        employees.put(1003, new Employee(1003, "E-CC", "cc@163.com", 0));
        employees.put(1004, new Employee(1004, "E-DD", "dd@163.com", 0));
        employees.put(1005, new Employee(1005, "E-EE", "ee@163.com", 1));
    }
    private static Integer initId = 1006;
    public void save(com.springmvc.entity.Employee employee){
        if(employee.getId() == null){
            employee.setId(initId++);
        }
    employees.put(employee.getId(), employee);
    }
    public Collection<Employee> getAll(){
        return employees.values();
    }
    public Employee get(Integer id){
        return employees.get(id);
    }
    public void delete(Integer id){
        employees.remove(id);
    }

}
```

#### 7.4.2、功能--访问首页

```java
package com.springmvc.entity;

/**
 * @ClassName Employee
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/22 10:58:49
 * @Version 1.0
 **/
public class Employee {
    private Integer id;
    private String lastName;
    private String email;
    //1 male, 0 female
    private Integer gender;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Integer getGender() {
        return gender;
    }

    public void setGender(Integer gender) {
        this.gender = gender;
    }

    public Employee(Integer id, String lastName, String email, Integer gender) {
        this.id = id;
        this.lastName = lastName;
        this.email = email;
        this.gender = gender;
    }

    public Employee() {
    }
}
```

```java
package com.springmvc.dao;

import com.springmvc.entity.Employee;
import org.springframework.stereotype.Repository;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;

@Repository
public class EmployeeDao {

    private static Map<Integer, Employee> employees = null;
    static{
        employees = new HashMap<Integer, Employee>();
        employees.put(1001, new Employee(1001, "E-AA", "aa@163.com", 1));
        employees.put(1002, new Employee(1002, "E-BB", "bb@163.com", 1));
        employees.put(1003, new Employee(1003, "E-CC", "cc@163.com", 0));
        employees.put(1004, new Employee(1004, "E-DD", "dd@163.com", 0));
        employees.put(1005, new Employee(1005, "E-EE", "ee@163.com", 1));
    }
    private static Integer initId = 1006;
    public void save(com.springmvc.entity.Employee employee){
        if(employee.getId() == null){
            employee.setId(initId++);
        }
    employees.put(employee.getId(), employee);
    }
    public Collection<Employee> getAll(){
        return employees.values();
    }
    public Employee get(Integer id){
        return employees.get(id);
    }
    public void delete(Integer id){
        employees.remove(id);
    }

}
```

#### 7.4.3、功能--查询所有员工数据

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Employee Info</title>
    <script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
</head>
<body>
<table border="1" cellpadding="0" cellspacing="0" style="text-align:
center;" id="dataTable">
    <tr>
        <th colspan="5">Employee Info</th>
    </tr>
    <tr>
        <th>id</th>
        <th>lastName</th>
        <th>email</th>
        <th>gender</th>
        <th>options(<a th:href="@{/toAdd}">add</a>)</th>
    </tr>
    <tr th:each="employee : ${employeeList}">
        <td th:text="${employee.id}"></td>
        <td th:text="${employee.lastName}"></td>
        <td th:text="${employee.email}"></td>
        <td th:text="${employee.gender}"></td>
        <td>
            <a class="deleteA" @click="deleteEmployee"
               th:href="@{'/employee/'+${employee.id}}">delete</a>
            <a th:href="@{'/employee/'+${employee.id}}">update</a>
        </td>
    </tr>
</table>

<!-- 作用：通过超链接控制表单的提交，将post请求转换为delete请求 -->
<form id="delete_form" method="post">
    <!-- HiddenHttpMethodFilter要求：必须传输_method请求参数，并且值为最终的请求方式 -->
    <input type="hidden" name="_method" value="delete"/>
</form>

<a class="deleteA" @click="deleteEmployee"
   th:href="@{'/employee/'+${employee.id}}">delete</a>

<a th:href="@{'/employee/'+${employee.id}}">update</a>

</body>
</html>
<script type="text/javascript">
    var vue = new Vue({
        el:"#dataTable",methods:{
//event表示当前事件
            deleteEmployee:function (event) {
//通过id获取表单标签
                var delete_form = document.getElementById("delete_form");
//将触发事件的超链接的href属性为表单的action属性赋值
                delete_form.action = event.target.href;
//提交表单
                delete_form.submit();
//阻止超链接的默认跳转行为
                event.preventDefault();
            }
        }
    });
</script>
```

#### 7.4.4、功能--删除

#### 7.4.5、功能--跳转到添加数据页面

#### 7.4.6、功能--保存

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Add Employee</title>
</head>
<body>
<form th:action="@{/employee}" method="post">
    lastName:<input type="text" name="lastName"><br>
    email:<input type="text" name="email"><br>
    gender:<input type="radio" name="gender" value="1">male
    <input type="radio" name="gender" value="0">female<br>
    <input type="submit" value="add"><br>
</form>
</body>
</html>
```

#### 7.4.7、功能--跳转到更新数据页面

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Update Employee</title>
</head>
<body>
<form th:action="@{/employee}" method="post">
    <input type="hidden" name="_method" value="put">
    <input type="hidden" name="id" th:value="${employee.id}">
    lastName:<input type="text" name="lastName" th:value="${employee.lastName}">
    <br>
    email:<input type="text" name="email" th:value="${employee.email}"><br>
    <!--
    th:field="${employee.gender}"可用于单选框或复选框的回显
    若单选框的value和employee.gender的值一致，则添加checked="checked"属性
    -->
    gender:<input type="radio" name="gender" value="1"
                  th:field="${employee.gender}">male
    <input type="radio" name="gender" value="0"
           th:field="${employee.gender}">female<br>
    <input type="submit" value="update"><br>
</form>
</body>
</html>
```

#### 7.4.8、功能--执行更新

```JAVA
package com.springmvc.controller;

import com.springmvc.dao.EmployeeDao;
import com.springmvc.entity.Employee;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import java.util.Collection;

/**
 * @ClassName EmployeeController
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/22 11:04:28
 * @Version 1.0
 **/
@Controller
public class EmployeeController {

    @Autowired
    private EmployeeDao employeeDao;
    
    @RequestMapping(value = "/employee",method = RequestMethod.GET)
    public String getEmployeeList(Model model) {
        Collection<Employee> employeeList = employeeDao.getAll();
        model.addAttribute("employeeList",employeeList);
        return "employee_list";
    }

    @RequestMapping(value = "/employee/{id}", method = RequestMethod.DELETE)
    public String deleteEmployee(@PathVariable("id") Integer id) {
        employeeDao.delete(id);
        return "redirect:/employee";
    }
    @RequestMapping(value = "/employee", method = RequestMethod.POST)
    public String addEmployee(Employee employee){
        employeeDao.save(employee);
        return "redirect:/employee";
    }

    @RequestMapping(value = "/employee/{id}", method = RequestMethod.GET)
    public String getEmployeeById(@PathVariable("id") Integer id, Model model){
        Employee employee = employeeDao.get(id);
        model.addAttribute("employee", employee);
        return "employee_update";
    }

    @RequestMapping(value = "/employee", method = RequestMethod.PUT)
    public String updateEmployee(Employee employee){
        employeeDao.save(employee);
        return "redirect:/employee";
    }
}
```

## 八、HttpMessageConverter

### 8.1、@RequestBody

@RequestBody可以获取请求体，需要在控制器方法设置以一个形参，使用@RequestBody标记，当前的请求的请求体就会为被标记的形参赋值

```java
@RequestMapping("testRequestBody")
public String testRequestBody(@RequestBody String requestBody) {
    System.out.println("requestBody = " + requestBody);
    return "success";
}
```

```html
<form th:action="@{/testRequestBody}" method="post">
    用户名:<input type="text" name="username"><br>
    密码:<input type="password" name="password"><br>
    <input type="submit">
</form>
```

### 8.2、RequestEntity

RequestEntity封装请求报文的一种形式，采用getHeaders()来获取请求头、getBody()方法获取请求体

```java
@RequestMapping("testRequestEntity")
public String testRequestEntity(RequestEntity<String> requestEntity)  {
    System.out.println("requestHeaders = " + requestEntity.getHeaders());
    System.out.println("requestBody = " + requestEntity.getBody());
    return "success";
}
```

### 8.3、@ResponseBody

![image-20230722140605949](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230722140606.png)

结果：浏览器显示success页面

### 8.4、SpringMVC处理json

@ResponseBody处理json的步骤如下：

1.   添加依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.12.1</version>
</dependency>
```

2. 在SpringMVC的核心配置文件中开启mvc的注解驱动，此时在HandlerAdaptor中会自动装配一个消息转换器：MappingJackson2HttpMessageConverter，可以将响应到浏览器的Java对象转换为Json格式的字符串。

3. 在处理器方法上使用@ResponseBody注解进行标识    
4. 将Java对象直接作为控制器方法的返回值返回，就会自动转换为Json格式的字符串 

```java
@RequestMapping("/testResponseUser")
@ResponseBody
public User testResponseUser() {
    return new User(1001,"admin","123456",23,"男");
}
```

### 8.5、SpringMVC处理Ajax

```js
<script type="text/javascript" th:src="@{/static/js/vue.js}"></script>
<script type="text/javascript" th:src="@{/static/js/axios.min.js}"></script>
<script type="text/javascript">var vue = new Vue({
    el:"#app",
    methods:{
        testAjax:function (event) {
            axios({
                method:"post",
                url:event.target.href,
                params:{
                    username:"admin",
                    password:"123456"
                }
            }).then(function (response) {
                alert(response.data);
            });
            event.preventDefault();
        }
    }
});
</script>
```

```html
<div id="app">
    <a th:href="@{/testAjax}" @click="testAjax">testAjax</a>
</div>
```

```java
@RequestMapping("/testAjax")
@ResponseBody
public String testAjax(String username,String password) {
    System.out.println("username = " + username);
    System.out.println("password = " + password);
    return "index";
}
```

### 8.6、@RestController注解

@RestController注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了
@Controller注解，并且为其中的每个方法添加了@ResponseBody注解 。

### 8.7、ResponseEntity

ResponseEntity用于控制器方法的返回值类型，该控制器方法的返回值就是响应到浏览器的响应报文  

## 九、文件上传和下载

### 9.1、文件上传

### 9.2、文件下载

## 十、拦截器

10.1、配置拦截器

10.2、拦截器的三个抽象方法

10.3、多个拦截器的执行顺序

## 十一、异常处理器

11.1、基于配置文件的异常处理器

11.2、基于注解的异常处理

## 十二、注解配置SpringMVC

12.1、创建初始化类，代替web.xml

12.2、创建SpingConfig配置类，替代Spring的配置文件

12.3、创建WebConfig配置类，替代SpringMVC的配置文件

12.4、测试功能

## 十三、SpringMVC的执行流程

13.1、SpringMVC的常用组件

13.2、DispatcherServlet初始化过程

13.3、DispatcherServlet调用组件处理请求

13.4、SpringMVC的执行流程