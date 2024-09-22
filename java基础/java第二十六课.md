# java 的动态绑定机制

看一个例子：

**DynamicBinding.java：**

```java
package com.hspedu.poly_.dynamic_;

public class DynamicBinding {
    public static void main(String[] args) {
        // a 的编译类型是 A, 运行类型是 B
        A a = new B();//向上转型
        System.out.println(a.sum());//40
        System.out.println(a.sum1());//30
    }
}
class A {

    public int i= 10;
    public int sum() {
        return getl()+ 10;
    }
    public int sum1(){
        return i + 10;
    }
    public int getl() {
        return i;
    }
}

class B extends A {

    public int i = 20;
    public int sum() {
        return i + 20;
    }
    public int getl() {
        return i;
    }
    public int sum1() {
        return i + 10;
    }
}
```

1. 当调用**对象方法**的时候，==该**方法**会和该对象的内存地址 / 运行类型绑定==。
2. 当调用**对象属性**时，==没有动态绑定机制==，哪里声明，哪里使用。

例子：

```java
package com.hspedu.poly_.dynamic_;

public class DynamicBinding {
    public static void main(String[] args) {
        // a 的编译类型是 A, 运行类型是 B
        A a = new B();//向上转型
        System.out.println(a.sum());//30
        System.out.println(a.sum1());//20
    }
}
class A {

    public int i= 10;
    //动态绑定机制：
    public int sum() {
        return getI()+ 10;
    }
    public int sum1(){
        return i + 10;
    }
    public int getI() {
        return i;
    }
}

class B extends A {

    public int i = 20;
    public int getI() {
        return i;
    }
}
```

# 多态的应用

## 多态数组

数组的定义类型为父类类型，里面保存的实际元素类型为子类类型。

**应用实例：**现有一个继承结构如下:要求创建 1 个 Person 对象、2个 Student 对象和 2 个 Teacher 对象，统一放在数组中，并调用每个对象 say 方法。

**PolyArray.java：**

```java
package com.hspedu.poly_.polyarr_;

public class PolyArray {
    public static void main(String[] args) {
        Person[] persons = new Person[5];
        persons[0] = new Person("Jack", 20);
        persons[1] = new Student("Jack", 18, 100);
        persons[2] = new Student("Smith", 19, 88);
        persons[3] = new Teacher("Scott", 30, 30000);
        persons[4] = new Teacher("Scott", 25, 25000);
        for (int i = 0; i < persons.length; i++) {
            //person[i]编译类型是 Person,运行类型是是根据实际情况有JVM来判断
            System.out.println(persons[i].say());//动态绑定机制
        }
    }
}
```

**Person：**

```java
package com.hspedu.poly_.polyarr_;

public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
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
    public String say(){// 返回名字和年龄
        return name + "\t" + age;
    }

}
```

**Student.java：**

```java
package com.hspedu.poly_.polyarr_;

public class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }
    //重写父类say
    @Override
    public String say() {
        return "学生 " + super.say() + " score=" + score;
    }
}
```

**Teacher.java：**

```java
package com.hspedu.poly_.polyarr_;

public class Teacher extends Person {
    private double salary;

    public Teacher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
    //重写父类的say方法

    @Override
    public String say() {
        return "老师 " + super.say() + " salary=" + salary;
    }
}
```

**应用实例升级：**

如何调用子类特有的方法，比如 Teacher 有一个 teach，Student 有一个 study 怎么调用？

**PolyArray.java：**

```java
package com.hspedu.poly_.polyarr_;

public class PolyArray {
    public static void main(String[] args) {
        Person[] persons = new Person[5];
        persons[0] = new Person("Tom", 20);
        persons[1] = new Student("Jack", 18, 100);
        persons[2] = new Student("Smith", 19, 88);
        persons[3] = new Teacher("Scott", 30, 30000);
        persons[4] = new Teacher("King", 25, 25000);
        for (int i = 0; i < persons.length; i++) {
            //person[i]编译类型是 Person,运行类型是是根据实际情况有JVM来判断
            System.out.println(persons[i].say());//动态绑定机制

            //可以向下转型
            if(persons[i] instanceof Student) {
                Student student = (Student)persons[i];
                student.study();// 或者 ((Student)person[i]).study();
            }else if(persons[i] instanceof Teacher){
                Teacher teacher = (Teacher)persons[i];
                teacher.teach();
            }else if(persons[i] instanceof Person){

            }else{
                System.out.println("你的类型有误，请自己检查...");
            }
        }
    }
}
```

**Person：**

```java
package com.hspedu.poly_.polyarr_;

public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
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
    public String say(){// 返回名字和年龄
        return name + "\t" + age;
    }

}
```

**Teacher.java：**

```java
package com.hspedu.poly_.polyarr_;

public class Teacher extends Person {
    private double salary;

    public Teacher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
    //重写父类的say方法

    @Override
    public String say() {
        return "老师 " + super.say() + " salary=" + salary;
    }
    //特有方法
    public void teach(){
        System.out.println("老师 " + getName() +
                " 正在讲 java 课程...");
    }
}
```

**Student.java：**

```java
package com.hspedu.poly_.polyarr_;

public class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }
    //重写父类say
    @Override
    public String say() {
        return "学生 " + super.say() + " score=" + score;
    }
    public void study(){
        System.out.println("学生 " + getName() + " 正在学习java...");
    }
}
```

