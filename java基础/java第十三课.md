# 排序

排序是将多个数据，依指定的顺序进行排列的过程。

## 排序的分类

### 内部排序

指将需要处理的所有数据都加载到内部存储器中进行排序。包括（交换式排序法、选择式排序法和插入式排序法）。
### 外部排序

数据量过大，无法全部加载到内存中，需要借助外部存储进行排序。包括（合并排序法和直接合并排序法）。

## 冒泡排序

冒泡排序（Bubble Sorting）的基本思想是：通过对待排序序列从后向前（从下标较大的元素开始），依次比较相邻元素的值，若发现逆序则交换，使值较大的元素逐渐从前移向后部，就象水底下的气泡一样逐渐向上冒。

案例来说明冒泡法。我们将五个无序：24，69，80，57，13，使用冒泡排序法将其排成一个**从小到大**的有序数列。

```java
import java.util.Scanner;
public class BubbleSort{

	public static void main(String[] args){
		int[] arr = {24, 69, 80, 57, 13};
		int temp = 0;
		System.out.println("现在数组为：");
		for (int i = 0; i < arr.length; i++ ) {
			System.out.print(arr[i] + " ");
		}
		for(int i = 0; i < arr.length -1; i++){ //length 个元素，需要 length - 1次排序
			for(int j = 0; j < arr.length - 1 - i; j++){ //每次排序会进行 length -1 - i 次比较
				if(arr[j] > arr[j + 1]){ //交换，每次排序把最大的元素换到后面
						temp = arr[j];
						arr[j] = arr[j + 1];
						arr[j + 1] = temp;	
				}
			}
			System.out.println("\n=== 第" + (i+1) + "次排序后数组为===");
			for(int k = 0; k < arr.length; k++){
				System.out.print(arr[k] + " ");
			}
		}
	}
}
```

# 查找

## 常用的查找

### 顺序查找

**例子**

有一个数列：白眉鹰王、金毛狮王、紫衫龙王、青翼蝠王。数游戏：从键盘中任意输入一个名称，判断数列中是否包含此名称。要求： 如果找到了，就提示找到，并给出下标值。

```java
import java.util.Scanner;
public class SeqSearch{

	public static void main(String[] args){
		String[] names = {"白眉鹰王", "金毛狮王", "紫衫龙王", "青翼蝠王"};
		int index = -1;
		System.out.println("请输入你要找的名字：");
		Scanner myScanner = new Scanner(System.in);
		String findname = myScanner.next();
		for(int i = 0; i < names.length; i++){
			if (findname.equals(names[i])){
				System.out.println("找到" + findname +"啦！");
				System.out.println("在数组中的下标是： " + i);
				index = 1;
				break;
			}
		}
		if(index == -1){
			System.out.println("很遗憾，没有找到" + findname);
		}
	}
}
```

# 二维数组

## 概念

1. 可以这样理解，原来的一维数组的每个元素是一维数组，就构成二维数组。
2. 如果需要得到每个一维数组的值，还需要再次遍历。
3. 如果我们要访问第 i + 1 个一维数组的第 j + 1 个值 `arr[i][j];`

**例子**
请用二维数组输出如下图形

`0 0 0 0 0 0 `

`0 0 1 0 0 0 `

`0 2 0 3 0 0 `

`0 0 0 0 0 0`

```java
import java.util.Scanner;
public class TwoDimensionalArray{

	public static void main(String[] args){
		int[][] arr = {
			{0, 0, 0, 0, 0, 0},
			{0, 0, 1, 0, 0, 0},
			{0, 2, 0, 3, 0, 0},
			{0, 0, 0, 0, 0, 0},
		};
		for(int i = 0; i < arr.length; i++){ // arr.length 是在统计有二维数组中有多少个一维数组
			for(int j = 0; j < arr[i].length; j++){
				System.out.print(arr[i][j] + " "); // arr[i].length 是得到对应一维数组的长度
			}
			System.out.print("\n");
		}
	}
}
```

