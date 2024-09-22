## 数组的传递(赋值)机制

### 值传递(值拷贝)

拷贝的是具体的**数据**。

### 引用传递(地址拷贝)

拷贝的是具体的**地址**。

## 数组拷贝

- 练习1：将 int[] arr1 ={10,20,30}; 拷贝到 arr2 数组，要求数据空间是独立的。

```java
port java.util.Scanner;
public class ArrayCopy{

	public static void main(String[] args){
		int[] arr1 = {10, 20, 30};
		int[] arr2 = new int[3]; //创建一个新的数组arr2,开辟新的数据空间，大小 arr1.length
		for(int i = 0; i < arr1.length; i++){
			arr2[i] = arr1[i]; //遍历 arr1，把每个元素拷贝到对应的位置
		}
		System.out.println("数组一的值分别是：");
		for(int j = 0; j < arr1.length; j++){
			System.out.println(arr1[j]);
		}
		System.out.println("数组二的值分为是：");
		for(int k = 0; k < arr2.length; k++){
			System.out.println(arr2[k]);
		}
	}
}
```

- 练习2：把数组的元素内容翻转。   ***eg: arr {11,22,33,44,55,66} => {66, 55,44,33,22,11}***

1. 逆序翻转：

```java
import java.util.Scanner;
public class ArrayReverse{

	public static void main(String[] args){
		int[] arr1 = {11, 22, 33, 44, 55, 66};
		int[] arr2 = new int[arr1.length];
		for(int i = 0; i < arr1.length; i++){
			arr2[i] = arr1[arr1.length - i -1];
		}
		System.out.println("翻转后数组的值分为是：");
		for(int k = 0; k < arr2.length; k++){
			System.out.println(arr2[k]);
		}
	}
}
```

2. 找规律翻转：

```java
import java.util.Scanner;
public class ArrayReverse{

	public static void main(String[] args){
		int[] arr1 = {11, 22, 33, 44, 55, 66};
		int len = arr1.length;
		int[] arr2 = new int[len];
		int temp = 0;
		for(int i = 0; i < len/2; i++){
			temp = arr1[i];
			arr2[i] = arr1[len - i -1];
			arr2[len - i - 1] = temp;
		}
		System.out.println("翻转后数组的值为：");
		for(int j = 0; j < len; j++){
			System.out.println(arr2[j]);
		}
	}
}
```

## 数组添加

实现动态的给数组添加元素效果，实现对数组扩容。

1. 原始数组使用静态分配 int[] arr = {1,2,3}
2. 增加的元素，直接放在数组的最后 arr = {1,2,3,4} 

```java
import java.util.Scanner;
public class ArrayAdd{

	public static void main(String[] args){
		int[] arr1 = {1, 2, 3};
		int len = arr1.length;
		int[] arr2 = new int[len + 1];
		for(int i = 0; i < len; i++){
			arr2[i] = arr1[i];
		}
		arr2[len] = 4;
		System.out.println("添加后数组的值为：");
		for(int j = 0; j < len + 1; j++){
			System.out.println(arr2[j]);
		}
	}
}
```

3. 用户可以通过如下方法来决定是否继续添加，添加成功，是否继续？y/n

```java
import java.util.Scanner;
public class ArrayAdd{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		int[] arr1 = {1, 2, 3, 4};
		System.out.println("现在数组为：");
		for (int i = 0; i < arr1.length; i++ ) {
			System.out.print(arr1[i] + " ");
		}
		do{
			System.out.println("\n是否要添加元素 y/n：");
			char ch = myScanner.next().charAt(0);
			if(ch == 'y'){
				int[] arr2 = new int[arr1.length + 1];
				for(int j = 0; j < arr1.length; j++){
					arr2[j] = arr1[j]; //遍历 arr1 数组，把 arr1 的元素依次拷贝到新数组 arr2 中
				}
				System.out.println("请输入你要添加元素的值：");
				int num = myScanner.nextInt();
				arr2[arr2.length - 1] = num; //把新添加的元素加到 arr2 的尾部
				arr1 = arr2; // 把添加好元素 arr2 的地址给 arr1， 也就是让 arr1 指向 arr2
				System.out.println("添加后的数组为：");
				for (int k = 0; k < arr1.length; k++ ) {
					System.out.print(arr1[k] + " ");
				}
			}
			else if(ch == 'n'){
				break;
			}
			else{
				System.out.println("输入格式有误,请重新输入");
			}

		}while(true);

	}
}
```

## 数组缩减

练习：一个数组 {1，2，3，4，5}，可以将该数组进行缩减，提示用户是否继续缩减，每次缩减最后哪个元素。
当只剩下最后一个元素，提示不能再缩减。

```java
import java.util.Scanner;
public class ArrayReduce{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		int[] arr1 = {1, 2, 3, 4, 5};
		System.out.println("现在数组为：");
		for (int i = 0; i < arr1.length; i++ ) {
			System.out.print(arr1[i] + " ");
		}
		do{
			System.out.println("\n是否要添加缩减 y/n：");
			char ch = myScanner.next().charAt(0);
			if(arr1.length == 1){
				System.out.println("不能再缩减了，程序退出。");
				break;
			}
			else if(ch == 'y'){
				int[] arr2 = new int[arr1.length - 1];
				for(int j = 0; j < arr2.length; j++){
					arr2[j] = arr1[j]; //遍历 arr1 数组，把 arr1 的元素依次拷贝到新数组 arr2 中
				}
				arr1 = arr2; // 把缩减好元素 arr2 的地址给 arr1， 也就是让 arr1 指向 arr2
				System.out.println("缩减后的数组为：");
				for (int k = 0; k < arr1.length; k++ ) {
					System.out.print(arr1[k] + " ");
				}
			}
			else if(ch == 'n'){
				break;
			}
			else{
				System.out.println("输入格式有误,请重新输入");
			}

		}while(true);

	}
}
```

