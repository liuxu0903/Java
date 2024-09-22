# 类与对象

## 如何创建对象

1. 先声明再创建         `Cat cat;   cat = new Cat();`
2. 直接创建 		       `Cat cat = new Cat();`

## 如何访问属性

对象名.属性名;

## 类和对象的内存分配机制

<img src="D:\消息记录\TyporaPages\内存示意图2.png" style="zoom:33%;" />

### java 内存的结构分析

1. 栈：一般存放**基本数据类型（局部变量）**
2. 堆：存放**对象**（Cat cat，**数组**等）
3. 方法区：常量池（**常量，比如字符串**），类加载信息（**属性信息，方法信息**）

### java 创建对象的流程简单分析

1. 先加载 Person 类信息（属性和方法信息，只会加载一次）。
2. 在堆中分配空间，进行默认初始化。
3. 把地址赋给 p，p 就指向对象。
4. 进行指定初始化，比如：`p.name =" jack"; p.age=10`

例子：

```java
Person a=new Person();
a.age=10;
a.name="小明";
Person b;
b=a;
System.out.println(b.name);
b.age=200;
b = null;
System.out.printn(a.age);
System.out.println(b.age);
```

输出结果：

> 小明
>
> 200
>
> 出现异常。 // 因为把 b = null 之后，b 已经不是一个对象了，所以 b 不可能找到 age 了。

## 成员方法

### 方法的调用机制

<img src="D:\消息记录\TyporaPages\内存示意图3.png" style="zoom:33%;" />

### 成员方法的定义

```java
public 返回数据类型 方法名(参数列表..){//方法体
    语句;
	return 返回值;
}
```

1. 形参列表：表示成员方法输入 cal (int n)。
2. 数据类型(返回类型)：表示成员方法输出，void 表示没有返回值。
3. 方法主体：表示为了实现某一功能代码块。
4. return 语句不是必须的。

### 细节注意

1. 访问修饰符（作用是控制方法使用的范围）如果不写默认访问，[有四种：public，protected，默认，private]

2. 返回数据类型

   - **一个方法最多有一个返回值**，思考，如何返回多个结果？（可以用数组返回）。

     例子：

     ```java
     import java.util.Scanner;
     public class MethodDetail{
     		public static void main(String[] args){
     			AA res = new AA();
     			int Arr[] = res.getSumAndSub(5, 3);
     			System.out.println("和是：" + Arr[0]);
     			System.out.println("差是：" + Arr[1]);
     		}
     	}
     class AA{
     	public int[] getSumAndSub(int m, int n){
     		int Sum = m + n;
     		int Sub = m - n;
     		int[] Arr = {Sum, Sub};
     		return Arr;
     	}
     }
     ```

   - 返回类型可以为任意类型，包含基本类型或引用类型（数组，对象）。

   - 如果方法要求有返回数据类型，则方法体中最后的执行语句必须为 return 值。

     而且要求返回值类型必须和 return 的值类型一致或兼容。

   - 如果方法是 void，则方法体中可以没有 return 语句，或者只写 return。
   - 方法名遵循驼峰命名法，最好见名知义，表达出该功能的意思即可，比如：得到两个数的和 getsum，开发中按照规范。