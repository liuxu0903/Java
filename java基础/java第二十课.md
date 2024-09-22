# 本章练习

1. 编写类 A01，定义方法 max，实现求某个 double 数组的最大值，并返回。

   ```java
   public class Chapter7{
   
   	public static void main(String[] args){
   		A01 m = new A01();
   		double[] doubleArray = null;
   		Double res = m.max(doubleArray);
   		if(res != null){
   			System.out.println("数组的最大值是：" + res);
   		}
   		else{
   			System.out.println("数组输入有误！数组不能为null或者{}。");
   		}
   	}
   }
   class A01{
   	public Double max(double[] doubleArray){ //Double 是一个包装类返回值是double
   		if(doubleArray != null && doubleArray.length > 0){ //先判断数组是否空，再判断数组长度是否大于0
   			double dMax = 0.0;
   			for(int i = 0; i < doubleArray.length; i++){
   				if (doubleArray[i] > dMax){
   					dMax = doubleArray[i];
   				}
   			}
   			return dMax;
   		}
   		else{
   			return null; //Double是类返回值可以为null
   		}
   
   	}
   }
   ```

   

2. 编写类 A02，定义方法 find，实现查找某字符串是否在数组中，并返回索引。

   ```java
   import java.util.Scanner;
   public class Chapter7{
   
   	public static void main(String[] args){
   		A02 m = new A02();
   		String[] stringArray = {"abc", "123", "hello", "张三","java"};
   		System.out.println("输入你要查找的字符串：");
   		Scanner myScanner = new Scanner(System.in);
   		String elem = myScanner.next();
   		int index = m.find(stringArray, elem);
   		if(index != -1){
   			System.out.println("找到啦！" + elem + "在数组中的下标是：" + index);
   		}
   		else{
   			System.out.println("很遗憾...未找到。");
   		}
   		
   	}
   }
   class A02{
   	public int find(String[] stringArray, String elem){
   		int index = -1;
   		for(int i = 0; i < stringArray.length; i++){
   			if (stringArray[i].equals(elem)){
   				index = i;
   			}
   		}
   		return index;
   	}
   }
   ```

   

3. 编写类 Book，定义方法 updatePrice，实现更改某本书的价格，具体：如果价格 >150，则更改为150，如果价格 >100，更改为100，否则不变。

   ```java
   public class Chapter7{
   	public static void main(String[] args){
   		Book m = new Book("java从入门到精通", 300);
   		System.out.println("书的信息：");
   		m.inFo();
   		System.out.println("更改后书的价格后：");
   		m.updatePrice();
   		m.inFo();
   	}
   }
   class Book{
   	String name;
   	int price;
   	public Book(String name, int price){
   		this.name = name;
   		this.price = price;
   
   	}
   	public void updatePrice(){
   		if(price > 150){
   			price = 150;
   		}
   		else if(price > 100){
   			price = 100;
   		}
   	}
   	public void inFo(){
   		System.out.println("书名：" + name + "价格：" + price);
   	}
   }
   ```

   

4. 编写类 A03，实现数组的复制功能 copyArr，输入旧数组，返回一个新数组，元素和旧数组一样。

   ``` java
   public class Chapter7{
   	public static void main(String[] args){
   		A03 m = new A03();
   		int[] arr = {0,11,5,99,6};
   		System.out.println("旧数组：");
   		m.inFo(arr);
   		System.out.println("\n新数组：");
   		int[] arrNew = m.copyArr(arr);
   		m.inFo(arrNew);
   	}
   }
   class A03{
   	
   	public int[] copyArr(int[] arr){
   		int[] newArr = new int[arr.length];
   		for(int i = 0; i < arr.length; i++){
   			newArr[i] = arr[i];
   		}
   		return newArr;
   
   	}
   	public void inFo(int[] arr){
   		for(int i = 0; i < arr.length; i++){
   			System.out.print(arr[i] + " ");
   		}
   		
   	}
   }
   ```

   

5. 定义一个圆类 Circle，定义属性：半径，提供显示圆周长功能的方法，提供显示圆面积的方法。

   ```java
   public class Chapter7{
   	public static void main(String[] args){
   		Circle m = new Circle(1.0);
   		m.inFo();
   	}
   }
   class Circle{
   	double radius;
   	public Circle(double r){
   		this.radius = r;
   	}
   	public double Perimeter(double r){
   		return 2 * Math.PI * radius;
   
   	}
   	public double Area(double r){
   		return Math.PI * radius * radius;
   
   	}
   	public void inFo(){
   		System.out.println("圆的周长为：" + Perimeter(radius));
   		System.out.println("圆的面积为：" + Area(radius));	
   	}
   }
   ```

   

