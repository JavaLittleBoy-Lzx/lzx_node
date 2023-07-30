[TOC]

# JavaSE OOP(面向对象编程思想)

## 一、OOP介绍

OOP是Object-Oriented-Programming(面向对象程序设计)的简称，主要特征有继承、封装和多态。此次主要总结学习的内容包括OOP的三大基本特征、内部类、抽象类、接口、泛型、重载/重写、注解、反射等。

## 二、OOP三大特性

### 继承

#### 介绍

继承就是简化了子类的代码，使用继承需要注意一下几点：

1. 若父类无没有无参构造器，子类继承的时候就需要用到super(参数)；来构建有参构造器，否则会报错，原因是Java默认会再子类构造器的第一行添加super()方法，因父类只有有参构造器所以super();没有起到作用，在子类就需要用super(参数)来构建
2. 子类只可以继承一个父类，Java实行的是单继承，多实现。例：Childern、Student均可以继承Person，但Student不能再继承Object
3. 继承不能采用private，一般采用protected，这个修饰符的作用域是父类和子类，允许子类访问父类的属性值和方法
4. Java可以实现向上转型(子类->父类)，不可实现向下转型(父类->子类)，因父类比子类复杂得多

#### 示例代码

```java
package JavaDemo.NewOOP;
import JavaDemo.OOP.Child;

import java.util.stream.Stream;

/**
 * @ClassName Demo
 * @Description TODO 面向对象编程基础
 * @Author 李子雄
 * @Date 2023/7/5 8:02
 * @Version 1.0
 **/
public class Demo {
    public static void main(String[] args) {
        //向上转型
        Children student = new Student(12,50);
        //向下转型
//        Children children = (Student)new Children(14,"李子雄");//可以不改变类型,报错Children cannot be cast to JavaDemo.NewOOP.Student
        Children student1 = new Children(15,"李子雄1");//报错JavaDemo.NewOOP.Children cannot be cast to JavaDemo.NewOOP.Student
        System.out.println(student.getClass());
        Student student2 = (Student) student;
//        System.out.println(student1.getClass());
//        System.out.println(children.getClass());
        //instanceof用来判断某个实例是不是具体某种类型
        System.out.println(student instanceof Children);
        System.out.println(student1 instanceof Student);
        System.out.println(student2 instanceof Object);
    }

}
class Children {
    private String name;
    private int age;

    //setter方法
    public void setAge(int age){
        this.age = age;
    }
    //getter方法
    public int getAge(){
        return this.age;
    }
    public void setName(String name){
//        for (int i = 0; i < this.name.length; i++) {
//            this.name[i] = name[i];
//        }
        this.name = name;
    }
    public String getName(){
        return this.name;
    }
    //无参构造器
//    public Children(){
//
//    }
//    有参构造器(单个参数)
    public Children(int age){
        this.age = age;
    }
    //有参构造器(多个参数)
    public Children(int age,String name){
        this.age = age;
        this.name = name;
    }
    public void names(String ...name){
        for (int i = 0; i < name.length; i++) {
            System.out.println("输入的name为：" + name[i]);
        }
    }

}
class Student extends Children{
    private int grade;

    public Student(int age, int grade) {
        super(age);
        this.grade = grade;
    }

    public Student(int age, String name, int grade) {
        super(age, name);
        this.grade = grade;
    }
}
```

### 封装

#### 介绍

采用private来对类的方法和属性值进行私有化

### 多态

#### 介绍

多态即是对不同接口的实现

#### 示例代码

