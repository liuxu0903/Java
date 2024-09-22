# break

## 基本语法

break 语句用于终止某个语句块的执行，一般使用在 switch 或者循环（for , while , do-while）中。

```java
{
    .......
    break;
    ......
}
```

### 以while循环为例

<img src="D:\消息记录\TyporaPages\while使用break.png" style="zoom:33%;" />

## 说明

1. break 语句出现在多层嵌套的语句块中时，可以通过标签指明要终止的是哪一层语句块。

2. ==标签==的基本使用

   ```java
   label1: {......
       label2:{......
           label3:{......
                  break label2;
                  ......
                  }
              }
           }
   ```

   - break 语句可以指定退出哪层。
   - label1 是标签，由程序员指定。
   - break 后指定到哪个label 就退出到哪里。
   - 在实际的开发中，尽量不要使用标签。
   - 如果没有指定 break,默认退出最近的循环体。

练习（登录验证）：

```java
import java.util.Scanner;
public class BreakExercise{

	public static void main(String[] args){
		int Sum = 1;
		do{
			System.out.println("*******登陆验证******");
			Scanner myScanner = new Scanner(System.in);
			System.out.println("请输入用户名：");
			String Name  = myScanner.next();
	        System.out.println("请输入密码：");
			String Key  = myScanner.next();			
			if(Name.equals("丁真") && Key.equals("666") ){ //补充说明字符串的内容比较使用的方法 equals
				System.out.println("登陆成功！");
				break;
			}
			else{
				System.out.println("用户名或密码输入错误！" );
				System.out.println("提示：还有" + (3 - Sum) + "次机会！");
			}
			Sum++;
		}while(Sum <= 3);
	}
}
```

# continue

## 基本语法

1. continue 语句用于结束本次循环，继续执行下一次循环。

   ```java
   {	.......    
       continue;    
       ......
   }
   ```

2. continue 语句出现在多层嵌套的循环语句体中时，可以通过标签指明要跳过的是哪一层循环，**这个和前面 break 的标签的使用的规则一样**。

   ### 以while循环为例

   <img src="D:\消息记录\TyporaPages\while使用continue.png" style="zoom:50%;" />

# return

## 基本语法

return 使用在方法，表示跳出所在的方法。

# 控制结构的练习题

## 第一题

某人有100,000元,每经过一次路口，需要交费，规则如下：

1. 当现金 > 50000时，每次交5%

2. 当现金 <= 50000时，每次交1000，编程计算该人可以经过多少次路口

   要求：使用 while break方式完成

   ```java
   import java.util.Scanner;//导入
   public class Chapter5{
   
   	public static void main(String[] args){
   		int Num = 0;
   		double Money = 100000;
   		while(true){
   			if(Money > 50000){//System.out.println("需要上交 5 % 的过路费。");
   				double FeeHigh = Money * 0.05;
   				Money -= FeeHigh;
   				Num++;
   			}
   			else if(Money > 1000){//System.out.println("需要上交 1000元 的过路费。");
   				double FeeLow = 1000;
   				Money -= FeeLow;
   				Num++;
   			}
   			else{
   				//System.out.println("没钱交过路费啦。");
   				break;
   			}
   		}
   		System.out.println("100,000现金可以经过" + Num + "次路口。");
   	}
   }
   ```

## 第二题

实现判断一个整数，属于哪个范围：大于0；小于0；等于0

```java
import java.util.Scanner;
public class  Chapter5{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		System.out.println("请输入一个整数：");
		int Num  = myScanner.nextInt();
		while(true){
			if(Num > 0){		
				System.out.println(Num + "是一个大于0的数字");
				break;
			}
			else if(Num == 0){
				System.out.println(Num + "是一个等于0的数字");
				break;				
			}
			else{
				System.out.println(Num + "是一个小于0的数字");
				break;
			}
		}
	}
}
```

## 第三题

判断一个年份是否为闰年

