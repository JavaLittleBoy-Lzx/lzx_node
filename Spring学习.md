[TOC]

## 一、Spring框架的概述

### 1.1 Spring框架介绍

Spring是一个轻量级的开源的Java2EE框架

### 1.2 Spring的主要优点

Spring可以解决企业开发的复杂性

### 1.3 Spring概念介绍

#### 1、IOC

IOC:全称 Inversion of Control(控制反转)，把创建对象的过程交给Spring进行管理

#### 2、AOP

AOP:全称 Aspect Orient Programming(面向切面编程)：不修改源码的基础上进行功能的增强

### 1.4 Spring的特点

1. 方便解耦，简化开发
2. 方便编程测试
3. 方便和其他程序进行整合
4. 降低API的使用难度

### 1.5 入门案例

#### 1、下载Spring5方法

- 输入https://spring.io/进入页面

  ![image-20230717152924995](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717152925.png)

  ![image-20230717153127398](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717153127.png)

  ![image-20230717153212097](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717153212.png)

  ![image-20230717153312303](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717153312.png)

当前版本为5.2.6

下载的地址为：(可直接复制下方地址进行访问)

https://repo.spring.io/release/org/springframework/spring/

下载完毕以后的压缩包

![image-20230717154237000](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717154237.png)

解压后的文件夹

![image-20230717154327739](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717154327.png)

![image-20230717154607599](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717154607.png)



#### 2、创建Spring项目

创建项目所需要的jar包

![image-20230717153833871](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717153833.png)

新建model模块

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717154819.png" alt="image-20230717154819466" style="zoom: 67%;" />

![image-20230717154939884](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717154939.png)

![image-20230717155158592](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717155158.png)

![image-20230717155400156](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717155400.png)

![image-20230717155505427](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717155505.png)

将项目所需要的jar包复制到libs目录下

将这些jar包引入到SpringDemo项目中

![image-20230717160132332](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717160132.png)

![image-20230717160307928](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717160308.png)

![image-20230717161451739](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230717161451.png)选择完毕以后点击"Apply"应用

#### 3、利用Spring创建对象 

创建对象的普通方法

```java
package com.lzx;

/**
 * @ClassName User
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/17 16:18:56
 * @Version 1.0
 **/
public class User {
    private Integer number;
    private String name;

    public Integer getNumber() {
        return number;
    }

    public void setNumber(Integer number) {
        this.number = number;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    public void add(){
        System.out.println("你好啊，Spring5");
    }
}
class UserDemo {
    public static void main(String[] args) {
        //实例化User对象
        User user = new User();
        user.add();
    }
}
```

利用Spring创建对象的方式有两种

1. 利用xml文件进行创建对象(本次使用此方法)

xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--配置User对象的创建-->
    <bean id="user" class="com.lzx.User"></bean>
</beans>
```

Test文件

```java
package com.lzx.testSpring5;

import com.lzx.User;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * @ClassName TestDemo
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/17 16:43:57
 * @Version 1.0
 **/
public class TestDemo {

    @Test
    public void testAdd() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/UserBean.xml");
        //获取配置对象
        User user = context.getBean("user", User.class);
        //调用获取对象的方法
        user.add();
    }
}
```

2. 利用注解的方式进行创建对象

## 二、IOC容器

### 2.1 IOC的基本概念

#### 2.1.1 IOC理解

- IOC(Inversion of Control):控制反转，就是将创建对象和对象之间的调用过程交给Spring进行管理
- IOC的主要作用是为了降低程序或者系统的耦合度
- 入门案例就是按照IOC来实现的

#### 2.1.2 IOC底层原理

##### 1、文字理解

1. IOC底层使用XML、工厂模式、反射等方式实现

##### 2、画图理解

![image-20230718082123584](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718082130.png)

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718083151.png" alt="image-20230718083151271" style="zoom: 67%;" />

### 2.2 IOC的BeanFactory接口

- IOC的思想是基于IOC容器实现的，IOC容器底层是利用工厂模式实现的

- Spring提供两种IOC容器的实现方式(两个接口):

  1. BeanFactory接口：IOC容器的基本实现方式，Spring内部使用的接口，不提供给开发人员使用

     **注：加载配置文件的时候不会创建对象，只有在获取对象的时候才会创建对象**

  2. ApplicationContext:BeanFactory接口的子接口，提供更加强大的功能，一般提给开发人员使用

     **注：加载配置文件的时候就会在配置文件中创建对象**	

Application接口所有实现类

![image-20230718085902866](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718085902.png)

### 2.3 IOC操作Bean管理

#### 2.3.1、概念

1. 什么是Bean管理

​	Bean管理就是两个操作：(1) Spring创建对象; (2)Spring注入属性

2. Bean管理的两种方式

​	(1) 基于XML方式实现；(2) 基于注释实现

#### 2.3.2、基于XML方式

##### (一)配置xml文件创建对象

![image-20230718102738696](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718102738.png)

1. 在Spring的配置文件，即xml文件中可以使用bean标签进行创建对象，具体在bean标签中添加对应的属性
2. 在bean标签中有很多属性，此处介绍两个常用的

​	id：对象的唯一标识

​	class：类的全路径(包类路径)

3. 创建对象时默认也是利用无参构造构建对象

##### (二)Spring注入注释

DI(Dependency Injection)：注入属性

基于xml注入属性方式

1. 使用set方法进行注入(无参构造)

   ```xml
    <!--  引入Book,创建Book对象  -->
       <bean id="book" class="com.lzx.Book">
       <!--   使用property属性进行属性注入
              name：类中的属性名称
              value：向属性中注入的值
         -->
           <property name="name" value="易筋经"></property>
           <property name="bauthor" value="达摩老祖"></property>
       </bean>
   ```

   ![image-20230718105621325](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718105621.png)

2. 使用有参构造进行注入

   ![image-20230718110150692](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718110150.png)

3. P名称空间注入(了解)

   - 引入p名称空间

     ![image-20230718111041967](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718111042.png)

   - 使用p名称空间可以简化set方法进行属性注入

     ![image-20230718111234125](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718111234.png)

##### (三)XML注入其他类型属性

字面量null

```xml
<property name="address">
<!--   <value><![CDATA[NULL]]></value>-->
           <null/>
