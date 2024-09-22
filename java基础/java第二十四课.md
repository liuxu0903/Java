# super 关键字

## 基本介绍

super 代表父类的引用，用于访问父类的属性、方法、构造器。

## 基本语法

1. 访问父类的属性，但不能访问父类的 private 属性。
   `super.属性名;`

2. 访问父类的方法，不能访问父类的 private 方法。

    `super.方法名(参数列表);`

3. 访问父类的构造器：

   `super(参数列表);` 只能放在构造器的第一句，只能出现一句！

## super 给编程带来的便利/细节

1. 调用父类的构造器的好处 (分工明确，父类属性由父类初始化，子类的属性由子类初始化)

2. 当子类中有和父类中的成员（属性和方法）重名时，为了访问父类的成员，必须通过 super。如果没有重名使用 super、this、直接访问是一样的效果！

3. super 的访问不限于直接父类，如果爷爷类和本类中有同名的成员，也可以使用 super 去访问爷爷类的成员；如果多个基类（上级类）中都有同名的成员，使用 super 访问遵循就近原则。Base->A->B 。

   **例子：**

   **Super01.java：**

   ```java
   package com.hspedu.super_;
   
   public class Super01 {
       public static void main(String[] args) {
           B b = new B();
           //b.sum();
           b.test();
       }
   }
   ```

   **Base.java：**

   ```java
   package com.hspedu.super_;
   
   public class Base {
       public int n1 = 1000;
       public void cal(){
           System.out.println("Base类的cal()方法...");
       }
       public void eat(){
           System.out.println("Base类的eat()方法...");
       }
   
   }
   ```

   **A.java：**

   ```java
   package com.hspedu.super_;
   
   public class A extends Base{
           //public int n1 = 100;
           protected int n2 =200;
           int n3 = 300;
           private int n4= 400;
           public A(){
   
           }
           public A(String name){
   
           }
           public A(String name, int age){
   
           }
   //        public void cal(){
   //            System.out.println("A类的cal()方法...");
   //        }
           public void test100(){};
           protected void test200(){};
           void test300(){};
           private void test400(){};
   
   }
   ```

   **B.java：**

   ```java
   package com.hspedu.super_;
   
   public class B extends A {
       public int n1 = 888;
       public void hi(){
           System.out.println(super.n1 + " " + super.n2 + " "
                               + super.n3 ); //访问父类的属性，但不能访问父类的 private 属性
       }
       public void test(){//super遵循就近原则去父类查找
           System.out.println("super.n1 = " + super.n1);
           super.cal();
       }
   
       public void cal(){
           System.out.println("B类的cal()方法...");
       }
       public void sum(){
           System.out.println("B类的sum()方法...");
           //调用父类A的cal方法，有三种方法：
           cal();//第一种
           this.cal();//第二种
           //第一二种方法，找cal方法时，顺序是，
           //1.先找本类，如果有，并且可以调用，则调用，
           //2.如果没有，则找父类（如果有，并可以调用，则调用）
           //3.如果父类没有，则继续找父类的父类，直到Object类
           //提示：如果查找方法的过程中，找到了，但是不能访问（private），则报错
           //如果没有找到，则提示方法不存在
           super.cal();//第三种找cal方法顺序是直接查找父类，其他的规则一样
           //调用父类A的n1属性，有三种方法，规则同上：
           System.out.println(n1);
           System.out.println(this.n1);
           System.out.println(super.n1);
       }
       public void ok(){
           super.test100();
           super.test200();
           super.test300();
           //super.test400();//访问父类的方法，不能访问父类的 private 方法。
       }
       public B(){
           //super();
           //super("Jack");
           super("Jack", 18);
       }
   
   }
   ```

   ## super 和 this 的比较

   <img src="D:\消息记录\TyporaPages\super和this的比较-1718444068084-2.png" style="zoom:33%;" />

# 方法重写/覆盖（override）

## 基本介绍

简单的说：方法覆盖(重写)就是子类有一个方法，和父类的某个方法的名称、返回类型、参数一样，那么我们就说子类的这个方法覆盖了父类的那个方法。

**例子：**

**Override01.java：**

```java
package com.hspedu.override_;

public class Override01 {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.cry();
    }
}
```

**Animal.java：**

```java
package com.hspedu.override_;

public class Animal {
    public void cry(){
        System.out.println("动物叫唤...");
    }

}
```

**Dog.java：**

```java
package com.hspedu.override_;

public class Dog extends Animal{
    //1.因为 Dog 是 Animal 子类
    //2.Dog 的 cry方法和 Animal 的 cry定义形式一样(名称、返回类型、参数)
    //3.这时我们就说 Dog 的 cry 方法，重写了 Animal 的 cry 方法
    public void cry(){
        System.out.println("小狗汪汪叫...");
    }
}
```

## 注意事项和使用细节

1. 子类方法的==形参列表，方法名称==，要和父类方法的==形参列表，方法名称==完全一样。

2. 子类方法的**返回类型和父类方法的返回类型一样，或者是父类返回类型的子类。**

   比如：父类返回类型是 Object，子类方法返回类型是 String，也可以。
   `public object getInfo(){}`

   `public string getInfo(){}`

3. 子类方法==不能缩小==父类方法的访问权限，可以**扩大权限**。
   `void sayok(){}`
   `public void sayok(){}`这里是可以的。

## 方法的重写和重载比较

<img src="D:\消息记录\TyporaPages\重载与重写的区别.png" style="zoom:33%;" />

## 练习题

第一题：

- 编写一个 Person 类，包括属性/private(name、age)，构造器、方法 say(返回自我介绍的字符串)。
- 编写一个 Student 类，继承 Person 类，增加 id、score 属性 /private，以及构造器，定义 say 方法(返回自我介绍的信息)。
- 在 main 中,分别创建 Person和 Student 对象，调用 say 方法输出自我介绍

**OverrideExercise.java：**

```java
package com.hspedu.override_.Exercise;

public class OverrideExercise {
    public static void main(String[] args) {
        Person person = new Person("Jack", 18);
        Student student = new Student("Tom",18, "123456",120);
        System.out.println(person.Say());
        System.out.println(student.Say());
    }
}
```

**Person.java：**

```java
package com.hspedu.override_.Exercise;

public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String Say(){
        return ("我的名字是：" + name + " 我的年龄是：" + age);
    }
}
```

**Student.java：**

```java
package com.hspedu.override_.Exercise;

public class Student extends Person{
    private String id;
    private int score;

    public Student(String name, int age, String id, int score) {
        super(name, age);
        this.id = id;
        this.score = score;
    }
    public String Say(){
        return (super.Say() + " id 是：" + id + " 成绩是：" + score);
    }
}
```

