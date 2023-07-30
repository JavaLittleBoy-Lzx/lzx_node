[TOC]

## MySQL基础概述

### SQL分类

#### DDL(Data Defination Language)数据定义语言

##### 作用

主要是针对表的结构进行操作，例如定义和该变表的结构、数据类型等

##### 主要命令

CREATE：创建表结构

ALTER：修改表中的字段

DROP：删除表

TRUNCATE：删除表中记录，不改变表的结构

#### DQL(Data Query Language)数据查询语言

##### 作用

主要是针对表中的记录进行查询

##### 主要命令

SELECT：查询表中的记录

#### DML(Data Manipulation Language)数据操纵语言

##### 作用

主要是对表中的记录进行增删改操作

##### 主要命令

INSERT：插入一条记录

UPDATE：修改表中的记录

DELETE：删除表中的记录

#### DCL(Data Control Language)数据控制语言

##### 作用

设置或更改数据库用户或角色权限

##### 主要命令

GRANT：授权

REVOKE：收回已授权的权限

#### TCL(Transactional Control Language)事务控制语言

##### 作用

控制事务

##### 主要命令

COMMIT：提交事务

ROLLBACK：事务的回退操作

SAVEPOINT：设置保存点，回滚到此处

## DQL数据查询语言

### 简单查询

查询单个字段

```mysql
select empno from emp;
```

查询多个字段

```mysql
select empno,empname from emp;
```

查询全部字段

```mysql
select * from emp;
```

查询的字段进行计算

```mysql
select empno,ename,sal*12 from emp;
```

将查询出来的字段进行重命名

```mysql
select empno as '员工编号',ename as '员工姓名',sal*12 as '年薪' from emp;
```

### 条件查询

条件查询在where关键字之后的运算符

| 运算符           | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| =                | 等于                                                         |
| <>或!=           | 不等于                                                       |
| <                | 小于                                                         |
| >                | 大于                                                         |
| <=               | 小于等于                                                     |
| <=               | 大于等于                                                     |
| between...and... | 两个之间，等同于 >= and <=                                   |
| is null          | 为空(is not null)                                            |
| and              | 并且                                                         |
| or               | 或者                                                         |
| not              | not 用于取非，常用于is、in                                   |
| like             | like称为模糊查询，可以匹配%、下划线    <br /> %：可以匹配任意字符，下划线：一个下划线只能匹配一个字符 |
| in               | 包含，相当于多个 or (not in 表示不在这个范围)                |

Tips：MySQL默认在Windows系统下是不区分大小写的，在Linux操作系统下是严格区分大小写的且是按照如下要求进行区分：

1. 数据库名与表名是严格区分大小写的；
2. 表的别名是严格区分大小写的；
3. 列名与列的别名在所有的情况下均是忽略大小写的；
4. 变量名也是严格区分大小写的；  

MySQL如需修改区分大小写需要修改my.ini配置文件中添加于以下语句

```ini
lower_case_table_names = 0
其中 0：区分大小写， 1：不区分大小写  
```

#### 等号操作符

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal = 5000;
```

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where job = 'manager';
```

manager为字符，需要用单引号或者双引号引用,数值型数据也可以用引号包裹起来

#### <>操作符

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal <> 5000;
```

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal != 5000;
```

#### between...and..操作符

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal >= 1600 and sal <= 3000;
```

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal between 1600 and 3000;
```

between...and...是包含最大值和最小值的

#### is null

null指的是为空的，但不是空字符串，使用的时候需用is null

```mysql
select * from emp where comm is null;
```

#### and 操作符

表示必须同时满足

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where job = 'manager' and sal > 2500;
```

#### or 操作符

满足一个就可

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where job = 'manager' or sal > 2500;
```

#### 表达式的优先级

错误示范

```mysql
select * from emp where sal > 1800 and deptno  = 30 or deptno = 20;
```

原因：先将sal > 1800 and deptno  = 30查询出来，接着对deptno = 20的合并起来

正确代码

```mysql
select * from emp where sal > 1800 and (deptno  = 30 or deptno = 20);
```

表达式的优先级不用刻意记，如果不是有把握的话，可以加括号

#### in 操作符

相当于多个or

```mysql
select * from emp where job in ('manager','salesman');
```

#### not 操作符

```mysql
select * from emp where sal not in (1600,3000);
```

#### like 操作符

需要有引号引用

Like 中的表达式必须放到单引号中或者双引号中  

```mysql
select * from emp where ename like '_A%';
```

### 排序数据

需要排序的话采用order by，order by后可以有多个待排序字段，字段之间用逗号隔开，order by默认采用升序排序，若order by和where子句同时出现，order by子句必须放在where语句后

#### 单一字段排序

```mysql
select * from emp where job = 'manager' order by sal;
```

#### 手动指定排序方式

```mysql
select * from emp order by sal asc; //升序
```

```mysql
select * from emp order by sal desc;//降序
```

#### 多个字段排序

```mysql
select * from emp order by job desc,sal desc;
```

排序字段顺序不一样，排序结果不同，会先按照第一个字段进行排序，接着按照第二个字段进行排序，若出现两个相同字段时，会按照第二个字段进行排序

#### 使用字段的位置来排序

不建议使用这个方法，不明确字段含义

```mysql
select * from emp order by 6;
```

### 数据处理函数/单行处理函数

| 函数        | 主要含义                                 |
| ----------- | ---------------------------------------- |
| Lower       | 转换为小写                               |
| upper       | 转换为大写                               |
| substr      | 取子串(被截的字符串，起始下标，截取长度) |
| length      | 取长度                                   |
| trim        | 去空格                                   |
| str_to_date | 将字符串转为日期                         |
| date_format | 格式化日期                               |
| format      | 设置为千分位                             |
| round       | 四舍五入                                 |
| rand()      | 生成随机数                               |
| Ifnull      | 将null转为一个具体值                     |

#### Lower

```mysql
select lower(ename) from emp;
```

#### upper

```mysql
select upper(ename) from emp;
select * from emp where job =  upper('manager');
```

#### substr

```mysql
select * from emp where substr(ename,1,1) = upper('m');
```

#### length

```mysql
select * from emp where length(ename) = 5;
```

#### trim

```mysql
select * from emp where job = trim(upper('manager '));
```

#### str_to_date

```mysql
select * from emp where HIREDATE = str_to_date('1981-02-20','%Y-%m-%d');
```

#### date_format

```mysql
select empno,ename,date_format(hiredate,'%Y-%m-%d%H:%i:%s') as hiredate from emp;
```

#### format

```mysql
select ename,empno,Format(sal,2) from emp;
```

#### round

```mysql
select round(1542.236);
```

#### rand()

```mysql
select rand();
select * from emp order by rand() limit 2; //限制显示的数量
```

#### Ifnull

```mysql
select empno,ename,sal,(sal + ifnull(comm,0))*12 as yearsal from emp;
```

#### case...when...then...else...end

```mysql
select e.*, sal,case job when 'manager'then sal * 1.1 when 'salesman' then sal*1.5 else sal end as newsal from emp e;
```

### 分组函数/聚合函数/多行函数

| 函数  | 功能       |
| ----- | ---------- |
| count | 取得记录数 |
| sum   | 求和       |
| avg   | 取平均值   |
| max   | 取最大值   |
| min   | 取最小值   |

Tips：分组函数自动忽略空值，且不能放到where之后