```java
import java.util.Scanner;
public class  Chapter5{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		System.out.println("请输入一个年份：");
		int Year  = myScanner.nextInt();
		if((Year % 4 == 0 && Year % 100 != 0) || (Year % 400 == 0)){
			System.out.println(Year + "年 是 闰年");
		}
		else{
			System.out.println(Year + "年 不是 闰年");
		}
	}
}
```

## 第四题

判断一个整数是否是水仙花数，所谓水仙花数是指一个3位数，其各个位上数字立方和等于其本身。

例如：153 = 1×1×1 + 3×3×3 + 5×5×5

```java
import java.util.Scanner;
public class  Chapter5{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		System.out.println("请输入一个3位数：");
		int Num  = myScanner.nextInt();
		int Num_hundredsplace = Num / 100;	//百位
		int Num_tensplace = Num % 100 / 10; //十位
		int Num_onesplace = Num % 10;	//个位
		if(Num == Num_hundredsplace*Num_hundredsplace*Num_hundredsplace 
			+ Num_tensplace*Num_tensplace*Num_tensplace
			+Num_onesplace*Num_onesplace*Num_onesplace ){
			System.out.println(Num  + " 是 水仙花数");
		}
		else{
			System.out.println(Num  + " 不是 水仙花数");
		}
	}
}
```

## 第五题

看看下面代码输出什么？

<img src="D:\消息记录\TyporaPages\第五题.png" style="zoom:33%;" />

答：没有输出。

## 第六题

输出1-100之间的不能被5整除的数，每5个一行

```java
import java.util.Scanner;
public class  Chapter5{

	public static void main(String[] args){
		Scanner myScanner = new Scanner(System.in);
		System.out.println("请输入开始数字：");
		int Start  = myScanner.nextInt();
		System.out.println("请输入结束数字：");
		int End  = myScanner.nextInt();
		int Sum = 0;
		while(Start <= End){
				if(Start % 5 != 0){		
				System.out.print(Start + "\t");
				Sum++;
				if(Sum % 5 == 0){
				System.out.print("\n");	
				}
			}
			Start ++;
		}
	}
}
```

## 第七题

输出小写的 a-z 以及大写的 Z-A

```java
import java.util.Scanner;
public class  Chapter5{

	public static void main(String[] args){
	
		char low = 'a';
		char high = 'Z';
		int num1 = 0;
		int num2 = 0;
		System.out.println("以下列出小写的a-z：");
		while(low <= 'z'){	
			System.out.print(low);
			low++;
			num1++;
			if(num1 % 7 == 0){ //每7个换行
				System.out.print("\n");
			}
		}
		System.out.print("\n");
		System.out.println("以下列出大写的Z-A：");
		while(high >= 'A'){	
			System.out.print(high);
			high--;
			num2++;
			if(num2 % 7 == 0){ //每7个换行
				System.out.print("\n");
			}
		}
	}
}
```

## 第八题

求出 1-1/2+1/3-1/4.....1/100 的和

```java
import java.util.Scanner;
public class Chapter5{

	public static void main(String[] args){

		int Start = 1;
		int End = 100;
		double Sum = 0.0;
		while(Start <= End){
			if(Start % 2 == 1){		
				Sum += 1.0/Start; 
			}
			else if(Start % 2 == 0){
				Sum -= 1.0/Start;
			}
			Start ++;
		}
		System.out.println(" 1-1/2+1/3-1/4.....1/100 的和为：" + Sum);
	}
}
```

这里有一个隐藏的陷阱，要把 公式分子 1 写出1.0 才能得到精确的小数。

## 第九题

求 1+(1+2)+(1+2+3)+(1+2+3+4)+...+(1+2+3+..+100) 的结果

```java
import java.util.Scanner;
public class Chapter5{

	public static void main(String[] args){

		int Start = 1;
		int End = 100;
		int Sum = 0;
		while(Start <= End){
			int S = Start;
			while(S >= 1){
				Sum += S;
				S--;
			}
			Start ++;
		}
		System.out.println("  1+(1+2)+(1+2+3)+(1+2+3+4)+...+(1+2+3+..+100) 的结果为：" + Sum);
	}
}
```

