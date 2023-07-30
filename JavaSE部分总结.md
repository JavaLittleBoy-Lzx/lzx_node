# Java SE部分总结

## 一、异常

### 介绍总结

异常指的是在程序运行过程时发生的错误，Java一般采用try{}多个catch{}finally{}来捕获异常

### 代码案例

```java
package JavaDemo.newoop.exception;

import java.util.logging.Logger;

/**
 * @ClassName Logging
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/6 14:21:38
 * @Version 1.0
 **/
public class Logging {
    public static void main(String[] args) {
//        Logger logger = Logger.getGlobal();
//        logger.info("start process...");
//        logger.warning("memory is running out...");
//        logger.fine("ignored");
//        logger.severe("process will be terminated...");
}
package JavaDemo.newoop.exception;

import java.util.Scanner;

/**
 * @ClassName Demo
 * @Description TODO
 * @Author 李子雄
 * @Date 2023/7/6 13:35:54
 * @Version 1.0
 **/
public class Demo {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        try {
            System.out.print("请输入：");
            int n = input.nextInt();
            if (n < 0){
                throw new IllegalArgumentException("n不能为负数");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 二、集合



## 三、IO

## 四、常用类之日期与时间

## 五、单元测试

## 六、正则表达式

## 七、加密与安全

## 八、多线程

## 九、Maven基础

