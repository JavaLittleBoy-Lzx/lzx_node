[TOC]

## Java概述

#### Java的特点

1. ##### 健壮性

   Java 的强类型机制、 异常处理、 垃圾的自动收集  

2. ##### 面向对象OOP

3. ##### 跨平台

   Java的跨平台主要是指编译以后的.class文件可以跨平台运行，有句话是"一次编译，到处运行"

   ![image-20230510165249995](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708110723.png)

   更进一步的原因是.class文件运行的JVM有不同版本。如下图：

   ![image-20230518134547535](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708110741.png)

4. ##### 解释性语言(重点理解)

   ​	解释性语言和编译性语言的区别在于编译性语言在编译后不需要编译器就可被机器执行，解释性语言编译后需要用编译器执行，不能直接被机器执行。

![image-20230510170319652](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708110810.png)

#### JVM、JDK、JRE之间的关系

JVM（Java Virtual Machine）：是一个虚拟的计算机， 具有指令集并使用不同的存储区域。 负责执行指令， 管理数据、 内存、 寄存器， 包含在JDK 中。

JDK（Java Development  Kit）：Java开发工具包，包括JRE和Java开发工具包

JRE（Java Runtime Environment）： Java运行环境，包括JVM和核心类，如果只需要运行类或者.class文件，只需安装JRE计即可。

#### Java快速开发

```java
package JavaDemo;

/**
 * @date 14：02$ 2023-5-19$ null$ null$
 **/
//在Java中只能有一个public类，其他类可以有多个
public class Day01 {
    //main函数可以在不同的类中运行，在不是public类中运行为非public的main函数
    public static void main(String[] args) {
        System.out.println("hello,主函数main");
    }
}
class test{
     //main函数在不是public类中运行为非public的main函数
    public static void main(String[] args) {
        System.out.println("hello，test");
    }
}
class test02{
    public static void main(String[] args) {
        System.out.println("hello,test1");
    }
}
```

上述代码有三个类，只有一个public标注的类，且编译的时候将三个类都编译成字节码文件，运行的时候只会出现的结果，运行结果是其中一个。运行流程如图：

![image-20230518141130688](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154517.png)

#### Java转义字符

在控制台， 输入 tab 键， 可以实现命令补全
		\t ： 一个制表位， 实现对齐的功能
		\n ： 换行符
		\\\ ： 一个\
		\\" :一个"
		\\' ： 一个'
		\r :一个回车 System.out.println("韩顺平教育\r 北京");  

#### Java的相对路径何绝对路径

相对路径：相对于当前目录开始形成路径。

绝对路径：从顶级目录开始形成路径。

![image-20230518142108639](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154518.png)

## Java数据类型

![image-20230518142808077](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154519.png)

上图说明Java数据类型有两种，一种是基本数据类型有8种，包括数值型byte、short、int、long、float、double和字符型char、布尔型boolean；引用类型包括类、接口、数组.........

#### 数值型

![image-20230518144030481](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154520.png)

![image-20230518144211708](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154521.png)

在Java中小数默认是double类型，所以double a = 1.1；是正确的，float b = 2.2；是错误的；应该加上float b = 2.2F；

#### 字符型

char字符型占一个字节

#### 布尔型

#### 引用类型

#### 数据类型之间的转换

##### 自动类型转换

![image-20230518150406548](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154522.png)

##### 强制类型转换

## 运算符

```java
  	 	/*%操作*/
		System.out.println(-10 % 3);
        System.out.println(10 % 3);
        System.out.println(10 % -3);
```

取余%运算符在运算时，只有除数会影响结果，上述结果为-1、1、1

#### 逻辑运算符

![image-20230518165534447](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154523.png)

&&逻辑与：第一个条件如果是false，则第二个不会判断，结果就是false，效率高

&逻辑与：无论第一个是不是false，第二个都要判断，效率低

||逻辑或：第一个条件如果是true，则第二个不会判断，结果就是true，效率高

|逻辑或：无论第一个是不是true，第二个都要判断，效率低。

#### 标识符命名规范

