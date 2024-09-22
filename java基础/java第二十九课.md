# 断点调试（debug）

## 实际需求

1. 在开发中，新手程序员在查找错误时，这时老程序员就会温馨提示，可以用断点调试步一步的看源码执行的过程，**从而发现错误所在**。

2. 重要提示：在断点调试过程中，是运行状态，是以==对象的运行类型来执行的==。

## 断点调试介绍

1. 断点调试是指在程序的某一行设置一个断点，调试时，程序运行到这行就会停住，出错的话，调然后你可以一步一步往下调试，调试过程中可以看各个变量当前的值，试到出错的代码行即显示错误，停下。进行分析从而找到这个 Bug。
2. 断点调试是程序员必须掌握的技能。断点调试也能帮助我们查看 Java 底层源代码的执行过程，提高程序员的 Java 水平。

## 断点调试的快捷键

F7(跳入)：跳入**方法内**

F8(跳过)：**逐行**执行代码

shift+F8(跳出)：跳出**方法**

F9(resume，执行到下一个断点)

<img src="D:\消息记录\TyporaPages\断点调试.png" style="zoom:33%;" />

# 零钱通项目

## 项目需求说明

使用 Java 开发零钱通项目，可以完成收益入账，消费，查看明细，退出系统等功能。

## 项目的界面

<img src="D:\消息记录\TyporaPages\项目界面.png" style="zoom:33%;" />

**SmallChangeSysApp.java：**

```java
package com.hspedu.smallchange.oop;

/**
 * 这里直接调用 SmallChangeSysOOP 对象，显示主菜单即可
 */

public class SmallChangeSysApp {
    public static void main(String[] args) {
        new SmallChangeSysOOP().mainMenu();
    }
}
```

**SmallChangeSysOOP.java：**

```java
package com.hspedu.smallchange.oop;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

/**
 * 该类是完成零钱通的各个功能的类
 * 使用OOP（面向对象编程）
 * 将各个功能对应一个方法
 *
 */

public class SmallChangeSysOOP {

    //属性
    boolean loop = true;
    Scanner scanner = new Scanner(System.in);
    String key = "";
    String details = "--------------------零钱通明细-------------------";
    double money = 0;
    double balance = 0;
    Date date = null;
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm");// 用于时间格式化
    String note = "";

    //显示菜单
    public void mainMenu(){
        do{
            System.out.println("\n====================零钱通选择菜单(OOP)===================");
            System.out.println("\t\t\t1 零钱通明细");
            System.out.println("\t\t\t2 收益入账");
            System.out.println("\t\t\t3 消费");
            System.out.println("\t\t\t4 退    出");
            System.out.println("请选择（1-4）：");
            key = scanner.next();
            switch (key){
                case "1":
                    this.detail();
                    break;
                case "2":
                    this.income();
                    break;
                case "3":
                    this.pay();
                    break;
                case "4":
                    this.exit();
                    break;
                default:
                    System.out.println("选择有误，请重新选择");
            }
        }while (loop);
    }

    //显示零钱通明细
    public void detail(){
        System.out.println(details);
    }
    //完成收益入账
    public void income(){
        System.out.println("收益入账金额：");
        money = scanner.nextDouble();
        //校验money的值
        if(money <= 0){
            System.out.println("收益入账金额需要大于 0 ");
            return;//退出方法，不再执行
        }
        balance += money;
        //拼接收益入账信息到 details
        date = new Date();//获取当前日期
        details += "\n收益入账\t+" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
    }
    //消费
    public void pay(){
        System.out.println("消费金额：");
        money = scanner.nextDouble();
        //校验money的值
        if(money <= 0 || money > balance){
            System.out.println("你的消费金额需要在 0 - " + balance + " 之间");
            return;
        }
        System.out.println("消费说明：");
        note = scanner.next();
        balance -= money;
        details += "\n" + note +"\t-" + money + "\t" + sdf.format(date) + "\t" + "余额：" + balance;
    }
    //退出
    public void exit(){
        System.out.println("4 退出");
        String choice = "";
        while (true){
            System.out.println("你确定要退出吗？y/n");
            choice = scanner.next();
            if("y".equals(choice) || "n".equals(choice)){
                break;
            }
        }
        if(choice.equals("y")){
            loop = false;
        }
    }
}
```