```java
package JavaDemo.NewOOP;

/**
 * @ClassName Demo2
 * @Description TODO 多态测试
 * @Author 李子雄
 * @Date 2023/7/5 11:19
 * @Version 1.0
 **/
public class Demo2 {
    public static void main(String[] args) {
        Income[] incomes = new Income[]{
                new Income(3000,150),
                new Salary(7500,1500),
                new StateCouncilSpecialAllowance(15000,2000)
        };
//        boolean totalTax;
        System.out.println(totalTax(incomes));

    }

    private static double totalTax(Income... incomes) {
        double total = 0;
        for (Income income : incomes) {
            total += income.getTex();
        }
        return total;
    }
}
class Income {
    protected double income;
    protected double sal;
    //setter
    public Income(double income,double sal){
        this.income = income;
        this.sal = sal;
    }
    //计算税率的方法
    public double getTex(){
        return (income + sal) * 0.1;
    }
}
class Salary extends Income {

    public Salary(double income,double sal) {
        super(income,sal);
    }
    //重写计算税率的方法
    @Override
    public double getTex(){
        if (income <= 5000){
            return 0;
        }else {
            return ((income - 5000) + sal) * 0.2;
        }
    }
}
class StateCouncilSpecialAllowance extends Income {

    public StateCouncilSpecialAllowance(double income,double sal) {
        super(income,sal);
    }
    @Override
    public double getTex(){
        return 0;
    }
}
```

#### 多态应用之重载和重写

##### 重载(Overload)

重载即重新加载，作用域为本类，重载是在本类中有相同的方法名，但参数列表不同，返回值可以相同也可以不同，但不能作为判断是否为重载的依据，此为编译时多态。

##### 重写(Override)

重写即为重新编写父类的方法，参数列表必须相同，返回值也必须相同，此为运行时多态。

##### 重写和重载的区别

1. 作用域不同：重写是作用于父类与子类之间，重载只作用于本类
2. 方法名和参数列表不同：重写要求方法名和参数以及返回值必须相同、重载则是要求只需要方法名相同即可，参数列表和返回值都可以不同

## 三、OOP之方法

### 私有方法

#### 介绍

Java的私有方法仅限于在类的内部使用，在main()方法中实例化对象也使用不了

#### 实例

```java
package JavaDemo.NewOOP;
import JavaDemo.OOP.Child;

/**
 * @ClassName Demo
 * @Description TODO 面向对象编程基础
 * @Author 李子雄
 * @Date 2023/7/5 8:02
 * @Version 1.0
 **/

public class Demo {
    public static void main(String[] args) {
        Children children = new Children();
    }

}
class Children {
    private String name;
    private int age;

    //setter方法
    public void setAge(int age){
        this.age = age;
    }
    //getter方法
    public int getAge(){
        this.getName();
        return this.age;
    }
    public void setName(String name){
        this.name = name;
    }
    private String getName(){
        return this.name;
    }
    public void names(String ...name){
        for (int i = 0; i < name.length; i++) {
            System.out.println("输入的name为：" + name[i]);
        }
    }

}
```

![image-20230705091704526](C:\Users\28649\AppData\Roaming\Typora\typora-user-images\image-20230705091704526.png)

### 参数传递

#### 值传递

##### 介绍

方法中的参数若为基本数据类型为值传递，局部变量的变化不会影响参数，两者之间互不影响

##### 实例

```java
package JavaDemo.NewOOP;
import JavaDemo.OOP.Child;

/**
 * @ClassName Demo
 * @Description TODO 面向对象编程基础
 * @Author 李子雄
 * @Date 2023/7/5 8:02
 * @Version 1.0
 **/
public class Demo {
    public static void main(String[] args) {
        Children children = new Children();
        int n = 5;
        children.setAge(n);
        System.out.println(children.getAge());
        n = 10;
        System.out.println(children.getAge()); //此处的值为5

    }

}
class Children {
    private String name;
    private int age;

    //setter方法
    public void setAge(int age){
        this.age = age;
    }
    //getter方法
    public int getAge(){
        this.getName();
        return this.age;
    }
    public void setName(String name){
        this.name = name;
    }
    private String getName(){
        return this.name;
    }
    //无参构造器
//    public Children(){
//
//    }
    //有参构造器(单个参数)
//    public Children(int age){
//        this.age = age;
//    }
//    //有参构造器(多个参数)
//    public Children(int age,String name){
//        this.age = age;
//        this.name = name;
//    }
    public void names(String ...name){
        for (int i = 0; i < name.length; i++) {
            System.out.println("输入的name为：" + name[i]);
        }
    }

}
```

