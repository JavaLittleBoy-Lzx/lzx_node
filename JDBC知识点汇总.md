[TOC]

## 一、JDBC概述

### 1.1 数据持久化

数据持久化就是将数据可以存储到掉电式存储设备中的加以使用，大多数企业级应用需要将数据保存到硬盘上加以固话，而持久化过程则需要通过数据库来完成。

数据化持久化主要应用是在将内存中的数据存储到关系型数据库。

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154403.png" alt="image-20230628104424257" style="zoom:67%;" />

### 1.2 Java中的数据库存储技术

在Java中的，数据库存储技术可以分为以下几类：

1. JDBC(Java Database Connectivity)直接访问数据库
2. JDO(Java Data Object)技术
3. 第三方O/R工具，如Hibernate、MyBatis等

JDBC是java访问数据库的基石，Hibernate、Mybstis、JDO等都是更好的封装了JDBC。

### 1.3 JDBC介绍

- JDBC(Java Database Connectivity)是一个独立的特定数据库管理系统，是一组SQL通用接口，主要用于数据库的存储和访问等公共操作。

- JDBC为访问数据库提供了一种统一的途径。

- JDBC可以连接任何数据库，只要数据库提供对应的JDBC驱动程序就可

- 没有JDBC如下方式访问SQL

  <img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154401.png" alt="image-20230628110152148" style="zoom: 50%;" />

  有了JDBC是如下方式访问

  ![image-20230628110244868](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154359.png)

### 1.4 JDBC的体系

- JDBC接口有两个层次：
  - **面向应用的接口：**Java API，抽象接口，供程序员使用，主要是用于对数据库的操作，主要包括连接数据库、对数据库的CRDU、获取数据结果等。
  - **面向数据库的API：**Java Driver API，供数据库开发商开发数据库驱动程序应用

### 1.5 JDBC的编写顺序

1. 导入java.sql包
2. 分两个方向，一是采用JDBC-ODBC桥的方式、另外一个是采用纯Java驱动方式
3. 无论是哪种都需要注册加载驱动程序
4. 创建Connection对象
5. 创建Statement对象
6. 执行SQL语句
7. 关闭Statement对象
8. 关闭Connection对象

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154356.png" alt="image-20230628111736725" style="zoom: 50%;" />

## 二、获取数据库连接(三大连接要素)

### 2.1 要素一：Driver接口实现类

#### 2.1.1 Driver 接口介绍

java.sql.Driver接口是所有JDBC驱动程序需要实现的接口，此接口为各大数据库开发商所使用，不同的数据库厂商提供不同的实现。

在程序中不需要直接访问实现了Driver接口的类，而是由驱动程序管理类(java.sql.DriverManager)去调用这些Driver实现

- Oracle的驱动：oracle.jdbc.dirver.OracleDriver
- MySQL的驱动：com.mysql.jdbc.Driver

#### 2.1.2加载和注册JDBC驱动

- 加载驱动：加载驱动需要用到Class的静态方法forName()，向其传递要加载的驱动名称

  ​	Class.fotName("com.mysql.jdbc.Driver");

- 注册驱动：调用DriverManager类来管理驱动程序

  ​	DriverManager.registerDriver("com.mysql.jdbc.Driver");

### 2.2 要素二：URL

JDBC URL主要作用是用于标识一个注册驱动程序，驱动管理程序通过这个URL选择正确的驱动程序，从而建立与数据库之间的连接

JDBC URL的格式为

​	**jdbc:子协议:子名称**

**协议：**JDBC URL 中的协议都是jdbc

**子协议：**用于标识一个数据库驱动程序

**子名称：**连接数据库的名称。包括主机名(对应服务端的ip地址)、端口号等

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154351.png" alt="image-20230628141103539" style="zoom: 50%;" />

MySQL连接的URL编写方式：

- jdbc:mysql://主机名称:mysql的服务端口号/数据库名称?参数=值&参数=值

  例：jdbc:mysql://localhost:3306/lzx_project?user=root&password=123456

  jdbc:mysql://localhost:3306/lzx_project?useUnicode=true&characterEncoding=utf8

### 2.3 要素三：用户名和密码

用户名和密码可以采用“属性名=属性值”的形式告诉数据库

采用DriverManager的getConnection来连接数据库

### 2.4 数据库连接方式

