# 作用域

1. 在 java 编程中，主要的变量就是属性（成员变量）和局部变量。
2. 我们说的局部变量一般是指在成员方法中定义的变量。
3. java 中作用域的分类
   - 全局变量：也就是属性，作用域为整个类体。
   - 局部变量：也就是除了属性之外的其他变量，作用域为定义它的代码块中！
4. **全局变量（属性）可以不赋值**，直接使用，因为**有默认值**，**局部变量必须赋值**后才能使用，因为**没有默认值**。

## 注意事项和细节使用

1. 属性和局部变量可以重名，访问时遵循就近原则。

2. 在同一个作用域中，比如在同一个成员方法中，两个局部变量，不能重名。

3. **属性**生命周期较长，伴随着对象的创建而创建，伴随着对象的销毁而销毁。

   **局部变量**生命周期较短，伴随着它的代码块的执行而创建，伴随着代码块的结束而销毁量，即在一次方法调用过程中。

4. **作用域范围不同：**

   全局变量/属性：可以被本类使用，或其他类使用（通过对象调用）。

   局部变量：只能在本类中对应的方法中使用。

5. **修饰符不同**
   全局变量/属性可以加修饰符。

   局部变量不可以加修饰符。

# 构造方法 / 构造器

## 基本语法

构造方法又叫构造器（constructor），是类的一种特殊的方法，它的主要作用是完成对新对象的初始化。

```java
[修饰符] 方法名(形参列表){
方法体;
}
```

1. 构造器的修饰符可以默认，也可以是 public protected private。
2. 参数列表和成员方法一样的规则。

## 注意事项和使用细节

1. 一个类可以定义多个不同的构造器，即构造器重载。
2. 构造器名和类名要相同。
3. 构造器==没有返回值==。
4. 构造器是完成对象的初始化，并不是创建对象。
5. 在创建对象时，系统自动的调用该类的构造方法。

6. 如果程序员没有定义构造方法，系统会自动给类生成一个默认无参构造方法（也叫默认构造方法），比如 `Person (){}`, 使用 ==javap 指令== 反编译看看
7. 一旦定义了自己的构造器，默认的构造器就覆盖了，就不能再使用默认的无参构造器，除非显式的定义一下，即：`Person(){}`

## 练习题

在前面定义的 Person 类中添加两个构造器：

第一个无参构造器：利用构造器设置所有人的 age 属性初始值都为 18
第二个带 pName 和 pAge 两个参数的构造器：使得每次创建 Person 对象的同时初始化对象的 age 属性值和 name 属性值。分别使用不同的构造器，创建对象。

```java
public class ConstructorExercise{
	public static void main(String[] args){
		Person person1 = new Person();
		System.out.println("无参构造器：" + person1.age + " " + person1.name);
		Person person2 = new Person(20,"张三");
		System.out.println("有参构造器：" + person2.age + " " + person2.name);		
	}
}
class Person{
	int age;
	String name;
	public Person(){
		age = 18;
	}
	public Person(int pAge, String pName){
		age = pAge;
		name = pName;
	}
}
```

# 对象创建的流程分析

例子：

```java
class Person{//类Person 
    int age=90;
    String name;
    Person(String n,int a){//构造器
        name=n;//给属性赋值
        age=a;//..
    }
}
Person p=new Person("小倩",20);
```

**上述例子流程分析（面试题）**

1. 加载 Person 类信息（Person.class），只会加载一次。

2. 在堆中分配空间（地址）

3. 完成对象初始化

   3.1 默认初始化 age = 0, name = null 

   3.2 显式初始化 age = 90, name = null

   3.3 构造器的初始化 age = 20, name = 小倩

4. 在对象在堆中的地址返回给 p（ p 是对象名，也可以理解成是对象的引用）。

# this 关键字

java 虚拟机会给每个对象分配 this，代表当前对象。

<img src="D:\消息记录\TyporaPages\this的理解.png" style="zoom:33%;" />

this 小结：简单的说，哪个对象调用，this 就代表哪个对象。

## 注意事项和使用细节

1. this 关键字可以用来访问本类的属性、方法、构造器。
2. this 用于区分当前类的属性和局部变量。
3. 访问成员方法的语法：`this.方法名(参数列表);`
4. 访问构造器语法：`this(参数列表); //必须放置在第一条语句`==注意只能在构造器中使用（即只能在构造器中访问另外一个构造器）==。
5.  this 不能在类定义的外部使用，只能在类定义的方法中使用。

## 练习题

定义 Person 类，里面有 name、age 属性，并提供 compareTo 比较方法，用于判断是否和另一个人相等，提供测试类TestPerson 用于测试，名字和年龄完全一样，就返回 true，否则返回 false

```java
public class TestPerson{
		public static void main(String[] args){
			Person p = new Person("张三", 18);
			Person p1 = new Person("张三", 18);
			System.out.println("他们是一样的对象吗："  + p.compareTo(p1));
		}
	}
class Person{
	String name;
	int age;
	public Person(String name, int age){
		this.name = name;
		this.age = age;
	}
	public boolean compareTo(Person p){
		return this.name.equals(p.name) && this.age == p.age;
	} 
}
```