#### 引用传递

##### 介绍

引用传递实际上就是地址的指向，在传值的时候引用传递是指向被引用的地址

##### 实例

```java
 public void setName(String[] name){
//        for (int i = 0; i < this.name.length; i++) {
//            this.name[i] = name[i];
//        }
        this.name = name;
    }
    String[] name = {"Tom","Baby","Amy","Hank","lll"};
    children.setName(name);
    for (String s : children.getName()) {
    System.out.println("姓名 = " + s);
    }
    System.out.println("======================");
    name[1] = "lzx"; children.setName(name);
    for (String s : children.getName()) {
    System.out.println("姓名 = " + s);  //两次的值不一样
    }
姓名 = Tom
姓名 = Baby
姓名 = Amy
姓名 = Hank
姓名 = lll
======================
姓名 = Tom
姓名 = lzx
姓名 = Amy
姓名 = Hank
姓名 = lll
```

### 可变参数

#### 介绍

Java方法中有个可变参数列表，实则可以作为数组使用，但和数组的区别在于这个参数不能传null，可以传空数组

#### 实例

```java
//通过数组的形式输入
String[] str = {"Tom","Baby","Amy","Hank","lll"};
children.names(str);
System.out.println("======================");
//通过参数的形式输入
children.names("李子雄","啦啦啦","咯西侧");
children.names(new String[10]);
public void names(String ...name){
for (int i = 0; i < name.length; i++) {
System.out.println("输入的name为：" + name[i]);
}
}
```

### 构造方法

#### 总结

1. 构造方法作用在于初始化实例对象
2. 构造方法可以有一个或者多个，按照传入的参数判断选择哪个
3. new实例对象若没有构造器的话会默认选择无参构造器
4. 构造器内部也可以调用其余构造器，采用this.构造器();

#### 修饰符的作用域

|                | public | protected | default | private |
| :------------- | :----: | :-------: | :-----: | :-----: |
| 同类           |   Y    |     Y     |    Y    |    Y    |
| 同包           |   Y    |     Y     |    Y    |    N    |
| 不同包子类     |   Y    |     Y     |    N    |    N    |
| 不同包的其他类 |   Y    |     N     |    N    |    N    |

## 四、抽象类

### 介绍

抽象类是基于多态的弊端而出现的，目的是为了简化父类的代码，以及子类对于父类代码的复用。

### 总结

1. 抽象类中可以有抽象方法，也可以有普通方法以及构造方法，构造方法的目的是为了供子类实例化的时候可以初始化父类的成员变量
2. 抽象类的命名方式为Abstract或者Beans开头
3. 抽象类中的抽象方法是不能private的，因抽象方法必须被重写
4. 抽象类不一定包含抽象方法，但有抽象方法的抽象类一定是抽象类

### 实例

```java
 Teacher teacher = new Teacher();
        teacher.run();abstract class Person {
    public abstract void run();
}

class Teacher extends Person {

    @Override
    public void run() {
        System.out.println("我在奔跑！！");
    }
}
```

## 五、接口

#### 介绍&&总结

接口是基于抽象类更加抽象，接口中不允许有其他方法，仅允许有default修饰的方法，抽象方法也不用abstract修饰，仅需要有方法返回类型以及方法名称即可

1. 接口用关键字interface来修饰，可以继承其他接口，但只能继承一个，否则会需要实现其中的一个接口中的抽象方法
2. 接口可以多实现

#### 与抽象类的对比

