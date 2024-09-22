# 面向对象的三大特征

## 封装

封装(encapsulation)就是把抽象出的数据[==属性==]和对数据的操作[==方法==]封装在一起,数据被保护在内部,程序的其它部分只有通过被授权的操作[==方法==],才能对数据进行操作。

### 封装的理解和好处

1. 隐藏实现细节: 方法(连接数据库) <== 调用(传入参数)

2. 可以对数据进行验证，保证安全合理

   如: Person {name, age}

   ```java
   Person p = new Person();
   p.name = "jack";
   p.age = 1200;
   ```

   ### 封装的实现步骤

   1. 将属性进行私有化 private 【不能直接修改属性】

   2. 提供一个公共的 (public)set方法，用于对属性判断并赋值

      ```java
      public void setXxx(类型 参数名){//Xxx 表示某个属性
          //加入数据验证的业务逻辑
          属性 = 参数名;
      }
      ```

   3. 提供一个公共的(public)get方法，用于获取属性的值

      ```java
      public 数据类型 getXxx(){ //权限判断,Xxx 某个属性
          return xx;
      }
      ```

   **案例:**

   请大家看一个小程序(com.hspedu.encap: Encapsulation01.java), 不能随便查看人的年龄, 工资等隐私，并对设置的年龄进行合理的验证。年龄合理就设置，否则给默认年龄, 必须在 1-120, 年龄， 工资不能直接査看 ， name 的长度在 2-6字符之间

   ```java
   package com.hspedu.encap;
   
   public class Encapsulation01 {
       public static void main(String[] args) {
           Person person = new Person();
           person.setName("Jack");
           person.setAge(30);
           person.setSalary(30000);
           System.out.println(person.info());
       }
   }
   class Person{
       public String name;
       private int age;
       private double salary;
   
       //使用快捷键 Alt + Insert
       //根据要求完善代码
       public String getName() {
           return name;
       }
       public void setName(String name) {
           //加入对数据的校验
           if(name.length() >= 2 && name.length() <= 6){
               this.name = name;
           }
           else{
               System.out.println("你设置的名字不对，需要在（2-6）个字符，给默认名字无名氏");
               this.name = "无名氏";
           }
       }
       public int getAge() {
           return age;
       }
       public void setAge(int age) {
           if(age >= 1 && age <= 120){
               this.age = age;
           }
           else {
               System.out.println("你设置的年龄不对，需要在（1-120），给默认年龄18");
               this.age = 18;
           }
       }
       public double getSalary() {
           //可以这里增加当前对象的权限判断
           return salary;
       }
       public void setSalary(double salary) {
           this.salary = salary;
       }
       public String info(){
           return "信息为: name = " + name + "\tage = " + age + "\t薪水 = " + salary;
       }
   
   }
   ```

   ### 将构造器和 setXxx 结合

   继续上面的案例:

   ```java
   package com.hspedu.encap;
   
   public class Encapsulation01 {
       public static void main(String[] args) {
           Person person = new Person();
           person.setName("Jack");
           person.setAge(30);
           person.setSalary(30000);
           System.out.println(person.info());
           
           System.out.println("将构造器和setXxx结合后：");
           Person smith = new Person("Smith", 1000, 20000);
           System.out.println(smith.info());
       }
   }
   class Person{
       public String name;
       private int age;
       private double salary;
   
       //使用快捷键 Alt + Insert
   
       public Person() {
       }
       //有3个属性的构造器
       public Person(String name, int age, double salary) {
   //        this.name = name;
   //        this.age = age;
   //        this.salary = salary;
           //可以将set方法写在构造器中，这样仍然可以验证
           setName(name);
           setAge(age);
           setSalary(salary);
       }
   
       //自己写setXxx和getXxx
       //根据要求完善代码
       public String getName() {
           return name;
       }
       public void setName(String name) {
           //加入对数据的校验
           if(name.length() >= 2 && name.length() <= 6){
               this.name = name;
           }
           else{
               System.out.println("你设置的名字不对，需要在（2-6）个字符，给默认名字无名氏");
               this.name = "无名氏";
           }
       }
       public int getAge() {
           return age;
       }
       public void setAge(int age) {
           if(age >= 1 && age <= 120){
               this.age = age;
           }
           else {
               System.out.println("你设置的年龄不对，需要在（1-120），给默认年龄18");
               this.age = 18;
           }
       }
       public double getSalary() {
           //可以这里增加当前对象的权限判断
           return salary;
       }
       public void setSalary(double salary) {
           this.salary = salary;
       }
       public String info(){
           return "信息为: name = " + name + "\tage = " + age + "\t薪水 = " + salary;
       }
   
   }
   ```

### 课堂练习

com.hspedu.encap 包:

AccountTest.java 和 Account.java 创建程序, 在其中定义两个类: Account 和 AccountTest 类体会 Java 的封装性。

1. Account类要求具有属性: 姓名 (长度为2位3位或4位)、余额(必须 > 20)、密码(必须是六位)，如果不满足，则给出提示信息，并给默认值
2. 通过 setXxx 的方法给 Account 的属性赋值。
3. 在 AccountTest 中测试

**Account 类:**

```java
package com.hspedu.encap;

public class Account{
   public String name;
   private double balance;
   private String password;

    public Account() {
    }

    public Account(String name, double balance, String password) {
        setName(name);
        setBalance(balance);
        setPassword(password);
    }

    public String getName() {
        return name;
    }
    public void setName(String name) {
        if(name.length() == 2 || name.length() == 3 || name.length() == 4){
            this.name = name;
        }
        else{
            System.out.println("你设置的名字不对，长度为2位或3位或4位，给默认名字无名氏");
            this.name = "无名氏";
        }
    }
    public double getBalance() {
            return balance;
    }
    public void setBalance(double balance) {
        if(balance > 20){
            this.balance = balance;
        }
        else{
            System.out.println("余额要大于20，默认为0");
        }

    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        if(password.length() == 6){
            this.password = password;
        }
        else{
            System.out.println("你设置的密码长度不对，长度为6位，给默认密码000000");
            this.password = "000000";
        }
    }
    public void Info(){
        //显示账号信息
        System.out.println("账号信息为: 姓名： " + name + "\t余额： " + balance + "\t密码： " + password);
        //权限查看
//        if(name == "Jack"){
//            System.out.println("账号信息为: 姓名： " + name + "\t余额： " + balance + "\t密码： " + password);
//        }
//        else{
//            System.out.println("你无权查看！");
//        }
    }
}
```

**AccountTest 类:**

```java
package com.hspedu.encap;

public class AccountTest {
    public static void main(String[] args){
        //创建Account
        Account account = new Account();
        account.setName("Jack");
        account.setBalance(30);
        account.setPassword("123456");
        
        account.Info();
    }

}
```

