# IDEA 快捷键

1. 删除行：Ctrl + Y
2. 复制行：Ctrl + D
3. 补全代码：Alt + /
4. 添加取消注释：Ctrl + /
5. 导入该行需要的类：Alt + Enter
6. 快速格式化代码：Ctrl + Shift + L
7. 快速运行程序：Ctrl + Shift + F10
8. 生成构造器：Alt + Insert
9. 查看一个类的层级关系：Ctrl + H
10. 自动分配变量名：在后面.var

# IDEA 模板 / 自定义模板

![](D:\消息记录\TyporaPages\模板.png)

# 包

## 包的三大作用

1. 区分相同名字的类
2. 当类很多时，可以很好的管理类 [看Java API 文档]
3. 控制访问范围

## 包的基本语法

`package com.hspedu;`

### 说明：

1. package 关键字，表示打包。
2. com.hspedu; 表示包名。

## 包的本质

实际上就是创建不同的==文件夹 / 目录==来保存类文件，示意图如下：

<img src="D:\消息记录\TyporaPages\包的本质.png" style="zoom:33%;" />

## 包的命名

### 命名规则

只能包含数字、字母、下划线、小圆点，但不能用数字开头，不能是关键字或保留字。

如：

```java
demo.class.exec1 //错误，包含关键字
demo.12a  //错误，数字开头
demo.ab12.oa  //正确
```

### 命名规范

一般是小写字母 + 小圆点一般是 com.公司名.项目名.业务模块名

比如：

```java
com.hspedu.oa.model;
com.hspedu.oa.controller;
举例:
com.sina.crm.user //用户模块
com.sina.crm.order //订单模块
com.sina.crm.utils //工具类
```

## 常用的包

```java
java.lang.*  //lang包是基本包，默认引入，不需要再引入
java.util.*  //util包，系统提供的工具包，工具类，使用 Scanner
java.net.*   //网络包，网络开发
java.awt.*   //是做java的界面开发，GUI
```

## 如何引入包

`语法: import 包;`

我们引入一个包的主要目的是要使用该包下的类。

比如：

1. `import java.util.Scanner;` // 就只是引入一个类 Scanner。

2. `import java.util.*;` // 表示将 java.util 包所有都引入。我们需要使用到哪个类，就导入哪个类即可，不建议使用 * 导入

## 包的注意事项和细节

1. package 的作用是声明当前类所在的包，需要放在类的最上面，一个类中最多只有一个 package。
2. xxxxxxxxxx import java.util.Scanner;public class Chapter7{    public static void main(String[] args){        Tom m = new Tom();        m.menu();    }}class Tom{    public int Guess(){        return (int) (Math.random() * 3); // 生成范围在 0 到 2 之间的随机整数    }    public void menu(){        int n = 0;        Scanner myScanner = new Scanner(System.in);        System.out.println("*******现在进行石头剪刀步游戏：（三局两胜）********");        for(int i = 0; i < 3; i++){            System.out.println("请输入石头/剪刀/步，注意：0 表示石头，1 表示剪刀，2 表示布");            int num1 = myScanner.nextInt();            int p = Guess();            if(p == 0 && num1 == 2 || p == 1 && num1 == 0 || p == 2 && num1 == 1){                n++;            }            System.out.println("机器出的是：" + p + "\t您出的是：" + num1);        }​        System.out.println("三次猜拳，您赢了" + n + "次！");        if(n >= 2){            System.out.println("游戏获胜啦！！！");        }        else{            System.out.println("游戏失败。。。");        }    }   }​java

## 类定义的进一步完善

<img src="D:\消息记录\TyporaPages\完善类的定义.png" style="zoom:33%;" />

# 访问修饰符

## 基本介绍

java 提供四种访问控制修饰符号，用于控制方法和属性（成员变量）的访问权限（范围）：

1. 公开级别：用 public 修饰，对外公开
2. 受保护级别：用 protected 修饰，对子类和同一个包中的类公开
3. 默认级别：没有修饰符号，向同一个包的类公开
4. 私有级别：用 private 修饰，只有类本身可以访问，不对外公开

4 种访问修饰符的访问范围：

<img src="D:\消息记录\TyporaPages\访问修饰符的访问范围.png" style="zoom:33%;" />

### 使用的注意事项

1. 修饰符可以用来修饰类中的**属性，成员方法以及类**。
2. 只有**默认**的和 **public** 才能修饰**类**！并且遵循上述访问权限的特点。
3. **成员方法**的访问规则和属性完全一样。

例子：

<img src="D:\消息记录\TyporaPages\修饰符例子.png" style="zoom:33%;" />

在 modifier 包下：

1. A 类

```java
package com.hspedu.modifier;

public class A {
    //四个属性，分别使用不同的访问修饰符来修饰
    public int n1 = 100;
    protected int n2 = 200;
    int n3 = 300;
    private int n4 = 400;
    //在同一个类中，可以访问 public protected 默认 private 修饰的属性和方法
    public void m1(){
        System.out.println("n1 = " + n1 + " n2 = " + n2 + " n3 = " + n3 + " n4 = " + n4);//属性，都可以访问
    }
    protected void m2(){}
    void m3(){}
    private void m4(){}

    public void hi(){
        m1();
        m2();
        m3();
        m4();//成员方法,都可以访问
    }
}
```

2. B 类

```java
package com.hspedu.modifier;

public class B {
    public void say(){
        A a = new A();
        //在同一个包下，可以访问 public，protected 和 默认修饰的属性或方法，不能访问 private 属性或方法。
        System.out.println("n1 = " + a.n1 + " n2 = " + a.n2 + " n3 = " + a.n3);//属性,不能访问 a.n4
        a.m1();
        a.m2();
        a.m3();//成员方法，不能访问 a.m4()
    }
}
```

3. Test 类

```java
package com.hspedu.modifier;

public class Test {
    public static void main(String[] args) {
        A a = new A();
        a.m1();
        B b = new B();
        b.say();
    }
}
// 只有默认的和 public 才能修饰类
class Tiger{

}
```

在 pkg 包下：

1. Test 类

```java
package com.hspedu.pkg;

import com.hspedu.modifier.A;

public class Test {
    public static void main(String[] args) {
        A a = new A();
        //在不同包下，可以访问 public 修饰的属性或方法
        //但是不能访问呢 protected ,默认， private 修饰的属性或方法
        System.out.println("n1 = " + a.n1);//属性，不能访问 a.n2, a.n3, a.n4
        a.m1();//成员方法,不能访问 a.m2(), a.m3(), a.m4()。
    }
}
```