1) 包名： 多单词组成时所有字母都小写： aaa.bbb.ccc //比如 com.hsp.crm
		2) 类名、 接口名： 多单词组成时， 所有单词的首字母大写： XxxYyyZzz [大驼峰] 比如： TankShotGame
		3) 变量名、 方法名： 多单词组成时,第一个单词首字母小写,第二个单词开始每个单词首字母大写xxxYyyZzz 			[小驼峰， 简称 驼峰法] 比如： tankShotGame
		4) 常量名：所有字母都大写。多单词时每个单词用下划线连接XX_YY_ZZ，比如定义一个所得税率 TAX_RATE
		5) 后面我们学习到 类，包、接口等时， 我们的命名规范要这样遵守,更加详细的看文档  

#### 位运算

1) int a=1>>2; //1 => 00000001 => 00000000 本质 1 / 2 / 2 =0
		2) int c=1<<2; //1 => 00000001 => 00000100 本质 1 * 2 * 2 = 4

### 程序控制结构

顺序控制结构

分支控制结构

循环控制结构

```java
//直角三角形
        for (int i = 1; i < 10; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
        System.out.println("---------------------------");
        //倒直角三角形
        for (int i = 1; i < 10; i++) {
            for (int j = i; j < 10; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
        System.out.println("---------------------------");
        //九九乘法表
        for (int i = 1; i < 10; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j + "X" + i + "=" + (i * j) + "\t");
            }
            System.out.println();
        }
        for (int i = 1; i <= 9; i++) {
            //控制空格的输出
            for (int k = 1; k <= 9 - i; k++) {
                System.out.print(" ");
            }
            for (int j = 1; j <= 2 * i - 1; j++) {
                if (j == 1 || j == 2 * i - 1 || i == 9){
                    System.out.print("*");
                }else {
                    System.out.print(" ");
                }
            }
            System.out.println("");
        }
  int totalLevel = 20; //层数
//        for(int i = 1; i <= totalLevel; i++) { //i 表示层数
//        //在输出*之前， 还有输出 对应空格 = 总层数-当前层
//            for(int k = 1; k <= totalLevel - i; k++ ) {
//                System.out.print(" ");
//            } //
//            // 控制打印每层的*个数
//            for(int j = 1;j <= 2 * i - 1;j++) {
//            //当前行的第一个位置是*,最后一个位置也是*, 最后一层全部 *
//                if(j == 1 || j == 2 * i - 1 || i == totalLevel) {
//                    System.out.print("*");
//                } else { //其他情况输出空格
//                    System.out.print(" ");
//                }
//            } //
//            //每打印完一层的*后， 就换行 println 本身会换行
//            System.out.println("");
//        }
```

![image-20230519135543276](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708150415.png)

## 数组和排序

#### 数组的赋值机制

默认情况下，数组采用引用传值，赋的值是地址；而基本数据类型所采用的是值传递

```java
 		 /**
         * Day03 TODO 数组
         */
        int a = 10;
        int b = a;
        b = 12;
        System.out.println(b);
        System.out.println("----------------");
        int[] arr1 = {1,2,3};
        int[] arr2 = arr1;
        arr2[0] = 10;
        for (int i = 0; i < arr1.length; i++) {
            System.out.println(arr1[i]);
        }
```

![image-20230520094629648](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154524.png)

如上图所见，基本数据类型传值不会影响到原来的数值，而数组的引用传递则会影响到原来的数值。

数组拷贝则不会影响到原来数组的数值，要求是新的数组需有独立的内存空间，且遍历将原数组中的值一一传递给新数组。

冒泡排序

```java
 //TODO 冒泡排序
        int[] arr = {5,9,6,1,31,6,5,4,3,16,5,41,3,14,6,4,1,3,5};
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr.length - 1 - i; j++) {
                if (arr[j] > arr[j + 1]){
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        for (int i : arr) {
            System.out.println(i);
        }
```

二分查找

```java
 public int searchBin(int[] arr,int num){
        int low = 0;
        int high = arr.length - 1;
        int mid;
        while (low <= high){
            mid = (low + high) / 2;
            if (num == arr[mid]){
                return mid;
            }else if (arr[mid] > num){
                high = mid - 1;
            }else {
                low = mid + 1;
            }
        }
        return -1;
    }
```

## 面向对象(OOP)初级

#### OverLoad方法重载

要求：

1. 方法名必须相同；
2. 形参列表必须不同；
3. 返回值无要求

#### 可变参数

要求：