|            | abstract class     | interface             |
| ---------- | ------------------ | --------------------- |
| 继承       | 单继承             | 单继承，但可以多实现  |
| 字段       | 可以定义实例字段   | 不可以定义实例字段    |
| 抽象方法   | 可以定义抽象方法   | 可以定义抽象方法      |
| 非抽象方法 | 可以定义非抽象方法 | 只可以定义default方法 |

#### 实例

```java
package JavaDemo.newoop;

interface PersonDemo {
    String getName();
    default void run(){
        System.out.println(getName() + "在奔跑");
    }
}
interface StudentDemo extends PersonDemo {
    int getAge();
    default void age(){
        System.out.println("年龄为：" + getAge());
    }
}
package JavaDemo.newoop;

/**
 * @ClassName PersonDemoImpl
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/5 14:57
 * @Version 1.0
 **/
public class PersonDemoImpl implements PersonDemo,StudentDemo{
    private int age;
    private String name;

    public PersonDemoImpl(int age, String name) {
        this.age = age;
        this.name = name;
    }

    @Override
    public String getName() {
        return this.name;
    }

    @Override
    public int getAge() {
        return this.age;
    }

    public static void main(String[] args) {
        PersonDemoImpl lzx = new PersonDemoImpl(12, "lzx");
        lzx.run();
        lzx.age();
    }
}
```

## 六、内部类

### 成员内部类

#### 总结介绍

成员内部类联想到成员变量和成员方法，位置在和他们同一个位置，成员内部类在外部无法直接实例化这里指的是不能直接new 内部类这种形式进行实例化。

1. 访问内部类对象的方法有两种，第一种是采用外部类的对象创建内部类对象，第二种是采用外部类对象的获取内部类的方法。
2. 可以采用外部类.this.成员的方式来获取外部类同名的信息

#### 实例

```java
package JavaDemo.newoop;

/**
 * @ClassName InnerClass
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/5 15:54
 * @Version 1.0
 **/
public class InnerClass {
    public int age = 15;
    //访问内部类的成员方法,不能直接访问
    public InnerTest getInnerTest(){ //获取内部类对象的方法
        new InnerTest().id = 20;
        return new InnerTest();
    }
    public void  eat(){
        System.out.println("会吃东西！！");
    }
    //成员内部类 其访问修饰符可以任意
    public static class InnerTest{
    private int id; //内部类的属性值
    // 访问外部类的属性值的时候需要用到外部类.this.外部类属性值，注意，访问一般实在方法中，在成员变量的位置不可以直接访问
    public void heart(){
        System.out.println("我的心在跳动！");
//        InnerClass.this.eat();
    }
    }

    public static void main(String[] args) {
        //获取成员内部类对象实例
        //方法一 通过实例化外部类对象创建内部类对象 new 外部类().new 内部类; 外部类对象.new 内部类
//        long start = System.currentTimeMillis();
//        InnerTest innerTest = new InnerClass().new InnerTest();
//        innerTest.heart();
//        System.out.println(innerTest.id);
//        long end = System.currentTimeMillis();
//        System.out.println(end - start);
        System.out.println("=========================");
//        long start1 = System.currentTimeMillis();
//        InnerClass innerClass = new InnerClass();
//        InnerTest innerTest1 = innerClass.new InnerTest();
//        innerTest1.heart();
//        System.out.println(innerTest1.id);
//        long end1 = System.currentTimeMillis();
//        System.out.println(end1 - start1);
        InnerTest innerTest = new InnerTest();
        System.out.println("==========================");
        long start2 = System.currentTimeMillis();
        //方法二通过外部类的获取内部类的方法
        InnerClass innerClass1 = new InnerClass();
        InnerTest innerTest2 = innerClass1.getInnerTest();
        innerTest2.heart();
        System.out.println(innerTest2.id);
        long end2 = System.currentTimeMillis();
        System.out.println(end2 - start2);
    }
}
```

### 静态内部类

#### 总结介绍

静态内部类和成员内部类类似，就是加了个static，这样的话就不能采用new 外部类.new 内部类这种形式来获取了

