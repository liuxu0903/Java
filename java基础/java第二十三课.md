# 面向对象的三大特征

## 继承

继承可以解决代码复用，让我们的编程更加靠近人类思维，当多个类存在相同的属性（变量）和方法时，可以从这些类中抽象出父类，在父类中定义这些相同的属性和方法，所有的子类不需要重新定义这些属性和方法，只需要通过 extends 来声明继承父类即可。

### 继承的示意图

<img src="D:\消息记录\TyporaPages\继承示意图.png" style="zoom:33%;" />

### 继承的基本语法

```java
class 子类 extends 父类{
    
}
```

1. 子类就会自动拥有父类定义的属性和方法
2. 父类又叫超类，基类。
3. 子类又叫派生类。

以 Extends01.java 为例，我们编写了两个类，一个是Pupil 类(小学生)，一个是Graduate(研究生)。体会使用继承的好处。

***使用继承前：***

**Extends01.java**：

```java
package com.hspedu.extend_;

public class Extends01 {
    public static void main(String[] args) {
        Pupil pupil = new Pupil();
        pupil.name = "小明";
        pupil.age = 10;
        pupil.setScore(95);
        pupil.testing();
        pupil.show();

        Graduate graduate = new Graduate();
        graduate.name = "李明";
        graduate.age = 18;
        graduate.setScore(135);
        graduate.testing();
        graduate.show();
    }
}
```

**Graduate.java：**

```java
package com.hspedu.extend_;

public class Graduate {
    public String name;
    public int age;
    private double score;

    public void setScore(double score) {
        this.score = score;
    }
    public void testing(){
        System.out.println("大学生 " + name + " 正在考大学数学...");
    }
    public void show(){
        System.out.println("姓名：" + name + " 年龄：" + age + " 分数：" + score );
    }
}
```

**Pupil.java：**

```java
package com.hspedu.extend_;

public class Pupil {
    public String name;
    public int age;
    private double score;

    public void setScore(double score) {
        this.score = score;
    }
    public void testing(){
        System.out.println("小学生 " + name + " 正在考小学数学...");
    }
    public void show(){
        System.out.println("姓名：" + name + " 年龄：" + age + " 分数：" + score );
    }
}
```

***使用继承后：***

**TestExtends.java**：

```java
package com.hspedu.extend_.improve_;

import com.hspedu.extend_.Graduate;
import com.hspedu.extend_.Pupil;

public class TestExtends {
    public static void main(String[] args) {
        com.hspedu.extend_.Pupil pupil = new Pupil();
        pupil.name = "小明";
        pupil.age = 10;
        pupil.setScore(95);
        pupil.testing();
        pupil.show();

        com.hspedu.extend_.Graduate graduate = new Graduate();
        graduate.name = "李明";
        graduate.age = 18;
        graduate.setScore(135);
        graduate.testing();
        graduate.show();
    }
}
```

**Student.java：**

```java
package com.hspedu.extend_.improve_;

public class Student {
    public String name;
    public int age;
    private double score;

    public void setScore(double score) {
        this.score = score;
    }
    public void show(){
        System.out.println("姓名：" + name + " 年龄：" + age + " 分数：" + score );
    }
}
```

**Graduate.java：**

```java
package com.hspedu.extend_.improve_;

public class Graduate extends Student{
    public void testing(){
        System.out.println("大学生 " + name + " 正在考大学数学...");
    }
}
```

**Pupil.java：**

```java
package com.hspedu.extend_.improve_;

public class Pupil extends Student{
    public void testing(){
        System.out.println("小学生 " + name + " 正在考小学数学...");
    }
}
```

### 继承给编程带来的便利

1. 代码的复用性提高了
2. 代码的扩展性和维护性提高了

### 继承的细节问题

1. 子类继承了所有的属性和方法，非私有的属性和方法可以在子类直接访问，但是私有属性和方法不能在子类**直接**访问（可以用公共的属性或者公共的方法访问），要通过==父类提供公共的方法==去访问。

   例子：

   **ExtendsDetail.java：**

   ```java
   package com.hspedu.extend_;
   
   public class ExtendsDetail {
       public static void main(String[] args) {
           Sub sub = new Sub();
           sub.sayOk();
   
       }
   }
   ```

   **Base.java：**

   ```java
   package com.hspedu.extend_;
   
   public class Base {//父类
       //4个属性
       public int n1 = 100;
       protected int n2 =200;
       int n3 = 300;
       private int n4 = 400;
       public Base(){//无参构造器
           System.out.println("base()....");
       }
       public void test100(){
           System.out.println("test100");
       }
       protected void test200(){
           System.out.println("test200");
       }
       void test300(){
           System.out.println("test300");
       }
       private void test400(){
           System.out.println("test400");
       }
       public int getn4(){
           return n4;
       }
       public void callTest400(){
           test400();
       }
   }
   ```

   **Sub.java：**

   ```java
   package com.hspedu.extend_;
   
   public class Sub extends Base{//子类
       public Sub(){//构造器
           System.out.println("sub()......");
       }
       public void sayOk(){//子类方法
          //我们发现 父类的非private属性和方法都可以访问
           System.out.println(n1);
           System.out.println(n2);
           System.out.println(n3);
           test100();
           test200();
           test300();
         //通过父类提供公共的方法去访问
           System.out.println("n4= " + getn4());
           callTest400();
       }
   }
   ```