1. 可变参数的实参可以是0个或多个；
2. 可变参数的实参可以是数组，且可变参数实质是数组；；
3. 可变参数可以和普通参数放在同一个形参列表，但可变参数必须放在形参列表最后；
4. 一个形参列表只能有一个可变参数；

#### 作用域

##### 全局变量/属性

作用域为整个类，且不需要赋值就可以直接使用。

##### 局部变量

作用域仅为某个方法，或者其定义的代码块，且必须赋值，没有默认值。

在同一个作用域中，两个局部变量不能重名。

##### 全局变量和局部变量的区别

1. 属性的生命周期较长，对象创建生，对象销毁亡；局部变量生命周期短，仅为某个代码块创建而生，伴随着代码块的结束而消亡。
2. 属性可以不加修饰符，但局部变量必须加修饰符；

#### Object类

##### equals()方法

==和equlas()方法的区别：

1. ==可以判断数据类型是否相等，也可以判断引用类型是否相等；
2. ==判断基本数值类型是判断值是否相等；
3. ==判断引用类型是判断两个对象是否是一个，即两个对象的地址是否相同；
4. equlas()方法只能判断引用类型，默认是判断地址是否相等，子类可以重写该方法

## 面向对象(OOP)高级

#### 类变量和类方法

##### 类变量

用static修饰的变量称作静态变量/静态属性，在加载类的时候就已经生成了，所有的对象都可以共享

##### 类方法(静态方法)

静态方法只能访问静态属性变量，可以通过类访问，若为普通方法则需要实例化成对象才可以使用。this和super仅限于对象使用，即只有在普通方法中可以使用。

```java
package JavaDemo.OOP;

/**
 * @ClassName Day02
 * @Description TODO 展示
 * @Author 李子雄
 * @Date 2023/6/19 17:09
 * @Version 1.0
 **/
public class Day02 {
    public static void main(String[] args) {
        new Day02Test().talk();
        new Day02Test().talk();
        System.out.println(Day02Test.count);
    }
}
class Day02Test{
      static int count = 9; //普通属性
//    public static int id = 1; //静态属性
    public void  talk(){  //普通方法
        System.out.println("count = " + (count++));
    }
    public static int Sum(int a, int b){  //静态方法
        return a + b;
    }
}
```

![image-20230620143247932](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154525.png)

Tips:在类中的普通方法可以使用静态属性，在static方法中不能使用this或者super关键字，静态方法只能访问静态属性，非静态方法可以访问所有的属性。

#### 代码块

静态代码块执行比构造器要早

```java
package JavaDemo.OOP;

/**
 * @ClassName Day02
 * @Description TODO 展示
 * @Author 李子雄
 * @Date 2023/6/19 17:09
 * @Version 1.0
 **/
public class Day02 {
    public static void main(String[] args) {
//        new Day02Test().talk();
//        new Day02Test().talk();
//        System.out.println(Day02Test.count);
        Test1 test1 = new Test1();
    }
}
class Day02Test{
    static int count = 9; //普通属性
//    public static int id = 1; //静态属性
    public static void  talk(){  //普通方法
        System.out.println("count = " + (count++));
//        System.out.println(this.count);
    }
    public static int Sum(int a, int b){  //静态方法
        return a + b;
    }
}
class Sample{
    Sample(String s){
        System.out.println(s);
    }
    Sample(){
        System.out.println("Sample 默认构造函数被调用");
    }
}
class Test1{
    Sample sam1 = new Sample("sam1 成员初始化");
    static Sample sam = new Sample("静态成员 sam 初始化");
    static {
        System.out.println("static静态代码块执行！");
        if (sam == null){
            System.out.println("sam is null");
        }
    }
    Test1(){
        System.out.println("Test 默认构造函数被调用");
    }
}
```

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154526.png" alt="image-20230620161304854" style="zoom:80%;" />

#### 单例设计模式

##### 饿汉式

1. 将构造器私有化
2. 在类的内部直接创建对象(该对象是static)
3. 创建一个公共的静态方法，返回对象

```java
class Cat{
    private String name;
    static Cat cat = new Cat("小花花");
    private Cat(String name) {
        System.out.println("构造器已经私有化！");
        this.name = name;
    }
    public static Cat getCat(){
        return cat;
    }
}
public class Day02 {
    public static void main(String[] args) {
        Test1 test1 = new Test1();
               Cat cat = Cat.getCat();
        Cat cat1 = Cat.getCat();
        System.out.println(cat == cat1);
    }
}
```