#### count

自动忽略为null的值，count(*)也会取得为null的值，count(字段名)不会取得值为null的值

```mysql
select count(*) from emp;
select count(job)from emp;
select count(distinct(job))from emp; //去重
```

#### sum

```mysql
select sum(sal + Ifnull(comm,0)) from emp;
select sum(sal) from emp;
```

sum求和会自动忽略null

#### avg

```mysql
select avg(sal) from emp;
```

#### max

```mysql
select max(sal) from emp;
```

#### min

```mysql
select min(sal) from emp;	
```

#### 组合聚合函数

```mysql
select min(sal),max(sal),sum(sal),avg(sal) from emp;
```

### 分组查询

#### group by

```mysql
select job as '岗位名称',deptno as '部门编号',sum(sal) as '工资合计' from emp group by job,deptno order by job;
```

分组查询必须遵循，select后的字段是group by 后的字段和分组函数，要是想对分组的数据进行排序order by必须在group by 之后

#### having 

对分组数据进行过滤

```mysql
select job as '工作岗位',avg(sal) as '工资均值' from emp group by job having  avg(sal)> 2000;
```

### select语句总结

```mysql
select 字段

from 表名

where 查询条件

group by 字段

having 字段  (为了过滤数据出现，故此不能单独出现)

order by 字段
```

执行顺序如下：

1. 首先对where的条件进行过滤查询
2. 接着group by 进行分组
3. 用having对分组后的数据进行筛选
4. 执行select语句
5. 用order by对查询出来的数据进行排序

原则上是能在where过滤的尽量在where过滤，效率更高，having是针对分组后的数据进行过滤的

### 连接查询

#### 内连接

只会筛选出符合连接表条件的数据，两表的交集

格式如下

```mysql
select 字段 from 表1，表2 where 表1和表2连接条件
<=>
select 字段 from 表1 inner join 表2 on 表1和表2连接条件
```

```mysql
select e.ename,d.dname from emp e inner join dept d on e.deptno = d.deptno;
```

#### 外连接

若两表有未匹配结果，显示为null

##### 左连接

保留左表的全部记录

格式如下

```mysql
select 字段 from 表1 left join 表2 on 表1和表2连接条件 //左外连接
```

```mysql
select e.ename,d.dname from emp e left join dept d on e.deptno = d.deptno;
```

##### 右连接

保留左表的全部记录

格式如下

```mysql
 select 字段 from 表1 left join 表2 on 表1和表2连接条件 //右外连接
```

```mysql
select e.ename,d.dname from emp e right join dept d on e.deptno = d.deptno;
```

### 子查询

#### 在where后添加子查询

```mysql
select empno as '员工编号',ename as '员工姓名', sal as '薪水' from emp where sal > (select avg(sal) from emp);
```

#### 在from后添加子查询

#### 在select后添加子查询

### limit的使用

格式如下

```mysql
select * from 表 limit m,n;
```

m表示开始的下标(从0开始)，n表示显示的条数

```mysql
select * from emp limit 2,6;
```

含义是：查询出第3条数据开始的后6条数据

在排序后的数据限制显示条数，即在order by之后再用limit

```mysql
select * from emp order by sal desc  limit 5;
```

## DDL数据定义语言

### 创建表

#### 基本数据类型

| 类型                         | 描述                                                 |
| ---------------------------- | ---------------------------------------------------- |
| Char(长度)                   | 固定字长字符串，存储空间大小固定，适合作为主键和外键 |
| Varchar(长度)                | 可变字长字符串，存储空间为实际数据空间               |
| double(有效数字位数，小数位) | 数值型                                               |
| float(有效数字位数，小数位)  | 数值型                                               |
| int(长度)                    | 整型                                                 |
| bigint(长度)                 | 长整型                                               |
| Date                         | 日期型                                               |
| BLOB                         | Binary Large OBject（二进制大对象）                  |
| CLOB                         | Character Large OBject（字符大对象）                 |

语法格式如下

```mysql
create table 表名(
	字段名字 字段数据类型 字段长度;
	.......
)
```

```mysql
create table t_student(
student_id int(10),
student_name varchar(20),
sex char(2),
birthday date,
email varchar(30),
classes_id int(3)
)
```

#### 创建表加入的约束

##### 	非空约束 not null

```mysql
create table student(
    student_id int(10),
    student_name varchar(20)not null,
    sex char(2) default 'm',
    birthday date,
    email varchar(30),
    class_id int(3)
	);
```

##### 	唯一约束 unique

```mysql
 create table student(
    student_id int(10),
   	student_name varchar(20)not null,
    sex char(2) default 'm',
    birthday date,
    email varchar(30) unique,
    class_id int(3)
    );
```

##### 	主键约束 primary key

```mysql
 create table student(
    student_id int(10) primary key
   	student_name varchar(20)not null,
    sex char(2) default 'm',
    birthday date,
    email varchar(30) unique,
    class_id int(3)
    );
```

##### 	外键约束 foreign key

外键主要是为了维护表的完整性，外键必须是来自于参照表的主键

##### 	自定义检查约束，check(不建议使用)(在MySQL中现在还不支持)

### 修改表

alter table 增加/修改/删除表结构，不影响表中的数据

#### 增加表结构

```mysql
 alter table student add contact_tel varchar(40);
```

#### 修改表结构

```mysql
alter table student modify contact_tel varchar(100); //修改字段基本数据类型
alter table student change contact_tel sex char(2) not null; //修改字段列的名称
```

#### 删除表结构

```mysql
 alter table student drop contact_tel;//切记不能加字段属性
```

### 删除表

## DML数据操纵语言

### 增加数据

Insert语法格式

```mysql
insert into 表名(字段....)values(值.....);//也可以省略字段进行添加
```

```mysql
insert into emp (empno,ename,job,mgr,hiredate,sal,comm,deptno) values(1245,'lisi','MANAGER', 5245, null,3000, 500, 10);
```

### 删除数据

Delete语法格式

```mysql
delete from 表名 where..... 
```

```mysql
delete from emp where comm = 500;
```

### 修改数据

Update语法格式

```mysql
update 表名 set 字段1 = 修改的值1,字段2 = 修改的值2....where......
```

```mysql
update emp set sal = sal * 1.1 where job = 'manager';
```

## 存储引擎

### 定义

存储引擎主要是一个表存储/组织数据的方式，不同的存储引擎表存储数据的方式不同。

### MyISAM存储引擎

-  MyISAM 存储引擎是 MySQL 最常用的引擎。

   它管理的表具有以下特征：

- 格式文件 — 存储表结构的定义（mytable.frm）

- 数据文件 — 存储表行的内容（ mytable.MYD）

- 索引文件 — 存储表上索引（ mytable.MYI）

-  灵活的 AUTO_INCREMENT 字段处理

- 可被转换为压缩、只读表来节省空间  

### InnoDB存储引擎

- InnoDB 存储引擎是 MySQL 的缺省引擎。
- 它管理的表具有下列主要特征：
  1. 每个 InnoDB 表在数据库目录中以.frm 格式文件表示
  2.  InnoDB 表空间 tablespace 被用于存储表的内容
  3.  提供一组用来记录事务性活动的日志文件
  4.  用 COMMIT(提交)、 SAVEPOINT 及 ROLLBACK(回滚)支持事务处理
  5.  提供全 ACID 兼容
  6.  在 MySQL 服务器崩溃后提供自动恢复
  7. 多版本（ MVCC）和行级锁定
  8. 支持外键及引用的完整性，包括级联删除和更新  

