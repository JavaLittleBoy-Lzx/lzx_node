

# 一、SpringBoot简介

## 1.1、Spring能做什么

### 1.1.1、Spring的能力及生态

![image-20230724140820289](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230724140827.png)

### 1.1.2、Spring5的响应式编程

![image-20230724141101796](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230724141101.png)

## 1.2、SpringBoot是什么

`百度百科：`Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新[Spring](https://baike.baidu.com/item/Spring/85061?fromModule=lemma_inlink)应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。通过这种方式，Spring Boot致力于在蓬勃发展的[快速应用开发](https://baike.baidu.com/item/快速应用开发/206653?fromModule=lemma_inlink)领域(rapid application development)成为领导者。

`自我理解：`SpringBoot是一个基于Spring框架的可以快速开发Web应用的轻量型框架，以前的Spring在开发Web应用的时候需要借助MVC，配置很多配置文件，整合MyBatis需要Spring和Mybatis的整合依赖以及配置文件等，SpringBoot的出现使得这一复杂的配置简化为了注解的方式。

## 1.3、SpringBoot的特点

- Create stand-alone Spring applications
  - 独立创建一个Spring应用程序
- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)
  - 内置Tomcat、Jetty、Undertow(不在需要部署WAR文件)
- Provide opinionated 'starter' dependencies to simplify your build configuration
  - 提供自动的"starter"依赖，用于简化配置参数
- Automatically configure Spring and 3rd party libraries whenever possible
  - 自动配置Spring以及第三方库
- Provide production-ready features such as metrics, health checks, and externalized configuration
  - 提供生产级别的指标监控、健康检测、外部化配置
- Absolutely no code generation and no requirement for XML configuration
  - 无代码生成不需要配置XML文件

## 1.4、时代背景

### 1.4.1、微服务

In short, the microservice architectural style is an approach to developing a single application as a **suite of small services**, each **running in its own process** and communicating with lightweight mechanisms, often an HTTP resource API. These services are **built around business capabilities** and **independently deployable** by fully automated deployment machinery. There is a **bare minimum of centralized management** of these services, which may be written in different programming languages and use different data storage technologies.

- 微服务是一种架构风格
- 一个应用拆分为一组小型服务
- 每个服务运行在自己的进程内，也就是可独立部署和升级
- 服务之间使用轻量级HTTP交互
- 服务围绕业务功能拆分
- 可以由全自动部署机制独立部署
- 去中心化，服务自治。服务可以使用不同的语言、不同的存储技术

### 1.4.2、分布式

### 1.4.3、云原生

## 1.5、如何学习SpringBoot

SpringBoot官方文档

https://docs.spring.io/spring-boot/docs/2.7.14/reference/html/

# 二、SpringBoot快速入门

## 2.1、创建maven项目

![image-20230725084809547](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725084816.png)

![image-20230725084938889](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725084938.png)

![image-20230725085038141](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725085038.png)

## 2.2、引入依赖

```xml
   <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>
	<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
	</dependencies>
```

## 2.3、添加主程序Application

```java
package com.lzx.springboot.main;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication; 

// TODO SpringBoot主程序入口
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```

> 🦄 在java包下一定要包否则会报错

## 2.4、创建Controller、添加注解

```java
package com.lzx.springboot.main.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController //包括 @Controller、@ResponseBody ==> 在浏览器中写入hello,SpringBoot 2!
public class HelloController {

    @RequestMapping("/hello")
    public String hello01() {
        return "hello,SpringBoot 2!";
    }
}
```

> 🐲 页面路由发生变化只是会在页面输出,不会发生页面跳转,需要用@ResponseBody进行标注。@RestController包含了@Controller、@ResponseBody两个注释

## 2.5、启动项目

> 🐱‍👤 直接点击绿色箭头进行运行，不需要添加Tomcat服务器

![image-20230725090633666](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725090633.png)

![image-20230725090553794](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725090553.png)

## 2.6、配置文件

在application.properties配置文件配置项目的文件

```properties
server.port=8888
```

参考SpringBoot配置的官方文档：https://docs.spring.io/spring-boot/docs/2.7.14/reference/html/application-properties.html#appendix.application-properties

## 2.7、部署项目

```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

> 🐲 项目打包成"jar"文件

![image-20230725091540095](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725091540.png)

![image-20230725091600900](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725091600.png)

![image-20230725091702542](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725091702.png)

![image-20230725091928176](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725091928.png)

![image-20230725092000500](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725092000.png)

![image-20230725092807539](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725092807.png)

![image-20230725092840180](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725092840.png)

> 🐖：已经打包的项目中的端口号若想修改需要吃重新打包

![image-20230725093016551](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230725093016.png)

# 三、自动配置原理

## 3.1、SpringBoot特点

### 3.1.1、依赖管理

- 父级依赖

```xml
<!--依赖管理，父级标签-->
<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
</parent>
<!--上述依赖的父级依赖如下-->
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.4.RELEASE</version>
  </parent>
<!--spring-boot-dependencies的文件如下-->
<properties>
    <activemq.version>5.15.13</activemq.version>
    <antlr2.version>2.7.7</antlr2.version>
    <appengine-sdk.version>1.9.82</appengine-sdk.version>
    <artemis.version>2.12.0</artemis.version>
    <aspectj.version>1.9.6</aspectj.version>
    <assertj.version>3.16.1</assertj.version>
    <atomikos.version>4.0.6</atomikos.version>
    <awaitility.version>4.0.3</awaitility.version>
    <bitronix.version>2.1.4</bitronix.version>
    <build-helper-maven-plugin.version>3.1.0</build-helper-maven-plugin.version>
  	..............
</properties>
```

> 👻 spring-boot-dependencies的文件中包含了很多已经内置的文件，导入他的子类就可以导入对应的配置文件对应的版本号

- starter场景启动器

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter</artifactId>
  <version>2.3.4.RELEASE</version>
  <scope>compile</scope>
</dependency>
```

> 🐱‍🚀 spring-boot-starter:场景启动器，引入它以后它对应的场景所需要的常规依赖就可以注入完毕了
>
> SpringBoot所有支持的场景如以下网址：
>
> https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-starter

- 无需关注版本号，自动版本仲裁

> 🦝 引入依赖的时候可以不写版本号，除非引入非版本仲裁的jar，必须写版本号

- 可以修改默认版本号

### 3.1.2、自动配置

#### 1、自动装配Tomcat服务器

```xml
<!--引入Tomcat服务器的依赖-->
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
</dependency>
```

#### 2、自动配置好SpringMVC

- 😀 引入SpringMVC全套组件

- 😁 自动配好SpringMVC常用组件（功能）

#### 3、自动配置Web常见功能

SpringBoot已经配置了所有web开发的常见场景

#### 4、添加注解包自动扫描

> 😼 默认添加@SpringBootApplication注释以后，标注的主程序所在的包及其下方的所有的包里面的组件都会被默认扫描出来

> 😽 若想改变扫描包的路径：@SpringBootApplication(scanBasePackages="xxxx")或者使用ComponentScan指定扫描路径。

```java
@SpringBootApplication
等同于
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("xxxxxxx")
```

#### 5、按需加载所有自动配置项

需要哪个场景就导入哪个starter，导入以后对应的场景就会开启，SpringBoot所有的自动配置功能都会在spring-boot-autoconfigure

## 3.2、容器功能

### 3.2.1、组件添加

#### 1、@Configuration

@Configuration通常标注一个类，@Bea通常标注一个方法，他们通常搭配使用。

> 🧐  简单粗暴理解就是：@Configuration标注的类相当于以前在Spring中配置的一个XML文件(用于创建对象的文件)，@Bean表示的方法相当于原Spring文件中\<bean>\</bean>标签。

  🦄 两个模式

- Lite模式  @Comfiguration(proxyBeanMethods = false)配置类组件之间没有任何依赖关系，此模式可以加速容器启动过程，减少判断，保证不管每个@Bean标识的方法调用多少次都是新创建方法。
- Full模式  @Comfiguration(proxyBeanMethods = true) 配置类组件之间有依赖关系，方法会被调用得到之前的单实例组件，此模式下可以保证不管每个@Bean方法被调用多少次都是单实例的