##### 懒汉式

1. 将构造器私有化
2. 创建私有的静态属性对象
3. 创建一个公共的返回对象的静态方法
4. 只有在使用上述方法的时候才会创建

```java
class Cat{
    private String name;
    private static Cat cat;
    private Cat(String name) {
        System.out.println("构造器已经私有化！");
        this.name = name;
    }
    public static Cat getCat(){
        if (cat == null){
            cat =  new Cat("小花花");
        }
        return cat;
    }
}
```

#### final关键字

1. 被final修饰的属性值会变做常量不可修改，局部变量同理，必须初始化赋值。
2. 被final修饰的类不可被子类继承，但可以实例化对象。
3. 被final修饰的方法不可被重写或者覆盖，类若没有被final修饰的话，该方法可以被继承。
4. 一般static和final关键字一起使用，效率会更高。
5. 包装类都是被final修饰的，不可以被继承

#### 抽象类

1. 用abstract修饰的类称作抽象类，抽象类中不一定含有abstract修饰的方法
2. 类中有用abstract修饰的抽象方法该类一定要声明为abstract
3. 抽象类中的方法不需要有方法体，可以被继承重写抽象方法，抽象类不可以被实例化
4. abstract只能修饰类和方法
5. 抽象方法不能被private、final、static修饰，这些都是与重写相违背

```java
package JavaDemo.OOP;

/**
 * @ClassName Day03
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:39
 * @Version 1.0
 **/
public class Day03 {
    public static void main(String[] args) {
        //测试普通员工
        CommonEmployee commonEmployee = new CommonEmployee(12, "小李", 125.5);
        commonEmployee.work();
        //测试经理
        Manager manager = new Manager(1, "啦啦啦", 5000);
        manager.setBonus(2500);
        manager.work();

    }
}
package JavaDemo.OOP;

/**
 * @ClassName Em
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:09
 * @Version 1.0
 **/
abstract class Employee {
    private int id;   //属性值
    private String name;
    private double salary;
    //抽象方法
    abstract void work();
    //无参构造器
    public Employee() { }
    //有参构造器
    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
}
package JavaDemo.OOP;

/**
 * @ClassName Manager
 * @Description TODO 管理抽象类
 * @Author 李子雄
 * @Date 2023/6/21 8:12
 * @Version 1.0
 **/
public class Manager extends Employee {
    private double bonus;//私有属性
    //有参构造器
    public Manager(int id, String name, double salary) {
        super(id, name, salary);
    }
    public double getBonus() {
        return bonus;
    }
    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    @Override
    void work() {
        System.out.println("经理" + getName() + "工作中....");
    }
}
```

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154527.png" alt="image-20230621084329169" style="zoom:80%;" />

#### 抽象类实践--模板设计模式

```java
package JavaDemo.OOP;

/**
 * @ClassName Template
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:52
 * @Version 1.0
 **/
abstract public class Template { //抽象类模板设计模式
    public abstract void job();  //用于实现不同的job方法
    /*用于计算不同工作时间所需要的时间*/
    public void calculateTime(){
        //开始时间
        long startTime = System.currentTimeMillis();
        job();
        //结束时间
        long endTime = System.currentTimeMillis();
        //计算差
        System.out.println("job()方法工作了" + (endTime - startTime) + "毫秒");
    }
}
package JavaDemo.OOP;

/**
 * @ClassName AA
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:56
 * @Version 1.0
 **/
public class AA extends Template {
    @Override
    public void job() {
        int sum = 0;
        for (int i = 0; i < 999999999; i++) {
            sum += i;
        }
    }
}
package JavaDemo.OOP;

/**
 * @ClassName BB
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:57
 * @Version 1.0
 **/
public class BB extends Template {
    @Override
    public void job() {
        int a = 1;
        for (int i = 1; i <= 999999999; i++) {
            a *= i;
        }
    }
}
package JavaDemo.OOP;

/**
 * @ClassName Day03
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 8:39
 * @Version 1.0
 **/
public class Day03 {
    public static void main(String[] args) {
        AA aa = new AA();
        aa.calculateTime();
        BB bb = new BB();
        bb.calculateTime();
    }
}
```

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154528.png" alt="image-20230621090217491" style="zoom:80%;" />