</property>
```

属性值包含特殊字符

```xml
<property name="name">
      <value><![CDATA[<<南京>>]]></value>
</property>
```

> 注入属性--外部Bean

步骤

1. 创建两个类一个UserService类和UserDao类

```java
package com.lzx.testSpring5.service;

import com.lzx.testSpring5.DAO.UserDao;

/**
 * @ClassName UserService
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/18 14:56:50
 * @Version 1.0
 **/
public class UserService {
    //创建UserDao类属性生成set方法
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void add() {
        System.out.println("service add.......");
        userDao.update();
    }
}

package com.lzx.testSpring5.DAO;

public interface UserDao {
    void update();
}
```

2. 实现UserDao接口

```java
package com.lzx.testSpring5.Impl;

import com.lzx.testSpring5.DAO.UserDao;

/**
 * @ClassName UserDaoImpl
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/18 14:57:35
 * @Version 1.0
 **/
public class UserDaoImpl implements UserDao {
    @Override
    public void update() {
        System.out.println("UserDaoImpl update.....");
    }
}
```

3. 在配置文件中创建UserService对象和UserDao对象

![image-20230718151811610](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718151812.png)

🐖：**在Spring中注入两个对象的原因是由于UserService类中将UserDao作为了成员属性值，故此在注入属性的时候需要再为UserDAO也就是UserService类中的成员属性创建对象，又由于UserDao是接口，要想创建UserDao对象的话需要实现UserDao，也就是需要创建UserDaoImpl对象**。

> 注入属性--内部Bean

🐉一对多：一个部门中有很多员工，而一个员工只能属于一个部门

在实体类中实现一对多的关系，员工表示所属部门，使用对象属性进行表示

👍步骤

1. 创建Epm类和Dept类(在Dept类中调用Emp类)

Dept类

```java
package com.lzx;

/**
 * @ClassName Dept
 * @Description TODO 部门类
 * @Author lzx
 * @Date 2023/7/18 15:39:36
 * @Version 1.0
 **/
public class Dept {
    private String dName;

    public void setdName(String dName) {
        this.dName = dName;
    }

    @Override
    public String toString() {
        return "Dept{" +
                "dName='" + dName + '\'' +
                '}';
    }
}
```

Emp类

```java
package com.lzx;

/**
 * @ClassName Emp
 * @Description TODO 员工类
 * @Author lzx
 * @Date 2023/7/18 15:40:39
 * @Version 1.0
 **/
public class Emp {
    private String eName;
    private String gender;
    //员工属于一个部门，使用对象形式表示
    private Dept dept;

    public void seteName(String eName) {
        this.eName = eName;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    @Override
    public String toString() {
        return "Emp{" +
                "eName='" + eName + '\'' +
                ", gender='" + gender + '\'' +
                ", dept=" + dept +
                '}';
    }
}
```

2. 在Spring配置文件中创建Emp和Dept对象采用内部Bean方式

![image-20230718155657485](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718155657.png)

🧐：在类中若有类作为属性值，可采用外部Bean和内部Bean两种方式。内部Bean的方式和外部Bean最大的区别在于Bean标签的位置，外部Bean的方式对象Bean在外部，内部Bean则在\<property>\<property/>标签内部定义Bean标签子

😸：外部Bean中，传入的对象需要在另外一个Bean中进行创建对象，在Property标签中采用ref属性来引用在外部创建的对象id唯一标识，相当于在原始实例化对象的时候首先实例化对象参数，再将此对象传给另外一个类作为参数进行实例化，而在内部Bean中则相当于 Children children = new Children(new Student());

> 注入属性--级联赋值

1. 采用ref级联

```xml
    <!-- 注入属性 内部Bean-->
    <!--  级联赋值  -->
    <bean id="emp" class="com.lzx.Emp">
        <property name="eName" value="Lucy"></property>
        <property name="gender" value="女"></property>
        <!--    级联赋值    -->
        <property name="dept" ref="dept"></property>
    </bean>
    <bean id="dept" class="com.lzx.Dept">
        <property name="dName" value="财政部"></property>
    </bean>
```

2. 采用get方法

   ![image-20230718162616537](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718162616.png)

##### (四)XML注入集合属性

- 注入数组类型属性
- 注入List类型属性
- 注入Map类型属性
- 注入Set类型属性

😁步骤：

1. 创建Stu类，定义数组类型、List类型、Map类型、Set类型的属性值

```java
package com.lzx;

import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.Set;

/**
 * @ClassName Stu
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/18 16:35:23
 * @Version 1.0
 **/
public class Stu {
    //String数组
    private String[] courses;
    //List集合
    private List<String> list;
    //Map集合类型
    private Map<String,String> maps;
    //Set集合类型
    private Set<String> sets;