👻 测试实例

```java
@Configuration(proxyBeanMethods = false) //创建的对象都是新创建的
public class MyConfiguration {

    @Bean  //创建对象，相当于<bean>标签
    public User user() {
        User zhangsan = new User("zhangsan",18);
        //user组件依赖了pet组件
        zhangsan.setPet(tomcatPet());
        return zhangsan;
    }
    @Bean("tom")
    public Pet tomcatPet() {
        return new Pet("tomcat");
    }
}
```

若按照上述写法的话会有错误，在@Configuration(proxyBeanMethods = false)限制了@Bean之间不能有关联

![image-20230726091203411](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726091210.png)

上述的错误意思是：在@Configuration参数中proxyBeanMethods设置为了false，直接调用了带有@Bean的方法，将proxyBeanMethods设置为true或者使用依赖注入DI。

```java
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        //返回IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);
        //查看容器中的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println("容器中的组件名称： " + name);
        }
        //从容器中获取容器
        Pet tom = run.getBean("tomcatPet", Pet.class);
        Pet tom1 = run.getBean("tomcatPet", Pet.class);
        System.out.println("组件：" + (tom == tom1));
        MyConfiguration myConfiguration = run.getBean(MyConfiguration.class);
        System.out.println("myConfiguration = " + myConfiguration);
    }
```

按照上述写法，会报错，按理来说IOC容器中获取bean对象，默认方法名就是id、可按照上述写法还是会报错。

![image-20230726093745861](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726093745.png)

🤔 解决办法

将main()方法中的@SpringBootApplication注释修改为@SpringBootConfiguration、@EnableAutoConfiguration
@ComponentScan("xxxxx")的组合，注意：不是@SpringBootApplication和他们的组合是@SpringBootConfiguration，否则的话也会报错。

![image-20230726094116762](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726094116.png)

> 😧 冗余声明：@SpringBootApplication已经声明了@EnableAutoCinfiguration，在@Bean中设置名称以后在容器创建以后获取对象时候不能在使用方法名获取，否则会报错：No bean named "xxx" available

![image-20230726095638879](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726095638.png)

```java
package com.lzx.springboot.main;

import com.lzx.springboot.config.MyConfiguration;
import com.lzx.springboot.entity.Pet;
import com.lzx.springboot.entity.User;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.SpringBootConfiguration;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.ComponentScan;

@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.lzx.springboot")
public class MainApplication {
    public static void main(String[] args) {
        //返回IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);
        //查看容器中的组件
        String[] names = run.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println("容器中的组件名称： " + name);
        }
        //从容器中获取容器
        Pet tom = run.getBean("tom", Pet.class);
        Pet tom1 = run.getBean("tom", Pet.class);
        System.out.println("组件：" + (tom == tom1));
        MyConfiguration myConfiguration = run.getBean(MyConfiguration.class);
        System.out.println("myConfiguration = " + myConfiguration);
        
        User user = myConfiguration.user();
        User user1 = myConfiguration.user();
        System.out.println("User组件：" + (user == user1));

        User user2 = run.getBean("user", User.class);
        Pet tom2 = run.getBean("tom",Pet.class);
        System.out.println("用户的宠物是：" + (user2.getPet() == tom2));
    }

}
```

![image-20230726100221117](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726100221.png)

> 🐾 因MyConfiguration被@Configuration(proxyBeanMethods = true)标识，故为Full模式，此模式下被@Bean标识的方法无论被调用多少次，都是单例对象，保证各个类组件之间有依赖关系。

#### 2、@Bean

详细说明：Bean注解用于在Spring容器中创建一个bean对象，被标识的地方返回一个对象，Spring将该对象注册为一个bean，使其他组件可以使用，一般都是和@Configuration一起使用，一般标识在方法上。

实例

```java
@Configuration
public class AppConfig {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

#### 3、@Component

详细说明：Component注解用于标识一个普通的spring bean组件，一般表示在类上。

实例

```java
@Component
public class  MyComponent {
   //代码逻辑
}
```

#### 4、@Controller

详细说明：Controller注解用于标识一个类是SpringMVC中的控制器组件，用于处理客服端请求和返回相应的响应结果。

实例

```java
@Controller
public class MyController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }
}
```

#### 5、@Service

详细说明：Service注解用于标识一个类是Service服务层的组件，主要封装业务逻辑。

实例

```java
@Service
public class UserService {
    public void createUser(User user) {
        // 创建用户的业务逻辑
    }
}
```

#### 6、@Repository

详细说明：Reposity注解用于标识一个类是数据访问层的组件，通常用于数据库交互

实例

```java
@Service
public class UserService {
    public void createUser(User user) {
        // 创建用户的业务逻辑
    }
}
```

#### 7、@ComponentScan

详细说明：ComponentScan注解用于指定Spring中进行组件扫描时所需要扫描的包和类路径

实例

```java
@Configuration
@ComponentScan("xxxxx")
public class AppConfig {
    // 配置代码
}
```

#### 8、@Import

详细说明：Import注解用于引入其他的配置类和组件类，将他们收纳到当前的配置类的上下文中。

实例

```java
@Configuration
@Import({OtherConfig.class, OtherComponent.class})
public class AppConfig {
    // 配置代码
}
```

#### 9、@Conditional

条件装配：满足Conditional条件进行注入

![image-20230726110934116](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726110936.png)

```java
@Configuration(proxyBeanMethods = true) //各个类之间不能有依赖关系，创建的对象都是新创建的
@ConditionalOnMissingBean(name = "tom")
public class MyConfiguration {
}
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan("com.lzx.springboot")
public class MainApplication {
    public static void main(String[] args) {
        //返回IOC容器
        ConfigurableApplicationContext run = SpringApplication.run(MainApplication.class, args);
				boolean tom = run.containsBean("tom");
        System.out.println("容器中的Tom组件：" + tom);
        boolean user01 = run.containsBean("user01");
        System.out.println("容器中的user01组件：" + user01);
        boolean tom22 = run.containsBean("tom22");
        System.out.println("容器中的tom22组件：" + tom22);
    }
```

![image-20230726111320739](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726111320.png)

### 3.2.2、原生配置文件引入

#### @ImportResource

![image-20230726113619706](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726113620.png)

![image-20230726113720230](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726113720.png)

![image-20230726113803925](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726113803.png)

### 3.2.3、配置绑定

#### 1、@ConfigurationProperties

将Java读取的properties文件中的内容，封装到JavaBean中

#### 2、@EnableConfigurationProperties + @ConfigurationProperties

通常ConfigurationProperties注解和EnableConfigurationProperties 一起使用，EnableConfigurationProperties 用于开启对@ConfigurationProperties注解类的配置

#### 3、@Component + @ConfigurationProperties

```java
@EnableConfigurationProperties(Car.class)
//1、开启Car配置绑定功能
//2、把这个Car这个组件自动注册到容器中
public class MyConfig {
}
```

## 3.3、自动配置原理入门

### 3.3.1、引导加载自动配置类

#### 1、@SpringBootConfiguration

#### 2、@ComponentScan

#### 3、@EnableAutoConfiguration

##### (1)、@AutoConfigurationPackage

##### (2)、@Import(AutoConfigurationImportSelector.class)

### 3.3.2、按需开启自动配置项

### 3.3.3、修改默认配置

### 3.3.4、最佳实战

## 3.4、开发技巧

### 3.4.1、Lombok

> 🐂 作用：简化JavaBean的配置

在pom.xml文件中添加以下依赖：

```xml
  <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
</dependency>
```

在IDEA中搜索Lombok下载

![image-20230726141819931](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726141822.png)

```java
===============================简化JavaBean开发===================================
@NoArgsConstructor
//@AllArgsConstructor
@Data
@ToString
@EqualsAndHashCode
public class User {

    private String name;
    private Integer age;

    private Pet pet;