#### 接口

小结：接口是更加抽象的类，抽象类中可以有方法体，但接口中不能出现具体的方法体(jdk7.0)，在jdk8.0以后在接口中可以有默认方法和静态方法

1. 实体类实现接口的时候必须将接口中的抽象方法全部实现，抽象类则不需要实现全部抽象方法。
2. 接口中的抽象方法都是public修饰，可以不用abstract修饰
3. 接口的修饰符只能是public和默认default

#### 内部类

##### 局部内部类

```java
package JavaDemo.OOP;

/**
 * @ClassName LocalInnerClass
 * @Description TODO 演示局部内部类
 * @Author 李子雄
 * @Date 2023/6/21 13:43
 * @Version 1.0
 **/
public class LocalInnerClass {
    public static void main(String[] args) {
        Outer02 outer02 = new Outer02();
        outer02.m1();
        System.out.println("outer的hashcode是" + outer02);
        System.out.println("outer的hashcode是" + outer02.hashCode());
    }
}
class Outer02{ //外部类
    private int id = 15; //私有属性
    private void m2(){ //私有方法
        System.out.println("Outer02 m2");
    }
    public void m1(){  //公有方法
        //局部内部类是定义在外部类的局部位置，一般是在方法内
        //局部内部类不能添加任何修饰符，除了final
        //作用域仅限在定义内部类的方法或者是代码块中
        final class Inner02{ //局部内部类可以直接访问外部类的成员,但只仅限于在方法内
            private int id = 20;
            public void f1(){
                //Outer02.this 类似与 外部类的对象
                System.out.println("id = " + id + "外部类的id为：" + Outer02.this.id);
                System.out.println("Outer02.this.hashcode = " + Outer02.this);
                m2();
            }
        }
        //外部类的方法中可以创建Inner02对象，然后调用该方法
        Inner02 inner02 = new Inner02();
        inner02.f1();
    }
}
```

![image-20230621140625019](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154529.png)

##### 匿名内部类(不会)

##### 成员内部类(不会)

##### 静态内部类(不会)

## 枚举和注解

### 枚举

枚举是一组常量的集合，一般不需要修改

#### 自定义枚举

小结Tips：

1. 将构造器私有化
2. 在类内部创建一组常数对象
3. 对外暴露对象，通过用publi final static 来修饰
4. 提供get方法不提供set方法

```java
package JavaDemo.OOP;

/**
 * @ClassName Enumeration
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 15:16
 * @Version 1.0
 **/
public class Enumeration {
    public static void main(String[] args) {
        System.out.println(Season.SPRING.getName());
        System.out.println(Season.AUTUMN);
    }
}
class Season{
    private String name;
    private String desc;
    //将构造器私有化
    private Season(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }
    //创建一组常量对象
    public final static Season SPRING = new Season("春天","温暖");
    public final static Season WINTER = new Season("冬天","寒冷");
    public final static Season AUTUMN = new Season("秋天","凉爽");
    public final static Season SUMMER = new Season("夏天","炎热");
    //创建get方法

    public String getName() {
        return name;
    }

    public String getDesc() {
        return desc;
    }
}
```

<img src="https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708152638.png" alt="image-20230621152732160" style="zoom:80%;" />

#### enum关键字实现枚举

```java
package JavaDemo.OOP;

/**
 * @ClassName AnonymousInnerClass02
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/21 15:30
 * @Version 1.0
 **/
public class AnonymousInnerClass02 {
    public static void main(String[] args) {
        System.out.println(Season1.AUTUMN.getName());
        System.out.println(Season1.SPRING);

    }
}
enum Season1{
    SPRING("春天","温暖"),WINNER("冬天","寒冷"),AUTUMN("秋天","凉爽"),SUMMER("夏天","炎热");
    private String name;
    private String desc;

    private Season1(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }
    private  Season1() {
    }
    public String getName() {
        return name;
    }
    public String getDesc() {
        return desc;
    }
}
```

使用enum关键字就不能再继承其他类了，默认enum就已经继承了Enum类了，Java类是单继承机制。

### 注解