2. 子类必须调用父类的构造器，完成父类的初始化。

3. 当创建子类对象时，不管使用子类的哪个构造器，默认情况下总会去调用父类的无参构造器，如果父类没有提供无参构造器，则必须在子类的构造器中用 super 去指定使用父类的哪个构造器完成对父类的初始化工作，否则，编译不会通过。

4. 如果希望指定去调用父类的某个构造器，则显式的调用一下：`super(参数列表)`。

5. super 在使用时，需要放在构造器第一行（super 只能在构造器中使用）。

6. super() 和 this() 都只能放在构造器第一行，因此这两个方法不能共存在一个构造器。

7. java 所有类都是 Object 类的子类，Object 是所有类的基类。

   使用 Ctrl + H 可以看到类的继承关系。

   <img src="D:\消息记录\TyporaPages\继承关系.png" style="zoom:33%;" />

8. 父类构造器的调用不限于直接父类！将一直往上追溯直到 Object 类(顶级父类)。

9. 子类最多只能继承一个父类(指直接继承)，即 java 中是**单继承机制**。

   如何让 A 类继承 B 类和 C 类？===>  A 继承 B， B 继承 C。

10. 不能滥用继承，子类和父类之间必须满足 is-a 的逻辑关系。

### 继承的本质分析

例子：

**ExtendsTheory.java：**

```java
package com.hspedu.extend_;

/**
 * 讲解继承的本质
 */

public class ExtendsTheory {
    public static void main(String[] args) {
        Son son = new Son(); //内存的布局是？
        //注意，要按照查找关系来返回信息
        //（1）首先看子类是否有该属性
        //（2）如果子类有这个属性，并且可以访问，则返回信息。
        //（3）如果子类没有这个属性，就看父类有没有这个属性（如果父类有该属性，并且可以访问，就返回信息。）
        //（4）如果父类没有就按照(3)的规则，继续找上级父类，直到0bject。
        System.out.println(son.name);
        System.out.println(son.age);
        System.out.println(son.hobby);
    }
}
class GrandPa { //爷类
    String name = "大头爷爷";
    String hobby = "旅游";
}
class Father extends GrandPa { //父类
    String name = "大头爸爸";
    int age = 39;
}
class Son extends Father { //子类
    String name = "大头儿子";
}
```

**内存布局：**

<img src="D:\消息记录\TyporaPages\继承内存示意图.png" style="zoom:33%;" />

## 练习题

第一题：main 中：B b = new B(); 会输出什么?

<img src="D:\消息记录\TyporaPages\继承第一题.png" style="zoom:33%;" />

```java
//结果：
a 
b name
b
```

第二题：main 中：C c = new C(); 会输出什么?

<img src="D:\消息记录\TyporaPages\继承第二题.png" style="zoom:33%;" />

```java
//结果：
我是A类
hahah我是B类的有参构造
我是c类的有参构造
我是c类的无参构造
```

第三题：ExtendsExercise03.java

- 编写 Computer 类，包含CPU、内存、硬盘等属性，getDetails 方法用于返回 computer 的详细信息

- 编写 PC 子类，继承 Computer 类，添加特有属性【品牌brand】

- 编写 NotePad 子类，继承 Computer 类，添加特有属性【color】

- ExtendsExercise03 类，在 main 方法中创建 PC 和 NotePad 对象，分别给对象中特有的属性赋值，以及从 Computer 类继承的属性赋值，并使用方法并打印输出信息。

**ExtendsExercise03.java：**

```java
package com.hspedu.extend_.Exercise;

public class ExtendsExercise03 {
    public static void main(String[] args) {
        PC pc = new PC("Intel",16 ,512, "联想");
        NotePad notePad = new NotePad("Intel", 32, 1024, "灰色");
        pc.printInfo();
        notePad.printNotePad();
    }
}
```

**Computer.java：**

```java
package com.hspedu.extend_.Exercise;

public class Computer {
    private String cpu;
    private int memory;
    private int disk;

    public Computer(String cpu, int memory, int disk) {
        this.cpu = cpu;
        this.memory = memory;
        this.disk = disk;
    }

    public String getDetail(){
        return ("cpu = " + cpu +
                " memory = " + memory + " disk = " + disk);
    }
    public String getCpu() {
        return cpu;
    }

    public void setCpu(String cpu) {
        this.cpu = cpu;
    }

    public int getMemory() {
        return memory;
    }

    public void setMemory(int memory) {
        this.memory = memory;
    }

    public int getDisk() {
        return disk;
    }

    public void setDisk(int disk) {
        this.disk = disk;
    }
}
```

**PC.java：**

```java
package com.hspedu.extend_.Exercise;

public class PC extends Computer{
   private String brand;

    public PC(String cpu, int memory, int disk, String brand) {
        super(cpu, memory, disk);
        this.brand = brand;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }
    public void printInfo(){
        System.out.println("PC 信息如下：");
        System.out.println(getDetail() + " Brand = " + brand);
    }
}
```

**NotePad.java：**

```java
package com.hspedu.extend_.Exercise;

public class NotePad extends Computer{
    private String color;
    public NotePad(String cpu, int memory, int disk, String color) {
        super(cpu, memory, disk);
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }
    public void printNotePad(){
        System.out.println("NotePad 信息如下：");
        System.out.println(getDetail() + " Color = " + color);
    }
}
```