    public void setCourses(String[] courses) {
        this.courses = courses;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public void setMaps(Map<String, String> maps) {
        this.maps = maps;
    }

    public void setSets(Set<String> sets) {
        this.sets = sets;
    }

    @Override
    public String toString() {
        return "Stu{" +
                "courses=" + Arrays.toString(courses) +
                ", list=" + list +
                ", maps=" + maps +
                ", sets=" + sets +
                '}';
    }
}
```

2. 在Spring中配置对应的属性值

```xml
<bean id="stu" class="com.lzx.Stu">
    <!--   数组类型注入     -->
        <property name="courses">
            <array>
                <value>java课程</value>
                <value>数据库课程</value>
            </array>
        </property>
    <!--   List类型注入     -->
    <property name="list">
        <list>
            <value>张三</value>
            <value>小三</value>
        </list>
    </property>
    <!--   Map集合注入     -->
    <property name="maps">
        <map>
            <entry key="JAVA" value="java"></entry>
            <entry key="PHP" value="php"></entry>
        </map>
    </property>
    <!--  Set集合注入  -->
    <property name="sets">
        <set>
            <value>MySQL</value>
            <value>Redis</value>
        </set>
    </property>
    </bean>
```

3. 在集合内部设置对象类型值

```xml
 <bean id="course1" class="com.lzx.testSpring5.Course">
        <property name="cname" value="Spring5框架"></property>
 </bean>
 <bean id="course2" class="com.lzx.testSpring5.Course">
        <property name="cname" value="MyBatis框架"></property>
 </bean>
<property name="list">
      <list>
          <!--            <ref bean="course1"></ref>-->
          <!--            <ref bean="course2"></ref>-->
          <value>张三</value>
          <value>小三</value>
      </list>
</property>
```

4. 将集合注入部门提取出来

![image-20230718171240581](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718171240.png)

![image-20230718171336969](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718171337.png)

![image-20230718171416303](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718171416.png)

##### (五)FactoryBean

🏭 Spring中又两种类型bean，一种是普通的bean一种是工厂bean(FactoryBean)

普通bean:在配置文件中定义的bean类型就是返回值

工厂bean：在定义配置文件中的bean类型可以和返回类型不一样

🐱‍🏍 步骤

1. 创建类让其成为工厂bean，实现FactoryBean

```java
package com.lzx;

import com.lzx.testSpring5.Course;
import org.springframework.beans.factory.FactoryBean;

/**
 * @ClassName MyBean
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/18 17:24:03
 * @Version 1.0
 **/
public class MyBean implements FactoryBean<Course> {
    //定义返回的bean类型
    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return false;
    }
}
```

2. 实现接口的方法，在实现的方法中定义返回的bean类型

```XML
 <bean id="myBean" class="com.lzx.MyBean"></bean>
```

3. 测试方法

```java
    @Test
    public void testMyBean() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/UserBean.xml");
        //获取配置对象
        Course course = context.getBean("myBean", Course.class);
        //调用获取对象的方法
        System.out.println(course);
    }
}
```

![image-20230718173139163](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230718173139.png)

##### (六)bean的作用域

🤔 在Spring中，设置创建的bean是单实例的还是多实例的？

😸 在Spring中默认情况下是单实例的

```java
    @Test
    public void  testEpmDept() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/UserBean.xml");
        //获取配置对象
        Stu stu = context.getBean("stu", Stu.class);
        Stu stu1 = context.getBean("stu", Stu.class);
//        //调用获取对象的方法
        System.out.println(stu);
        System.out.println(stu1);
    }
```

![image-20230719081503732](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719081510.png)

🐱 设置Spring中的bean为多实例步骤：

1. 在bean中设置属性scope参数为prototype
2. 测试结果

```xml
 <bean id="emp" class="com.lzx.Emp" scope="prototype">
        <property name="eName" value="Lucy"></property>
        <property name="gender" value="女"></property>
    <!-- 设置对象类型属性-->
<!--        <property name="dept">-->
<!--            <bean id="dept" class="com.lzx.Dept">-->
<!--                <property name="dName" value="安保部"></property>-->
<!--            </bean>-->
<!--        </property>-->
        <!--    级联赋值    -->
        <property name="dept" ref="dept"></property>
        <property name="dept.dName" value="技术部"></property>
    </bean>
```

```java
 @Test
    public void  testEpmDept() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/UserBean.xml");
        //获取配置对象
        Emp emp = context.getBean("emp", Emp.class);
        Emp emp1 = context.getBean("emp", Emp.class);
//        //调用获取对象的方法
        System.out.println("=======================多实例对象======================");
        System.out.println(emp);
        System.out.println(emp1);
    }
```

![image-20230719081739759](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719081739.png)

🐖 在bean标签中默认是singleton表示单实例对象，而prototype则表示多实例对象，两者之间的区别在于：singleton是在加载Spring配置文件的时候就已经创建了对象，prototype则是在调用getBean()方法的时候才会创建多实例对象。

##### (七)bean的生命周期

生命周期：对象从创建到销毁的过程

😄bean的生命周期：

1. 通过构造器创建bean实例(无参构造)
2. 为bean的属性值赋值和调用其他的bean引用(set方法)
3. 调用初始化方法(需要进行配置初始化的方法)
4. bean可以用了(对象获取到了)
5. 容器关闭的时候销毁bean(需要进行配置销毁的方法)		

代码实现如下

```java
package com.lzx;

/**
 * @ClassName Orders
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/19 8:26:48
 * @Version 1.0
 **/
public class Orders {
    private String oname;
    public Orders() {
        System.out.println("第一步 执行无参构造方法创建bean实例");
    }
    //set方法
    public void setOname(String oname){
        this.oname = oname;
        System.out.println("第二步 调用set方法设置属性值");
    }
    //执行初始化方法
    public void initMethod() {
        System.out.println("第三步 执行初始化方法");
    }
    //执行摧毁的方法
    public void destroyMethod() {
        System.out.println("第五步 执行摧毁的方法");
    }
```

```xml
    <bean id="myBean" class="com.lzx.MyBean"></bean>
    <bean id="orders" class="com.lzx.Orders" init-method="initMethod" destroy-method="destroyMethod">
        <property name="oname" value="手机"></property>
    </bean>
```

```java
    @Test
    public void testMyBean() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/UserBean.xml");
        //获取配置对象
        Orders orders = context.getBean("orders", Orders.class);
        System.out.println("第四步 获取创建的bean对象");
        //调用获取对象的方法
        System.out.println(orders);
        //手动销毁bean实例对象
        context.close();
    }