### MEMORY存储引擎

- 使用 MEMORY 存储引擎的表，其数据存储在内存中，且行的长度固定，这两个特点使得 MEMORY 存储引擎非常快。
- MEMORY 存储引擎管理的表具有下列特征：
  1. 在数据库目录内，每个表均以.frm 格式的文件表示。
  2. 表数据及索引被存储在内存中。
  3. 表级锁机制。
  4. 不能包含 TEXT 或 BLOB 字段。
- MEMORY 存储引擎以前被称为 HEAP 引擎。  

### 选择合适的存储引擎

- MyISAM 表最适合于大量的数据读而少量数据更新的混合操作。 MyISAM 表的另一种适用情形是使用压缩的只读表。
- 如果查询中包含较多的数据更新操作，应使用 InnoDB。其行级锁机制和多版本的支持为数据读取和更新的混合操作提供了良好的并发机制。
- 可使用 MEMORY 存储引擎来存储非永久需要的数据，或者是能够从基于磁盘的表中重新生成的数据。  

## TCL事务控制语言

### 事务

事务可以保证多个操作原子性，要么全部成功，要么全部失败。对于数据库而言事务批量的DML要么全部成功，要么全部失败。事务具有以下四个特点(ACID)

原子性(Atomicity)

- 整个事务的操作中，必须作为一个单元全部完成(或全部取消)

一致性(consistency)

- 在事务开始与结束之后，数据库都保持一致状态

隔离性(Isolation)

- 一个事务不会影响另外一个事务的运行

持久性(Durability)

- 在事务完成后，该事务对数据库所做的更改将永久的保存在数据中，并不会回滚。

事务中的一些概念

1. 事务(Transaction)：一批操作(一组DML)
2. 开启事务(StartTransaction)
3. 回滚事务(Rollback)
4. 提交事务(Commit)
5. SER AUTOCOMMIT :禁用或启用事务的自动提交模式

Tips：执行DML语句其实就是开启一个事务，回滚只能是对于delete、update、insert语句，对于select语句回滚无意义，对于create、drop、alter这些无法回滚，事务只对DML有用。

注意：rollback、commit后事务就已经结束了

### 事务提交和回滚演示

创建表

```mysql
mysql> create table user(
    -> id int(5) not null primary key,
    -> username varchar(255),
    -> password varchar(255)
    -> );
```

开启事务

```mysql
start transaction;
```

插入数据

```mysql
 insert into user (id,username,password)
    -> values
    -> (1,'李子雄','123456');
```

修改数据

```mysql
update user set password = '2864988956' where id = 1;
```

回滚

```mysql
rollback
```

![image-20230626103310018](F:\JavaSE基础知识汇总--韩顺平\MySQL知识点汇总.assets\image-20230626103310018.png)

### 事务的隔离级别

#### 隔离级别

- 事务的隔离级别决定了事务之间的可见级别

当多个用户并发地访问同一个表的时候，就会出现以下几种情况：

- 脏读取(Dirty Read)

当事务开始访问了一条数据，另外一个事务已经更新了此条数据但是还未来得及提交，此时产生脏数据读取。

- 不可重复读(Non-repeatable Read)

在同一个事务中，同一个读操作对同一条数据的前后读去会产生不同的结果。

- 幻想读(Phantom Read)

在同一个事务中以前没有的行，经过其他事务的干预而出现了新的行

#### InnoDB四个隔离级别

##### 读未提交

允许一个事务可以看到其余事务未提交的修改

##### 读已提交

允许事务查看其余事务已经提交的修改，不允许查看未提交的修改

##### 可重复读

同一个事务中对同一条数据的先后访问数据结果相同，不管其余事务是否提交已经修改的

##### 串行化(序列化)

将一个事务与其余的事务完全隔离开

例如：A可以开启事务，B也可以开启事务，A对事务进行修改，未提交，B不执行DML、DQL

### 隔离与一致性问题的关系

| 隔离级别 | 脏读取 | 不可重复读 | 幻像读         |
| -------- | ------ | ---------- | -------------- |
| 读未提交 | 可能   | 可能       | 可能           |
| 读已提交 | 不可能 | 可能       | 可能           |
| 可重复读 | 不可能 | 不可能     | 对InnoDB不可能 |
| 串行化   | 不可能 | 不可能     | 不可能         |

## 索引

索引是用来快速找到某一列上特定的行，没有索引的话，MySQL会从第一条记录开始查找，表越大，查找的效率越来越慢，MyISAM和InnoDB存储引擎是用B+Tree作为索引结构(主键、unique都会默认添加索引。

索引创建语法

```mysql
create unique index 索引名 on 表名(列名);
```

```mysql
create unique index u_ename on emp(ename);
```

索引添加语法

```mysql
alter table 表名 add unique index 索引名(列名);
```

查看索引

```mysql
show index from emp;
```

删除索引

```mysql
 alter table emp drop index u_ename;
```

## 视图

视图是为了查询效率而存在的一张虚拟表，是一张逻辑表，本身并不包含数据。

### 创建视图

#### 语法

```mysql
create view 视图名 as <select语句>
```

```mysql
create view v_emp as select * from emp;
```

### 修改视图

#### 语法

```mysql
alter view 视图名 as <select语句>
```

```mysql
alter view v_emp as select ename from emp;
```

### 删除视图

#### 语法

```mysql
drop view 视图名 if exists
```

```mysql
drop view if exists v_student;
```

## DCL数据控制语言

### 创建用户

```mysql
create user 用户名 identified by 密码;
```

### 授权

#### 语法格式

```mysql
grant all privileges on dbname.tbname to 'username'@'login ip' identified by 'password' with grant option;
```

1) dbname=表示所有数据库 

2) tbname=*表示所有表

3) login ip=%表示任何 ip 

4) password 为空，表示不需要密码即可登录 

5) with grant option; 表示该用户还可以授权给其他用户

## 数据库设计三范式

### 第一范式

数据库中不能出现重复记录，每个字段都有原子性，不可再分

![image-20230626142705339](F:\JavaSE基础知识汇总--韩顺平\MySQL知识点汇总.assets\image-20230626142705339.png)

不符合第一范式，主要原因如下：

1. 第一条数据和第三条数据重复，无主键
2. 联系方式字段可以再分，不满足原子性

### 第二范式

基于第一范式，若表中有多个主键，其余非主键字段必须完全依赖与这些主键

如果一个表是单一主键，那么它就复合第二范式，部分依赖和主键有关系  

### 第三范式

基于第二范式，非主键字段不能传递依赖与主键字段

## 练习

**1、 取得每个部门最高薪水的人员名称**  

思路

1）先获取各个部门的最高薪水

```mysql
select max(sal) as maxSal,deptno from emp group by deptno;
```

2）接着将查询出来的结果作为临时表和emp表连接查询出人员名称

```mysql
select e.ename,t.*
from emp e
join (select max(sal) as maxSal,deptno from emp group by deptno) t
on t.deptno = e.deptno and t.maxSal = e.sal;
```

**2、哪些人的薪水在部门的平均薪水之上**  

思路

1）先获取各部门的平均薪水

```mysql
select avg(sal),deptno from emp group by deptno;
```

2）接着将查询出来的结果作为临时表和emp表连接查询薪水高于平均薪水的人员名称

