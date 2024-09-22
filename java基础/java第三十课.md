# 面向对象编程练习题

## 第一题

定义一个 Person 类 {name, age, job}，初始化 Person 对象数组，有 3 个 person 对象，并按照 age 从大到小进行排序，提示，使用冒泡排序。

```java
package com.hspedu.homework;

import java.util.SortedMap;

public class Homework01 {
    public static void main(String[] args) {

        Person[] persons = new Person[3];
        persons[0] = new Person("Tom", 20, "student");
        persons[1] = new Person("Jack", 18, "worker");
        persons[2] = new Person("Smith", 19, "singer");
        //输出当前对象数组
        System.out.println("当前对象数组:");
        for(int i = 0; i < persons.length; i++){
            System.out.println(persons[i]);
        }
        //使用冒泡排序
        for(int i = 0; i < persons.length - 1; i++){
            for(int j = 0; j <persons.length - i - 1; j++){
                if(persons[j].getAge() < persons[j + 1].getAge()){
                    Person temp = persons[j];
                    persons[j] = persons[j + 1];
                    persons[j + 1] = temp;
                }
            }
        }
        System.out.println("对象数组按照年龄(从大到小)排序后：");
        for(int i = 0; i < persons.length; i++){
            System.out.println(persons[i]);
        }
    }
}
class Person{
    private String name;
    private int age;
    private String job;

    public Person(String name, int age, String job) {
        this.name = name;
        this.age = age;
        this.job = job;
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

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", job='" + job + '\'' +
                '}';
    }
}
```



## 第二题

写出四种访问修饰符和各自的访问权限。

<img src="D:\消息记录\TyporaPages\访问修饰符的访问范围.png" style="zoom:33%;" />

## 第三题

编写老师类。

<img src="D:\消息记录\TyporaPages\第八章习题3.png" style="zoom:33%;" />

**Homework03.java：**

```java
package com.hspedu.homework;

public class Homework03 {
    public static void main(String[] args) {
        Teacher[] teachers = new Teacher[3];
        teachers[0] = new Professor("John", 50, "教授", 30000, 1.3);
        teachers[1] = new FProfessor("Tom", 40, "副教授", 20000, 1.2);
        teachers[2] = new JiangShi("Mary", 30, "讲师", 10000, 1.1);
        for(int i = 0; i < teachers.length; i++){
            teachers[i].introduce();
        }
    }
}
```

**Teacher.java：**

```java
package com.hspedu.homework;

public class Teacher{
    private String name;
    private int age;
    private String post;
    private double salary;
    private double grade;

    public Teacher(String name, int age, String post, double salary, double grade) {
        this.name = name;
        this.age = age;
        this.post = post;
        this.salary = salary;
        this.grade = grade;
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

    public String getPost() {
        return post;
    }

    public void setPost(String post) {
        this.post = post;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public double getGrade() {
        return grade;
    }

    public void setGrade(double grade) {
        this.grade = grade;
    }

    @Override
    public String toString() {
        return "Teacher{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", post='" + post + '\'' +
                ", salary=" + salary +
                ", grade=" + grade +
                '}';
    }

    public void introduce(){
        System.out.println(toString());
    }
}
```

**Professor.java：**

```java
package com.hspedu.homework;

public class Professor extends Teacher{
    public Professor(String name, int age, String post, double salary, double grade) {
        super(name, age, post, salary,grade);
    }
    @Override
    public void introduce() {
        System.out.println("这是教授信息：");
        super.introduce();
    }
}
```

**FProfessor.java：**

```java
package com.hspedu.homework;

public class FProfessor extends Teacher{
    public FProfessor(String name, int age, String post, double salary, double grade) {
        super(name, age, post, salary, grade);
    }

    @Override
    public void introduce() {
        System.out.println("这是副教授信息：");
        super.introduce();
    }
}
```

**JiangShi.java：**

```java
package com.hspedu.homework;

public class JiangShi extends Teacher{
    public JiangShi(String name, int age, String post, double salary, double grade) {
        super(name, age, post, salary, grade);
    }

    @Override
    public void introduce() {
        System.out.println("这是讲师信息：");
        super.introduce();
    }
}
```

## 第四题

通过继承实现员工工资核算打印功能。

<img src="D:\消息记录\TyporaPages\第八章习题4.png" style="zoom:33%;" />

**Homework04.java：**