```

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719090203.png" alt="image-20230719090203172" style="zoom:80%;" />

在上述基础上添加bean后置处理器：

1. 创建bean实例对象(调用无参构造)
2. 为bean的属性值赋值和引用其余bean(调用set方法)
3. 将bean实例对象传给bean后置处理器的方法postProcessBeforeInitialization
4. 调用bean的初始化方法(需要进行配置初始化方法)
5. 将bean实例传递给后置处理器的方法postProcessAfterInitialization
6. 获取到了bean对象(获取对象)
7. 当容器关闭的时候，销毁bean对象(需要进行配置的销毁的方法)

```java
package com.lzx;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

/**
 * @ClassName MyBeanPost
 * @Description TODO
 * @Author lzx
 * @Date 2023/7/19 8:45:32
 * @Version 1.0
 **/
public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之前的方法");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之后的方法");
        return bean;
    }
}
```

![image-20230719091003971](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719091004.png)

![image-20230719175232795](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175232.png)

##### (八)XML的自动装配

🤠 理解：根据指定装配规则，Spring会自动将匹配的属性值进行注入

1. 根据属性名称自动注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!-- 实现自动装配
       bean标签中的autowire属性为配置自动装配
       autowire属性有两个值：
            byName:根据属性名称注入，注入值的bean标签的id值和类属性值一样
            byType：根据属性类型注入
       -->
    <bean id="emp" class="com.lzx.Emp" autowire="byName">
    </bean>
    <bean id="dept" class="com.lzx.Dept"></bean>
</beans>
```

2. 根据属性类型自动注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!-- 实现自动装配
       bean标签中的autowire属性为配置自动装配
       autowire属性有两个值：
            byName:根据属性名称注入，注入值的bean标签的id值和类属性值一样
            byType：根据属性类型注入
       -->
    <bean id="emp" class="com.lzx.Emp" autowire="byType">
    </bean>
    <bean id="dept" class="com.lzx.Dept"></bean>
</beans>
```

##### (九)外部属性文件

配置德鲁伊连接池两种方式

1. 直接在bean标签中配置属性值

```xml
<!--直接配置连接池-->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
<property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
<property name="url"
value="jdbc:mysql://localhost:3306/project_lzx"></property>
<property name="username" value="root"></property>
<property name="password" value="123456"></property>
</bean>
```

2. 引入外部jdbc.properties文件

![image-20230719095633620](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719095633.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd">
<!-- 引入外部属性文件   -->
    <context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
<!--      配置连接池 -->
        <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
            <property name="driverClassName" value="${prop.driverCLass}"></property>
            <property name="url" value="${prop.url}"></property>
            <property name="name" value="${prop.name}"></property>
            <property name="password" value="${prop.password}"></property>
        </bean>
```

🐖：jdbc.properties文件必须位于src下否则会报错

![image-20230719175309793](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175309.png)

#### 2.3.3、基于注释的方式

##### (一) 什么是注解

1. 注解是代码的特殊标记。格式为：@注解名称(属性名称 = 属性值,属性名称 = 属性值.......)
2. 注解可以使用在类、方法、属性上上方
3. 使用注解的好处在于可以简化xml文件配置

##### (二)Spring针对创建bean对象提供的注解

1. @Component
2. @Service
3. @Controller
4. @Repository

**🐖：上述四个注解的功能一样，都可以用来创建bean对象**

##### (三)基于注解方式实现对象创建

🐽 步骤如下:

1. 引入依赖

![image-20230719175326727](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175326.png)

2. 开启组件扫描

```xml
<!-- 开启组件扫描
    扫描包：如果扫描的是多个包的话，多个包用逗号隔开
            扫描包上层目录-->
<context:component-scan base-package="com.lzx"></context:component-scan>
```

3. 创建类，在类上方添加注释

```java
//在注解中的value可以不写，默认值是类名，首字母小写
@Component(value = "userService") // <bean id="userService" class="...."></bean>
public class UserService {
    //创建UserDao类属性生成set方法
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void add() {
        System.out.println("service add.......");
        userDao.update();
    }
}
```

4. 开启组件扫描细节配置

```xml
<!-- use-default-filters="false"表示不使用默认的 filter 自己配置 -->

<context:component-scan base-package="com.lzx" use-default-filters="false">
  <!--        context:include-filter 设置扫描哪些内容 -->
  <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
  <!--        context:exclude-filter 设置不扫描哪些内容 -->
  <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

5. 基于注解方式实现属性注入

🐹 @Autowired 根据属性类型进行注入

🐭 @Qualifier 根据属性名称进行注入，和@Autowired注解搭配使用

😼 @Resource 既可以根据属性名称也可以根据属性类型进行注入

😸 @Value 注入普通类型属性

🦒 @Configuration 作为配置类代替xml配置文件

🦮 @ComponentScan 扫描包

## 三、AOP

### 3.1、AOP概念

**什么是AOP**

1. AOP(Aspect Oriented Programming)面向切面编程，可以对业务逻辑的各个部分进行隔离，使得业务逻辑代码部分之间 的耦合度降低，提高程序的可重用性，同时提高开发效率；
2. 通俗的讲就是：在不修改原始代码的基础上在主干功能上添加新的功能；
3. 举出登录的例子具体说明AOP

![image-20230719175342633](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175342.png)

在原系统功能上添加权限判断功能

🦙 原始方式：修改源码方式实现 if 管理员 ... else if 普通用户

### 3.2、底层原理

两种情况动态代理

#### 3.2.1、有接口的情况，使用JDK动态代理

创建动态代理实现类对象，增强类方法

![image-20230719175356314](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175356.png)

#### 3.2.2、没有接口的情况，使用CGLIB动态代理

![image-20230719175428699](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175428.png)

### 3.3、JDK动态代理

#### 3.3.1、使用JDK动态代理，使用Proxy类里面的方法创建代理对象

 newProxyInstance()方法

![image-20230719142355378](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719142355.png)

🧐方法有三个参数：

- 第一个参数 ClassLoader:类加载器
- 第二个参数 类<?>[] interfaces ：增强方法所在的类，这个类实现的接口，支持多个接口
- 第三个参数 InvocationHandler:实现这个InvacationHandler接口，创建代理对象，写增强的部分

#### 3.3.2、编写JDK动态代理代码

```java
package com.lzx.DAO;