    public User(String name,Integer age){
        this.name = name;
        this.age = age;
    }


}
================================简化日志开发===================================
@Slf4j
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(@RequestParam("name") String name){
        
        log.info("请求进来了....");
        
        return "Hello, Spring Boot 2!"+"你好："+name;
    }
}
```

### 3.4.2、dev-tools

> 🐂 作用：在修改项目或者页面以后，按住ctrl + F9；

在pom.xml文件中添加以下依赖

```xml
<dependency>
  		<groupId>org.springframework.boot</groupId>
  		<artifactId>spring-boot-devtools</artifactId>
  		<optional>true</optional>
</dependency>
```

### 3.4.3、Spring Initailizr(项目初始化向导)

1、选择新建模块或者新建项目(此处是以新建模块为例)

![image-20230726142324038](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726142324.png)

2、修改项目配置

![image-20230726142628225](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726142628.png)

3、选择想要添加的配置

![image-20230726142825058](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726142825.png)

4、选择文件位置

![](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726142913.png)

# 四、配置文件

## 4.1、文件类型

### 4.1.1、properties

同以前Properties的用法

### 4.1.2、yaml

#### 1、简介

YAML，用来表达数据[序列化](https://baike.baidu.com/item/序列化?fromModule=lemma_inlink)的格式。是"YAML Ain't a Markup Language"（YAML不是一种[标记语言](https://baike.baidu.com/item/标记语言?fromModule=lemma_inlink)）的[递归缩写](https://baike.baidu.com/item/递归缩写?fromModule=lemma_inlink)。在开发的这种语言时，YAML的意思其实是："Yet Another Markup Language"（仍是一种[标记语言](https://baike.baidu.com/item/标记语言?fromModule=lemma_inlink)），但为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。

YAML非常适合用来做以数据为中心的配置文件。

#### 2、基本语法

- key: value；kv之间有空格
- 大小写敏感
- 使用缩进表示层级关系
- 缩进不允许使用tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- '#'表示注释
- 字符串无需加引号，如果要加，''与""表示字符串内容 会被 转义/不转义

#### 3、数据类型

- 字面量：单个的、不可再分的值。date、boolean、string、number、null

```yaml
k: v
```

- 对象：键值对的集合。map、hash、set、object 


```yaml
行内写法：  k: {k1:v1,k2:v2,k3:v3}
#或
k: 
	k1: v1
  k2: v2
  k3: v3
```

- 数组：一组按次序排列的值。array、list、queue

```yaml
行内写法：  k: [v1,v2,v3]
#或者
k:
 - v1
 - v2
 - v3
```

#### 4、实例

```yaml
# yaml表示上述对象
person:
  userName: zhangsan
  boss: false
  birth: 20919/12/12
  age: 18
  pet:
    name: tomcat
    weight: 23.4
  interests: [篮球,游泳]
  animal:
    -jerry
    -mario
  sorce:
    english: # 按照map集合的写法
      first: 30
      second: 40
      third: 50
    math: [143,45,4]
    chinese: {first: 123} # 按照map集合的写法
  salarys: [125,45,78,56]
  allPets:
    sick:
      - {name: tom}
      - {name: jerry,weight: 21}
    heakthy: [{name: mario,weight: 45}]
```

## 4.2、配置提示

自定义的类和配置文件绑定一般没有提示。

```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>

 <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.springframework.boot</groupId>
                            <artifactId>spring-boot-configuration-processor</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

# 五、Web开发

## 5.1、SpringMVC自动配置概览

Spring Boot provides auto-configuration for Spring MVC that **works well with most applications.(大多场景我们都无需自定义配置)**

The auto-configuration adds the following features on top of Spring’s defaults:

- Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.

- - 内容协商视图解析器和BeanName视图解析器

- Support for serving static resources, including support for WebJars (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content))).

- - 静态资源（包括webjars）

- Automatic registration of `Converter`, `GenericConverter`, and `Formatter` beans.

- - 自动注册 `Converter，GenericConverter，Formatter `

- Support for `HttpMessageConverters` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-spring-mvc-message-converters)).

- - 支持 `HttpMessageConverters` （后来我们配合内容协商理解原理）

- Automatic registration of `MessageCodesResolver` (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-spring-message-codes)).

- - 自动注册 `MessageCodesResolver` （国际化用）

- Static `index.html` support.

- - 静态index.html 页支持

- Custom `Favicon` support (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-spring-mvc-favicon)).

- - 自定义 `Favicon`  

- Automatic use of a `ConfigurableWebBindingInitializer` bean (covered [later in this document](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-spring-mvc-web-binding-initializer)).

- - 自动使用 `ConfigurableWebBindingInitializer` ，（DataBinder负责将请求数据绑定到JavaBean上）

  - If you want to keep those Spring Boot MVC customizations and make more [MVC customizations](https://docs.spring.io/spring/docs/5.2.9.RELEASE/spring-framework-reference/web.html#mvc) (interceptors, formatters, view controllers, and other features), you can add your own `@Configuration` class of type `WebMvcConfigurer` but **without** `@EnableWebMvc`.

    **不用@EnableWebMvc注解。使用** `**@Configuration**` **+** `**WebMvcConfigurer**` **自定义规则**

    

    If you want to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, or `ExceptionHandlerExceptionResolver`, and still keep the Spring Boot MVC customizations, you can declare a bean of type `WebMvcRegistrations` and use it to provide custom instances of those components.

    **声明** `**WebMvcRegistrations**` **改变默认底层组件**

    

    If you want to take complete control of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`, or alternatively add your own `@Configuration`-annotated `DelegatingWebMvcConfiguration` as described in the Javadoc of `@EnableWebMvc`.

    **使用** `**@EnableWebMvc+@Configuration+DelegatingWebMvcConfiguration 全面接管SpringMVC**`

## 5.2、静态页面功能分析

### 5.2.1、静态资源访问

#### 1、静态资源目录

静态资源放在类路径下： called `/static` (or `/public` or `/resources` or `/META-INF/resources`

访问：当前项目根目录 + 静态资源名

原理：静态映射/**；

> 🐱‍🏍 客户端发出请求以后，先在Controller处理，若不能处理就将所有的请求交给静态资源处理器，若静态资源处理器找不到则会报出404页面未找到

#### 2、静态资源访问前缀

默认无前缀

```yaml
spring:
  mvc:
    static-path-pattern: /res/**
```

#### 3、webjar

自动映射 /[webjars](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)/**

pom.xml文件引入以下依赖

```xml
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.5.1</version>
        </dependency>
```

访问地址：[http://localhost:8080/webjars/**jquery/3.5.1/jquery.js**](http://localhost:8080/webjars/jquery/3.5.1/jquery.js)   后面地址要按照依赖里面的包路径

![image-20230726162930203](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230726162932.png)

### 5.2.2、欢迎页支持

- 静态资源路径下  index.html
- - 可以配置静态资源路径
  - 但是不可以配置静态资源的访问前缀。否则导致 index.html不能被默认访问

```YAML
spring:
#  mvc:
#    static-path-pattern: /res/**   这个会导致welcome page功能失效

  resources:
    static-locations: [classpath:/haha/]
```

### 5.2.3、自定义Favicon

favicon.ico放在静态资源目录下即可

```yaml
spring:
#  mvc:
#    static-path-pattern: /res/**   这个会导致 Favicon 功能失效
```

### 5.2.4、静态资源配置原理

- SpringBoot启动默认加载  xxxAutoConfiguration 类（自动配置类）
- SpringMVC功能的自动配置类 WebMvcAutoConfiguration，生效

> 😎 源码分析

```java
/**
* WebMvcAutoConfiguration自动配置类
*/
@Configuration(proxyBeanMethods = false)  //标识配置类灭有代理bean对象的方法，以后每次调用此类的时候都是创建新的对象
@ConditionalOnWebApplication(type = Type.SERVLET) //原生的Servlet
@ConditionalOnClass({ Servlet.class, DispatcherServlet.class, WebMvcConfigurer.class })
@ConditionalOnMissingBean(WebMvcConfigurationSupport.class)//没有WebMvcConfigurationSupport类的话才创建
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE + 10)
@AutoConfigureAfter({ DispatcherServletAutoConfiguration.class, TaskExecutionAutoConfiguration.class,
		ValidationAutoConfiguration.class })