```java
package com.hspedu.homework.homework04;

public class Homework04 {
    public static void main(String[] args) {
        Manager john = new Manager("John", 100, 30, 1.2);
        Worker tom = new Worker("Tom", 60, 30, 1.0);
        john.setBonus(1000);
        john.show();
        tom.show();
    }
}
```

**Employee.java：**

```java
package com.hspedu.homework.homework04;

public class Employee {
    private String name;
    private double salary;
    private int days;
    private double grade;

    public Employee(String name, double salary, int days, double grade) {
        this.name = name;
        this.salary = salary;
        this.days = days;
        this.grade = grade;
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
    public int getDays() {
        return days;
    }
    public void setDays(int days) {
        this.days = days;
    }
    public double getGrade() {
        return grade;
    }
    public void setGrade(double grade) {
        this.grade = grade;
    }
    public void show(){
        System.out.println(name + " 的工资为：" + salary);
    }
}
```

**Worker.java：**

```java
package com.hspedu.homework.homework04;

public class Worker extends Employee{
    public Worker(String name, double salary, int days, double grade) {
        super(name, salary, days, grade);
    }

    @Override
    public void show() {
        System.out.print("普通员工 ");
        setSalary(getSalary() * getDays() * getGrade());
        super.show();
    }
}
```

**Manager.java：**

```java
package com.hspedu.homework.homework04;

public class Manager extends Employee{
    private double bonus;
    public Manager(String name, double salary, int days, double grade) {
        super(name, salary, days, grade);
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    @Override
    public void show() {
        System.out.print("经理 ");
        setSalary(bonus + getSalary() * getDays() * getGrade());
        super.show();
    }
}
```

## 第五题

设计父类——员工类。子类：工人类，农民类，教师类，科学家类，服务生类。

<img src="D:\消息记录\TyporaPages\第八章习题5.png" style="zoom:33%;" />

**Homework05.java：**

```java
package com.hspedu.homework.homework05;

public class Homework05 {
    public static void main(String[] args) {
        Employee[] employees = new Employee[3];
        employees[0] = new Worker("张三", 3000);
        employees[1] = new Farmer("小李", 2000);
        employees[2] = new Waiter("丽丽", 2500);
        Teacher tom = new Teacher("Tom", 5000);
        Scientist liu = new Scientist("LIU", 20000);
        for(int i = 0; i < 3; i++){
            employees[i].setMonth(12);//设置薪资月份
            employees[i].show();
        }

        tom.setMonth(13);//十三薪
        tom.setBonus(10);//课时费
        tom.setDays(100);//上了多少天课
        tom.show();

        liu.setMonth(15);//十五新
        liu.setBonus(100000);//年终奖金
        liu.show();
    }
}
```

**Employee.java：**

```java
package com.hspedu.homework.homework05;

public class Employee {
    private String name;
    private double salary;
    private int month;

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

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public Employee(String name, double salary) {

        this.name = name;
        this.salary = salary;
    }
    public void show(){
        System.out.println(name + " 的全年工资为：" + salary);
    }

}
```

**Worker.java：**

```java
package com.hspedu.homework.homework05;

public class Worker extends Employee{
    public Worker(String name, double salary) {
        super(name, salary);
    }

    @Override
    public void show() {
        System.out.print("工人 ");
        setSalary(getSalary() * getMonth());
        super.show();
    }
}
```

**Waiter.java：**

```java
package com.hspedu.homework.homework05;

public class Waiter extends Employee{
    public Waiter(String name, double salary) {
        super(name, salary);
    }

    @Override
    public void show() {
        System.out.print("服务生 ");
        setSalary(getSalary() * getMonth());
        super.show();
    }
}
```

**Farmer.java：**

```java
package com.hspedu.homework.homework05;

public class Farmer extends Employee{
    public Farmer(String name, double salary) {
        super(name, salary);
    }

    @Override
    public void show() {
        System.out.print("农民 ");
        setSalary(getSalary() * getMonth());
        super.show();
    }
}
```

**Teacher.java：**

```java
package com.hspedu.homework.homework05;

public class Teacher extends Employee{
    private int days;
    private double bonus;
    public Teacher(String name, double salary) {
        super(name, salary);
    }

    public int getDays() {
        return days;
    }

    public void setDays(int days) {
        this.days = days;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    @Override
    public void show() {
        System.out.print("老师 ");
        setSalary(getSalary() * getMonth() + days * bonus);
        super.show();
    }
}
```

**Scientist.java：**

