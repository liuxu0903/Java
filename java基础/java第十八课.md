# 方法重载

## 基本介绍

java 中允许同一个类中，多个同名方法的存在，但要求==形参列表==不一致！

比如：System.out.println(); out 是 PrintStream 类型

## 重载的好处

1. 减轻了起名的麻烦 
2. 减轻了记名的麻烦 

## 注意事项和使用细节

1. 方法名：必须相同
2. 参数列表：必须不同（参数**类型**或**个数**或**顺序**，至少有一样不同，参数名无要求）
3. 返回类型：**无要求**

## 练习题

第一题：b c d e 

<img src="D:\消息记录\TyporaPages\重载1-1716884594490-3.png" style="zoom:33%;" />

第二题：编写程序，类 Methods 中定义三个重载方法并调用。方法名为 m。三个方法分别接收一个 int 参数、两个 int 参数、一个字符串参数。分别执行平方运算并输出结果，相乘并输出结果，输出字符串信息。在主类的 main() 方法中分别用参数区别调用三个方法。

```java
import java.util.Scanner;
public class OverLoadExercise{

	public static void main(String[] args){
		Methods method = new Methods();
		int result1 = method.m(10);
		System.out.println("平方运算：" + result1);	
		int result2 = method.m(9,10);	
		System.out.println("两数相乘并输出：" + result2);
		String s = method.m("方法的重载");
		System.out.println("打印字符串：" + s);			
	}
}
class Methods{
	public int m(int num){
		return num * num;
	}
	public int m(int num1, int num2){
		return num1 * num2;
	}
	public String m(String s){
		return s;
	}

}
```

第三题：在 Methods 类，定义三个重载方法 max()，第一个方法，返回两个 int 值中的最大值，第二个方法，返回两个double 值中的最大值，第三个方法，返回三个 double 值中的最大值，并分别调用三个方法。

```java
import java.util.Scanner;
public class OverLoadExercise{

	public static void main(String[] args){
		Methods method = new Methods();
		int result1 = method.max(1,10);
		System.out.println("两个int值的最大值：" + result1);	
		double result2 = method.max(9.0,10.0);	
		System.out.println("两个double值的最大值：" + result2);
		double result3 = method.max(1.0,2.0,3.0);
		System.out.println("三个double值的最大值：" + result3);			
	}
}
class Methods{
	public int max(int num1, int num2){
		return num1 > num2 ? num1 : num2;
	}
	public double max(double num1, double num2){
		return num1 > num2 ? num1 : num2;
	}
	public double max(double num1, double num2, double num3){
		double max1 = num1 > num2 ? num1 : num2;
		return max1 > num3 ? max1 : num3;
	}

}
```

# 可变参数

## 基本概念

java 允许将同一个类中**多个同名**同功能但**参数个数不同**的方法，封装成一个方法。就可以通过可变参数实现。
## 基本语法

```java
访问修饰符 返回类型 方法名(数据类型... 形参名){

}
```

例子：求和。

```java
//1. int... 表示接受的是可变参数，类型是int,即可以接收多个int(0-多)
//2.使用可变参数时，可以当做数组来使用 即 nums 可以当做数组
//3.遍历nums求和
public class VarParameter{

	public static void main(String[] args){
		HspMethod m = new HspMethod();
		System.out.println("和为：" + m.sum(1,9,80));
	}
}
class HspMethod{
	public int sum(int... nums){
		int sum = 0;
		for(int i = 0; i < nums.length; i++){
			sum += nums[i];
		}
		//System.out.println("接收的参数个数= "+ nums.length);
		return sum;
	}
}
```

## 注意事项和使用细节

1. 可变参数的实参可以**为 0 个或任意多个**。

2. 可变参数的实参可以为**数组**。

   例子：

   ```java
   public class VarParameter{
   	public static void main(String[] args){
   		HspMethod m = new HspMethod();
   		int[] arr = {1,2,3};
   		m.sum(arr);
   		
   	}
   }
   class HspMethod{
   	public void sum(int... nums){
   		System.out.println("接收的参数个数="+ nums.length);
   	}
   }
   ```

3. 可变参数的本质就是**数组**。

4. 可变参数可以和普通类型的参数一起放在形参列表，但必须保证**可变参数在最后**。

   ```java
   public class VarParameter{
   	public static void main(String[] args){
   		HspMethod m = new HspMethod();
   		m.sum("Str",2,1.0,2.0);
   		
   	}
   }
   class HspMethod{
   	public void sum(String m, int n, double... nums){
   		System.out.println("接收的参数为：" + m + " " + n + " " + nums[0] + " " + nums[1]);
   	}
   }
   ```

5. 一个形参列表中**只能出现一个可变参数**。

## 练习题

有三个方法，分别实现返回姓名和两门课成绩（总分），返回姓名和三门课成绩（总分），返回姓名和五门课成绩（总分）。封装成一个可变参数的方法。

```java
public class VarParameter{
	public static void main(String[] args){
		HspMethod m = new HspMethod();
		m.showScore("王二",99.5,100);
		m.showScore("张三",99,100,98.5);
		m.showScore("李五",99,100,100,100,90.5);
		
	}
}
class HspMethod{
	public void showScore(String name, double... nums){
		double sum = 0.0;
		int i = 0;
		for(; i < nums.length; i++){
			sum += nums[i];
		}
		System.out.println("姓名：" + name );
		System.out.println("一共有"+ i + "门成绩，课程总成绩为：" + sum);
	}
}
```