public class WebMvcAutoConfiguration {}
```

```java
@Configuration(proxyBeanMethods = false)
@Import(EnableWebMvcConfiguration.class)
@EnableConfigurationProperties({ WebMvcProperties.class, ResourceProperties.class })
@Order(0)
public static class WebMvcAutoConfigurationAdapter implements WebMvcConfigurer {}
```

#### 1、配置类只有一个参数

![image-20230727085705298](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727085712.png)

#### 2、资源处理的默认规则

![image-20230727090549741](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727090549.png)

```yaml
spring:
#  mvc:
#    static-path-pattern: /res/**
  resources:
    add-mappings: false   禁用所有静态资源规则
```

![image-20230727091003373](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727091003.png)

#### 3、欢迎页的处理规则

![image-20230727091346587](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727091346.png)

#### 4、favicon

## 5.3、请求参数处理

### 5.3.1、请求映射

#### 1、rest映射原理

Rest风格(使用Http请求动词来表示对资源的操作)

- 以前：/getUser 获取用户信息、/deleteUser 删除用户信息、/editUser修改用户信息、/saveUser保存用户信息

- 现在：/user GET-获取用户信息、/user DELETE-删除用户信息、/user PUST-保存用户信息、/user PUT-修改用户信息

- ```java
   @RequestMapping(value = "/user",method = RequestMethod.GET)
      public String getUser(){
          return "GET-张三";
      }
    
      @RequestMapping(value = "/user",method = RequestMethod.POST)
      public String saveUser(){
          return "POST-张三";
      }


      @RequestMapping(value = "/user",method = RequestMethod.PUT)
      public String putUser(){
          return "PUT-张三";
      }
      
      @RequestMapping(value = "/user",method = RequestMethod.DELETE)
      public String deleteUser(){
          return "DELETE-张三";
      }
  ```

- > 😺 默认表单提交只能是post和get请求，若想将put和delete请求传给浏览器，则必须修改表单的隐藏提交方式

```html
测试REST风格；
<form action="/user" method="get">
    <input value="REST-GET 提交" type="submit"/>
</form>
<form action="/user" method="post">
    <input value="REST-POST 提交" type="submit"/>
</form>
<form action="/user" method="post">
    <input name="_method" type="hidden" value="delete">
    <input value="REST-DELETE 提交" type="submit"/>
</form>
<form action="/user" method="post">
    <input name="_method" type="hidden" value="put">
    <input value="REST-PUT 提交" type="submit"/>
</form>
  ```

![image-20230727094150038](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727094150.png)

![image-20230727093639958](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727093640.png)

> 🐖 单单是修改隐藏域_method，点击发现没有任何效果，在hiddenHttpMethodFilter()方法中才发现，功能未开启，所以需要手动配置

![image-20230727094426522](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727094426.png)

```yaml
  hiddenmethod:
      filter:
        enabled: true
```

Rest执行过程：

1. 在表单中绑定_method方法，并且在表单提交的是post请求，在\_method方法中绑定的是"delete、put、patch"等请求
2. 浏览器点击发送请求被服务器的HiddenHttpMethodFilter拦截器所拦截，这个拦截器组件创建默认是未开启的，matchIfMissing = false，故此需要手动配置拦截器开启 "spring.mvc.hiddenmethod.filter.enabled"为true
3. 在被拦截器成功拦截以后，拦截器会在doFilterInternal()请求方法中做判断请求方式是否是"post"同时有没有错误，接着获取_method的值作为paramValue，再将paramValue转为大写
4. 接着判断此方法是否在PUT.name、DELETE.name、ATCH.name中，在的话就将请求方法和请求封装到HttpMethodRequestWrapper中，HttpMethodRequestWrapper重写了getMethod()方法
5. 最后在浏览器访问Controller的时候，接受的是requesWrapper

> 🐽 客户端发送put、delete请求的方式时候，不需要fliter

#### 2、请求映射原理

![image-20230727102659808](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727102659.png)

### 5.3.2、普通参数和基本注解

@PathVariable 路径参数

实例

```java
@RestController
public class ParamTestController {

    @GetMapping("/car/{id}/owner/{username}")
    public Map<String,Object> getCar(@PathVariable("id") Integer id,
                                     @PathVariable("username") String username,
                                     @PathVariable Map<String,String> pv) {
        HashMap<String, Object> map = new HashMap<>();
        map.put("id",id);
        map.put("username",username);
        map.put("pv",pv);
        return map;
    }
}
```

![image-20230727104912291](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727104912.png)

@RequestHeader 请求头

```java
@RestController
public class ParamTestController {

    @GetMapping("/car/{id}/owner/{username}")
    public Map<String,Object> getCar(@PathVariable("id") Integer id,
                                     @PathVariable("username") String username,
                                     @PathVariable Map<String,String> pv) {
        HashMap<String, Object> map = new HashMap<>();
        map.put("id",id);
        map.put("username",username);
        map.put("pv",pv);
        return map;
    }
}
```

![image-20230727105345412](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727105345.png)

@RequestParam 请求参数

@CookieValue cookie的值

```java
package com.lzx.springboot.demo.controller;

@RestController
public class ParamTestController {

    @GetMapping("/car/{id}/owner/{username}")
    public Map<String,Object> getCar(@PathVariable("id") Integer id,
                                     @PathVariable("username") String username,
                                     @PathVariable Map<String,String> pv,
                                     @RequestHeader("User-Agent") String userAgent,
                                     @RequestHeader Map<String,String> header,
                                     @RequestParam("age") Integer age,
                                     @RequestParam("inters") List<String> inters,
                                     @RequestParam Map<String,String> params,
                                     @CookieValue("Idea") String Idea,
                                     @CookieValue("Idea") Cookie cookie) {
        HashMap<String, Object> map = new HashMap<>();
//        map.put("id",id);
//        map.put("username",username);
//        map.put("pv",pv);
//        map.put("userAgent",userAgent);
//        map.put("headers",header);
        map.put("age",age);
        map.put("inters",inters);
        map.put("params",params);
        map.put("Idea",Idea);
        System.out.println(cookie.getName()+"===>"+cookie.getValue());
        return map;
    }
}
```

@RequestBody请求体

```java
 @PostMapping("/save")
    public Map postMethod(@RequestBody String content){
        Map<String,Object> map = new HashMap<>();
        map.put("content",content);
        return map;
    }
```

```html
<form action="/save" method="post">
    测试@RequestBody获取数据 <br/>
    用户名：<input name="userName"/> <br>
    邮箱：<input name="email"/>
    <input type="submit" value="提交"/>
</form>
```

@RequestAttribute 请求域中的值

```java
package com.lzx.springboot.demo.controller;

import org.springframework.http.HttpRequest;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestAttribute;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.servlet.http.HttpServletRequest;
import java.util.HashMap;
import java.util.Map;

/**
 * @ClassName RequestController
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/27 11:19:01
 * @Version 1.0
 **/
@Controller
public class RequestController {

    @GetMapping("/goto")
    public String goToPage(HttpServletRequest request) {

        request.setAttribute("msg","成功了。。。");
        request.setAttribute("code",200);
        return "forward:/success";
    }
    @ResponseBody
    @GetMapping("/success")
    public Map success (@RequestAttribute("msg") String msg,
                        @RequestAttribute("code") Integer code,
                        HttpServletRequest request) {
        Object msg1 = request.getAttribute("msg");
        HashMap<String, Object> map = new HashMap<>();
        map.put("reqMethod_msg",msg1);
        map.put("annotation_msg",msg);
        return map;
    }
}
```



### 5.3.3、POJO封装过程

自定义类型参数 封装POJO

```java
@Data
public class Person {
    private String userName;
    private Integer age;
    private Date birth;
    private Pet pet;
}
---------------------------------
@Data
public class Pet {
    private String name;
    private String age;
}

```

```html
<form action="/saveperson" method="post">
    姓名： <input name="userName" value="zhangsan"/> <br/>
    年龄： <input name="age" value="18"/> <br/>
    生日： <input name="birth" value="2019/12/10"/> <br/>
    宠物姓名：<input name="pet.name" value="阿猫"/><br/>
    宠物年龄：<input name="pet.age" value="5"/>
<!--    宠物： <input name="pet" value="啊猫3"/>-->
    <input type="submit" value="保存"/>