```mysql
select t.avgSal,e.ename 
from emp e 
join (select avg(sal) as avgSal,deptno from emp group by deptno) t 
on t.deptno = e.deptno and e.sal > t.avgSal;
```

**3、取得部门中（所有人的）平均的薪水等级**  

思路

1）先将emp和薪水等级表做连接

```mysql
select e.sal,e.deptno,s.grade from emp e join salgrade s on e.sal between s.losal and s.hisal;
```

2）在此基础之上再按照部门进行分组，求出薪水等级的平均值

```mysql
select e.deptno,avg(s.grade) from emp e join salgrade s on e.sal between s.losal and s.hisal group by e.deptno order by deptno;
```

**4、不准用组函数（ Max），取得最高薪水（给出两种解决方案）**  

思路

1）按照sal进行降序排序，取第一个

```mysql
select sal from emp order by sal desc limit 1;
```

2）自连接，查出除了最大值以外的其余薪水

```mysql
select distinct e2.sal from emp e1 join emp e2 on e1.sal > e2.sal;
```

接着将原emp表中的薪水去除自连接表中的薪水

```mysql
select sal 
from emp 
where sal not in (select distinct e2.sal from emp e1 join emp e2 on e1.sal > e2.sal);
```

**5、取得平均薪水最高的部门的部门编号（至少给出两种解决方案）**  

思路

1）按照部门分组，求出各个部门的平均薪水

```mysql
select avg(sal),deptno from emp group by deptno;
```

​	 按降序去第一条数据

```mysql
select avg(sal) as avgSal,deptno from emp group by deptno order by avgSal desc limit 1;
```

2）同上求出平均薪水，用max函数求出平均薪水中最高的

```mysql
select max(s.avgSal) from (select avg(sal) as avgSal,deptno from emp group by deptno) as s;
```

对于此前求出平均薪水的表中的查询薪水为上述求出的值

```mysql
select avg(sal) as avgSal,deptno from emp group by deptno having avgSal = (select max(s.avgSal) from (select avg(sal) as avgSal,deptno from emp group by deptno) as s);
```

**6、 取得平均薪水最高的部门的部门名称**  

思路

1）按照部门分组，求出各个部门的平均薪水，求出平均薪水最高的部门编号

2）将此表与dept部门表连接，查出部门名称

```mysql
select d.dname from dept d join (select avg(sal) as avgSal,deptno from emp group by deptno order by avgSal desc limit 1) s on d.deptno = s.deptno;
```

**7、求平均薪水的等级最低的部门的部门名称**  

思路

1）先求出各个部门的平均薪水

```mysql
select avg(sal) as avgSal,deptno from emp group by deptno;
```

2）将此表与薪水等级连接查询出对应的各部门的平均薪水对应的等级

```mysql
select s.grade, e.deptno from salgrade s join (select avg(sal) as avgSal,deptno from emp group by deptno) as e on e.avgSal between s.losal and s.hisal;
```

3）将此表与部门表dept进行连接查询出各部门的平均薪水对应的薪水等级，将薪水等级按照升序排序，取出第一个

```mysql
select d.dname from dept d join (select s.grade, e.deptno from salgrade s join (select avg(sal) as avgSal,deptno from emp group by deptno) as e on e.avgSal between s.losal and s.hisal) as g on g.deptno = d.deptno order by g.grade asc limit 1;
```

**8、 取得比普通员工(员工代码没有在 mgr 字段上出现的)的最高薪水还要高的领导人姓名**  

思路

1）查询出普通员工的最高薪水

```mysql
select max(sal)
from emp
where empno not in (select mgr from emp where mgr is not null);
```

2)查询出比最高薪水还要高的领导人姓名

```mysql
select ename,sal
from emp
where sal > (select max(sal)
from emp
where empno not in (select mgr from emp where mgr is not null));
```

**9、取得薪水最高的前五名员工**  

思路

按照薪水排序取前五个

```mysql
select ename,sal from emp order by sal desc limit 5;
```

**10、 取得薪水最高的第六到第十名员工**  

```mysql
 select ename,sal from emp order by sal desc limit 5,5;
```

**11、 取得最后入职的 5 名员工**  

```mysql
select ename,hiredate from emp order by hiredate desc limit 5;
```

**12、 取得每个薪水等级有多少员工**  

思路

1）将emp表和薪水等级连接

```mysql
select e.ename,e.sal,s.grade from emp e join salgrade s on sal between s.losal and s.hisal;
```

2）将连接后的表按照薪水等级进行分组，对各个组中的员工进行求和

```mysql
select s.grade,count(*) from emp e join salgrade s on sal between s.losal and s.hisal group by s.grade order by s.grade;
```

**13、 面试题**
		有 3 个表 S(学生表)， C（课程表）， SC（学生选课表）
		S（ SNO， SNAME）代表（学号，姓名）
		C（ CNO， CNAME， CTEACHER）代表（课号，课名，教师）
		SC（ SNO， CNO， SCGRADE）代表（学号，课号，成绩）
问题：
			1，找出没选过“黎明”老师的所有学生姓名。

思路

1）先查询出“黎明”老师的编号

```mysql
select cno from c where cteacher = '黎明'
```

2）接着作为条件查询出“黎明”编号老师教的学生编号

```mysql
select sno from sc where sc.cno = (select cno from c where cteacher = '黎明');
```

3）在s表中查询出不在上述查询范围内的

```mysql
select sname from s where s.sno not in (select sno from sc where sc.cno = (select cno from c where cteacher = '黎明'));
```

​	2，列出 2 门以上（含 2 门）不及格学生姓名及平均成绩。

思路

1）先查询出不及格科目，按照学生编号分组，查看各个分组下不及格科目的数量 >= 2的

```mysql
select count(cno) as c_cno,sno from sc where scgrade < 60 group by sno having c_cno >= 2;
```

2）和学生表连接求出科目平均值和学生姓名

```mysql
select sname,sc.scgrade from (select count(cno) as c_cno, avg(scgrade) as scgrade,sno from sc where scgrade < 60 group by sno having c_cno >= 2) as sc join s on s.sno = sc.sno;
```

3，即学过 1 号课程又学过 2 号课所有学生的姓名。  

1）在sc表中查询出cno是1或者2号课程的sno和cno编号

```mysql
select sno,cno from sc where cno in (1,2);
```

2）在此基础之上对学生进行分组，计算各个学生所学1、2号课程的数量，筛选出课程数量 >= 2的数据

```mysql
select sno,count(cno) as c_cno from sc where cno in (1,2) group by sno having c_cno >= 2;
```

3）和s表进行连接查询学生姓名

```mysql
select sname from (select sno,count(cno) as c_cno from sc where cno in (1,2) group by sno having c_cno >= 2) as sc join s on sc.sno = s.sno;
```

**14、 列出所有员工及领导的姓名**  

思路

左连接，若选择内连接的话会把mgr为null的给去除掉

```mysql
select e1.ename,ifnull(e2.ename,'没有上级') from emp e1 left join emp e2 on e1.mgr = e2.empno;
```

**15、 列出受雇日期早于其直接上级的所有员工的编号,姓名,部门名称**  

思路

1）查询出所有员工和直接上级的受雇日期，并查出受雇日期早于其直接上级的所有员工