```java
package com.hspedu.homework.homework05;

public class Scientist extends Employee{
    private double bonus;
    public Scientist(String name, double salary) {
        super(name, salary);
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    @Override
    public void show() {
        System.out.print("科学家 ");
        setSalary(getSalary() * getMonth() + bonus);
        super.show();
    }
}
```



## 第六题

在父类和子类中通过 this 和 super 都可以调用哪些属性和方法，假定Grand、Father 和 Son 在同一个包。

```java
class Grand{//超类
	String name = "AA";
	private int age = 100;
	public void g1(){
	
	}
}
class Father extends Grand{//父类
    String id = "001";
    private double score;
    public void f1(){
    //super 可以访问哪些成员（属性和方法）？super.name;super.g1(); 
    //this 可以访问哪些成员？this.id;this.score;this.f1();this.name;this.g1();
    }
}
class Son extends Father{//子类
    String name = "BB";
    public void g1(){
        
    }
    private void show(){
    //super 可以访问哪些成员（属性和方法）？super.id;super.f1();super.name;super.g1(); 
    //this 可以访问哪些成员？ this.name;this.g1();this.id;this.f1();
    }
}
```

## 第七题

答案：

Test;Demo;Rose;Jack;  

john;Jack;

<img src="D:\消息记录\TyporaPages\第八章习题7.png" style="zoom:33%;" />

## 第八题

扩展如下的 BankAccount 类。

```java
class BankAccount{
    private double balance;
    public BankAccount(double initialBalance){
		this.balance = initialBalance;
    }
    public void deposit(double amount){
        balance += amount;
    }
    public void withdraw(double amount){
        balance -= amount;
    }
}
```

要求：

1. 在上面类的基础上扩展，新类 CheckingAccount 对每次存款和取款都收取1美元的手续费。
2. 扩展前一个练习的 BankAccount 类，新类 SavingsAccount 每个月都有利息产生 ( earnMonthlyInterest 方法被调用)，并且有每月三次免手续费的存款或取款。在 earnMonthlyInterest 方法中重置交易计数。

**Homework08.java：**

```java
package com.hspedu.homework.homework08;

public class Homework08 {
    public static void main(String[] args) {
//        CheckingAccount checkingAccount = new CheckingAccount(1000);
//        checkingAccount.deposit(10);//1000+10-1 = 1009
//        checkingAccount.withdraw(10);//1009-10-1 = 998
//        System.out.println(checkingAccount.getBalance());
        SavingsAccount savingsAccount = new SavingsAccount(1000);
        savingsAccount.deposit(100);//1000+100=1100
        savingsAccount.deposit(100);//1100+100=1200
        savingsAccount.deposit(100);//1200+100=1300
        System.out.println(savingsAccount.getBalance());
        savingsAccount.deposit(100);//1300+100-1=1399
        System.out.println(savingsAccount.getBalance());
        //月初，定时器自动调用一下 earnMonthlyInterest
        savingsAccount.earnMonthlyInterest();//1399*1.01=1412.99
        savingsAccount.deposit(100);//免手续费 1412.99+100=1512.99
        System.out.println(savingsAccount.getBalance());
        savingsAccount.withdraw(100);//免手续费 1512.99-100=1412.99
        savingsAccount.withdraw(100);//免手续费 1412.99-100=1312.99
        savingsAccount.deposit(100);//扣手续费  1312.99+100-1=1411.99
        System.out.println(savingsAccount.getBalance());
    }
}
```

**BankAccount.java：**

```java
package com.hspedu.homework.homework08;

class BankAccount{
    private double balance;
    public BankAccount(double initialBalance){
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    public void deposit(double amount){
        balance += amount;

    }
    public void withdraw(double amount){
        balance -= amount;

    }
}
```

**CheckingAccount.java：**

```java
package com.hspedu.homework.homework08;

public class CheckingAccount extends BankAccount{
    //属性


    public CheckingAccount(double initialBalance) {
        super(initialBalance);
    }

    @Override
    public void deposit(double amount) {
        super.deposit(amount - 1);
    }

    @Override
    public void withdraw(double amount) {
        super.withdraw(amount + 1);
    }
}
```

**SavingsAccount.java：**