</form>
```

![image-20230727150921026](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727150922.png)

![image-20230727152829410](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727152829.png)

> 😁 以上错误的解决办法

```html
<form action="/saveperson" method="post">
    姓名： <input name="userName" value="zhangsan"/> <br/>
    年龄： <input name="age" value="18"/> <br/>
    生日： <input name="birth" value="2019/12/10"/> <br/>
<!--    宠物姓名：<input name="pet.name" value="阿猫"/><br/>-->
<!--    宠物年龄：<input name="pet.age" value="5"/>-->
    宠物： <input name="pet" value="啊猫,3"/>
    <input type="submit" value="保存"/>
</form>
```

```java
  @Override
		public void addFormatters(FormatterRegistry registry) {
      		registry.addConverter(new Converter<String, Pet>() {
            @Override
            public Pet convert(String s) {
              	if (!StringUtils.isEmpty(s)){
                  Pet pet = new Pet();
                  	String[] split = s.split(",");
                  		pet.setName(split[0]);
                  		pet.setAge(Integer.parseInt(split[1]));
                  return pet;
                }
              return null;
            }
          });
    }
```

![image-20230727152907834](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727152907.png)

## 5.4、数据响应与内容协商

### 5.4.1、响应JSON

#### 1、jackson.jar+@ResponseBody

导入以下依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
web场景自动引入了json场景
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-json</artifactId>
      <version>2.3.4.RELEASE</version>
      <scope>compile</scope>
    </dependency>
```

```java
@Controller
public class ResponseTestController {

    @ResponseBody  //标注为响应体，否则会报404错误
    @GetMapping("/test/person")
    public Person getPerson() {
        Person person = new Person();
        person.setUserName("张安");
        person.setAge(18);
        person.setBirth(new Date());
        return person;
    }
}
```

![image-20230727155415479](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727155415.png)

> 😎 给前端返回json数据

##### 1.1、返回值解析器

##### 1.2、返回值解析器原理

RequestResponseBodyMethodProcessor 可以处理返回值标了@ResponseBody 注解的。

- 利用 MessageConverters 进行处理 将数据写为json

- - 1、内容协商（浏览器默认会以请求头的方式告诉服务器他能接受什么样的内容类型）

  - 2、服务器最终根据自己自身的能力，决定服务器能生产出什么样内容类型的数据，

  - 3、SpringMVC会挨个遍历所有容器底层的 HttpMessageConverter ，看谁能处理？

- - - (1)、得到MappingJackson2HttpMessageConverter可以将对象写为json

    - (2)、利用MappingJackson2HttpMessageConverter将对象转为json再写出去

#### 2、SpringMVC到底支持哪些返回值

```java
ModelAndView
Model
View
ResponseEntity 
ResponseBodyEmitter
StreamingResponseBody
HttpEntity
HttpHeaders
Callable
DeferredResult
ListenableFuture
CompletionStage
WebAsyncTask
有 @ModelAttribute 且为对象类型的
@ResponseBody 注解 ---> RequestResponseBodyMethodProcessor；
```

### 5.4.2、内容协商

根据客户端不同的接收能力，返回不同的媒体类型数据	

##### 1、引入xml依赖

```xml
 <dependency>
            <groupId>com.fasterxml.jackson.dataformat</groupId>
            <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

![image-20230727161844598](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727161844.png)

##### 2、postman分别测试返回json和xml

![image-20230727162028559](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727162028.png)

> 😏 默认postman的Accept是\*/\*，可以执行所有的类型

![image-20230727162247606](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727162247.png)

![image-20230727162329117](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727162329.png)

##### 3、开启浏览器参数方式内容协商功能

导入以下依赖

```yaml
spring:
    contentnegotiation:
      favor-parameter: true  #开启请求参数内容协商模式
```

访问路径：http://localhost:8080/test/person?format=json

![image-20230727164307352](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727164307.png)

访问路径：http://localhost:8080/test/person?format=xml

![image-20230727164322818](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230727164322.png)

## 5.5、视图解析与模板引擎

### 5.5.1、视图解析

#### 视图解析原理流程

### 5.5.2、模板引擎-Thymeleaf

#### 1、thymeleaf简介

Thymeleaf is a modern server-side Java template engine for both web and standalone environments, capable of processing HTML, XML, JavaScript, CSS and even plain text.

现代化、服务端Java模板引擎

#### 2、基本语法

##### 2.1、表达式

| 表达式名字 | 语法   | 用途                               |
| ---------- | ------ | ---------------------------------- |
| 变量取值   | ${...} | 获取请求域、session域、对象等值    |
| 选择变量   | *{...} | 获取上下文对象值                   |
| 消息       | #{...} | 获取国际化等值                     |
| 链接       | @{...} | 生成链接                           |
| 片段表达式 | ~{...} | jsp:include 作用，引入公共页面片段 |

##### 2.2、字面量

文本值: **'one text'** **,** **'Another one!'** **,…**数字: **0** **,** **34** **,** **3.0** **,** **12.3** **,…**布尔值: **true** **,** **false**

空值: **null**

变量： one，two，.... 变量不能有空格

##### 2.3、文本操作

字符串拼接: **+**

变量替换: **|The name is ${name}|** 

##### 2.4、数学运算

运算符: + , - , * , / , %

##### 2.5、布尔运算

运算符:  **and** **,** **or**

一元运算: **!** **,** **not** 

##### 2.6、比较运算

比较: **>** **,** **<** **,** **>=** **,** **<=** **(** **gt** **,** **lt** **,** **ge** **,** **le** **)**等式: **==** **,** **!=** **(** **eq** **,** **ne** **)** 

##### 2.7、条件运算

If-then: **(if) ? (then)**

If-then-else: **(if) ? (then) : (else)**

Default: (value) **?: (defaultvalue)** 

##### 2.8、特殊操作

无操作： _

#### 3、设置属性值-th:attr

```html
<form action="subscribe.html" th:attr="action=@{/subscribe}">
  <fieldset>
    <input type="text" name="email" />
    <input type="submit" value="Subscribe!" th:attr="value=#{subscribe.submit}"/>
  </fieldset>
</form>
```

#### 4、迭代

```html
<tr th:each="prod : ${prods}">
        <td th:text="${prod.name}">Onions</td>
        <td th:text="${prod.price}">2.41</td>
        <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

#### 5、条件运算

```html
<a href="comments.html"
th:href="@{/product/comments(prodId=${prod.id})}"
th:if="${not #lists.isEmpty(prod.comments)}">view</a>
```

#### 6、属性优先级

### 5.5.3、thymeleaf使用

#### 1、引入Starter

```xml
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
```

#### 2、自动配置thymeleaf

- 1、所有thymeleaf的配置值都在 ThymeleafProperties
- 2、配置好了 **SpringTemplateEngine** 
- **3、配好了** **ThymeleafViewResolver** 
- 4、我们只需要直接开发页面

```java
@Configuration(proxyBeanMethods = false)
@EnableConfigurationProperties(ThymeleafProperties.class)
@ConditionalOnClass({ TemplateMode.class, SpringTemplateEngine.class })
@AutoConfigureAfter({ WebMvcAutoConfiguration.class, WebFluxAutoConfiguration.class })
public class ThymeleafAutoConfiguration { }
```

```java
	public static final String DEFAULT_PREFIX = "classpath:/templates/";

	public static final String DEFAULT_SUFFIX = ".html";  //xxx.html
```

#### 3、页面开发

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>成功</title>
</head>
<body>
<h1 th:text="${msg}">含哈哈</h1>
    <a href="www.atguigu.com" th:href="${link}">去百度</a><br/>
    <a href="http://www.atguigu.com" th:href="@{link}">去百度</a>
</h1>
</body>
</html>
```

```java
@Controller
public class ThymeleafTestController {