/**
 * 接口
 */
public interface MyDao {
    public int add(int a, int b);
    public String Update(String id);
}
```

```java
package com.lzx.Impl;

import com.lzx.DAO.MyDao;

public class MyDaoImpl implements MyDao {
    @Override
    public int add(int a, int b) {
        return a + b;
    }

    @Override
    public String Update(String id) {
        return id;
    }
}
```

```java
package com.lzx;

import com.lzx.DAO.MyDao;
import com.lzx.Impl.MyDaoImpl;

import java.lang.reflect.Proxy;

public class JDKProxy {
    public static void main(String[] args) {
        //调用newProxyInstance方法三个参数
        //创建接口实现类代理对象
        Class[] interfaces = {MyDao.class};
        //匿名内部类
//        Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new InvocationHandler() {
//            @Override
//            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
//                return null;
//            }
//        })
        MyDaoImpl myDao = new MyDaoImpl();
        MyDao dao = (MyDao)Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new MyDaoProxy(myDao));
        int result = dao.add(1,2);
        System.out.println("result = " + result);
    }
}
```

```java
package com.lzx;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.util.Arrays;

public class MyDaoProxy implements InvocationHandler {

    //有参构造，是谁的代理对象就传递谁
    private Object object;
    public MyDaoProxy(Object object) {
        this.object = object;
    }

    //增强逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("方法执行之前...." + method.getName() + ":传递的参数..." + Arrays.toString(args));
        //被增强的方法执行之后
        Object res = method.invoke(object, args);
        //方法之后
        System.out.println("方法执行之后...." + object);
        return res;
    }
}
```

![image-20230719145545918](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719145545.png)

🤔 总结：增强逻辑代码可以采用匿名内部类也可以采用实现InvocationHandler接口的方式，后者可以传入参数，参数是谁的代理对象就传入谁，要求是得有有参构造器，且得实现invoke()方法；newProxyInstance()方法中第一个参数一般为调用该方法所在的类，`第二个参数是实现接口代理对象`因MyDao是个接口无法创建对象，所以要创建对象必须实现该接口，故此在代理对象的那个参数传递的是myDaoImpl，而不是myDao。

### 3.4 AOP术语

#### 连接点

类中可以被增强的方法称作`连接点`

#### 切入点

类中实际真正被增强的方法称作`切入点`

#### 通知(增强)

实际增强的逻辑部分称作是通知(增强)

👿 通知的类型:

- 前置通知
- 后置通知
- 环绕通知
- 异常通知
- 最终通知

#### 切面

把通知应用到切入点的过程称作是`切面`，切面是过程

### 3.5、AOP操作

#### 3.5.1、准备工作

1. Spring一般是基于AspectJ实现的AOP操作，但AspectJ不是Spring的组成部分，AspectJ是独立的AOP框架
2. 基于AspectJ实现AOP操作

​	(1) 基于xml配置文件实现

​	(2) 基于注解方式实现

😆 导入以下包

![image-20230719154305032](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719154305.png)

😈 切入点表达式

- 作用在于可以定位到哪个类中的哪个方法被增强

- 语法结构：

  - execution([权限修饰符]\[返回值类型]\[类全路径]\[方法名称]([参数列表]))

- 举例子：

  ​	🐷：对com.lzx.dao.BookDao类里边的add进行增强

  execution(* com.lzx.dao.BookDao.add(..))

  ​	🐼:对com.lzx.dao.BookDao类里边的所有方法进行增强

  exection(* com.lzx.dao.BookDao.*(..))

  ​	🦄:对com.lzx.dao包中所有的类，类中所有的方法进行增强

  exection(* com.lzx.dao.\*.\*(..))

#### 3.5.2、AspectJ注解

#### 3.5.3、AspectJ配置文件

## 四、JDBCTemplate

### 4.1、概念

JDBCTemplate:是Spring框架对JDBC进行封装。实现JDBCTemplate对数据库的操作

😁 引入以下jar包

![image-20230719175449721](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230719175449.png)

1. 在Spring配置文件中配置数据库连接池

```xml
<!--      配置连接池 -->
        <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
            <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
            <property name="url" value="jdbc:mysql://localhost:3306/lzx"></property>
            <property name="username" value="root"></property>
            <property name="password" value="123456"></property>
        </bean>
```

2. 配置JdbcTemplate对象，注入DataSoucrce

```xml
   <!--JDBCTemplate对象-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <!-- 注入属性   -->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!-- 组件扫描   -->
    <context:component-scan base-package="com.lzx"></context:component-scan>
```

3. 创建service类、dao类，在dao中注入jdbcTemplate对象

```java
@Service
public class UserService {
    //创建UserDao类属性生成set方法
    @Autowired
    private UserDao userDao;
    }
@Repository
public class UserDaoImpl implements UserDao {
    //注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;
}
```

### 4.2、操作数据库

#### 4.2.1、添加

1. 创建实体类

2. 创建service类和dao类

   (1) 在dao类中添加add(User user)方法

   (2) 在UserService类中添加UserDao类(将UserDao注入到UserService中)

   (3) 实例化UserDao，将JdbcTemplate注入到UserDaoImpl类中，调用JDBCTemplate中的update方法

   (4) 在Bean标签中创建UserDao对象

```java
package com.lzx;

/**
 * @ClassName User
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/17 16:18:56
 * @Version 1.0
 **/
public class User {
    private Integer userId;
    private String userName;
    private String uStatus;

    public Integer getUserId() {
        return userId;
    }