```java
package com.hspedu.homework.homework08;

public class SavingsAccount extends BankAccount{
    private int count = 3;
    private double rate = 0.01;//利率

    public SavingsAccount(double initialBalance) {
        super(initialBalance);
    }

    public int getCount() {
        return count;
    }

    public void setCount(int count) {
        this.count = count;
    }

    public double getRate() {
        return rate;
    }

    public void setRate(double rate) {
        this.rate = rate;
    }

    @Override
    public void deposit(double amount) {
        // 判断是否可以免手续费
        if(count > 0){
            super.deposit(amount);
        }else{
            super.deposit(amount - 1);
        }
        count--;
    }

    @Override
    public void withdraw(double amount) {
        if(count > 0){
            super.withdraw(amount);
        }else{
            super.withdraw(amount + 1);
        }
        count--;
    }
    public void earnMonthlyInterest(){
        count = 3;//每个月我们统计上个月利息，同时将count = 3
        super.deposit(getBalance() * rate);
    }
}
```

## 第九题

设计一个 Point 类，其 x 和 y 坐标可以通过构造器提供。提供一个子类 LabeledPoint，其构造器接受一个标签值和 x,y 坐标，比如：new LabeledPoint(“Black Thursday",1929,230.07)，写出对应的构造器即可。

```java
//Point类构造器
public class Point {
    private double x;
    private double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
}
//LabeledPoint类构造器
public class LabeledPoint extends Point{
    private  String label;

    public LabeledPoint(String label, double x, double y) {
        super(x, y);
        this.label = label;
    }
}
```

## 第十题

编写 Doctor 类 {name, age,job, gender, sal} 相应的 getter() 和 setter() 方法，5个参数的构造器，重写父类的 equals()方法：public boolean equals(Obiect obj) 并判断测试类中创建的两个对象是否相等。相等就是判断属性是否相同。

**Homework10.java：**

```java
package com.hspedu.homework.homework10;

public class Homework10 {
    public static void main(String[] args) {
        Doctor doctor = new Doctor("Tom", 18, "工人", '男', 5000);
        Doctor doctor1 = new Doctor("Tom", 18, "工人", '男', 5000);
        System.out.println(doctor.equals(doctor1));
    }
}
```

**Doctor.java：**

```java
package com.hspedu.homework.homework10;

public class Doctor {
    private String name;
    private int age;
    private String job;
    private char gender;
    private double sal;

    public Doctor(String name, int age, String job, char gender, double sal) {
        this.name = name;
        this.age = age;
        this.job = job;
        this.gender = gender;
        this.sal = sal;
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

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    public char getGender() {
        return gender;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }

    public double getSal() {
        return sal;
    }

    public void setSal(double sal) {
        this.sal = sal;
    }
    public boolean equals(Object obj){
        if(this == obj){
            return true;//判断两个对象是否相同
        }
        if(!(obj instanceof Doctor)){
            return false;//不是Doctor类型或其子类
        }
        //向下转型，因为obj的运行类型是Doctor类型或其子类
        Doctor doctor = (Doctor)obj;
        return this.name.equals(doctor.name) && this.age == doctor.age
                && this.job.equals(doctor.job) && this.gender == doctor.gender
                && this.sal == doctor.sal;
    }
}
```

## 第十一题

<img src="D:\消息记录\TyporaPages\第八章习题11.png" style="zoom:33%;" />

**Homework11.java：**

```java
package com.hspedu.homework.homework11;

public class homework11 {
    public static void main(String[] args) {
        Person person = new Student("Tom");//向上转型
        person.run();
        person.eat();

        Student student = (Student)person;//向下转型
        student.run();
        student.study();
        student.eat();
    }
}
```

**Person.java：**

```java
package com.hspedu.homework.homework11;

public class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Person(String name) {
        this.name = name;
    }
    public void run(){
        System.out.println("person run");
    }
    public void eat(){
        System.out.println("person eat");
    }

}
```

**Student.java：**

```java
package com.hspedu.homework.homework11;

public class Student extends Person{
    public Student(String name) {
        super(name);
    }

    @Override
    public void run() {
        System.out.println("student run");
    }
    public void study(){
        System.out.println("student study...");
    }
}
```

## 第十二题

说出 == 与 equals 的区别。

<img src="D:\消息记录\TyporaPages\第八章习题12.png" style="zoom:33%;" />

## 第十三题

<img src="D:\消息记录\TyporaPages\第八章习题13.png" style="zoom:33%;" />

**Homework13.java：**

```java
package com.hspedu.homework.homework13;

public class Homework13 {
    public static void main(String[] args) {
        Person[] persons = new Person[4];
        persons[0] = new Student("小明", '男', 10, "00023102");
        persons[1] = new Student("小红", '女', 12, "00023101");
        persons[2] = new Teacher("Tom", '男', 30, 8);
        persons[3] = new Teacher("Mary", '女', 35, 10);

        System.out.println("==========排序前：==========");
        for(int i = 0; i < persons.length; i++){
            System.out.println(persons[i].toString());
            new Homework13().print(persons[i]);
            System.out.println(persons[i].play());
            System.out.println("--------------------------");
        }
        new Homework13().sort(persons);
        System.out.println("==========排序后：==========");
        for(int i = 0; i < persons.length; i++){
            System.out.println(persons[i].toString());
            new Homework13().print(persons[i]);
            System.out.println(persons[i].play());
            System.out.println("--------------------------");
        }
    }
    public void sort(Person[] persons){
        for(int i = 0; i < persons.length - 1; i++){
            for(int j = 0; j < persons.length - i - 1; j++){
                if(persons[j].getAge() < persons[j + 1].getAge()){//按年龄从高到低排序
                    Person temp = persons[j];
                    persons[j] = persons[j + 1];
                    persons[j + 1] = temp;
                }
            }
        }
    }
    public void print(Person person){
        if(!(person instanceof Teacher || person instanceof Student)){
            System.out.println("不是老师也不是学生");
        }
        if(person instanceof Student){
            ((Student) person).study();
        }
        if(person instanceof Teacher){
            ((Teacher) person).teach();
        }
    }
}
```

**Person.java：**

```java
package com.hspedu.homework.homework13;

public class Person {
    private String name;
    private char sex;
    private int age;

    public Person(String name, char sex, int age) {
        this.name = name;
        this.sex = sex;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "姓名：" + name + "\n" +
                "年龄：" + sex + "\n" +
                "性别：" + age + "\n";
    }

    public String play(){
        return name + "爱玩";
    }
}
```

**Teacher.java：**

```java
package com.hspedu.homework.homework13;

public class Teacher extends Person{
    private int work_age;

    public Teacher(String name, char sex, int age, int work_age) {
        super(name, sex, age);
        this.work_age = work_age;
    }

    public int getWork_age() {
        return work_age;
    }

    public void setWork_age(int work_age) {
        this.work_age = work_age;
    }
    public void teach(){
        System.out.println("我承诺，我会认真教学。");
    }

    @Override
    public String toString() {
        return "老师的信息：\n" + super.toString() +
                "工龄：" + work_age;
    }

    @Override
    public String play() {
        return super.play() + "象棋。";
    }
}
```

**Student.java：**

```java
package com.hspedu.homework.homework13;

public class Student extends Person{
    private String stu_id;

    public Student(String name, char sex, int age, String stu_id) {
        super(name, sex, age);
        this.stu_id = stu_id;
    }

    public String getStu_id() {
        return stu_id;
    }

    public void setStu_id(String stu_id) {
        this.stu_id = stu_id;
    }
    public void study(){
        System.out.println("我承诺，我会好好学习。");
    }

    @Override
    public String toString() {
        return "学生的信息：\n" + super.toString() +
        "学号：" + stu_id;
    }

    @Override
    public String play() {
        return super.play() + "足球。";
    }
}
```

## 第十四题

答案：我是A类；hahah我是B类的有参构造；我是c类的有参构造；我是c类的无参构造；

<img src="D:\消息记录\TyporaPages\第八章习题14.png" style="zoom:33%;" />

## 第十五题

什么是多态，多态具体体现有哪些？(可举例说明)

<img src="D:\消息记录\TyporaPages\第八章习题15.png" style="zoom:33%;" />

举例：

```java
package com.hspedu.homework;

public class Homework15 {
    public static void main(String[] args) {
        AAA obj = new BBB();//向上转型
        AAA b1 = obj;
        System.out.println("obj的运行类型="+ obj.getClass());//BBB
        obj = new CCC();//向上转型
        System.out.println("obj的运行类型="+ obj.getClass());//CCC
        obj = b1;
        System.out.println("obj的运行类型="+ obj.getClass());//BBB
    }
}
class AAA{}
class BBB extends AAA{}
class CCC extends BBB{}
```

## 第十六题

java 的动态绑定机制是什么?

1. 当调用对象的方法时，该方法会和对象的内存地址 / 运行类型绑定。
2. 当调用对象的属性时，没有动态绑定机制，哪里声明，哪里使用。