```mysql
select e1.empno, e1.ename, e1.deptno from emp e1 left join emp e2 on e1.mgr = e2.empno where e1.hiredate < e2.hiredate;
```

2）上述查询结果作为条件和部门表dept做内连接，查询结果

```mysql
select e.empno,e.ename, d.dname from (select e1.empno, e1.ename, e1.deptno from emp e1 left join emp e2 on e1.mgr = e2.empno where e1.hiredate < e2.hiredate) as e join dept as d on e.deptno = d.deptno;
```

**16、 列出部门名称和这些部门的员工信息,同时列出那些没有员工的部门.**  

思路

保证部门表的所有数据都在，不能是内连接

```mysql
select * from emp e right join dept d on e.deptno = d.deptno;
```

**17、 列出至少有 5 个员工的所有部门**  

思路

在上述查询的基础上按照部门分组，筛选出员工数量 >= 5的数据

```mysql
select d.dname,count(e.ename) as c_ename from emp e right join dept d on e.deptno = d.deptno group by d.dname having c_ename >= 5;
```

**18、 列出薪金比"SMITH"多的所有员工信息**  

思路

1）先查出员工姓名为"SMITH"的薪资

```mysql
select sal from emp where ename = 'SMITH';
```

2）查询出薪资比上述查询结果多的员工信息

```mysql
select * from emp where sal > (select sal from emp where ename = 'SMITH');
```

**19、 列出所有"CLERK"(办事员)的姓名及其部门名称,部门的人数.**  

思路

1）查出job为"CLERK"(办事员)的数据，将其与dept表进行连接

```mysql
 select e.ename,d.dname from (select ename,deptno from emp where job = 'CLERK') as e join dept d on d.deptno = e.deptno;
```

2）统计出各个部门对应的人数

```mysql
select count(e.empno),d.dname from emp e join dept d on d.deptno = e.deptno group by d.dname;
```

3）将上述查询的两个表做连接，查询出需要的结果

```mysql
select d1.*,e1.c_empno from (select count(e.empno) as c_empno,d.dname from emp e join dept d on d.deptno = e.deptno group by d.dname) as e1 join (select e.ename,d.dname from (select ename,deptno from emp where job = 'CLERK') as e join dept d on d.deptno = e.deptno) as d1 on d1.dname = e1.dname;
```

**20、 列出最低薪金大于 1500 的各种工作及从事此工作的全部雇员人数**  

思路

​	按照job进行分组，而后求出最低薪资 > 1500的人数

```mysql
select job,count(*) from emp group by job having min(sal) > 1500;
```

**21、 列出在部门"SALES"<销售部>工作的员工的姓名,假定不知道销售部的部门编号.**

思路

将emp表和dept做内连接而后筛选出部门名称为“SALES”的员工姓名

```mysql
select e.ename from emp e join dept d on d.deptno = e.deptno where d.dname = 'SALES';
```

**22、 列出薪金高于公司平均薪金的所有员工,所在部门,上级领导,雇员的工资等级**  

思路

```mysql
select 
e2.ename as '姓名',e2.dname as '部门名称',ifnull(e2.e_ename,'无') as '领导姓名',s.grade as '薪资等级' 
from (
    select e1.ename,e1.dname,e.ename as e_ename,e1.sal 
    from emp e 
    right join (
        select e.ename,e.mgr,e.sal,d.dname 
        from dept d 
        join (
            select * 
            from emp 
            where sal > (
                select avg(sal) 
                from emp)
        	 ) as e on e.deptno = d.deptno
    			) as e1 on e1.mgr = e.empno
	) as e2 
	left join salgrade s on e2.sal between s.losal and s.hisal;
```

**23、 列出与"SCOTT"从事相同工作的所有员工及部门名称.**  

思路

1）查出姓名为“SCOTT”的工作名称

```mysql
select * from emp e where job = (select job from emp where ename = 'SCOTT');
```

2）与dept相连查出部门名称

```mysql
select e.ename,d.dname 
from dept d 
join (
    select * 
    from emp e 
    where job = (
        select job 
        from emp 
        where ename = 'SCOTT'
    			)
	) as e on e.deptno = d.deptno 
where e.ename <> 'SCOTT';
```

**24、 列出薪金等于部门 30 中员工的薪金的其他员工的姓名和薪金.**  

思路

```mysql
mysql> select sal from emp where deptno = 30;
+---------+
| sal     |
+---------+
| 1600.00 |
| 1250.00 |
| 1250.00 |
| 2850.00 |
| 1500.00 |
|  950.00 |
+---------+
6 rows in set (0.00 sec)

mysql> select * from emp where sal in (select sal from emp where deptno = 30);
+-------+--------+----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
+-------+--------+----------+------+------------+---------+---------+--------+
6 rows in set (0.13 sec)

mysql> select * from emp where sal in (select sal from emp where deptno = 30) and deptno <> 30;
Empty set (0.00 sec)
```

**25、 列出薪金高于在部门 30 工作的所有员工的薪金的员工姓名和薪金.部门名称.**

思路

```mysql
mysql> select * from emp where sal > (select max(sal) from emp where deptno = 30);
+-------+-------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7788 | SCOTT | ANALYST   | 7566 | 1987-04-19 | 3000.00 | NULL |     20 |
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+-------+-----------+------+------------+---------+------+--------+
4 rows in set (0.00 sec)

mysql> select * from dept d join (select * from emp where sal > (select max(sal) from emp where deptno = 30)) as s on s.deptno = d.deptno;
+--------+------------+----------+-------+-------+-----------+------+------------+---------+------+--------+
| DEPTNO | DNAME      | LOC      | EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+--------+------------+----------+-------+-------+-----------+------+------------+---------+------+--------+
|     20 | RESEARCH   | DALLAS   |  7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|     20 | RESEARCH   | DALLAS   |  7788 | SCOTT | ANALYST   | 7566 | 1987-04-19 | 3000.00 | NULL |     20 |
|     10 | ACCOUNTING | NEW YORK |  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|     20 | RESEARCH   | DALLAS   |  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+--------+------------+----------+-------+-------+-----------+------+------------+---------+------+--------+
4 rows in set (0.00 sec)

mysql> select s.ename,s.sal,d.dname from dept d join (select * from emp where sal > (select max(sal) from emp where deptno = 30)) as s on s.deptno = d.deptno;
+-------+---------+------------+
| ENAME | SAL     | dname      |
+-------+---------+------------+
| JONES | 2975.00 | RESEARCH   |
| SCOTT | 3000.00 | RESEARCH   |
| KING  | 5000.00 | ACCOUNTING |
| FORD  | 3000.00 | RESEARCH   |
+-------+---------+------------+
4 rows in set (0.00 sec)
```

**26、 列出在每个部门工作的员工数量,平均工资和平均服务期限**  

在mysql当中怎么计算两个日期的“年差”，差了多少年？
	TimeStampDiff(间隔类型, 前一个日期, 后一个日期)

```mysql
timestampdiff(YEAR, hiredate, now())
间隔类型：
	SECOND   秒，
	MINUTE   分钟，
	HOUR   小时，
	DAY   天，
	WEEK   星期
	MONTH   月，
	QUARTER   季度，
	YEAR   年
```

思路

```mysql
select deptno, count(*),avg(sal),ifnull(avg(timestampdiff(YEAR,hiredate,now())),0) as avgtime from emp group by deptno;
```

**27、 列出所有员工的姓名、部门名称和工资。**  

