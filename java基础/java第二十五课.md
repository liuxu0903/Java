# 多态

传统的方法带来的问题是什么?如何解决？问题是：代码的复用性不高，而且不利于代码维护。

***未使用多态时候的例子：***

**Poly01.java：**

```java
package com.hspedu.poly_;

public class Poly01 {
    public static void main(String[] args) {
        Master master = new Master("Tom");
        Dog dog = new Dog("旺旺");
        Bone bone = new Bone("大棒骨");
        Cat cat = new Cat("喵喵");
        Fish fish = new Fish("黄花鱼");
        master.feed(dog, bone);
        master.feed(cat, fish);

    }
}
```

**Master.java：**

```java
package com.hspedu.poly_;

public class Poly01 {
    public static void main(String[] args) {
        Master master = new Master("Tom");
        Dog dog = new Dog("旺旺");
        Bone bone = new Bone("大棒骨");
        Cat cat = new Cat("喵喵");
        Fish fish = new Fish("黄花鱼");
        master.feed(dog, bone);
        master.feed(cat, fish);

    }package com.hspedu.poly_;

public class Master {
    private String name;

    public Master(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    //主人给小狗吃骨头
    public void feed(Dog dog, Bone bone){
        System.out.println("主人 " + name + " 给 " + dog.getName() + " 吃 " + bone.getName());
    }
    //主人给小猫吃黄花鱼
    public void feed(Cat cat, Fish fish){
        System.out.println("主人 " + name + " 给 " + cat.getName() + " 吃 " + fish.getName());
    }
    //如果动物很多，食物很多
    // ===> feed 方法很多，不利于管理和维护
}
```

**Animal.java：**

```java
package com.hspedu.poly_;

public class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

**Dog.java：**

```java
package com.hspedu.poly_;

public class Dog extends Animal{
    public Dog(String name) {
        super(name);
    }
}
```

**Cat.java：**

```java
package com.hspedu.poly_;

public class Cat extends Animal{
    public Cat(String name) {
        super(name);
    }
}
```

**Food.java：**

```java
package com.hspedu.poly_;