### 方法内部类

#### 总结介绍

方法内部类主要是在方法内部定义的

#### 实例

```java
package JavaDemo.newoop;

/**
 * @ClassName Demo4
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/5 16:41
 * @Version 1.0
 **/
public class Demo4 {
    //方法内部类
    int id;
    String name = "大大";
    public static int age = 20;
    public Object getHeart(){
        class Heart{
            String name = "小小";
            //类成员可以使用访问修饰符，但不能使用static修饰
            public final int age = 11;
            public String beat(){
                new Demo4().eat();
                //访问同名的属性值的时候，优先访问内部类的属性值
                return  name + Demo4.age + "心脏在跳动";
            }
        }
        return new Heart().beat();
    }
    public void eat(){
        System.out.println("人会吃东西！");
    }

    public static void main(String[] args) {
        //测试成员内部类
        Demo4 demo4 = new Demo4();
        System.out.println(demo4.getHeart());
    }
}
```

### 匿名内部类

#### 总结介绍

主要用于继承、接口、抽象类重写方法

#### 实例

```java
abstract public class Demo5 {
    //阅读方法
    public abstract void read();
}
package JavaDemo.newoop;

/**
 * @ClassName Test1
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/5 16:58
 * @Version 1.0
 **/
public class Test1 {
    public void getRead(Demo5 demo5){
        demo5.read();
    }
    public static void main(String[] args) {
        Test1 test = new Test1();
        test.getRead(new Demo5() {
            @Override
            public void read() {
                System.out.println("男生喜欢看科幻类书籍");
            }
        });
        test.getRead(new Demo5() {
            @Override
            public void read() {
                System.out.println("女生喜欢读言情小说");
            }
        });
    }
}
```

## 七、泛型

### 简介

为了简化代码，没必要每次都需要重新定义，静态方法不能使用泛型

### 实例

```java
package JavaDemo.newoop;
import JavaDemo.newoop.day02.Person;

import java.lang.reflect.Array;
import java.util.ArrayList;
import java.util.Arrays;

/**
 * @ClassName Demo6
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/6 8:01
 * @Version 1.0
 **/
public class Demo6 {
    public static void main(String[] args) {
        //初始化数组
//        ArrayList<String> list = new ArrayList<String>();
//        list.add("hello");
//        list.add("world");
//        String first = list.get(0);
//        String second = list.get(1);
//        System.out.println(first + "," + second);
          Person[] persons = new Person[]{
                  new Person(21,"Tom"),
                  new Person(22,"Amy"),
                  new Person(18,"Hank")
          };
        System.out.println(Array.get(persons, 0));
        Arrays.sort(persons);
        for (Person person : persons) {
            System.out.println(person);
        }
//        System.out.println(Arrays.toString(persons));
    }
}
package JavaDemo.newoop.day02;

public class Person implements Comparable<Person>{
    private int score;
    private String name;
    //有参构造器
    public Person(int score,String name) {
        this.score = score;
        this.name = name;
    }
    @Override
    public String toString() {
        return  this.score + "," + this.name;
    }
    @Override
    public int compareTo(Person o) {
        return this.name.compareTo(o.name);
    }
}
```

## 八、反射

