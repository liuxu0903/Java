# Object 类详解

## hashCode 方法

1. 提高具有哈希结构的容器的效率！

2. 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的！

3. 两个引用，如果指向的是不同对象，则哈希值是不一样的。

4. 哈希值主要根据地址号来的！不能完全将哈希值等价于地址 。

5. 案例演示

   ```java
   package com.hspedu.object_;
   
   public class HashCode {
       public static void main(String[] args) {
           AA aa = new AA();
           AA aa2 = new AA();
           AA aa3 = aa;
           System.out.println("aa.hashCode() =  " + aa.hashCode());
           System.out.println("aa2.hashCode() =  " + aa2.hashCode());
           System.out.println("aa3.hashCode() =  " + aa3.hashCode());
       }
   }
   class AA{}
   ```

6. 后面在集合中，hashcode 如果需要的话，也会重写。

## toString 方法

### 基本介绍

1. 默认返回：全类名 + @ + 哈希值的十六进制，（查看Object 的 toString方法）子类往往重写toString方法，用于返回对象的属性信息。

2. 案例演示

   ```java
   package com.hspedu.object_;
   
   public class ToString {
       public static void main(String[] args) {
           /* Object的toString()源码
           （1） getClass().getName() 类的全类名（包名 + 类名）
           （2） Integer.toHexString(hashCode()) 将对象的hashCode值转成16进制字符串
                public String toString() {
                   return getClass().getName() + "@" + Integer.toHexString(hashCode());
               }
           */
           Monster monster = new Monster("小妖怪", "巡山的", 1000);
           System.out.println("monster.toString() = " + monster.toString() + "\nmonster.hashCode() = " + monster.hashCode());
       }
   }
   class Monster{
       private String name;
       private String job;
       private double sal;
   
       public Monster(String name, String job, double sal) {
           this.name = name;
           this.job = job;
           this.sal = sal;
       }
   }
   ```

3. 重写 tostring 方法，打印对象或拼接对象时，都会自动调用该对象的 toString形式。

   案例演示

   ```java
       //重写toString方法，输出对象属性
       //使用快捷键 alt+insert -> toString
       @Override
       public String toString() { //重写后，一般是把对象的属性值输出，当然程序员也可以自己定制
           return "Monster{" +
                   "name='" + name + '\'' +
                   ", job='" + job + '\'' +
                   ", sal=" + sal +
                   '}';
       }
   ```

4. 当直接输出一个对象时，toString 方法会被默认的调用。

   ```java
   System.out.println(monster); // 就会默认调用 monster.toString()
   ```

## finalize 方法

1. 当对象被回收时，系统自动调用该对象的finalize方法。子类可以重写该方法做一些释放资源的操作。

2. 什么时候被回收：当某个对象没有任何引用时，则 jvm 就认为这个对象是一个垃圾对象，就会使用垃圾回收机制来销毁该对象，在销毁该对象前，会先调用，finalize方法。

3. 垃圾回收机制的调用，是由系统来决定（即有自己的GC算法），也可以通过 System.gc() 主动触发垃圾回收机制。

   ```java
   package com.hspedu.object_;
   
   public class Finalize {
       public static void main(String[] args) {
           Car bmw = new Car("宝马");
           //这时 car 对象就是一个垃圾,垃圾回收器就会回收(销毁)对象，在销毁对象前，会调用该对象的finalize方法。
           //程序员就可以在 finalize 中，写自己的业务逻辑代码(比如释放资源:数据库连接,或者打开文件...)
           //如果程序员重写了 finalize，就可以实现自己的逻辑。
           //如果程序员不重写 finalize，那么就会调用 Object 类的 finalize，即默认处理。
           bmw = null;
           System.gc();//主动调用垃圾回收器
           System.out.println("程序退出了...");
       }
   }
   class Car{
       //属性，资源
       private String name;
   
       public Car(String name) {
           this.name = name;
       }
       //重写 finalize 方法
       @Override
       protected void finalize() throws Throwable {
           System.out.println("我们销毁 汽车 " + name);
           System.out.println("释放了某些资源... ");
       }
   }
   ```