6. 编程创建一个 Cale 计算类，在其中定义 2 个变量表示两个操作数，定义四个方法实现求和、差、乘、商（要求除数为 0 的话，要提示）并创建两个对象，分别测试。

   ```java
   public class Chapter7{
   	public static void main(String[] args){
   		Cale m1 = new Cale(1.0, 2.0);
   		Cale m2 = new Cale(1.0, 0.0);
   		m1.inFo();
   		m2.inFo();
   	}
   }
   class Cale{
   	double num1;
   	double num2;
   	public Cale(double num1, double num2){
   		this.num1 = num1;
   		this.num2 = num2;
   	}
   	public double Sum(double num1, double num2){
   		return num1 + num2;
   
   	}
   	public double Difference(double num1, double num2){
   		return num1 - num2;
   
   	}
   	public double Multiplication(double num1, double num2){
   		return num1 * num2;
   
   	}
   	public Double Quotient(double num1, double num2){
   		if(num2 != 0){
   			return num1 / num2;
   		}
   		else{
   			return null;
   		}
   	}
   	public void inFo(){
   		System.out.println("num1:" + num1 +"\t"+ "num2:" + num2);
   		System.out.println("和：" + Sum(num1,num2));
   		System.out.println("差：" + Difference(num1,num2));	
   		System.out.println("乘：" + Multiplication(num1,num2));
   		if(num2 != 0.0){
   			System.out.println("商：" + Quotient(num1,num2));	
   		}else
   		{
   			System.out.println("分母不能为0!");
   		}	
   
   	}
   }
   ```

   

7. 设计一个 Dog 类，有名字、颜色和年龄属性，定义输出方法 show() 显示其信息并创建对象，进行测试、【提示 this.属性】。

   ```java
   public class Chapter7{
   	public static void main(String[] args){
   		Dog m = new Dog("二哈", "黄色", 1);
   		m.show();
   	}
   }
   class Dog{
   	String name;
   	String color;
   	int age;
   	public Dog(String name, String color, int age){
   		this.name = name;
   		this.color = color;
   		this.age = age;
   	}
   	
   	public void show(){
   		System.out.print("名字：" + name + "\t");
   		System.out.print("颜色：" + color + "\t");	
   		System.out.print("年龄：" + age + "\n");			
   	}
   }
   ```

   

8. 给定一个 Java 程序的代码如下所示，则编译运行后，输出结果是 (10,9,10)

   <img src="D:\消息记录\TyporaPages\类与对象练习题.png" style="zoom:33%;" />

   ```java
   题目中：
       new Test().count1();中的 new Test() 是匿名对象。使用后就不能使用，故只能使用一次！
   ```

   

9. 定义 Music 类，里面有音乐名 name、音乐时长 times 属性，并有播放 play 功能和返回本身属性信息的功能方法 getlnfo。

   ```java
   public class Chapter7{
   	public static void main(String[] args){
   		Music m = new Music("枕着光的她", 1.0);
   		m.play();
   		m.getInfo();
   	}
   }
   class Music{
   	String name;
   	double times;
   	public Music(String name, double times){
   		this.name = name;
   		this.times = times;
   	}
   	public void play(){
   		System.out.println("音乐 " + name + " 正在播放中...... 播放时长为： " + times + "分钟。");
   	}
   	
   	public void getInfo(){
   		System.out.print("名字：" + name + "\t");
   		System.out.println("时长：" + times + "h");		
   	}
   }
   ```

   

10. 试写出以下代码的运行结果 (101 100;101 101)

    <img src="D:\消息记录\TyporaPages\类与对象练习题10.png" style="zoom:33%;" />

11. 在测试方法中，调用 method 方法，代码如下，编译正确，试写出 method 方法的定义形式，调用语句为：`System.out.println(method(method(10.0,20.0),100);`

    ```java
    public class Chapter7{
    	public static void main(String[] args){
    		A11 m = new A11(1.0, 2.0);
    		m.getInfo();
    	}
    }
    class A11{
    	double num1;
    	double num2;
    	public A11(double num1, double num2){
    		this.num1 = num1;
    		this.num2 = num2;
    	}
    	public double method(double num1, double num2){
    		return (num1 + num2);
    	}
    	
    	public void getInfo(){
    		System.out.print(method(method(10.0,20.0),100));
    	}
    }
    ```

    

