# 类与对象

## 类与对象的关系示意图

<img src="D:\消息记录\TyporaPages\类与对象.png" style="zoom:33%;" />

### 使用面向对象的方式来解决养猫问题

```java
import java.util.Scanner;
public class Object{
		public static void main(String[] args){
		Cat cat1 = new Cat();
		Cat cat2 = new Cat();
		cat1.name = "小白";
		cat1.age = 1;
		cat1.color = "白色";
		cat1.weight = 10.0;
		cat2.name = "小花";
		cat2.age = 2;
		cat2.color = "白黄色";
		cat2.weight = 20.0;
		System.out.println("猫1的信息如下：");
		System.out.println("名字：" + cat1.name + "\n" + "年龄：" + cat1.age + "\n" + "颜色：" + cat1.color + "\n" + "体重：" + cat1.weight);		
		System.out.println("猫2的信息如下：");
		System.out.println("名字：" + cat2.name + "\n" + "年龄：" + cat2.age + "\n" + "颜色：" + cat2.color + "\n" + "体重：" + cat2.weight);
	}
}
class Cat{
		String name;
		int age;
		String color;
		double weight;
}
```

### 类和对象的区别和联系

1. 类是抽象的，概念的，代表一类事物，比如人类，猫类。 即它是数据类型。
2. 对象是具体的，实际的，代表一个具体事物，即是实例。
3. 类是对象的模板，对象是类的一个个体，对应一个实例。

## 对象在内存中的存在形式

**内存示意图**

<img src="D:\消息记录\TyporaPages\内存示意图.png" style="zoom:33%;" />

## 属性概念

1. 从概念或叫法上看: 成员变量 = 属性 = field（字段）
2. 属性是类的一个组成部分，一般是基本数据类型，也可是引用类型（对象，数组）比如我们前面定义猫类 的 int age 就是属性。

### 注意细节

1. 属性的定义语法同变量，示例：访问修饰符 属性类型 属性名。
2. 访问修饰符：控制属性的访问范围，有四种访问修饰符 public，proctected，默认，private 。
3. 属性的定义类型可以为任意类型，包含基本类型或引用类型。
4. 属性如果不赋值，有默认值，规则和数组一致。具体说：int 0，short 0，byte 0，long 0，float 0.0，double 0.0，char \u0000，boolean false，String null。

例子：

```java
import java.util.Scanner;
public class Object{
		public static void main(String[] args){
		Person p1 = new Person();
            //p1 是对象名，（对象的引用）
            //new Person() 创建的对象空间（数据）才是真正的对象
		System.out.println("\n人的信息如下：");
		System.out.println("名字：" + p1.name + "\n" + "年龄：" + p1.age + "\n" + "薪水：" + p1.sal + "\n" + "是否通过：" + p1.isPass);	
		//对象的属性如果不赋值，就是默认值，遵守上面列的数组规则。
	}
}
class Person{
		String name;
		int age;
		double sal;
		boolean isPass;
}
```