## 二维数组的使用

### 动态初始化

1. 第一种：`类型[][] 数组名 = new 类型[大小][大小] //如：int a[][] = new int[2][3];`
2. 第二种：
   - 先声明  `类型 数组名[][]; `
   - 再定义  `数组名 = new 类型[大小][大小];`
   - 赋值（有默认值，比如 int 类型的就是 0 ）

3. 第三种：**列数不确定的二维数组**

- 例子：动态创建下面二维数组，并输出

​		`i = 0: 1`

​		`i = 1: 2    2`

​		`i = 2: 3    3    3    `

```java
import java.util.Scanner;
public class TwoDimensionalArray{

	public static void main(String[] args){
		int[][] arr = new int[3][]; //创建二维数组，但只能确定一维数组的个数
		for(int i = 0; i < arr.length; i++){
			arr[i] = new int[i + 1]; //为每一个一维数组开辟空间
			for(int j = 0; j < arr[i].length; j++){
				arr[i][j] = i + 1; //赋值
				System.out.print(arr[i][j] + "\t");
			}
			System.out.println();
		}
	}
}
```

4. 静态初始化

   `定义 类型 数组名[][] ={{值1,值2..},{值1,值2..},{值1,值2..}}`

例子：`int[][] arr = {{4, 6},{1, 4, 5, 7},{-2}}; 遍历二维数组，并得到和`

```java
import java.util.Scanner;
public class TwoDimensionalArray{

	public static void main(String[] args){
		int[][] arr = {{4, 6},{1, 4, 5, 7},{-2}};
		int sum = 0;
		for(int i = 0; i < arr.length; i++){
			for(int j = 0; j < arr[i].length; j++){
				sum += arr[i][j];
			}
		}
		System.out.println("二维数组的和为：" + sum);
	}
}
```

### 杨辉三角

```java
import java.util.Scanner;
public class Yanghui{

	public static void main(String[] args){
		int[][] arr = new int[10][];
		for(int i = 0; i < arr.length; i++){
			arr[i] = new int[i + 1];
			for(int j = 0; j <= i; j++){
				arr[i][0] = 1; // 每行第一个元素赋值为1
				arr[i][i] = 1; // 每行最后一个元素赋值为1
				if(i >= 2 && j >= 1 && j <= i - 1){  // 从第三行起，每行中间元素等于上一行元素加上一行元素的前一个元素
					arr[i][j] = arr[i - 1][j] + arr[i - 1][j - 1];
				}
			}
			for(int k = 0; k <= i; k++){
				System.out.print(arr[i][k] + "\t");
			}
			System.out.println();
		}
	}
}
```

## 练习

1. `int[] x, y[]`以下选项允许通过编译的是（ b, e ）：

   ```java
   //说明：x int 类型的一维数组（int[] x），y 是 int 类型的二维数组（int[] y[]）
   a) x[0] = y; //n
   b) y[0] = x; //y
   c) y[0][0]= x; //n
   d) x[0][0] = y; //n
   e) y[0][0] = x[0]; //y
   f) x = y; //n
   ```

2. 下面数组定义正确的有（B, D）：

   <img src="D:\消息记录\TyporaPages\数组题1.png" style="zoom:33%;" />

   ```java
   String strs[] = new[]{"a", "b", "c"} //y
   String strs[] = new[3]{"a", "b", "c"} //n
   //编译器能自动识别[]中应该填几，右侧[]中不可以写数字，否则编译不通过。
   ```

3. 写出结果（ blue ）：

   <img src="D:\消息记录\TyporaPages\数组题2.png" style="zoom:33%;" />

```java
boolean 类型的数组，在默认情况下为 false
```

4. 以下 Java 代码的输出结果为（ 1357 ）：

   <img src="D:\消息记录\TyporaPages\数组题3.png" style="zoom:33%;" />