## 异常Exception

异常体系图

![image-20230621155541064](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154530.png)

### 异常类型

#### 运行时异常

逻辑错误，是编译器检查不出来的，需要避免的

常见的运行时异常

1. NullPointerException 空指针异常
2. ArithmeticException 数学运算异常
3. ArrayIndexOutOfBoundsException 数组下标越界异常
4. ClassCastException 类型转换异常
5. NumberFormatException 数字格式不正确异常  

#### 编译时异常

编译器处理的异常

### try-catch-finally执行顺序小结

1. 若try中的代码没有异常，则执行try中的全部代码，不执行catch中的代码，若有finally，最后执行finally中的代码
2. 若try中有异常，则执行到出现异常的代码停止，后边的代码不再执行，执行对应catch中的代码，最后执行finally中的代码

### 自定义异常

#### throws和throw的区别

throws是异常处理的一种方式，主要是在方法中声明

throw是手动生成异常对象的关键字

```java
package JavaDemo.Exception;

import java.util.Scanner;

/**
 * @ClassName ThrowException
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/24 8:06
 * @Version 1.0
 **/
public class ThrowException {
    public static void main(String[] args) {
        System.out.print("请输入年龄：");
        Scanner scanner = new Scanner(System.in);
        int age = scanner.nextInt();
        if (age <= 18 || age >= 120) {
            throw new AgeException("年龄需要在18~120岁之间！");
        }
        System.out.println("您输入的年龄正确！");
    }
}
class  AgeException extends RuntimeException{
    public AgeException(String message) {
        super(message);
    }
}
```

## 常用类

### 包装类

#### 基本数据类型与其对应的包装类

double -> float -> long -> int -> short  -> byte -> char ->boolean

Double -> Float -> Long -> Integer -> Byte -> Character -> Boolean

#### 拆箱和装箱

##### 拆箱

包装类 -> 基本类型

jdk 5 之前需要手动拆箱和装箱

##### 装箱

基本类型 -> 包装类

jdk 5之后包括5之后采用自动拆箱装箱，底层原理是调用的valueOf方法，如Integer.valueOf

### String类

#### 两种创建String类的方式

##### String str = “hsp”；

##### String str1 = new String("hsp")

1. String str1= “abc”； 在编译期，JVM会去常量池来查找是否存在“abc”，如果不存在，就在常量池中开辟一个空间来存储“abc”；如果存在，就不用新开辟空间。然后在栈内存中开辟一个名字为str1的空间，来存储“abc”在常量池中的地址值。
2. String str2 = new String("abc") ;在编译阶段JVM先去常量池中查找是否存在“abc”，如果过不存在，则在常量池中开辟一个空间存储“abc”。在运行时期，通过String类的构造器在堆内存中new了一个空间，然后将String池中的“abc”复制一份存放到该堆空间中，在栈中开辟名字为str2的空间，存放堆中new出来的这个String对象的地址值。

也就是说，前者在初始化的时候可能创建了一个对象，也可能一个对象也没有创建；后者因为new关键字，至少在内存中创建了一个对象，也有可能是两个对象。

#### String、StringBulider、StringBuffer

### Arrays类

自定义排序方式