    @GetMapping("/lzx")
    public String getLzx(Model model) {
        //model中的数据会被方到请求域中 request.setAttribute(""),将数据放到前端页面进行渲染
        model.addAttribute("msg","你好，李子雄");
        model.addAttribute("link","http://www.baidu.com");
        return "success";
    }
}
```

### 5.5.4、构建后台管理系统

#### 1、项目创建

thymeleaf、web-starter、devtools、lombok

#### 2、静态资源处理

自动配置好，我们只需要把所有静态资源放到 static 文件夹下

#### 3、路径构建

```html
 <form class="form-signin" action="index.html" method="post" th:action="@{/login}">
        <div class="form-signin-heading text-center">
            <h1 class="sign-title">Sign In</h1>
            <img src="images/login-logo.png" alt=""/>
        </div>
        <div class="login-wrap">
            <input type="text" class="form-control" placeholder="User ID" autofocus>
            <input type="password" class="form-control" placeholder="Password">

            <button class="btn btn-lg btn-login btn-block" type="submit">
                <i class="fa fa-check"></i>
            </button>

            <div class="registration">
                Not a member yet?
                <a class="" href="registration.html">
                    Signup
                </a>
            </div>
            <label class="checkbox">
                <input type="checkbox" value="remember-me"> Remember me
                <span class="pull-right">
                    <a data-toggle="modal" href="#myModal"> Forgot Password?</a>

                </span>
            </label>

        </div>

        <!-- Modal -->
        <div aria-hidden="true" aria-labelledby="myModalLabel" role="dialog" tabindex="-1" id="myModal" class="modal fade">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                        <h4 class="modal-title">Forgot Password ?</h4>
                    </div>
                    <div class="modal-body">
                        <p>Enter your e-mail address below to reset your password.</p>
                        <input type="text" name="email" placeholder="Email" autocomplete="off" class="form-control placeholder-no-fix">

                    </div>
                    <div class="modal-footer">
                        <button data-dismiss="modal" class="btn btn-default" type="button">Cancel</button>
                        <button class="btn btn-primary" type="button">Submit</button>
                    </div>
                </div>
            </div>
        </div>
        <!-- modal -->

    </form>
```

```java
@Controller
public class LoginController {

    @GetMapping(value = {"/","/login"})
    public String login() {
        return "login";
    }

    //处理请求登录的表单  每次刷新都需要重新提交表单
    @PostMapping("/login")
    public String login(String username,String password) {
        return "redirect:/main.html";
    }
    //重定向页面解决了上述问题,重定向是get请求
    @GetMapping("/main.html")
    public String getMain() {
        return "main";
    }
}
```

#### 4、页面跳转

```java
package com.lzx.springboot.demo.controller;

import javax.servlet.http.HttpSession;

@Controller
public class LoginController {

    @GetMapping(value = {"/","/login"})
    public String login() {
        return "login";
    }

    //处理请求登录的表单  每次刷新都需要重新提交表单
    @PostMapping("/login")
    public String login(User user, HttpSession session, Model model) {
        if (StringUtils.hasLength(user.getUsername()) && "123456".equals(user.getPassword())) {
            //把登录成功的用户保存起来
            session.setAttribute("loginUser",user);
            //账号密码正确重定向到main.html，重定向防止表单重复提交
            return "redirect:/main.html";
        }else {
            model.addAttribute("msg","账号密码错误");
            return "login";
        }

    }
    //重定向页面解决了上述问题,重定向是get请求
    @GetMapping("/main.html")
    public String getMain(HttpSession session,Model model) {
        Object loginUser = session.getAttribute("loginUser");
        if (loginUser != null) {
            return "main";
        }else {
            model.addAttribute("msg","请重新登录");
            return "login";
        }
    }
}
```

#### 5、数据渲染

```java
    @GetMapping("/dynamic_table")
    public String dynamic_table(Model model){
        //表格内容的遍历
        List<User> users = Arrays.asList(new User("zhangsan", "123456"),
                new User("lisi", "123444"),
                new User("haha", "aaaaa"),
                new User("hehe ", "aaddd"));
        model.addAttribute("users",users);

        return "table/dynamic_table";
    }
```

```html
<table class="display table table-bordered" id="hidden-table-info">
  <thead>
    <tr>
      <th>#</th>
      <th>用户名</th>
      <th>密码</th>
    </tr>
  </thead>
  <tbody>
    <tr class="gradeX" th:each="user,stats:${users}">
      <td th:text="${stats.count}">Trident</td>
      <td th:text="${user.userName}">Internet</td>
      <td >[[${user.password}]]</td>
    </tr>
  </tbody>
</table>
```

## 5.6、拦截器

### 5.6.1、拦截器实现的步骤

#### 1、创建拦截器类实现HandlerInterceptor 接口

```java
package com.lzx.springboot.demo.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

/**
 * @ClassName LoginInterceptor
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/28 10:03:45
 * @Version 1.0
 **/
public class LoginInterceptor implements HandlerInterceptor {
    /**
     * 目标方法执行之前
     * @param request
     * @param response
     * @param handler
     * @return
     * @throws Exception
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //登录检查的逻辑
        HttpSession session = request.getSession();
        Object user = session.getAttribute("loginUser");
        if (user != null) {
            //放行
            return true;
        }
        //拦截，未登录 跳转到登录页面
        request.setAttribute("msg","请先登录");
        request.getRequestDispatcher("/").forward(request,response);
        return false;
    }

    /**
     * 目标方法执行之后
     * @param request
     * @param response
     * @param handler
     * @param modelAndView
     * @throws Exception
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    /**
     * 页面渲染之后
     * @param request
     * @param response
     * @param handler
     * @param ex
     * @throws Exception
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}
```

#### 2、配置拦截器，将拦截器注册到容器中(实现WebMvcConfigurer的addInterceptors)

```java
package com.lzx.springboot.demo.config;

import com.lzx.springboot.demo.interceptor.LoginInterceptor;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * @ClassName AdminWebConfig
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/28 10:10:16
 * @Version 1.0
 **/
@Configuration
public class AdminWebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor())
                .addPathPatterns("/**")//所有请求都会被拦截，包括静态资源
                .excludePathPatterns("/","/login","/css/**","/fonts/**","/images/**","/js/**");//放行的请求

    }
}
```

#### 3、指定拦截器拦截规则(🐖 若是拦截所有，静态资源也会被拦截)

```java
      //登录检查的逻辑
        HttpSession session = request.getSession();
        Object user = session.getAttribute("loginUser");
        if (user != null) {
            //放行
            return true;
        }
        //拦截，未登录 跳转到登录页面
        request.setAttribute("msg","请先登录");
        request.getRequestDispatcher("/").forward(request,response);
        return false;
    }
```

### 5.6.2、拦截器实现的原理

![image-20230728100607453](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728100616.png)

## 5.7、文件上传

### 5.7.1、页面上传代码

```html
 <form role="form" th:action="@{/upload}" method="post" enctype="multipart/form-data">
                            <div class="form-group">
                                <label for="exampleInputEmail1">邮箱</label>
                                <input type="email" name="email" class="form-control" id="exampleInputEmail1" placeholder="请输入邮箱">
                            </div>
                            <div class="form-group">
                                <label for="exampleInputPassword1">名字</label>
                                <input type="text" name="username" class="form-control" id="exampleInputPassword1" placeholder="请输入名字">
                            </div>
                            <div class="form-group">
                                <label for="exampleInputFile">头像</label>
                                <input type="file" name="headerImg" id="exampleInputFile">
                                <p class="help-block">Example block-level help text here.</p>
                            </div>
                            <div class="form-group">
                                <label for="exampleInputFile">生活照</label>
                                <input type="file" name="photos" multiple>
                                <p class="help-block">Example block-level help text here.</p>
                            </div>
                            <div class="checkbox">
                                <label>
                                    <input type="checkbox"> Check me out
                                </label>
                            </div>
                            <button type="submit" class="btn btn-primary">Submit</button>
                        </form>
```

### 5.7.2、后台逻辑处理代码

```java
    //文件上传的方法
    @PostMapping("upload")
    public String upload(@RequestParam("email") String email,
                         @RequestParam("username") String username,
                         @RequestPart("headerImg") MultipartFile headerImg,
                         @RequestPart("photos") MultipartFile[] photos)  throws IOException{
        if (!headerImg.isEmpty()) {
            //保存到文件服务器
            String originalFilename = headerImg.getOriginalFilename(); //原始文件名称
            headerImg.transferTo(new File("E:\\img\\" + originalFilename));
        }
        if (photos.length > 0) {
            for (MultipartFile photo : photos) {
                if (!photo.isEmpty()) {
                    String photoOriginalFilename = photo.getOriginalFilename();
                    photo.transferTo(new File("E:\\img\\" + photoOriginalFilename));
                }
            }
        }
        return "main";
    }
