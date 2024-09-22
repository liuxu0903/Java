# 多态的应用

## 多态参数

方法定义的形参类型为父类类型，实参类型允许为子类类型。

应用实例1：[前面的主人喂动物例子](https://blog.csdn.net/Lauxuxu/article/details/139757669)

应用实例2：定义员工类 Employee，包含姓名和月工资 [private] ，以及计算年工资 getAnnual 的方法。普通员工和经理继承了员工，经理类多了奖金 bonus 属性和管理 manage 方法，普通员工类多了 work 方法，普通员工和经理类要求分别重写 getAnnual 方法。

1. 测试类中添加一个方法，showEmpAnnual(Employee e)，实现获取任何员工对象的年工资，并在 main 方法中调用该方法[e.getAnnual()]。
2. 测试类中添加一个方法，testWork，如果是普通员工，则调用 work 方法，如果是经理，则调用 manage 方法

**PolyParameter.java：**

```java
package com.hspedu.poly_.polyparameter_;

public class PolyParameter {
    public static void main(String[] args) {
        Worker tom = new Worker("Tom", 3000);
        Manager john = new Manager("John", 30000, 100000);
        PolyParameter polyParameter = new PolyParameter();
        polyParameter.showEmpAnnual(tom);
        polyParameter.showEmpAnnual(john);
        polyParameter.testWork(tom);
        polyParameter.testWork(john);
    }
    public void showEmpAnnual(Employee employee){
        System.out.println(employee.getName() + " 的年工资为： " + employee.getAnnual());
    }
    public void testWork(Employee employee){
        if(employee instanceof Worker){
            ((Worker) employee).work();//向下转型
        }else if(employee instanceof Manager){
            ((Manager) employee).manage();//向下转型
        }else {
            System.out.println("输入有误...");
        }
    }
}
```

**Employee.java：**

```java
package com.hspedu.poly_.polyparameter_;

public class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
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
    public double getAnnual(){
        return 12 * salary;
    }
}
```

**Manager.java：**

```java
package com.hspedu.poly_.polyparameter_;

public class Manager extends Employee {
    private double bonus;

    public Manager(String name, double salary, double bonus) {
        super(name, salary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    public void manage(){
        System.out.println("经理 " + getName() + " 正在工作...");
    }

    @Override
    public double getAnnual() {
        return super.getAnnual() + bonus;
    }
}
```

**Worker.java：**

```java
package com.hspedu.poly_.polyparameter_;

public class Worker extends Employee {
    public Worker(String name, double salary) {
        super(name, salary);
    }
    public void work(){
        System.out.println("普通员工 " + getName() + " 正在工作...");
    }

    @Override
    public double getAnnual() {//因为普通员工没有其他收入，直接调用父类方法
        return super.getAnnual();
    }
}
```

# Object 类详解

## equals 方法

### == 和 equals 的对比（面试题）

***== 是一个比较运算符。***

1. 既可以判断基本类型，又可以判断引用类型。

2. 如果判断基本类型，判断的是值是否相等。**eg：** `int i = 10; double d = 10.0;`

3. 如果判断引用类型，判断的是地址是否相等，即判定是不是同一个对象。

   **Equals01.java：**

   ```java
   package com.hspedu.object_;
   
   public class Equals01 {
       public static void main(String[] args) {
           A a = new A();
           A b = a;
           A c = b;
           System.out.println(a == c);//true
           System.out.println(b == c);//true
           B bObj = a;
           System.out.println(bObj == c);//true
           int num1 = 10;
           double num2 = 10.0;
           System.out.println(num1 == num2);//true
       }
   }
   class B{}
   class A extends B{}
   ```

***equals 是 Object 类中的方法。***

1. 只能判断引用类型。

   ```java
   System.out.println("hello".equals("abc"));
   ```

2. 默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等。比如，Integer，String

   ```java
   Integer integer1 = new Integer(1000);
   Integer integer2 = new Integer(1000);
   System.out.println(integer1 == integer2);//false 因为是两个不同的对象
   System.out.println(integer1.equals(integer2));//true 因为这里比较的是内容
   
   String str1 = new String("hspedu");
   String str2 = new String("hspedu");
   System.out.println(str1 == str2);//false
   System.out.println(str1.equals(str2));//true
   ```

   ## 如何重写 equals 方法

   应用实例: 判断两个 Person 对象的内容是否相等，如果两个 Person 对象的各个属性值都一样，则返回 true，反之 false。

   **EqualsExercise01.java：**

   ```java
   package com.hspedu.object_;
   
   public class EqualsExercise01 {
       public static void main(String[] args) {
           Person person = new Person("Jack", 18, '男');
           Person person1 = new Person("Jack", 18, '男');
           System.out.println(person.equals(person1));//true
   
       }
   }
   class Person{// 默认 extends Object
       private String name;
       private int age;
       private char gender;
       
       // 重写 Object 的 equals 方法
       public boolean equals(Object obj){
           //削断如果比较的两个对象是同一个对象，则直接返回true
           if(this == obj){
               return true;
           }else if (obj instanceof Person){
               //进行向下转型
               Person person = (Person)obj;//需要拿到obj的构造属性
               return this.name.equals(person.name) && this.age == person.age && this.gender == person.gender;
   
           }else{
               return false;
           }
       }
       
       public Person(String name, int age, char gender) {
           this.name = name;
           this.age = age;
           this.gender = gender;
       }
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public int getAge() {
           return age;
       }
   
       public void setAge(int age) {
           this.age = age;
       }
   
       public char getGender() {
           return gender;
       }
   
       public void setGender(char gender) {
           this.gender = gender;
       }
   }
   ```

   ## 练习题

第一题：

```java
class Person{
	public String name;
}
Person p1 = new Person();
p1.name = "hspedu";
Person p2 = new Person();
p2.name = "hspedu";
System.out.println(p1 == p2);//false
System.out.println(p1.name.equals(p2.name));//true
System.out.println(p1.equals(p2));//false
String s1 = new String("asdf");
String s2 = new String("asdf");
System.out.println(s1.equals(s2));//true
System.out.println(s1 == s2);//false
```

第二题：

```java
int it = 65;
float f1 = 65.0f;
System.out.printIn("65 和 65.0f 是否相等?"+ (it == fl));//true
char ch1 = 'A';
char ch2 = 12;
System.out.println("65 和 'A’ 是否相等?" + (it == ch1));//true
System.out.println("12 和 ch2 是否相等?" + (12 == ch2));//true
String str1 = new String("hello");
String str2 = new String("hello");
System.out.println(" str1 和 str2 是否相等?" + (str1 == str2))//false
System.out.println("str1 是否 equals str2?" + (str1.equals(str2)));//true
System.out.println("hello" == new java.sql.Date());//对象不同，无法比较，编译器报错
```

