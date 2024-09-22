# 数组

## 数组介绍

数组可以存放多个同一类型的数据。数组也是一种数据类型，是引用类型。即：数组就是一组数据。

## 数组的使用一

### 1. 数组的定义

**数据类型 数组名[] = new 数据类型[大小]**  ***eg: int a[] = new int[5];*** //创建了一个数组，名字a，存放5个 int。

也可以把 [] 换位置为： **数据类型[]  数组名= new 数据类型[大小]**

### 2. 数组的引用(使用/访问/获取数组元素)

**数组名[下标/索引/index]**  比如：你要使用 a 数组的第3个数 a[2]

## 数组的使用二

### 1. 先声明数组

语法：**数据类型 数组名[];** 也可以 数据类型[] 数组名; ***eg: int a[]; 或者 int[] a;***
### 2. 创建数组

语法: **数组名= new 数据类型[大小];** ***eg: a=new int[10];***

## 数组的使用三

### 静态初始化

语法：**数据类型 数组名[] = {元素值,元素值...}**  ***eg: int a[] = {2,5,6,7,8,89,90,34,56}***。

## 注意事项

1. 数组是多个相同类型数据的组合，实现对这些数据的统一管理。
2. 数组中的元素可以是任何数据类型，包括基本类型和**引用类型**，但是不能混用。
3. 数组创建后，如果没有赋值，有默认值 int 0, short 0, byte 0, long 0, float 0.0, double 0.0, char \u0000, boolean false, String null。
4. 数组的下标是从0开始的。
5. 使用数组的步骤
   - 声明数组并开辟空间
   - 给数组各个元素赋值 
   - 使用数组
6. 数组下标必须在指定范围内使用，否则报错：下标越界异常，比如 int [] arr = new int[5]; 则有效下标为 0-4。
7. 数组属引用类型，数组型数据是 ==对象(obiect)==。

### 练习

1. 创建一个 char 类型的26个元素的数组，分别放置 'A'-'Z'。使用for循环访问，所有元素并打印出来。提示：char类型数据运算'A'+1->'B'。

   ```java
   import java.util.Scanner;
   public class ArrayExercise{
   
   	public static void main(String[] args){
   		char[] Alphabet = new char[26];
   		for(int i = 0; i < Alphabet.length; i++){
   			Alphabet[i] = (char)('A' + i);//Alphabet 是 char[]类型, Alphabet 是 char类型
   			// 'A' +  i 是 int类型，需要强制转换 
   			System.out.print(Alphabet[i] + "\t");
   		}
   	}
   }
   ```

2. 请求出一个数组 int[] 的最大值 {4,-1,9,10,23}，并得到对应的下标。

   ```java
   import java.util.Scanner;
   public class ArrayExercise{
   
   	public static void main(String[] args){
   		int[] Array = {4,-1,9,10,23};
   		int Max = 0;
   		int flag = 0;
   		int i = 0;//增大作用域
   		for(; i < Array.length; i++){
   			if (Array[i] > Max){
   				Max = Array[i];
   				flag = i;
   			}
   		}
   		System.out.println("数组中的最大值是：" + Max);
   		System.out.println("最大值的下标是：" + flag);
   
   	}
   }
   ```

3. 请求出一个数组的和和平均值。

   ```java
   import java.util.Scanner;
   public class ArrayExercise{
   
   	public static void main(String[] args){
   		System.out.println("请输入数组元素个数：");
   		Scanner myScanner = new Scanner(System.in);
   		int Num = myScanner.nextInt();
   		double[] Array = new double[Num];
   		double Sum = 0.0;
   		int i = 0;//增大作用域
   		for(; i < Array.length; i++){
   			System.out.println("请输入第" + (i+1) + "个元素：");
   			Array[i] = myScanner.nextDouble();
   			Sum += Array[i];
   		}
   		System.out.println("数组的和的平均值为：" + Sum / Num);
   
   	}
   }
   ```

   

