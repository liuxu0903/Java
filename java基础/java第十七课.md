# 方法递归调用

递归就是方法自己调用自己，每次调用时传入不同的变量，递归有助于编程者解决复杂问题，同时可以让代码变得简洁。

## 递归重要规则

1. 执行一个方法时，就创建一个新的受保护的独立空间（栈空间）。
2. 方法的**局部变量是独立的**，不会相互影响。
3. 如果方法中使用的是**引用类型变量**（比如数组），就会共享该引用类型的数据。
4. 递归必须向退出递归的条件逼近，否则就是无限递归，出现 StackOverflowError。
5. 当一个方法执行完毕，或者遇到 return，就会返回，遵守谁调用就将结果返回给谁，同时当方法执行完毕或者返回时，该方法也就执行完毕。

### 练习题

1. 请使用递归的方式求出**斐波那契** 1,1,2,3,5,8,13... 给你一个整数n，求出它的值是多少。

   ```java
   import java.util.Scanner;
   public class RecursionExercise{
   		public static void main(String[] args){
   			Scanner myScanner = new Scanner(System.in);
   			System.out.println("请输入一个整数：");
   			int n = myScanner.nextInt();
   			if(n < 1){
   				System.out.println("要求输入是大于1的整数！！！");
   			}
   			else{
   				ReExercise obj = new ReExercise();
   				System.out.println("斐波那契的结果为：" + obj.Fib(n));
   			}
   	}
   }
   class ReExercise{
   	public int Fib(int n){
   		if (n == 1 || n == 2){
   			return 1;
   		}
   		else{
   			return Fib(n - 1) + Fib(n - 2);
   		}
   	} 
   }
   ```

2. **猴子吃桃**子问题：有一堆桃子，猴子第一天吃了其中的一半，然后再多吃了一个！以后
   每天猴子都吃其中的一半，然后再多吃一个。当到第10天时，想再吃时（即还没吃）发现只有1个桃子了。问题：最初共多少个桃子?

   ```java
   import java.util.Scanner;
   public class RecursionExercise{
   		public static void main(String[] args){
   			ReExercise obj = new ReExercise();
   			System.out.println("吃到第10天时，最初共有：" + obj.Func(10) + "个桃子。");
   
   	}
   }
   class ReExercise{
   	public int Func(int day){
   		if (day == 1){
   			return 1;
   		}
   		else{
   			return (Func(day - 1) + 1) * 2;
   		}
   	} 
   }
   // 1
   // (1+1)  *2 = 4
   // (4+1)  *2 = 10
   // (10+1) *2 = 22
   ```

3. **迷宫问题：** 小球在左上角出发，到右下角则走出迷宫，其中红色部分均是墙。

   <img src="D:\消息记录\TyporaPages\迷宫.png" style="zoom:25%;" />

   ```java
   import java.util.Scanner;
   public class MiGong{
   		public static void main(String[] args){
   			ReExercise obj = new ReExercise();
   			int[][] Map = new int[8][7];
   			//打印墙
   			for(int i = 0; i < 7; i++){
   				Map[0][i] = 1;
   				Map[7][i] = 1;
   			}
   			for(int i = 0; i < 8; i++){
   				Map[i][0] = 1;
   				Map[i][6] = 1;
   			}
   			Map[3][1] = 1;
   			Map[3][2] = 1;
   			//让老鼠找路
   			obj.FindWay(Map, 1, 1);
   			System.out.println("老鼠找的路径如下：");
   			for(int i = 0; i < Map.length; i++){
   				for(int j = 0; j < Map[i].length; j++){
   					System.out.print(Map[i][j] + " ");
   				}
   				System.out.print("\n");
   			}
   			
   
   	}
   }
   
   //FindWay是找出迷宫路径，找到返回true,否则false
   //i,j是老鼠的位置
   //找路策略：下右上左
   //Map[i][j] = 0表示未走过，1表示障碍物，2表示可以走的位置，3表示已经走过此路不通
   //当Map[6][5] = 2就说明找到通路啦。
   class ReExercise{
   	public boolean FindWay(int Map[][], int i, int j){
   		if(Map[6][5] == 2){
   			return true;
   		}
   		else{
   			if(Map[i][j] == 0){
   				Map[i][j] = 2;
   				if(FindWay(Map, i + 1, j)){
   					return true;	
   				}
   				else if(FindWay(Map, i, j + 1)){
   					return true;
   				}
   				else if(FindWay(Map, i - 1, j)){
   					return true;
   				}
   				else if(FindWay(Map, i, j - 1)){
   					return true;
   				}
   				else{
   					Map[i][j] = 3;
   					return false;
   				}
   			}
   			else{//Map[i][j] = 1,2,3都是不能走的位置。
   				return false;
   			}
   
   		}
   	} 
   }
   ```