    public void setUserId(Integer userId) {
        this.userId = userId;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getuStatus() {
        return uStatus;
    }

    public void setuStatus(String uStatus) {
        this.uStatus = uStatus;
    }
}
----------------------------------------------------------------------
package com.lzx.DAO;

import com.lzx.User;

public interface UserDao {
    void add(User user);
}
----------------------------------------------------------------------
  package com.lzx.Impl;

import com.lzx.DAO.UserDao;
import com.lzx.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository
public class UserDaoImpl implements UserDao {
    //注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(User user) {
        //创建sql语句
        String sql = "insert into user values(?,?,?)";
        //调用方法实现
        Object[] args = {user.getUserId(),user.getUserName(),user.getuStatus()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println(update);
    }
}
----------------------------------------------------------------------
  package com.lzx.service;

import com.lzx.DAO.UserDao;
import com.lzx.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    //创建UserDao类属性生成set方法
    @Autowired
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    public void addUser(User user) {
        userDao.add(user);
    }
}
----------------------------------------------------------------------
package com.lzx.testSpring5;

import com.alibaba.druid.pool.DruidDataSource;
import com.lzx.User;
import com.lzx.service.UserService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class IOCTest {
    @Test
    public void  testAutoDI() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/BeanIOC.xml");
        //获取配置对象
//        Emp emp = context.getBean("emp", Emp.class);
        UserService userService = context.getBean("userService", UserService.class);
        User user = new User();
        user.setUserId(1);
        user.setUserName("小李");
        user.setuStatus("0");
        userService.addUser(user);
    }
}
```

```xml
<!--      配置连接池 -->
        <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" destroy-method="close">
            <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
            <property name="url" value="jdbc:mysql://localhost:3306/lzx"></property>
            <property name="username" value="root"></property>
            <property name="password" value="123456"></property>
        </bean>
    <!--JDBCTemplate对象-->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <!-- 注入属性   -->
        <property name="dataSource" ref="dataSource"></property>
    </bean>

 <bean id="userService" class="com.lzx.service.UserService">
        <!-- 注入UserDao对象
        name属性：类里面的属性即在UserService中的成员属性
        ref属性：创建userDao对象(此处的对象是UserService的成员属性)的bean标签的id值
        -->
        <property name="userDao" ref="userDaoImpl"></property>
    </bean>
    <bean id="userDaoImpl" class="com.lzx.Impl.UserDaoImpl"></bean>
</beans>
```

#### 4.2.2、修改和删除

🦓 代码如下:

UserService类

```java
package com.lzx.service;

import com.lzx.DAO.UserDao;
import com.lzx.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
//在注解中的value可以不写，默认值是类名，首字母小写
//@Component(value = "userService") // <bean id="userService" class="...."></bean>
@Service
public class UserService {
    //创建UserDao类属性生成set方法
    @Autowired
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    public void addUser(User user) {
        userDao.add(user);
    }
    public void updateUser(User user) {
        userDao.updateUser(user);
    }
    public void deleteUser(Integer id) {
        userDao.delete(id);
    }

}
```

UserDao类和UserDaoImpl类

```java
package com.lzx.DAO;

import com.lzx.User;

public interface UserDao {
    void add(User user);
    //修改方法
    void updateUser(User user);
    //删除方法
    void delete(Integer id);
}
-----------------------------------------
package com.lzx.Impl;

import com.lzx.DAO.UserDao;
import com.lzx.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

@Repository
public class UserDaoImpl implements UserDao {
    //注入JdbcTemplate
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(User user) {
        //创建sql语句
        String sql = "insert into user values(?,?,?)";
        //调用方法实现
        Object[] args = {user.getUserId(),user.getUserName(),user.getuStatus()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println(update);
    }
    //修改
    @Override
    public void updateUser(User user) {
        //创建sql语句
        String sql = "update user set user_name=?,u_status=?where user_id=?";
        //调用方法实现
        Object[] args = {user.getUserName(),user.getuStatus(),user.getUserId()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println("update = " + update);

    }
    //删除
    @Override
    public void delete(Integer id) {
        //创建sql语句
        String sql = "delete from user where user_id=?";
        //调用方法实现
        int update = jdbcTemplate.update(sql, id);
        System.out.println("update = " + update);
    }
}
```

![image-20230720083440303](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720083447.png)

#### 4.2.3、查询返回某个值

UserService类：

```java
public void selectUse() {
    int count = userDao.selectUse();
    System.out.println("user表中的count是：" + count);
}
public void findUserInfo(Integer id) {
    User userInfo = userDao.findUserInfo(id);
    System.out.println("user的id是：" + userInfo.getUserId());
    System.out.println("user的姓名是：" + userInfo.getUserName());
    System.out.println("user的status是：" + userInfo.getuStatus());
}
public void findAllUser() {
    for (User user : userDao.findAllUser()) {
        System.out.println(user);
    }
}
```

```java
  //查询数据表的数量，返回某个值
    @Override
    public int selectUse() {
        //创建sql语句
        String sql = "select count(*) from user";
        //调用方法实现
        Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
        return count;
    }
```

#### 4.2.4、查询返回对象

```java
//查询数据表中的数据，查询返回对象
@Override
public User findUserInfo(Integer id) {
    //创建sql语句
    String sql = "select * from user where user_id=?";
    //调用方法实现
    User user = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<User>(User.class), id);
    return user;
}
```

#### 4.2.5、查询返回集合

```java
//查询返回对象集合
@Override
public List<User> findAllUser() {
    //创建sql语句
    String sql = "select * from user";
    //调用方法
    List<User> userList = jdbcTemplate.query(sql, new BeanPropertyRowMapper<User>(User.class));
    return userList;
}
```

![image-20230720094726887](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720094726.png)

#### 4.2.6、批量操作

🤖 批量添加数据操作

![image-20230720095401626](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720095401.png)

调用上述方法进行批量操作

🙄 有两个参数：

- 第一个参数是：sql语句
- 第二个参数是：List集合，添加多条数据

```java
package com.lzx.testSpring5;

import com.lzx.service.UserService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;

public class IOCTest {
    @Test
    public void  testAutoDI() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/BeanIOC.xml");
        //获取配置对象
//        Emp emp = context.getBean("emp", Emp.class);
        UserService userService = context.getBean("userService", UserService.class);
        //批量添加
        ArrayList<Object[]> list = new ArrayList<>();
        Object[] o1 = {4,"java","a"};
        Object[] o2 = {5,"C++","b"};
        Object[] o3 = {6,"MySQL","c"};
        list.add(o1);
        list.add(o2);
        list.add(o3);
        //批量添加
        userService.batchAddUser(list);
    }
}
```

  UserDaoImpl类   

```java
  //批量增加User
    @Override
    public void batchAddUser(List<Object[]> batchArgs) {
        //创建sql语句
        String sql = "insert into user values(?,?,?)";
        //调用方法
        int[] batchAddUser = jdbcTemplate.batchUpdate(sql, batchArgs);
        System.out.println(Arrays.toString(batchAddUser));
    }