12. 创建一个 Employee 类，属性有(名字，性别，年龄，职位，薪水)，提供 3 个构造方法，可以初始化 

    (1) (名字，性别，年龄，职位，薪水)

    (2) (名字，性别，年龄) 

    (3) (职位，薪水)

    要求充分复用构造器。 

    ```java
    public class Chapter7{
    	public static void main(String[] args){
    		Employee m1 = new Employee("张三", '男', 18, "主任", 10000.0);
    		m1.getInfo();
    		Employee m2 = new Employee("张三", '男', 18);
    		m2.getInfo();
    		Employee m3 = new Employee("主任", 10000.0);
    		m3.getInfo();
    	}
    }
    class Employee{
    	String name;
    	char sex;
    	int age;
    	String job;
    	double salary;
    
    	public Employee(String name, char sex, int age){
    		this.name = name;
    		this.sex = sex;
    		this.age = age;
    	}
    	public Employee(String job, double salary){
    		this.job = job;
    		this.salary = salary;
    	}
    	public Employee(String name, char sex, int age, String job, double salary){
    		this(name, sex, age);//使用前面的构造器，对this的调用必须是构造器的第一个语句。
    		this.job = job;
    		this.salary = salary;
    	}
    	public void getInfo(){
    		System.out.println("name:" + name);
    		System.out.println("sex:" + sex);
    		System.out.println("age:" + age);
    		System.out.println("job:" + job);
    		System.out.println("salary:" + salary);
    		System.out.println("--------------------");
    	}
    }
    ```

    

13. 将对象作为参数传递给方法。

    题目要求：

    (1) 定义一个 Circle 类，包含一个 double 型的 radius 属性代表圆的半径，findArea() 方法返回圆的面积。

    (2) 定义一个类 PassObject，在类中定义一个方法 printAreas()，该方法的定义如下：`public void printAreas(Circle c, int times) //方法签名`

    (3) 在 printAreas 方法中打印输出 1 到 times 之间的每个整数半径值，以及对应的面积。例如，times 为 5，则输出半径 1，2，3，4，5，以及对应的圆面积。

    (4) 在 main 方法中调用 printAreas() 方法，调用完毕后输出当前半径值。程序运行结果如图所示

    <img src="D:\消息记录\TyporaPages\类与对象练习题13.png" style="zoom:33%;" />

    ```java
    public class Chapter7{
    	public static void main(String[] args){
    		Circle m = new Circle(1.0);
    		PassObject m1 = new PassObject();
    		m1.printAreas(m, 5);
    	}
    }
    class Circle{
    	double radius;
    	public Circle(double radius){
    		this.radius = radius;
    	}
    	public double findArea(){
    		return Math.PI * radius * radius;
    	}	
    }
    class PassObject{
    	public void printAreas(Circle c, int times){
    		System.out.println("圆的半径:\t圆的面积:");
    		for(int i = 1; i <= times; i++){
    			c.radius = i;
    			System.out.print(c.radius + "\t\t");
    			System.out.print(c.findArea());
    			System.out.println();
    		}
    		
    	}	
    }
    ```

    

14. 有个人 Tom 设计他的成员变量。成员方法, 可以电脑猜拳电脑每次都会随机生成 0，1，2

    0 表示石头，1 表示剪刀，2 表示布

    并要可以显示 Tom 的输赢次数 (清单)

    <img src="D:\消息记录\TyporaPages\类与对象练习题14.png" style="zoom:33%;" />

```java
import java.util.Scanner;
public class Chapter7{
	public static void main(String[] args){
		Tom m = new Tom();
		m.menu();
	}
}
class Tom{
	public int Guess(){
		return (int) (Math.random() * 3); // 生成范围在 0 到 2 之间的随机整数
	}
	public void menu(){
		int n = 0;
		Scanner myScanner = new Scanner(System.in);
		System.out.println("*******现在进行石头剪刀步游戏：（三局两胜）********");
		for(int i = 0; i < 3; i++){
			System.out.println("请输入石头/剪刀/步，注意：0 表示石头，1 表示剪刀，2 表示布");
			int num1 = myScanner.nextInt();
			int p = Guess();
			if(p == 0 && num1 == 2 || p == 1 && num1 == 0 || p == 2 && num1 == 1){
				n++;
			}
			System.out.println("机器出的是：" + p + "\t您出的是：" + num1);
		}

		System.out.println("三次猜拳，您赢了" + n + "次！");
		if(n >= 2){
			System.out.println("游戏获胜啦！！！");
		}
		else{
			System.out.println("游戏失败。。。");
		}
	}	
}

```
