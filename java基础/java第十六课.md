# 类与对象

## 成员方法使用细节

### 形参列表

1. 一个方法可以有 0 个参数，也可以有多个参数，中间用逗号隔开，比如 `getSum(int n1, int n2)`
2. 参数类型可以为任意类型，包含基本类型或引用类型，比如 `printArr(int[][] map)`
3. 调用带参数的方法时，一定对应着参数列表传入相同类型或兼容类型的参数 !
4. 方法定义时的参数称为**形式参数**，简称形参；方法调用时的传入参数称为**实际参数**，简称实参，实参和形参的类型要一致或兼容、个数、顺序必须一致！

### 方法体

里面写完成功能的具体的语句，可以为输入、输出、变量、运算、分支、循环、方法调用，但里面不能再定义方法！即:方法**不能嵌套定义**。

### 方法调用细节说明

1. 同一个类中的方法调用：直接调用即可，不需要再创建对象。
2. 跨类中的方法 A 类调用 B 类方法：需要先创建 B 类对象，然后通过对象名调用。
3. 跨类的方法调用和方法的**访问修饰符**相关。

### 练习题

1. 编写类 AA 新方法：判断一个数是奇数 odd 还是偶数，返回 boolean。

   ```java
   import java.util.Scanner;
   public class MethodExerciseod{
   		public static void main(String[] args){
   			AA res = new AA();
   			Scanner myScanner = new Scanner(System.in);
   			System.out.println("请输入一个数：");
   			int n = myScanner.nextInt();
   			if(res.isOdd(n)){
   				System.out.println("是偶数");
   			}
   			else{
   				System.out.println("是奇数");
   			}
   		}
   	}
   class AA{
   	public boolean isOdd(int n){
   		if(n % 2 == 0){
   			return true;
   		}
   		else{
   			return false;
   		}
   	}
   }
   ```

2. 根据行、列、字符打印对应行数和列数的字符。

   `比如：行：4，列：4，字符 #，则打印相应的效果。`

   `####`

   `####`

   `####`

   `####`

   ```java
   import java.util.Scanner;
   public class MethodExercise{
   		public static void main(String[] args){
   			AA res = new AA();
   			Scanner myScanner = new Scanner(System.in);
   			System.out.println("请输入一个行数：");
   			int m = myScanner.nextInt();
   			System.out.println("请输入一个列数：");
   			int n = myScanner.nextInt();
   			System.out.println("请输入想要打印的字符：");
   			char c = myScanner.next().charAt(0);
   			System.out.print("==========结果==========\n");
   			res.printChars(m, n, c);
   		}
   	}
   class AA{
   	public void printChars(int m, int n, char c){
   		for(int i = 0; i < m; i++){
   			for(int j = 0; j < n; j++){
   				System.out.print(c);
   			}
   			System.out.print("\n");
   		}
   	}
   }
   ```

## 成员方法的传参机制

基本数据类型，传递的是值（值拷贝），形参的任何改变不影响实参！

引用类型传递的是地址（传递也是值，但是值是地址）可以通过形参影响实参。

### 练习题

1. 编写类 MyTools 类，编写一个方法可以打印维数组的数据。

   ```java
   import java.util.Scanner;
   public class MethodExercise{
   		public static void main(String[] args){
   			MyTools res = new MyTools();
   			int[][] twoArray = {{1, 2, 3},
   								{4, 5, 6}};
   			res.printTwoArray(twoArray);
   
   		}
   	}
   class MyTools{
   	public void printTwoArray(int[][] arr){
   		for(int i = 0; i < arr.length; i++){
   			for(int j = 0; j < arr[i].length; j++){
   				System.out.print(arr[i][j] + " ");
   			}
   			System.out.print("\n");
   		}
   	}
   }
   ```

   

2. 编写一个方法 copyPerson，可以复制一个 Person 对象，返回复制的对象。克隆对象，注意要求得到新对象和原来的对象是两个独立的对象，只是他们的属性相同。

   ```java
   import java.util.Scanner;
   public class MethodExercise{
   		public static void main(String[] args){
   			Person p = new Person();
   			p.name = "张三";
   			p.age = 100;
   			Tool res = new Tool();
   			Person p2 = res.copyPerson(p);
   			System.out.println("姓名一：" + p.name + "\t" + "年龄一：" + p.age);
   			System.out.println("姓名二：" + p2.name + "\t" + "年龄二：" + p2.age);
   			System.out.print("他们是一样的对象吗：" );
   			System.out.print(p == p2);
   		}
   	}
   class Person{
   	String name;
   	int age;
   }
   class Tool{
   	public Person copyPerson(Person p){
   		Person p2 = new Person();
   		p2.name = p.name;
   		p2.age = p.age;
   		return p2;
   	}
   }
   ```

   