```mysql
mysql> select * from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | DEPTNO | DNAME      | LOC      |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |     30 | SALES      | CHICAGO  |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |     30 | SALES      | CHICAGO  |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |     30 | SALES      | CHICAGO  |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |     30 | SALES      | CHICAGO  |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
14 rows in set (0.00 sec)

mysql> select d.dname,e.ename from emp e join dept d on e.deptno = d.deptno;
+------------+--------+
| dname      | ename  |
+------------+--------+
| RESEARCH   | SMITH  |
| SALES      | ALLEN  |
| SALES      | WARD   |
| RESEARCH   | JONES  |
| SALES      | MARTIN |
| SALES      | BLAKE  |
| ACCOUNTING | CLARK  |
| RESEARCH   | SCOTT  |
| ACCOUNTING | KING   |
| SALES      | TURNER |
| RESEARCH   | ADAMS  |
| SALES      | JAMES  |
| RESEARCH   | FORD   |
| ACCOUNTING | MILLER |
+------------+--------+
14 rows in set (0.00 sec)

mysql> select e.ename,d.dname from emp e join dept d on e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
14 rows in set (0.00 sec)

mysql> select e.ename,d.dname e.sal from emp e join dept d on e.deptno = d.deptno;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.sal from emp e join dept d on e.deptno = d.deptno' at line 1
mysql> select e.ename,d.dname,e.sal from emp e join dept d on e.deptno = d.deptno;
+--------+------------+---------+
| ename  | dname      | sal     |
+--------+------------+---------+
| SMITH  | RESEARCH   |  800.00 |
| ALLEN  | SALES      | 1600.00 |
| WARD   | SALES      | 1250.00 |
| JONES  | RESEARCH   | 2975.00 |
| MARTIN | SALES      | 1250.00 |
| BLAKE  | SALES      | 2850.00 |
| CLARK  | ACCOUNTING | 2450.00 |
| SCOTT  | RESEARCH   | 3000.00 |
| KING   | ACCOUNTING | 5000.00 |
| TURNER | SALES      | 1500.00 |
| ADAMS  | RESEARCH   | 1100.00 |
| JAMES  | SALES      |  950.00 |
| FORD   | RESEARCH   | 3000.00 |
| MILLER | ACCOUNTING | 1300.00 |
+--------+------------+---------+
14 rows in set (0.00 sec)

mysql> select e.ename,d.dname,e.sal,e.sal from emp e join dept d on e.deptno = d.deptno;
+--------+------------+---------+---------+
| ename  | dname      | sal     | sal     |
+--------+------------+---------+---------+
| SMITH  | RESEARCH   |  800.00 |  800.00 |
| ALLEN  | SALES      | 1600.00 | 1600.00 |
| WARD   | SALES      | 1250.00 | 1250.00 |
| JONES  | RESEARCH   | 2975.00 | 2975.00 |
| MARTIN | SALES      | 1250.00 | 1250.00 |
| BLAKE  | SALES      | 2850.00 | 2850.00 |
| CLARK  | ACCOUNTING | 2450.00 | 2450.00 |
| SCOTT  | RESEARCH   | 3000.00 | 3000.00 |
| KING   | ACCOUNTING | 5000.00 | 5000.00 |
| TURNER | SALES      | 1500.00 | 1500.00 |
| ADAMS  | RESEARCH   | 1100.00 | 1100.00 |
| JAMES  | SALES      |  950.00 |  950.00 |
| FORD   | RESEARCH   | 3000.00 | 3000.00 |
| MILLER | ACCOUNTING | 1300.00 | 1300.00 |
+--------+------------+---------+---------+
14 rows in set (0.00 sec)

mysql> select e.ename as '姓名',d.dname as '部门名称',e.sal as '薪水' from emp e join dept d on e.deptno = d.deptno;
+--------+--------------+---------+
| 姓名   | 部门名称     | 薪水    |
+--------+--------------+---------+
| SMITH  | RESEARCH     |  800.00 |
| ALLEN  | SALES        | 1600.00 |
| WARD   | SALES        | 1250.00 |
| JONES  | RESEARCH     | 2975.00 |
| MARTIN | SALES        | 1250.00 |
| BLAKE  | SALES        | 2850.00 |
| CLARK  | ACCOUNTING   | 2450.00 |
| SCOTT  | RESEARCH     | 3000.00 |
| KING   | ACCOUNTING   | 5000.00 |
| TURNER | SALES        | 1500.00 |
| ADAMS  | RESEARCH     | 1100.00 |
| JAMES  | SALES        |  950.00 |
| FORD   | RESEARCH     | 3000.00 |
| MILLER | ACCOUNTING   | 1300.00 |
+--------+--------------+---------+
14 rows in set (0.00 sec)
```

**28、 列出所有部门的详细信息和人数**  

```mysql
mysql> select * from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | DEPTNO | DNAME      | LOC      |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |     30 | SALES      | CHICAGO  |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |     30 | SALES      | CHICAGO  |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |     30 | SALES      | CHICAGO  |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |     30 | SALES      | CHICAGO  |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
14 rows in set (0.00 sec)

mysql> select e.* from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
14 rows in set (0.00 sec)

mysql> select e.*,d.dname from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+------------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | dname      |
+-------+--------+-----------+------+------------+---------+---------+--------+------------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 | RESEARCH   |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 | SALES      |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 | SALES      |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 | RESEARCH   |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 | SALES      |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 | SALES      |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 | ACCOUNTING |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 | RESEARCH   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 | ACCOUNTING |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 | SALES      |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 | RESEARCH   |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 | SALES      |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 | RESEARCH   |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 | ACCOUNTING |
+-------+--------+-----------+------+------------+---------+---------+--------+------------+
14 rows in set (0.00 sec)

mysql> select e.*,d.dname,d.loc from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+------------+----------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | dname      | loc      |
+-------+--------+-----------+------+------------+---------+---------+--------+------------+----------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 | RESEARCH   | DALLAS   |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 | SALES      | CHICAGO  |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 | SALES      | CHICAGO  |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 | RESEARCH   | DALLAS   |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 | SALES      | CHICAGO  |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 | SALES      | CHICAGO  |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 | ACCOUNTING | NEW YORK |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 | RESEARCH   | DALLAS   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 | ACCOUNTING | NEW YORK |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 | SALES      | CHICAGO  |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 | RESEARCH   | DALLAS   |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 | SALES      | CHICAGO  |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 | RESEARCH   | DALLAS   |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 | ACCOUNTING | NEW YORK |
+-------+--------+-----------+------+------------+---------+---------+--------+------------+----------+
14 rows in set (0.00 sec)

mysql> select d.*,count(e.ename) from dept d left join emp e on d.deptno = e.deptno group by d.deptno;
+--------+------------+----------+----------------+
| DEPTNO | DNAME      | LOC      | count(e.ename) |
+--------+------------+----------+----------------+
|     10 | ACCOUNTING | NEW YORK |              3 |
|     20 | RESEARCH   | DALLAS   |              5 |
|     30 | SALES      | CHICAGO  |              6 |
|     40 | OPERATIONS | BOSTON   |              0 |
+--------+------------+----------+----------------+
4 rows in set (0.00 sec)
```

**29、 列出各种工作的最低工资及从事此工作的雇员姓名**  