```java
package JavaDemo.newoop.day02;

import com.mysql.cj.log.LogFactory;

import java.lang.reflect.Field;

/**
 * @ClassName Reflection
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/6 10:02
 * @Version 1.0
 **/
public class Reflection {
    public static void main(String[] args) throws NoSuchFieldException, IllegalAccessException {
//        printClassInfo("".getClass());
//        printClassInfo(Runnable.class);
//        printClassInfo(java.time.Month.class);
//        printClassInfo(String[].class);
//        printClassInfo(int.class);
//        LogFactory factory = null;
//        if (isClassPresent("org.apache.logging.log4j.Logger")){
//            factory = createLog4j();
//        }else {
//            factory = createJdkLog();
//        }
//        Class<Stu> stuClass = Stu.class;
//        //获取public的字段
//        System.out.println(stuClass.getField("score"));
//        //获取继承的public的字段
//        System.out.println(stuClass.getField("name"));
//        //获取“private”字段“grade”
//        System.out.println(stuClass.getDeclaredField("grade"));
        PersonTest personTest = new PersonTest("xiMing");
        System.out.println(personTest.getName());
        Class aClass = personTest.getClass();
        Field name = aClass.getDeclaredField("name");
        name.setAccessible(true);
        name.set(personTest,"李子雄");
        System.out.println(personTest.getName());
    }
//    static void printClassInfo(Class cls) {
//        System.out.println("Class name = " + cls.getName());
//        System.out.println("Simple name = " + cls.getSimpleName());
//        if (cls.getPackage() != null){
//            System.out.println("Package name = " + cls.getPackage().getName());
//        }
//        System.out.println("is interface = " + cls.isInterface());
//        System.out.println("is enum = " + cls.isEnum());
//        System.out.println("is array = " + cls.isArray());
//        System.out.println("is primitive = " + cls.isPrimitive());
//    }
static boolean isClassPresent(String name) {
        try {
            Class.forName(name);
            return true;
        } catch (ClassNotFoundException e) {
            return false;
        }
    }
}
class PersonTest {
    public String name;

    public PersonTest(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
class Stu extends PersonTest {
    public int score;
    private int grade;

    public Stu(String name) {
        super(name);
    }
}
package JavaDemo.newoop.day02;

import java.lang.reflect.*;

/**
 * @ClassName Reflection1
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/6 10:45:02
 * @Version 1.0
 **/
public class Reflection1 {
    public static void main(String[] args) throws Exception{
//        Constructor<Integer> cons1 = Integer.class.getConstructor(int.class);
//        //调用构造方法
//        Integer n1 = (Integer)cons1.newInstance(123);
//        System.out.println(n1);
//        //获取构造方法Integer(String)
//        Constructor<Integer> cons2 = Integer.class.getConstructor(String.class);
//        //调用构造方法
//        Integer n2 = (Integer)cons2.newInstance("456");
//        System.out.println(n2);
        InvocationHandler handler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                System.out.println(method);
                if (method.getName().equals("morning")) {
                    System.out.println("Good morning " + args[0]);
                }
                return null;
            }
        };
        Hello hello = (Hello) Proxy.newProxyInstance(
                Hello.class.getClassLoader(),//传入ClassLoad()
                new Class[] {Hello.class },//传入要实现的接口
                handler);//传入处理调用方法的InvocationHandler
        hello.morning("Bob");

    }
}
interface Hello {
    void morning(String name);
}
```



## 九、注释(Annotation)

#### 解释：用于工具处理的标注

### 1、编译器使用的注释

#### 介绍

此类注解就是告诉编译器该执行那些操作，不会编译进入.class文件，编译后就被被编译器给扔掉了

例如：@Override：让编译器检查是否进行了方法的重写

@SuppressWarnings：告诉编译器忽略此行代码产生的警告

### 2、编译后的.class文件使用的注释

#### 介绍

此类注解一般是对.class文件所加载，对class文件做动态修改，但编译完成以后不会进入内存中，这类注解只会被一些底层库所使用。

### 3、程序运行时使用的注释

#### 介绍

此类注解会一直存在与JVM中，这也是最常用的注解

### 自定义注解

步骤：

1. 创建注解类型即：public @interface 注解名 {}
2. 在注解体内定义字段以及默认值
3. 使用元注解即@Target和@Retention一个是注解Annotation的适用范围，另外一个是该何时读取该注解

```java
package JavaDemo.newoop.day02;

import java.lang.annotation.*;

@Target(ElementType.METHOD)
//@Repeatable(Reports.class)
@Retention(RetentionPolicy.RUNTIME)
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