5. 己知有个升序的数组，要求插入一个元素，该数组顺序依然是升序，比如：[10，12，45，90]，添加23后，数组为[10，12，23，45，90]。

   ```java
   import java.util.Scanner;
   public class Chapter6{
   
   	public static void main(String[] args){
   		int[] ascendArray = {10, 12, 45, 90};
   		int temp = 0;
   		System.out.println("当前数组为：");
   		for(int i = 0; i < ascendArray.length; i++){
   			System.out.print(ascendArray[i] + " ");
   		}
   		System.out.println("\n请输入要插入的元素：");
   		Scanner myScanner = new Scanner(System.in);
   		int num = myScanner.nextInt();
   		int[] ArrayNew = new int[ascendArray.length + 1];
   		ArrayNew[0] = num; // 让新元素添加到数组最前端
   		for(int i = 0; i < ascendArray.length; i++){
   			ArrayNew[i + 1] = ascendArray[i]; // 原来的数组元素从过后往前赋值给新数组
   		}
   		
   		// 新数组中，除了第一个元素都是有序的，只需要给第一个元素找位置就行，相当于冒泡排序的一次排序。
   		for(int i = 0; i < ArrayNew.length - 1; i++){
   			if(ArrayNew[i] > ArrayNew[i + 1]){  
   				temp = ArrayNew[i];
   				ArrayNew[i] = ArrayNew[i + 1];
   				ArrayNew[i + 1] = temp;
   			}
   		}
   		System.out.println("插入后的数组为：");
   		for(int i = 0; i < ArrayNew.length; i++){
   			System.out.print(ArrayNew[i] + " ");
   		}
   	}
   }
   ```

6. 随机生成10个整数（1到100的范围）保存到数组，求平均值、求最大值和最大值的下标、并查找里面是否有数字8，并降序打印。

   `//随机生成1-100的整数：(int)(Math.random() * 100) + 1`

   ```java
   import java.util.Scanner;
   public class Chapter6{
   
   	public static void main(String[] args){
   		int[] arr = new int[10];
   		double Sum = 0.0;
   		int Max = 0;
   		int Index = -1;
   		boolean flag = false;
   		int temp = 0;
   
   		for(int i = 0; i < arr.length; i++){ //随机生成10个（1~100）的整数
   			arr[i] = (int)(Math.random() * 100) + 1;
   		}
   		System.out.print("随机生成的数组为：\n");
   		for(int i = 0; i < arr.length; i++){
   			System.out.print(arr[i] + " ");
   			Sum += arr[i];    
   			if(arr[i] > Max){
   				Max = arr[i]; //记录最大值
   				Index = i; //记录最大值的下标
   			}
   			if(arr[i] == 8){
   				flag = true; //随机数组中有数字8，则把flag置为true
   			}
   		}
   		System.out.println("\n数组的平均值为：" + Sum/arr.length);
   		System.out.println("数组的最大值为：" + Max + "，它的下标是" + Index);
   		if(flag){
   			System.out.println("数组里面含有数字8");
   		}
   		else{
   			System.out.println("数组里面没有数字8");
   		}
   		System.out.println("数组倒序打印结果为：");	
   		for(int i = 0; i < arr.length - 1; i++){   //冒泡排序，因为想要倒序输出，每次把最小的排到最后
   			for(int j = 0; j < arr.length - 1 - i; j++){
   				if(arr[j] < arr[j + 1]){
   					temp = arr[j];
   					arr[j] = arr[j + 1];
   					arr[j + 1] = temp;
   				}
   			}
   		}
   		for(int i = 0; i < arr.length; i++){
   			System.out.print(arr[i] + " ");
   		}
   	}
   }
   ```

7. 试写出以下代码的打印结果（）：

   <img src="D:\消息记录\TyporaPages\数组题4.png" style="zoom:33%;" />

```java
a,a
z,z
韩,韩
c,c
```