```mysql
mysql> select e.*,t.job from emp e join (select job,min(sal) as minSal from emp group by job) as t on t.job = e.job and t.minSal = e.sal;
+-------+--------+-----------+------+------------+---------+---------+--------+-----------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | job       |
+-------+--------+-----------+------+------------+---------+---------+--------+-----------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 | CLERK     |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 | SALESMAN  |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 | SALESMAN  |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 | MANAGER   |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 | ANALYST   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 | PRESIDENT |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 | ANALYST   |
+-------+--------+-----------+------+------------+---------+---------+--------+-----------+
7 rows in set (0.00 sec)
```

**30、 列出各个部门的 MANAGER(领导)的最低薪金**  

```mysql
mysql> select deptno,min(sal) from emp where job = 'manager' group by deptno;
+--------+----------+
| deptno | min(sal) |
+--------+----------+
|     20 |  2975.00 |
|     30 |  2850.00 |
|     10 |  2450.00 |
+--------+----------+
3 rows in set (0.00 sec)
```

**31、 列出所有员工的年工资,按年薪从低到高排序**  

```mysql
mysql> select ename,(sal * 12) as income from emp order by income;
+--------+----------+
| ename  | income   |
+--------+----------+
| SMITH  |  9600.00 |
| JAMES  | 11400.00 |
| ADAMS  | 13200.00 |
| WARD   | 15000.00 |
| MARTIN | 15000.00 |
| MILLER | 15600.00 |
| TURNER | 18000.00 |
| ALLEN  | 19200.00 |
| CLARK  | 29400.00 |
| BLAKE  | 34200.00 |
| JONES  | 35700.00 |
| SCOTT  | 36000.00 |
| FORD   | 36000.00 |
| KING   | 60000.00 |
+--------+----------+
14 rows in set (0.00 sec)
```

**32、 求出员工领导的薪水超过 3000 的员工名称与领导名称**  

```mysql
mysql> select sal * 12 from emp;
+----------+
| sal * 12 |
+----------+
|  9600.00 |
| 19200.00 |
| 15000.00 |
| 35700.00 |
| 15000.00 |
| 34200.00 |
| 29400.00 |
| 36000.00 |
| 60000.00 |
| 18000.00 |
| 13200.00 |
| 11400.00 |
| 36000.00 |
| 15600.00 |
+----------+
14 rows in set (0.04 sec)

mysql> select ename,(sal * 12) as income from emp order by income;
+--------+----------+
| ename  | income   |
+--------+----------+
| SMITH  |  9600.00 |
| JAMES  | 11400.00 |
| ADAMS  | 13200.00 |
| WARD   | 15000.00 |
| MARTIN | 15000.00 |
| MILLER | 15600.00 |
| TURNER | 18000.00 |
| ALLEN  | 19200.00 |
| CLARK  | 29400.00 |
| BLAKE  | 34200.00 |
| JONES  | 35700.00 |
| SCOTT  | 36000.00 |
| FORD   | 36000.00 |
| KING   | 60000.00 |
+--------+----------+
14 rows in set (0.00 sec)

mysql> select * from emp e1 left join emp e2 on e1.mgr = e2.empno;
+-------+--------+-----------+------+------------+---------+---------+--------+-------+-------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+-------+-------+-----------+------+------------+---------+------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |  7902 | FORD  | ANALYST   | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |  7698 | BLAKE | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |  7698 | BLAKE | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |  7698 | BLAKE | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |  7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |  NULL | NULL  | NULL      | NULL | NULL       |    NULL | NULL |   NULL |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |  7698 | BLAKE | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |  7788 | SCOTT | ANALYST   | 7566 | 1987-04-19 | 3000.00 | NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |  7698 | BLAKE | MANAGER   | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |  7566 | JONES | MANAGER   | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |  7782 | CLARK | MANAGER   | 7839 | 1981-06-09 | 2450.00 | NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+-------+-------+-----------+------+------------+---------+------+--------+
14 rows in set (0.00 sec)

mysql> select e1.ename,e2.ename from emp e1 left join emp e2 on e1.mgr = e2.empno;
+--------+-------+
| ename  | ename |
+--------+-------+
| SMITH  | FORD  |
| ALLEN  | BLAKE |
| WARD   | BLAKE |
| JONES  | KING  |
| MARTIN | BLAKE |
| BLAKE  | KING  |
| CLARK  | KING  |
| SCOTT  | JONES |
| KING   | NULL  |
| TURNER | BLAKE |
| ADAMS  | SCOTT |
| JAMES  | BLAKE |
| FORD   | JONES |
| MILLER | CLARK |
+--------+-------+
14 rows in set (0.00 sec)

mysql> select e1.ename as employee,e2.ename as leader from emp e1 left join emp e2 on e1.mgr = e2.empno;
+----------+--------+
| employee | leader |
+----------+--------+
| SMITH    | FORD   |
| ALLEN    | BLAKE  |
| WARD     | BLAKE  |
| JONES    | KING   |
| MARTIN   | BLAKE  |
| BLAKE    | KING   |
| CLARK    | KING   |
| SCOTT    | JONES  |
| KING     | NULL   |
| TURNER   | BLAKE  |
| ADAMS    | SCOTT  |
| JAMES    | BLAKE  |
| FORD     | JONES  |
| MILLER   | CLARK  |
+----------+--------+
14 rows in set (0.00 sec)

mysql> select e1.ename as employee,e2.ename as leader e2.sal from emp e1 left join emp e2 on e1.mgr = e2.empno;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'e2.sal from emp e1 left join emp e2 on e1.mgr = e2.empno' at line 1
mysql> select e1.ename as employee,e2.ename as leader,e2.sal from emp e1 left join emp e2 on e1.mgr = e2.empno;
+----------+--------+---------+
| employee | leader | sal     |
+----------+--------+---------+
| SMITH    | FORD   | 3000.00 |
| ALLEN    | BLAKE  | 2850.00 |
| WARD     | BLAKE  | 2850.00 |
| JONES    | KING   | 5000.00 |
| MARTIN   | BLAKE  | 2850.00 |
| BLAKE    | KING   | 5000.00 |
| CLARK    | KING   | 5000.00 |
| SCOTT    | JONES  | 2975.00 |
| KING     | NULL   |    NULL |
| TURNER   | BLAKE  | 2850.00 |
| ADAMS    | SCOTT  | 3000.00 |
| JAMES    | BLAKE  | 2850.00 |
| FORD     | JONES  | 2975.00 |
| MILLER   | CLARK  | 2450.00 |
+----------+--------+---------+
14 rows in set (0.00 sec)

mysql> select e1.ename as employee,e2.ename as leader,e2.sal as leaderSal from emp e1 left join emp e2 on e1.mgr = e2.empno having leaderSal > 3000;
+----------+--------+-----------+
| employee | leader | leaderSal |
+----------+--------+-----------+
| JONES    | KING   |   5000.00 |
| BLAKE    | KING   |   5000.00 |
| CLARK    | KING   |   5000.00 |
+----------+--------+-----------+
3 rows in set (0.00 sec)

mysql> select e1.ename as employee,e2.ename as leader from emp e1 left join emp e2 on e1.mgr = e2.empno having e2.sal> 3000;
ERROR 1054 (42S22): Unknown column 'e2.sal' in 'having clause'
mysql> select e1.ename as employee,e2.ename as leader from emp e1 left join emp e2 on e1.mgr = e2.empno having e2.sal > 3000;
ERROR 1054 (42S22): Unknown column 'e2.sal' in 'having clause'
mysql> select e1.ename as employee,e2.ename as leader from emp e1 left join emp e2 on e1.mgr = e2.empno where e2.sal > 3000;
+----------+--------+
| employee | leader |
+----------+--------+
| JONES    | KING   |
| BLAKE    | KING   |
| CLARK    | KING   |
+----------+--------+
3 rows in set (0.00 sec)
```