```

👻 批量修改

```java
package com.lzx.testSpring5;

import com.lzx.service.UserService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;

public class IOCTest {
    @Test
    public void  testAutoDI() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/BeanIOC.xml");
        //获取配置对象
        UserService userService = context.getBean("userService", UserService.class);
        //批量修改
        ArrayList<Object[]> list = new ArrayList<>();
        Object[] o1 = {"PHP","P",1};
        Object[] o2 = {"C","C",2};
        Object[] o3 = {"Python","p",3};
        list.add(o1);
        list.add(o2);
        list.add(o3);
        userService.batchUpdateUser(list);

    }
}
```

![image-20230720104106092](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720104106.png)

😨 批量删除

```java
package com.lzx.testSpring5;

import com.lzx.service.UserService;
import org.junit.Test;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import java.util.ArrayList;

public class IOCTest {
    @Test
    public void  testAutoDI() {
        //加载配置文件
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("com/lzx/BeanIOC.xml");
        //获取配置对象
        UserService userService = context.getBean("userService", UserService.class);
        //批量修改
        ArrayList<Object[]> list = new ArrayList<>();
        Object[] o1 = {1};
        Object[] o2 = {3};
        list.add(o1);
        list.add(o2);
        userService.batchDeleteUser(list);
    }
}
```

![image-20230720104415736](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720104415.png)

## 五、事务管理

### 5.1、概念

🧐 什么是事务

- 事务是数据库操作的最基本的单元，逻辑上一组操作要么成功要么失败，若有一个失败的话，则所有操作都失败。

😍 事务的特点(ACID)

- 原子性
- 一致性
- 隔离性
- 持久性

### 5.2、搭建操作环境

🏦 经典案例：银行转账

- Lucy转账给Mary100元，Lucy少了100元，Mary多了100元

代码实现如下

![image-20230720111421955](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720111422.png)

1. 创建数据库表添加记录

![](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720111715.png)

2. 创建dao类和service类，在service类中注入dao类，在dao类中注入JdbcTemplate，在JdbcTemplate中注入DataSource

```java
package com.lzx.service;

import com.lzx.DAO.TUserDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

/**
 * @ClassName TUserService
 * @Description TODO 处理业务代码
 * @Author lzx
 * @Date 2023/7/20 11:23:43
 * @Version 1.0
 **/
@Service
public class TUserService {
    //注入dao类
    @Autowired
    private TUserDao tUserDao;
    //转账的方法
    public void accountMoney() {
        try {
            //第一步、开启事务
            //第二步、进行业务操作
            //少钱
            tUserDao.reduceMoney();
            //模拟异常
            int i = 10 / 0;
            //多钱
            tUserDao.addMoney();
            //第三步、没有发生异常，提交事务
        } catch (Exception e) {
            //第四步、出现异常，事务回滚
            e.printStackTrace();
        }
    }

    public void settUserDao(TUserDao tUserDao) {
        this.tUserDao = tUserDao;
    }
}
```

3. 实现dao类中的方法

```java
package com.lzx.Impl;

import com.lzx.DAO.TUserDao;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Repository;

/**
 * @ClassName TUserDaoImpl
 * @Description TODO TUserDao对象实体类
 * @Author lzx
 * @Date 2023/7/20 11:25:10
 * @Version 1.0
 **/
@Repository
public class TUserDaoImpl implements TUserDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;
    //少钱
    @Override
    public void reduceMoney() {
        String sql = "update t_user set money=money-? where username=?";
        int update = jdbcTemplate.update(sql, 1000, "Lucy");
        System.out.println("update = " + update);
    }
    //多钱
    @Override
    public void addMoney() {
        String sql = "update t_user set money=money+? where username=?";
        int update = jdbcTemplate.update(sql, 1000, "Mary");
        System.out.println("update = " + update);
    }
}
```

### 5.3、Spring事务管理介绍

(一) 事务添加到JavaEE的Service层(业务逻辑层)

(二) Spring进行事务管理操作

🐳 方式：`编程式事务管理`(不使用)、`声明式事务管理`(在使用)

(三) 声明式事务管理

​	🦮 基于注解方式(在使用)

​	🐩 基于XML配置文件的方式

(四) Spring中的声明式事务管理底层使用的是AOP原理

(五) Spring事务管理API

![image-20230720140753634](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720140753.png)

### 5.4、注解声明式事务管理

1.  在Spring中配置事务管理器

```xml
<!--  配置事务管理器  -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
<!--    注入数据源    -->
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