4. **汉诺塔**

   ```java
   import java.util.Scanner;
   public class HanoiTower{
   		public static void main(String[] args){
   			Tower tower = new Tower();
   			tower.move(5, 'A', 'B', 'C');
   		}
   	}
   class Tower{
   	public void move(int num, char a, char b, char c){ //num 表示要移动的个数，a，b，c分别表示A塔，B塔，C塔
   		if(num == 1){
   			System.out.println(a + " --> " + c);
   		}
   		else{ //如果有多个盘，可以看成两个 ，最下面的和上面的所有盘(num-1)//(1)先移动上面所有的盘到 b，借助c
   			move(num - 1, a, c, b); //先移动上面所有的盘到 b，借助c
   			System.out.println(a + " --> " + c); //把最下面的这个盘，移动到c
   			move(num - 1, b, a, c); //再把 b塔的所有盘，移动到c，借助a
   		}
   	}
   }
   ```

5. **八皇后**

   ```java
   public class EightQueens {
    
       //定义max表示有多少个皇后
       int max = 8;
       int num = 0;//解法个数
       
       //定义数组array,保存皇后放置位置的结果，比如 arr = {0,4,7,5,2,6,1,3}
       int [] array = new int[max];
       public static void main(String[] args) {
           //测试8皇后
           EightQueens queen8 = new EightQueens();
           queen8.check(0);//从第一个皇后开始放
           System.out.println("一共有"+queen8.num+"解法");
       }
    
       /**
        * 编写一个方法，放置第n个皇后
        *  check的每一次递归时都有一个for循环，因此会有回溯
        * @param n
        */
       private void check(int n){
           if (n == max){
               //n=8 相当于该放第九个皇后了（其实一共就八个皇后），有结果了，输出
               print();
               return;
           }
    
           //依次放入皇后，并判断是否冲突
           for (int i=0;i<max;i++){
               //先把当前皇后n，放到该行的第一列
               array[n]=i;
               //判断当放置第n个皇后到i列时是否冲突
               if (judge(n)){
                   //不冲突，接着放N+1，即开始递归
                   check(n+1);
               }
               //如果冲突就继续执行array[n]=i,在此之前i已经++了；
               //即将第n个皇后在本行后移一位
           }
       }
    
       /**
        *当我们放置第n个皇后，就去检测该皇后是否和前面已经摆放的皇后冲突
        * @param n 表示第n个皇后
        * @return
        */
       private boolean judge(int n){
           for (int i = 0; i < n; i++) {
               //判断第n个皇后是否和前面n-1个皇后在同一列 || 是否同一斜线
               if (array[i]==array[n]||Math.abs(n-i)==Math.abs(array[n]-array[i])){
                   return false;
               }
           }
           return true;
       }
    
    
       //写一个方法，可以将皇后摆放的位置输出
       private void print (){
           num++;
           for (int i = 0; i < array.length; i++) {
               System.out.print(array[i]+ " ");
           }
           System.out.println();
       }
   }
    
   ```

   [八皇后参考文章](https://blog.csdn.net/m0_55884707/article/details/135568619?ops_request_misc=&request_id=&biz_id=102&utm_term=%E5%85%AB%E7%9A%87%E5%90%8E%E9%97%AE%E9%A2%98%E5%9B%9E%E6%BA%AFjava&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~sobaiduweb~default-0-135568619.nonecase&spm=1018.2226.3001.4450)