**33、 求出部门名称中,带'S'字符的部门员工的工资合计、部门人数.**  

```mysql
mysql> select * from emp e join dept d on e.deptno = d.deptno;
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO | DEPTNO | DNAME      | LOC      |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |     30 | SALES      | CHICAGO  |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |     30 | SALES      | CHICAGO  |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |     30 | SALES      | CHICAGO  |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |     30 | SALES      | CHICAGO  |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |     30 | SALES      | CHICAGO  |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |     20 | RESEARCH   | DALLAS   |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |     10 | ACCOUNTING | NEW YORK |
+-------+--------+-----------+------+------------+---------+---------+--------+--------+------------+----------+
14 rows in set (0.00 sec)

mysql> select e.ename,d.dname from emp e join dept d on e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| SMITH  | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| JONES  | RESEARCH   |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| CLARK  | ACCOUNTING |
| SCOTT  | RESEARCH   |
| KING   | ACCOUNTING |
| TURNER | SALES      |
| ADAMS  | RESEARCH   |
| JAMES  | SALES      |
| FORD   | RESEARCH   |
| MILLER | ACCOUNTING |
+--------+------------+
14 rows in set (0.00 sec)

mysql> select e.ename,d.dname from emp e join dept d on e.deptno = d.deptno where d.dname like '%s%';
+--------+----------+
| ename  | dname    |
+--------+----------+
| SMITH  | RESEARCH |
| ALLEN  | SALES    |
| WARD   | SALES    |
| JONES  | RESEARCH |
| MARTIN | SALES    |
| BLAKE  | SALES    |
| SCOTT  | RESEARCH |
| TURNER | SALES    |
| ADAMS  | RESEARCH |
| JAMES  | SALES    |
| FORD   | RESEARCH |
+--------+----------+
11 rows in set (0.07 sec)

mysql> select e.ename,d.dname,sum(e.sal) from emp e join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
ERROR 1055 (42000): Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'bjpowernode.e.ENAME' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by
mysql> select d.dname,sum(e.sal) from emp e join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+----------+------------+
| dname    | sum(e.sal) |
+----------+------------+
| RESEARCH |   10875.00 |
| SALES    |    9400.00 |
+----------+------------+
2 rows in set (0.00 sec)

mysql> select e.ename,d.dname from emp e right join dept d on e.deptno = d.deptno;
+--------+------------+
| ename  | dname      |
+--------+------------+
| CLARK  | ACCOUNTING |
| KING   | ACCOUNTING |
| MILLER | ACCOUNTING |
| SMITH  | RESEARCH   |
| JONES  | RESEARCH   |
| SCOTT  | RESEARCH   |
| ADAMS  | RESEARCH   |
| FORD   | RESEARCH   |
| ALLEN  | SALES      |
| WARD   | SALES      |
| MARTIN | SALES      |
| BLAKE  | SALES      |
| TURNER | SALES      |
| JAMES  | SALES      |
| NULL   | OPERATIONS |
+--------+------------+
15 rows in set (0.00 sec)

mysql> select d.dname,sum(e.sal) from emp e right join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+------------+------------+
| dname      | sum(e.sal) |
+------------+------------+
| RESEARCH   |   10875.00 |
| SALES      |    9400.00 |
| OPERATIONS |       NULL |
+------------+------------+
3 rows in set (0.00 sec)

mysql> select d.dname,ifnull(sum(e.sal),0) from emp e right join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+------------+----------------------+
| dname      | ifnull(sum(e.sal),0) |
+------------+----------------------+
| RESEARCH   |             10875.00 |
| SALES      |              9400.00 |
| OPERATIONS |                 0.00 |
+------------+----------------------+
3 rows in set (0.00 sec)

mysql> select d.dname,ifnull(sum(e.sal),0),count(d.dname) from emp e right join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+------------+----------------------+----------------+
| dname      | ifnull(sum(e.sal),0) | count(d.dname) |
+------------+----------------------+----------------+
| RESEARCH   |             10875.00 |              5 |
| SALES      |              9400.00 |              6 |
| OPERATIONS |                 0.00 |              1 |
+------------+----------------------+----------------+
3 rows in set (0.00 sec)

mysql> select d.dname,ifnull(sum(e.sal),0),count(d.deptno) from emp e right join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+------------+----------------------+-----------------+
| dname      | ifnull(sum(e.sal),0) | count(d.deptno) |
+------------+----------------------+-----------------+
| RESEARCH   |             10875.00 |               5 |
| SALES      |              9400.00 |               6 |
| OPERATIONS |                 0.00 |               1 |
+------------+----------------------+-----------------+
3 rows in set (0.00 sec)

mysql> select d.dname,ifnull(sum(e.sal),0),count(e.ename) from emp e right join dept d on e.deptno = d.deptno where d.dname like '%s%' group by d.dname;
+------------+----------------------+----------------+
| dname      | ifnull(sum(e.sal),0) | count(e.ename) |
+------------+----------------------+----------------+
| RESEARCH   |             10875.00 |              5 |
| SALES      |              9400.00 |              6 |
| OPERATIONS |                 0.00 |              0 |
+------------+----------------------+----------------+
3 rows in set (0.00 sec)
```

**34、 给任职日期超过 30 年的员工加薪 10%.**  

```mysql
mysql> select sal * 1.1 from emp where timestampdiff(YEAR, hiredate, now()) > 30;
+-----------+
| sal * 1.1 |
+-----------+
|    880.00 |
|   1760.00 |
|   1375.00 |
|   3272.50 |
|   1375.00 |
|   3135.00 |
|   2695.00 |
|   3300.00 |
|   5500.00 |
|   1650.00 |
|   1210.00 |
|   1045.00 |
|   3300.00 |
|   1430.00 |
+-----------+
14 rows in set (0.03 sec)

mysql> select sal (sal * 1.1) as newSal from emp where timestampdiff(YEAR, hiredate, now()) > 30;
ERROR 1305 (42000): FUNCTION bjpowernode.sal does not exist
mysql> select e.sal (e.sal * 1.1) as newSal from emp e where timestampdiff(YEAR, hiredate, now()) > 30;
ERROR 1305 (42000): FUNCTION e.sal does not exist
mysql> select sal,(sal * 1.1) as newSal from emp where timestampdiff(YEAR, hiredate, now()) > 30;
+---------+---------+
| sal     | newSal  |
+---------+---------+
|  800.00 |  880.00 |
| 1600.00 | 1760.00 |
| 1250.00 | 1375.00 |
| 2975.00 | 3272.50 |
| 1250.00 | 1375.00 |
| 2850.00 | 3135.00 |
| 2450.00 | 2695.00 |
| 3000.00 | 3300.00 |
| 5000.00 | 5500.00 |
| 1500.00 | 1650.00 |
| 1100.00 | 1210.00 |
|  950.00 | 1045.00 |
| 3000.00 | 3300.00 |
| 1300.00 | 1430.00 |
+---------+---------+
14 rows in set (0.00 sec)
```