```

![image-20230728105721555](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728105721.png)

## 5.8、Web原生组件注入(Servlet、Filter、Listener)

### 5.8.1、原生注入Servlet

```java
@ServletComponentScan(basePackages = "com.lzx.springboot.demo.servlet")
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

```java
package com.lzx.springboot.demo.servlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet(urlPatterns = "/my")
public class MyServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("66666");
    }
}
```

### 5.8.2、原生注入Filter

![image-20230728112409899](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728112410.png)

```java
package com.lzx.springboot.demo.filter;

import lombok.extern.slf4j.Slf4j;
import sun.rmi.runtime.Log;

import javax.servlet.*;
import javax.servlet.annotation.WebFilter;
import java.io.IOException;

/**
 * @ClassName MyFilter
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/28 11:16:55
 * @Version 1.0
 **/
@Slf4j
@WebFilter(urlPatterns ={"/css/*","/images/*"})
public class MyFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        log.info("MyFilter初始化完成");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        log.info("MyFilter工作");
        chain.doFilter(request,response);
    }

    @Override
    public void destroy() {
        log.info("MyFilter销毁");
    }
}
```

### 5.8.3、原生注入Listener

![image-20230728112738153](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728112738.png)

```java
@Slf4j
@WebListener
public class MyListener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        log.info("MyListener监听到项目初始化完成");
    }
    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        log.info("MyListener监听到项目销毁完成");
    }
}
```

# 六、数据访问

## 6.1、数据源的自动配置-HikariDataSource

### 6.1.1、导入JDBC场景

导入以下依赖

```xml
   <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jdbc</artifactId>
    </dependency>
```

### 6.1.2、修改配置项

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db_account
    username: root
    password: 123456
    driver-class-name: com.mysql.jdbc.Driver
```

### 6.1.3、测试

```java
@Slf4j
@SpringBootTest
class Boot05WebAdminApplicationTests {
    @Autowired
    JdbcTemplate jdbcTemplate;
    @Test
    void contextLoads() {

//        jdbcTemplate.queryForObject("select * from account_tbl")
//        jdbcTemplate.queryForList("select * from account_tbl",)
        Long aLong = jdbcTemplate.queryForObject("select count(*) from account_tbl", Long.class);
        log.info("记录总数：{}",aLong);
    }
}
```

## 6.2、使用Druid数据源

### 6.2.1、druid官方github地址

https://github.com/alibaba/druid

整合第三方技术的两种方式

- 自定义
- 找starter

### 6.2.2、自定义方式

创建数据源

```xml
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.17</version>
        </dependency>

<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
		destroy-method="close">
		<property name="url" value="${jdbc.url}" />
		<property name="username" value="${jdbc.username}" />
		<property name="password" value="${jdbc.password}" />
		<property name="maxActive" value="20" />
		<property name="initialSize" value="1" />
		<property name="maxWait" value="60000" />
		<property name="minIdle" value="1" />
		<property name="timeBetweenEvictionRunsMillis" value="60000" />
		<property name="minEvictableIdleTimeMillis" value="300000" />
		<property name="testWhileIdle" value="true" />
		<property name="testOnBorrow" value="false" />
		<property name="testOnReturn" value="false" />
		<property name="poolPreparedStatements" value="true" />
		<property name="maxOpenPreparedStatements" value="20" />
```

### 6.2.3、使用官方starter方式

#### 1、引入druid-starter

```xml
<dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid-spring-boot-starter</artifactId>
      <version>1.1.17</version>
</dependency>
```

#### 2、配置示例

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/db_account
    username: root
    password: 123456
    driver-class-name: com.mysql.jdbc.Driver

    druid:
      aop-patterns: com.atguigu.admin.*  #监控SpringBean
      filters: stat,wall     # 底层开启功能，stat（sql监控），wall（防火墙）

      stat-view-servlet:   # 配置监控页功能
        enabled: true
        login-username: admin
        login-password: admin
        resetEnable: false
        
      web-stat-filter:  # 监控web
        enabled: true
        urlPattern: /*
        exclusions: '*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*'

      filter:
        stat:    # 对上面filters里面的stat的详细配置
          slow-sql-millis: 1000
          logSlowSql: true
          enabled: true
        wall:
          enabled: true
          config:
            drop-table-allow: false
```

SpringBoot配置示例