```java
package jdbc;

import com.mysql.jdbc.Driver;

import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.util.Properties;

/**
 * @ClassName Demo1
 * @Description TODO 用于JDBC的测试
 * @Author 李子雄
 * @Date 2023/6/28 14:29
 * @Version 1.0
 **/
public class Demo1 {
    public static void main(String[] args) throws Exception {
//        try {
////            Driver driver = new Driver(); //1、提供实现java.sql.Driver接口的类
//            Driver driver = null;
//            try {
//                driver = (Driver)Class.forName("com.mysql.jdbc.Driver").newInstance();
//            } catch (InstantiationException e) {
//                e.printStackTrace();
//            } catch (IllegalAccessException e) {
//                e.printStackTrace();
//            }
//            //2、JDBC URL
//            String url = "jdbc:mysql://localhost:3306/project";
//            //3、Properties的对象，用于指明用户名和密码
//            Properties properties = new Properties();
//            properties.setProperty("user","root");
//            properties.setProperty("password","123456");
//            //4、调用getConnection()方法来连接数据库
////            Connection connection = DriverManager.getConnection(url, properties);
//            Connection connect = driver.connect(url, properties);
//            System.out.println(connect);
//        } catch (SQLException | ClassNotFoundException e) {
//            e.printStackTrace();
//        }
        InputStream inputStream = ClassLoader.getSystemClassLoader().getResourceAsStream("jdbc.properties");
        Properties properties = new Properties();
        properties.load(inputStream);
        //读取配置信息
        String user = properties.getProperty("user");
        String password = properties.getProperty("password");
        String url = properties.getProperty("url");
        String driverClass = properties.getProperty("driverClass");
        //加载驱动
        Class.forName(driverClass);
        //获取连接
        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println(connection);
    }

}
```

![image-20230628151156224](F:\Java知识点总结&&CSDN博客\JDBC知识点汇总.assets\image-20230628151156224.png)

**使用配置文件的好处**

1. 实现了代码与数据的分离，若需要修改配置信息的话，只需要修改配置文件即可
2. 修改配置文件的话不需要重写编译

## 三、PreparedStatement实现CRUD	

### 	3.1 操作和访问数据库

数据库连接用于向数据库服务器端发送请求和SQL语句，接受数据库服务器返回的结果

java.sql包主要有以下三个接口来定义对数据库的调用不同方式

- Statement：用于执行静态SQL语句并返回生成结果的对象
- PrepatedStatement：SQL语句被编译保存在对象中，可以使用此对象来多次高效的执行该语句
- CallableStatement：用于执行SQL存储过程

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154411.png" alt="image-20230628153259809" style="zoom:50%;" />

### 	3.2 Statement弊端

1. 需要拼接字符串

2. 存在SQL注入问题，SQL注入问题就是恶意拼接字符串达到登录成功，例如 select username,password from user where password = '123456' and '1' = '1';这句SQL永远正确

   <img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154414.png" alt="image-20230630145857302" style="zoom:50%;" />

   PreparedStatement预编译的Statement可以预防SQL注入问题

### 3.3 PreparedStatement的使用

Perparedment接口是Statement的子接口，可以通过Connection的preparedStatement()方法来获取PreparedStatement对象，PreparedStatement接口表示一条预编译过SQL语句，PreparedStatement所表示的SQL语句中的参数用"?"来表示，通过用setXXX()方法来设置参数，setXXX()方法有两个参数，一个是要设置SQL语句的参数的索引(从1开始)，第二个是要设置参数的值

#### 3.3.1 PreparedStatement VS Statement

PreparedStatement代表一条预编译的SQL语句，DBServer对预编译的语句提供性能优化，因预编译的语句可能会经常被重复调用，故此DBServer会将这些代码放入缓存中，下次使用该语句的时候只需要传入参数即可，不需对该语句再次进行编译

Statement语句相同的操作不同的语句都会进行编译，事实是数据库对这些代码没有缓存

#### 3.3.2 Java和MySQL的数据对应表

| Java类型           | SQL类型                  |
| ------------------ | ------------------------ |
| boolean            | BIT                      |
| byte               | TINYINT                  |
| short              | SMALLINT                 |
| int                | INTEGER                  |
| long               | BIGINT                   |
| String             | CHAR,VARCHAR,LONGVARCHAR |
| byte array         | BINARY , VAR BINARY      |
| java.sql.Date      | DATE                     |
| java.sql.Time      | TIME                     |
| java.sql.Timestamp | TIMESTAMP                |

#### 3.3.4 PreparedStatement的CRUD



## 四、PreparedStatement其他操作

### 操作BLOB字段

### 批量插入

## 五、数据库事务

## 六、DAO以及实现类

## 七、数据库连接池

## 八、Apache-DBUtils实现CRUD