public class Food {
    private String name;
    public Food(String name){
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

**Bone.java：**

```java
package com.hspedu.poly_;

public class Bone extends Food{
    public Bone(String name) {
        super(name);
    }
}
```

**Fish.java：**

```java
package com.hspedu.poly_;

public class Fish extends Food {
    public Fish(String name) {
        super(name);
    }
}
```

## 基本介绍

==方法==或==对象==具有多种形态。是面向对象的第三大特征，**多态是建立在封装和继承基础之上的**。

## 方法的多态

**重写和重载**就体现多态。

## 对象的多态

1. 一个对象的编译类型和运行类型可以不一致。
2. 编译类型在定义对象时，就确定了，不能改变。
3. 运行类型是可以变化的。
4. 编译类型看定义时 = 号的左边，运行类型看 = 号的右边。

**对象的多态案例：**

`Animal animal = new Dog();` animal 编译类型是 Animal，运行类型 Dog。
`animal = new Cat();` 编译类型仍然是 Animal，animal 的运行类型变成了 Cat。 

**PolyObject.java：**

```java
package com.hspedu.poly_.objpoly_;

public class PolyObject {
    public static void main(String[] args) {
        //体验对象多态的特点
        Animal animal = new Dog();//animal 编译类型就是 Animal，运行类型 Dog
        //因为运行时 ，执行到改行时，animal 运行类型是 Dog,所以 cry 就是 Dog 的 cry
        animal.cry();//小狗汪汪叫

        //animal 编译类型 Animal,运行类型就是 Cat
        animal = new Cat();
        animal.cry();//小猫喵喵叫
    }
}
```

**Animal.java：**

```java
package com.hspedu.poly_.objpoly_;

public class Animal {
    public void cry(){
        System.out.println("Animal cry() 动物在叫...");
    }
}
```

**Dog.java：**

```java
package com.hspedu.poly_.objpoly_;

public class Dog extends Animal{
    public void cry() {
        System.out.println("Dog cry() 小狗汪汪叫...");
    }
}
```

**Cat.java：**

```java
package com.hspedu.poly_.objpoly_;

public class Cat extends Animal{
    public void cry() {
        System.out.println("Cat cry() 小猫喵喵叫...");
    }
}
```

***使用多态后文章开头例子中的 Master.java 可以修改为：***

**Master.java：**

```java
package com.hspedu.poly_;

public class Master {
    private String name;

    public Master(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
    // 使用多态机制，可以统一的管理主人喂食的问题
    // animal 编译类型是 Animal,可以指向(接收) Animal 子类的对象
    // food 编译类型是 Food 可以指向(接收) Food 子类的对象
    public void feed(Animal animal, Food food){
        System.out.println("主人 " + name + " 给 " + animal.getName() + " 吃 " + food.getName());
    }
}
```

## 多态的注意事项和细节

1. 多态的前提是：两个对象(类)存在继承关系。

2. 多态的**==向上转型==**。

   - 本质：父类的引用指向了子类的对象。

   - 语法：`父类类型 引用名 = new 子类类型();`

   - 特点：编译类型看左边，运行类型看右边。

     **可以调用父类中的所有成员(需遵守访问权限)**，

     ==不能调用子类中特有成员==；因为在编译阶段，能调用哪些成员,是由编译类型来决定的。

     **最终运行效果看子类的具体实现！**即调用方法时，按照从子类开始查找方法，然后调用。

例子：

**PolyDetail.java：**

```java
package com.hspedu.poly_.detail_;

public class PolyDetail {
    public static void main(String[] args) {
        //向上转型:父类的引用指向了子类的对象
        //语法:父类类型 引用名 = new 子类类型();
        Animal animal = new Cat();
        Object obj = new Cat();//可以吗? 可以 0bject 也是 Cat 的父类

        //可以调用父类中的所有成员(需遵守访问权限)
        //animal.catchMouse();错误

        //最终运行效果看子类的具体实现！
        animal.eat();//猫吃鱼
        animal.run();//跑
        animal.show();//Hello, 你好
        animal.sleep();//睡
    }
}
```

**Animal.java：**

```java
package com.hspedu.poly_.detail_;

public class Animal {
    String name = "动物";
    int age = 10;
    public void sleep(){
        System.out.println("睡");
    }
    public void run(){
        System.out.println("跑");
    }
    public void eat(){
        System.out.println("吃");
    }
    public void show(){
        System.out.println("Hello, 你好");
    }
}
```

**Cat.java：**

```java
package com.hspedu.poly_.detail_;

public class Cat extends Animal{
    public void eat(){//方法重写
        System.out.println("猫吃鱼");
    }
    public void catchMouse(){//Cat()特有的方法
        System.out.println("猫抓老鼠");
    }
}
```

3. 多态的**==向下转型==**。
   - 语法：`子类类型 引用名 = (子类类型) 父类引用;`
   - 只能强转父类的引用，不能强转父类的对象。
   - 要求父类的引用必须指向的是当前目标类型的对象。
   - 当向下转型后，可以调用子类类型中所有的成员。

**PolyDetail.java：**

```java
package com.hspedu.poly_.detail_;

public class PolyDetail {
    public static void main(String[] args) {
        //向上转型:父类的引用指向了子类的对象
        //语法:父类类型 引用名 = new 子类类型();
        Animal animal = new Cat();

        //希望可以调用Cat的 catchMouse 方法
        //多态的向下转型
        //语法:子类类型 引用名=(子类类型)父类引用;
        //cat 的编译类型 Cat,运行类型是 Cat
        Cat cat = (Cat)animal;
        cat.catchMouse();

        //要求父类的引用必须指向的是当前目标类型的对象。
        //Dog dog = (Dog)animal; 错误。父类的引用指向的是 Cat 而不是 Dog
    }
}
```

4. 属性没有重写之说！属性的值看编译类型。

**PolyDetail02.java：**

```java
package com.hspedu.poly_.detail_;

import com.hspedu.super_.B;

public class PolyDetail02 {
    public static void main(String[] args) {
        //属性没有重写之说！属性的值看编译类型。
        Base base = new Sub();//向上转型
        System.out.println(base.count);//10，看编译类型。
    }
}
class Base{
    public int count = 10;
}
class Sub extends Base{
    public int count = 20;
}
```

5. **instanceof 比较操作符**，用于判断==对象的运行类型==是否为 XX 类型或 XX 类型的子类型。

## 练习题

1. 请说出下面的每条语言，哪些是正确的，哪些是错误的，为什么?

<img src="D:\消息记录\TyporaPages\多态练习题1.png" style="zoom:33%;" />

```java
public class PolyExercise01{
public static void main(String[] args) {
    double d = 13.4;//ok
    long l = (long)d;//ok
    System.out.println(l);//13
    int in = 5;//ok
    boolean b =(boolean)in;//不对，boolean 类型不参与转化
    Object obj = "Hello";//ok,向上转型
    String objstr = (String)obj;//ok,向下转型
    System.out.println(objStr);//Hello
	Object objPri = new Integer(5);//ok,向上转型
    String str = (String)objPri;//不对，父类的引用指向的是 Integer 而不是 String
    Integer str1 =(Integer)objPri;//ok,向下转型
}}
```

2. 题目：

   <img src="D:\消息记录\TyporaPages\多态练习题2.png" style="zoom:33%;" />



```java
public class PolyExercise02{
    public static void main(String[] args){
        Sub s = new Sub();
        System.out.println(s.count);//20
        s.display();//20
        Base b = s;//向上转型
        System.out.println(b == s);//true,两个对象比较的是地址，都指向了同一个Sub对象。
        System.out.println(b.count);//10
        b.display();//20
}}
class Base{//父类
    int count = 10;
    public void display(){
        System.out.println(this.count);
}
class Sub extends Base{//子类
    int count = 20;
    public void display(){
        System.out.println(this.count);
}
```