https://github.com/alibaba/druid/tree/master/druid-spring-boot-starter

 配置项列表[https://github.com/alibaba/druid/wiki/DruidDataSource%E9%85%8D%E7%BD%AE%E5%B1%9E%E6%80%A7%E5%88%97%E8%A1%A8](https://github.com/alibaba/druid/wiki/DruidDataSource配置属性列表)

## 6.3、整合MyBatis操作

https://github.com/mybatis

starter

SpringBoot官方的Starter：spring-boot-starter-*

第三方的： *-spring-boot-starter

导入以下依赖：

```xml
<dependency>
      <groupId>org.mybatis.spring.boot</groupId>
      <artifactId>mybatis-spring-boot-starter</artifactId>
      <version>2.1.4</version>
</dependency>
```

### 6.3.1、配置模式

- 全局配置文件
- SqlSessionFactory: 自动配置好了
- SqlSession：自动配置了 SqlSessionTemplate 组合了SqlSession
- @Import(AutoConfiguredMapperScannerRegistrar**.**class）；
- Mapper： 只要我们写的操作MyBatis的接口标准了 @Mapper 就会被自动扫描进来

```yaml
# 配置mybatis规则
mybatis:
  #  config-location: classpath:mybatis/mybatis-config.xml
  mapper-locations: classpath:mybatis/mapper/*.xml
  configuration:
    map-underscore-to-camel-case: true
  # 可以不写全局；配置文件，所有全局配置文件的配置都放在configuration配置项中即可
```

### 6.3.2、注解模式

- 引入mybatis-starter
- 配置application.yaml中，指定mapper-location位置即可
- 编写Mapper接口并标注@Mapper注解
- 简单方法直接注解方式
- 复杂方法编写mapper.xml进行绑定映射
- @MapperScan("com.atguigu.admin.mapper") 简化，其他的接口就可以不用标注@Mapper注解

```java
@Mapper
public interface CityMapper {

    @Select("select * from city where id=#{id}")
    public City getById(Long id);
    public void insert(City city);

}
```

## 6.4、整合 MyBatis-Plus

### 6.4.1、什么是MyBatis-Plus

[MyBatis-Plus](https://github.com/baomidou/mybatis-plus)（简称 MP）是一个 [MyBatis](http://www.mybatis.org/mybatis-3/) 的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

[mybatis plus 官网](https://baomidou.com/)

建议安装 **MybatisX** 插件 

### 6.4.2、整合MyBatis-Plus

导入以下依赖：

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.1</version>
</dependency>
```

自动配置

- MybatisPlusAutoConfiguration 配置类，MybatisPlusProperties 配置项绑定。**mybatis-plus：xxx 就是对****mybatis-plus的定制**
- **SqlSessionFactory 自动配置好。底层是容器中默认的数据源**
- **mapperLocations 自动配置好的。有默认值。****classpath\*:/mapper/\**/\*.xml；任意包的类路径下的所有mapper文件夹下任意路径下的所有xml都是sql映射文件。  建议以后sql映射文件，放在 mapper下**
- **容器中也自动配置好了** **SqlSessionTemplate**
- **@Mapper 标注的接口也会被自动扫描；建议直接** @MapperScan(**"com.atguigu.admin.mapper"**) 批量扫描就行

**优点：**

-  只需要我们的Mapper继承 **BaseMapper** 就可以拥有crud能力

### 6.4.3、CRUD功能

#### 1、创建数据库表

```mysql
CREATE DATABASE `mybatis_plus` /*!40100 DEFAULT CHARACTER SET utf8mb4 */;
use `mybatis_plus`;
CREATE TABLE `user` (
`id` bigint(20) NOT NULL COMMENT '主键ID',
`name` varchar(30) DEFAULT NULL COMMENT '姓名',
`age` int(11) DEFAULT NULL COMMENT '年龄',
`email` varchar(50) DEFAULT NULL COMMENT '邮箱',
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

添加数据

```mysql
INSERT INTO user (id, name, age, email) VALUES
(1, 'Jone', 18, 'test1@baomidou.com'),
(2, 'Jack', 20, 'test2@baomidou.com'),
(3, 'Tom', 28, 'test3@baomidou.com'),
(4, 'Sandy', 21, 'test4@baomidou.com'),
(5, 'Billie', 24, 'test5@baomidou.com');
```

#### 2、导入MyBatis-Plus的依赖并且配置相关类

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.5.1</version>
</dependency>
```

```yaml
spring:
# 配置数据源信息
datasource:
# 配置数据源类型
type: com.zaxxer.hikari.HikariDataSource
# 配置连接数据库信息
driver-class-name: com.mysql.cj.jdbc.Driver
url: jdbc:mysql://localhost:3306/mybatis_plus?characterEncoding=utf-
8&useSSL=false
username: root
password: 123456
```

#### 3、创建实体类

```java
@Data
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
}
```

#### 4、创建mapper

```java
public interface UserMapper extends BaseMapper<User> {}
```

#### 5、创建测试类

```java
@SpringBootTest
public class MybatisPlusTest {

    @Autowired
    private UserMapper userMapper;

    @Test
    public void testSelectList() {
        userMapper.selectList(null).forEach(System.out::println);
    }
}
```

![image-20230728164404323](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728164406.png)

# 七、MyBatis-Plus

## 7.1、基本CRUD

### 7.1.1、插入

```java
@Test
    public void testInsert() {
        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        int insert = userMapper.insert(user);
        System.out.println("受影响的行数：" + insert);
        System.out.println("id自动获取的值：" + user.getId());
    }
```

![image-20230728170004440](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728170004.png)

### 7.1.2、删除

##### 1、通过id删除

```java
@Test
    public void testDelete() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        int deleteById = userMapper.deleteById(1684852328060022785L);
        System.out.println("受影响的行数：" + deleteById);
    }
```

##### 2、通过id批量删除

```java
 @Test
    public void testDeleteBatchIds() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        List<Long> asList = Arrays.asList(1L, 2L, 3L);
        int deleteById = userMapper.deleteBatchIds(asList);
        System.out.println("受影响的行数：" + deleteById);
    }
```

![image-20230728170509099](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728170509.png)

##### 3、通过map条件删除

```java
 @Test
    public void testDeleteByMap() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        HashMap<String, Object> map = new HashMap<>();
        map.put("name","张三");
        map.put("age",23);
        int deleteById = userMapper.deleteByMap(map);
        System.out.println("受影响的行数：" + deleteById);
    }
```

![image-20230728170754282](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728170754.png)

### 7.1.3、修改

```java
@Test
    public void testUpdateById() {
        User user = new User(4L, "admin", 22, null);
//        HashMap<String, Object> map = new HashMap<>();
        int deleteById = userMapper.updateById(user);
        System.out.println("受影响的行数：" + deleteById);
    }
```

![image-20230728170943609](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728170943.png)

### 7.1.4、查询

#### 1、查询所有数据

```java
@Test
    public void testSelectList() {userMapper.selectList(null).forEach(System.out::println);}
```

![image-20230728171238109](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728171238.png)

#### 2、通过id查询

```java
 @Test
    public void testSelectById() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        User user = userMapper.selectById(4L);
        System.out.println("user = " + user);
    }
```

![image-20230728171841224](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728171841.png)

#### 3、通过map条件查询

```java
@Test
    public void testSelectByMap() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        HashMap<String, Object> map = new HashMap<>();
        map.put("name", "admin");
        map.put("age",23);
        List<User> users = userMapper.selectByMap(map);
        for (User user : users) {
            System.out.println("user = " + user);
        }
    }
```

![image-20230728171926784](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728171926.png)

#### 4、通过多个id进行条件查询

```java
 @Test
    public void testSelectBatchIds() {
//        User user = new User(null, "张三", 23, "zhangsan@atguigu.com");
        List<Long> asList = Arrays.asList(2L, 3L, 4L);
        List<User> users = userMapper.selectBatchIds(asList);
        for (User user : users) {
            System.out.println("user = " + user);
        }
    }
```

![image-20230728172010312](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728172010.png)

#### 5、通用Service

创建Service接口和实现类

```java
public interface UserService extends IService<User> {}
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService {}
--------------------------------------
   @Autowired
    private UserService userService;

    @Test
    public void testGetCount() {
        long count = userService.count();
        System.out.println("总记录数为：" + count);
    }
```

![image-20230728174252948](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728174253.png)

#### 6、批量插入

```java
    @Test
    public void testSaveBatch() {
        ArrayList<User> users = new ArrayList<>();

        for (int i = 0; i < 5; i++) {
            User user = new User();
            user.setName("abc" + i);
            user.setAge(21 + i);
            users.add(user);
        }
        userService.saveBatch(users);
    }
```

![image-20230728174948656](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728174948.png)

## 7.2、常见注解

#### @TableLogic

```java
public class User {
    private Long id;
    private String name;
    private Integer age;
    private String email;
    @TableLogic
    private Integer isDeleted;
}
```

![image-20230728180106550](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728180106.png)

![image-20230728180222016](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728180222.png)

## 7.3、插件

### 分页插件

##### 添加配置类

```java
@Configuration
@MapperScan("com.lzx.springboot.demo.mapper")
public class MybatisPlusConfig {

    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new
                PaginationInnerInterceptor(DbType.MYSQL));
        return interceptor;
    }
}
```

##### 测试

```java
    @Test
    public void testPage(){
        //设置分页参数
        Page<User> page = new Page<>(1, 5);
        userMapper.selectPage(page, null);
        //获取分页数据
        List<User> list = page.getRecords();
        list.forEach(System.out::println);
        System.out.println("当前页："+page.getCurrent());
        System.out.println("每页显示的条数："+page.getSize());
        System.out.println("总记录数："+page.getTotal());
        System.out.println("总页数："+page.getPages());
        System.out.println("是否有上一页："+page.hasPrevious());
        System.out.println("是否有下一页："+page.hasNext());
    }
```

![image-20230728181004457](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728181004.png)

## 7.5、代码生成器

引入依赖

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.5.1</version>
</dependency>
<dependency>
    <groupId>org.freemarker</groupId>
    <artifactId>freemarker</artifactId>
    <version>2.3.31</version>
</dependency>
```

```java
 public static void main(String[] args) {
        FastAutoGenerator.create("jdbc:mysql://127.0.0.1:3306/lzx?characterEncoding=utf-8&userSSL=false", "root", "123456")
                        .globalConfig(builder -> {
                            builder.author("lzx") // 设置作者//.enableSwagger() // 开启 swagger 模式
                                    .fileOverride() // 覆盖已生成文件
                                    .outputDir("D://mybatis_plus"); // 指定输出目录
                        })
                        .packageConfig(builder -> {
                            builder.parent("com.lzx.springboot.demo") // 设置父包名
                                    .moduleName("mybatisplus") // 设置父包模块名
                                    .pathInfo(Collections.singletonMap(OutputFile.mapperXml, "D://mybatis_plus"));// 设置mapperXml生成路径
                        })
                        .strategyConfig(builder -> {
                            builder.addInclude("t_emp") // 设置需要生成的表名
                                    .addTablePrefix("t_", "c_"); // 设置过滤表前缀
                        })
                        .templateEngine(new FreemarkerTemplateEngine())// 使用Freemarker引擎模板，默认的是Velocity引擎模板
                        .execute();
 }
```

![image-20230728181659793](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230728181659.png)

# 八、单元测试

## 8.1、JUnit5 的变化

## 8.2、JUnit5常用注解

## 8.3、断言（assertions）

## 8.4、前置条件（assumptions）

## 8.5、嵌套测试

## 8.6、参数化测试

## 8.7、迁移指南