```java
package JavaDemo.Class;

/**
 * @ClassName Book
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/24 10:07
 * @Version 1.0
 **/
public class Book {
    private String name; //私有属性
    private double price;
    //无参构造器
    public Book() {}

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public Book(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public String toString() {
        return "Book{" +
                "name='" + name + '\'' +
                ", price=" + price +
                '}';
    }
}
package JavaDemo.Class;

import java.lang.reflect.Array;
import java.util.Arrays;
import java.util.Comparator;

/**
 * @ClassName BookTest
 * @Description TODO 对Book对象的名称长度和价格大小进行排序
 * @Author 李子雄
 * @Date 2023/6/24 10:09
 * @Version 1.0
 **/
public class BookTest {
    public static void main(String[] args) {
        Book[] books = new Book[4];
        books[0] = new Book("红楼梦", 100);
        books[1] = new Book("金瓶梅新", 90);
        books[2] = new Book("青年文摘20年", 5);
        books[3] = new Book("java从入门到放弃~", 300);

        //price从大到小
//        Arrays.sort(books, new Comparator<Book>() {
//            @Override
//            public int compare(Book o1, Book o2) {
//                double priceVal = o2.getPrice() - o1.getPrice();
//                //做出判断
//                if (priceVal > 0){
//                    return 1;
//                }else if (priceVal < 0){
//                    return -1;
//                }else {
//                    return 0;
//                }
//            }
//        });

        //price从小到大
//        Arrays.sort(books, new Comparator<Book>() {
//            @Override
//            public int compare(Book o1, Book o2) {
//                double priceVal = o2.getPrice() - o1.getPrice();
//                //做出判断
//                if (priceVal > 0){
//                    return -1;
//                }else if (priceVal < 0){
//                    return 1;
//                }else {
//                    return 0;
//                }
//            }
//        });
        //name的长度从大到小
        Arrays.sort(books, new Comparator<Book>() {
            @Override
            public int compare(Book o1, Book o2) {
                String o1Name = o1.getName();
                String o2Name = o2.getName();
                int length = o2Name.length() - o1Name.length();
                if (length > 0){
                    return 1;
                }else if (length < 0){
                    return -1;
                }else{
                    return 0;
                }
            }
        });
        System.out.println(Arrays.toString(books));
    }
}
```

![image-20230624102456959](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154531.png)

## 集合

![image-20230624104657957](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154532.png)

### Collection(单例集合)

#### 遍历方式

Iterator迭代器

增强for循环

```java
package JavaDemo.Collection;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

/**
 * @ClassName List
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/24 10:57
 * @Version 1.0
 **/
public class List {
    public static void main(String[] args) {
        Collection<Book> bookArrayList = new ArrayList<>();
        bookArrayList.add(new Book("三国演义", "罗贯中", 10.1));
        bookArrayList.add(new Book("小李飞刀", "古龙", 5.1));
        bookArrayList.add(new Book("红楼梦", "曹雪芹", 34.6));
        //用迭代器遍历
        Iterator<Book> bookIterator = bookArrayList.iterator();
        while (bookIterator.hasNext()){
            Book book = bookIterator.next();
            System.out.println("book = " + book);
        }
        //增强for循环
        System.out.println("====================================");
        for (Book book : bookArrayList) {
            System.out.println("book = " + book);
        }
    }
}
```

### Map(双列集合)

#### 遍历方式(先遍历所有的键，接着遍历所有的值)

增强for循环

迭代器Interator

使用EntrySet方法

```java
package JavaDemo.Map;

import java.util.Collection;
import java.util.HashMap;
import java.util.Set;

/**
 * @ClassName Map
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/6/24 13:57
 * @Version 1.0
 **/
public class Map {
    public static void main(String[] args) {
        HashMap<Integer, String> hashMap = new HashMap<>();
        hashMap.put(1,"语文");
        hashMap.put(2,"数学");
        hashMap.put(3,"英语");
        hashMap.put(4,"高等数学");
        hashMap.put(5,"线性代数");
        hashMap.put(6,"计算机组成与原理");
        hashMap.put(7,"Python编程语言");
        //遍历
        //遍历所有的键
        Set<Integer> keySet = hashMap.keySet();
        for (Integer integer : keySet) {
            System.out.println("integer = " + integer);
        }
        //遍历所有的值
        Collection<String> values = hashMap.values();
        for (String value : values) {
            System.out.println("value = " + value);
        }
        //采用EntrySet来遍历
        Set<java.util.Map.Entry<Integer, String>> entries = hashMap.entrySet();
        for (java.util.Map.Entry<Integer, String> entry : entries) {
            System.out.println(entry.getKey() + "-" + entry.getValue());
        }
    }
}
```

![image-20230624140852892](https://gitee.com/li__son__male/my_pic_bed/raw/master/img/20230708154533.png)

## 多线程

### 线程

线程是在进程中的一个实体，是由进程创建的

单线程就是同一时刻之下只允许有一个线程执行；

多线程是指在同一时刻可以执行多条线程，即QQ可以开多个窗口

并行：同一时刻多个程序同时执行，多核CPU可以实现并行执行

并发：在同一时刻，多个任务交替执行(即获取CPU的使用权)，给人一种错觉就是多个程序同时执行

### 进程

进程就是运行在操作系统中的程序，运行程序操作系统会给其分配必要的内存空间。