2. 引入名称空间tx

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd">
```

3. 开启事务管理

```xml
<!--  开启事务管理  -->
<tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>
```

4. 在Service类上方添加 @Transactional 事务注解

🐷：将@Transactional标注在类上，这个类的所有方法都添加事务

🐱：将@Transactional标注在方法中，这个方法添加事务

### 5.5、声明式事务管理参数配置

😎 在类上方添加@Transactional注解，在这个注解里边可以配置事务相关参数

![image-20230720143703143](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720143703.png)

#### Propagation:事务传播行为

😕 当一个事务方法被另外一个事务方法调用的时候，这个事务该如何进行？

![image-20230720145320177](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720145320.png)

事务的传播行为可以由传播属性指定，Spring指定了7种类传播行为

![image-20230720145733109](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720145733.png)

![image-20230720145832380](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720145832.png)

#### isolation:事务隔离级别

1. 事务的特性称作隔离性，使得多个事务之间操作不受影响。不考虑隔离性产生的很多问题

2. 有三个读问题：脏读、不可重复读、虚(幻)读

   🦥 脏读:一个未提交的事务读取到另一个未提交的事务的数据

   ![image-20230720151056232](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720151056.png)

   🐯 不可重复读：一个未提交事务读取到另外一个提交事务修改数据

   ![image-20230720151631686](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720151631.png)

   👽 虚(幻)读：一个未提交事务读取到一个提交事务添加数据

3. 解决：通过设置事务的隔离级别，解决读问题

|                                  | 脏读 | 不可重复度 | 幻读 |
| :------------------------------: | :--: | :--------: | :--: |
| READ UNCOMMITTED<br />(读未提交) |  有  |     有     |  有  |
|  READ COMMITTED<br />(读已提交)  |  无  |     有     |  有  |
|  REPEATBLE READ<br />(可重复读)  |  无  |     无     |  有  |
|    SERIALIZABLE<br />(串行化)    |  无  |     无     |  无  |

![image-20230720152509363](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230720152509.png)

#### timeOut:超时时间

1. 事务必须在一定时间内进行提交，若不提交则回滚；
2. 默认值为-1，设置时间以秒单位进行计算

#### readOnly：是否只读

1. 读：查询数据，写：添加、修改、删除数据
2. readOnly默认是false，表示可以进行CRUD
3. readOnly的值设置为true，则只能读

#### rollbackFor：回滚

设置出现哪些异常进行事务回滚

#### noRollbackFor：不回滚

设置哪些异常不回滚

### 5.6、xml声明式事务管理

🦄 在Spring配置文件中添加事步骤：

1. 配置事务管理器
2. 配置通知
3. 配置切入点和切面

```xml
    <!--  配置事务管理器  -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <!--    注入数据源    -->
        <property name="dataSource" ref="dataSource"></property>
    </bean>
    <!--  配置通知-->
    <tx:advice id="txadvice">
    <!-- 配置事务参数  -->
        <tx:attributes>
            <!-- 指定哪个方法上面添加事务 -->
            <tx:method name="accountMoney" propagation="REQUIRED"/>
        </tx:attributes>
    </tx:advice>
    <!--  配置切入点和切面  -->
    <aop:config>
        <!-- 配置切入点 -->
        <aop:pointcut id="pt" expression="execution(* com.lzx.service.UserService.*(..))"/>
        <!-- 配置切面 -->
        <aop:advisor advice-ref="txadvice" pointcut-ref="pt"></aop:advisor>
    </aop:config>					
```

### 5.7、完全直接声明式事务管理

创建配置类，使用配置类代替xml文件

```java
package com.lzx;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;

import javax.sql.DataSource;

@Configuration //配置类
@ComponentScan(basePackages = "com.lzx") //组件扫描
@EnableTransactionManagement //开启事务
public class TxConfig {
    //创建数据库连接池
    @Bean
    public DruidDataSource getDruidDataSource() {
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/lzx");
        dataSource.setUsername("root");
        dataSource.setPassword("123456");
        return dataSource;
    }
    //创建JdbcTemplate对象
    @Bean
    public JdbcTemplate getJdbcTemplate(DataSource dataSource) {
        //到IOC容器中根据类型找到dataSource
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        //注入dataSource
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }
    //创建事务管理器
    @Bean
    public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource) {
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }

}
```

## 六、Spring5的新特性

### 6.1、新功能

Spring5已经移除了Log4jConfigListener，官方建议使用Log4j2

#### Spring5框架整合Log4j2

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--日志级别以及优先级排序：OFF > FATAL > ERROR > WARN >INFO > DEBUG > TRACE > ALL-->
<!--Configuration后的status用于设置log4j2自身内部的信息输出，可以设置，当设置成trace时，可以看到log4j2内部各种详细信息输出-->
<Configuration status="INFO">
<!-- 先定义所有的appender-->
    <Appenders>
    <!-- 输出日志信息到控制台 -->
       <Console name="Console" target="SYSTEM_OUT">
    <!-- 控制日志输出的格式 -->
           <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"></PatternLayout>
       </Console>
    </Appenders>
    <!-- 定义logger，只有定义logger并引入appender，appender才会生效-->
    <loggers>
        <root level="info">
            <appender-ref ref="Console"/>
        </root>
    </loggers>
</Configuration>
```

### 6.2、WebFlux

SpringWebFlux是以一种以Spring5添加的新的模块，用于web开发，功能和SpringMVC类似，WebFlux使用的是一种比较流行的响应式编程出现的框架，SpringMVC框基于Servlet容器的，WebFlux是一种异步非阻塞的框架，异步非阻塞的框架必须在Servlet3.1以上才支持，核心是基于Reactor的相关API实现的响应式编程。

🦍 异步非阻塞

异步和同步针对调用者：调用者发送请求，若等待对方回应才去做其他的事称作是同步，若是发送完请求不等对方就去做其他的事情称呼之为异步。

阻塞和非阻塞针对被调用者：被调用者在接受到请求以后，做完请求任务之后才各处反馈就是阻塞，若被调用者在接受请求任务后立即做出反馈(未做完请求任务)然后再去做其他的事情就是非阻塞。

