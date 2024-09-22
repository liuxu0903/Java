# 房屋出租系统

- 实现基于文本界面的《房屋出租软件》
- 能够实现对房屋信息的添加、修改和删除 (用数组实现) 并能够打印房屋明细表。

## 界面

### 主菜单

![](D:\消息记录\TyporaPages\项目界面-1720495497455-1.png)

### 新增房源

![](D:\消息记录\TyporaPages\新增房源-1720796341498-1.png)

### 查找房源 

![](D:\消息记录\TyporaPages\查找房源-1720796418041-3.png)

### 删除房源

![](D:\消息记录\TyporaPages\删除房源-1720796455440-5.png)

### 修改房源

如果不希望修改某个信息，则直接回车即可。

![](D:\消息记录\TyporaPages\修改房源-1720796475846-7.png)

### 房屋列表

![](D:\消息记录\TyporaPages\房屋列表-1720796556157-9.png)

### 退出系统

![](D:\消息记录\TyporaPages\退出系统-1720796591285-11.png)

## 程序框架图

![](D:\消息记录\TyporaPages\界面.png)

## 准备工具类Utility，提高开发效率
在实际开发中，公司都会提供相应的工具类和开发库，可以提高开发效率，程序员也需要能够看懂别人写的代码，并能够正确的调用。

## 结构图

![](D:\消息记录\TyporaPages\结构图-1720940473326-14.png)

***HouseRentApp.java：***

```java
package com.hspedu.houserent;

import com.hspedu.houserent.view.HouseView;

public class HouseRentApp {
    //创建HouseView对象,并且显示主菜单,是整个程序的入口
    public static void main(String[] args) {
        new HouseView().mainMenu();
        System.out.println("================您退出了房屋出租系统===============");
    }
}
```

***House.java：***

```java
package com.hspedu.houserent.domain;

/**
 * House的对象表示一个房屋信息
 */
public class House {
    //编号    房主  电话  地址  租金   状态(未出租/已出租)
    private int id;
    private String name;
    private String phone;
    private String address;
    private int rent;
    private String state;

    public House(int id, String name, String phone, String address, int rent, String state) {
        this.id = id;
        this.name = name;
        this.phone = phone;
        this.address = address;
        this.rent = rent;
        this.state = state;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public int getRent() {
        return rent;
    }

    public void setRent(int rent) {
        this.rent = rent;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }
    //为了方便输出对象信息，我们实现toString方法
    @Override
    public String toString() {
        return  id +
                "\t\t" + name +
                "\t\t" + phone +
                "\t\t" + address +
                "\t\t" + rent +
                "\t\t" + state ;
    }
}
```

***HouseService.java：***

```java
package com.hspedu.houserent.service;

import com.hspedu.houserent.domain.House;

/**
 * HouseService.java <=> 类[业务层]
 * 定义House[]，保存House对象
 * 1. 响应HouseView的调用
 * 2. 完成对房屋信息的各种操作(增删改査c[create]r[read]u[update]d[delete])
 */
public class HouseService {
    private House[] houses;//保存House对象
    private int houseNum = 1;//记录当前有多少个房屋信息
    private int idCounter = 1;//记录当前的id增长到哪个值
    //构造器
    public HouseService(int size){
        houses = new House[size];//当创建HouseService对象，指定数组大小。
        //初始化一个House对象
        houses[0] = new House(1,"Jack","123456","外星球",3000,"未出租");

    }
    //list方法，返回houses
    public House[] list(){
        return houses;
    }
    //add方法，添加新对象，返回boolean值
    public boolean add(House newHouse){
        //判断是否还可以继续添加(我们暂时不考虑数组扩容的问题)
    if(houseNum == houses.length){
        System.out.println("数组已满不能再添加了");
        return false;
    }
    houses[houseNum++] = newHouse;
    //需要设计id自增长机制,然后更新newHouse的id
    newHouse.setId(++idCounter);
    return true;
    }
    //del方法，删除一个房屋信息
    public boolean del(int delId){
        //应当先找到要删除的房屋信息对应的下标
        //下标和房屋编号不是一回事
        int index = -1;
        for(int i = 0; i < houseNum; i++){
            if(delId == houses[i].getId()){//要删除的房屋（id），是数组下标为i的元素
                index = i;//使用index记录i
            }
        }
        if(index == -1){//说明delId在数组中不存在
            return false;
        }
        //如果找到
        for(int i = index; i < houseNum - 1; i++){
            houses[i] = houses[i + 1];
        }
        houses[--houseNum] = null;//把当前存在的房屋信息的最后一个 设置null
        return true;
    }
    //find方法，找到房屋信息
    public int find(int findId){
        int index = -1;
        for(int i = 0; i < houseNum; i++){
            if(findId == houses[i].getId()){//要查找的房屋（id），是数组下标为i的元素
                index = i;//使用index记录i
            }
        }
        //如果找到
        return index;
    }
}
```

***HouseView.java：***

```java
package com.hspedu.houserent.view;

import com.hspedu.houserent.domain.House;
import com.hspedu.houserent.service.HouseService;
import com.hspedu.houserent.utils.Utility;

/**
 * 1.显示界面
 * 2.接收用户的输入
 * 3.调用HouseService完成对房屋信息的各种操作
 */

public class HouseView {
    private boolean loop = true;//控制显示菜单
    private char key = ' ';//接收用户选择
    private HouseService houseService = new HouseService(10);//设置数组的大小为10

    //修改房屋
    public void updateHouse(){
        System.out.println("\n==================修改房屋信息=================");
        System.out.println("请选择待修改房屋编号(-1退出)：");
        int updateId = Utility.readInt();
        if(updateId == -1){
            System.out.println("===============你放弃修改房屋信息===============");
            return;
        }
        House[] houses = houseService.list();//得到所有房屋
        //根据输入得到updateId查找对象
        int findResult = houseService.find(updateId);
        if(findResult == -1){
            System.out.println("修改房屋的编号不存在...");
            return;
        }
        System.out.print("姓名(" + houses[findResult].getName() + ")：");
        String name = Utility.readString(8,"");//这里如果用户直接回车表示不修改该信息
        if(name != ""){
            houses[findResult].setName(name);
        }
        System.out.print("电话(" + houses[findResult].getPhone()+ ")：");
        String phone = Utility.readString(12,"");
        if(phone != ""){
            houses[findResult].setPhone(phone);
        }
        System.out.print("地址(" + houses[findResult].getAddress()+ ")：");
        String address = Utility.readString(18,"");
        if(address != ""){
            houses[findResult].setAddress(address);
        }
        System.out.print("租金(" + houses[findResult].getRent()+ ")：");
        int rent = Utility.readInt(-1);
        if(rent != -1){
            houses[findResult].setRent(rent);
        }
        System.out.print ("状态(" + houses[findResult].getState() + ")：");
        String state = Utility.readString(8,"");
        if(state != ""){
            houses[findResult].setState(state);
        }
        System.out.println("=====================修改完成====================");
    }
    //查找房屋
    public void findHouse(){
        System.out.println("\n=====================查找房屋====================");
        System.out.println("请输入你要查找id：");
        int findId = Utility.readInt();
        House[] houses = houseService.list();//得到所有房屋
        int index = houseService.find((findId));
        if(index != - 1){
            System.out.println(houses[index].toString());
        }else {
            System.out.println("===================没有该查找房屋==================");
        }
    }
    //完成退出确认
    public void exit(){
        char choice = Utility.readConfirmSelection();
        if (choice == 'Y'){
            loop = false;
        }
    }
    //编写addHouse()接收输入，创建House对象，调用add方法
    public void addHouse(){
        System.out.println("\n=====================添加房屋====================");
        System.out.println("姓名： ");
        String name = Utility.readString(8);
        System.out.println("电话： ");
        String phone = Utility.readString(12);
        System.out.println("地址： ");
        String address  = Utility.readString(16);
        System.out.println("月租： ");
        int rent = Utility.readInt();
        System.out.println("状态(出租/已出租)： ");
        String state = Utility.readString(3);
        House newHouse = new House(0, name, phone, address, rent, state);
       if(houseService.add(newHouse)){
           System.out.println("==================添加房屋成功！=================");
       }else{
           System.out.println("==================添加房屋失败！=================");

       }
    }
    //编写delHouse()接收输入的id,调用Service 的del方法
    public void delHouse(){
        System.out.println("\n=====================删除房屋====================");
        System.out.println("请选择待删除房屋编号(-1退出)");
        int delId = Utility.readInt();
        if(delId == -1){
            System.out.println("==================放弃删除房屋信息=================");
            return;
        }
        //注意该方法本身就有循环判断的逻辑,必须输出Y/N
        char choice =  Utility.readConfirmSelection();
        if(choice == 'Y'){
            if(houseService.del(delId)){
                System.out.println("==================删除房屋信息成功！================");
            }else {
                System.out.println("===============房屋编号不存在，删除失败。=============");
            }

        }else{
            System.out.println("==================放弃删除房屋信息=================");
        }


    }


    //编写listHouses()显示房屋列表
    public void listHouse(){
        System.out.println("\n=====================房屋列表====================");
        System.out.println("编号\t\t房主\t\t\t电话\t\t\t地址\t\t\t月租\t\t\t状态（未出租/已出租）");
        House[] houses = houseService.list();//得到所有房屋
        for(int i = 0; i < houses.length; i++){
            if(houses[i] == null){
                break;
            }
            System.out.println(houses[i].toString());
        }
        System.out.println("=====================房屋列表完成====================");
    }
    //显示主菜单
    public void mainMenu(){
        do{
            System.out.println("=====================房屋出租系统====================");
            System.out.println("\t\t\t\t1 新 增 房 屋");
            System.out.println("\t\t\t\t2 查 找 房 屋");
            System.out.println("\t\t\t\t3 删 除 房 屋");
            System.out.println("\t\t\t\t4 修 改 房 屋 信 息");
            System.out.println("\t\t\t\t5 房 屋 列 表");
            System.out.println("\t\t\t\t6 退      出");
            System.out.println("请输入你的选择（1-6）：");
            key = Utility.readChar();
            switch (key){
                case '1':
                    addHouse();
                    break;
                case '2':
                    findHouse();
                    break;
                case '3':
                    delHouse();
                    break;
                case '4':
                    updateHouse();
                    break;
                case '5':
                    listHouse();
                    break;
                case '6':
                    exit();
                    break;
            }

        }while(loop);
    }
}
```

***Utility.java：***

```java
package com.hspedu.houserent.utils;


/**
 工具类的作用:
 处理各种情况的用户输入，并且能够按照程序员的需求，得到用户的控制台输入。
 */

        import java.util.*;
/**


 */
public class Utility {
    //静态属性。。。
    private static Scanner scanner = new Scanner(System.in);


    /**
     * 功能：读取键盘输入的一个菜单选项，值：1——5的范围
     * @return 1——5
     */
    public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false);//包含一个字符的字符串
            c = str.charAt(0);//将字符串转换成字符char类型
            if (c != '1' && c != '2' &&
                    c != '3' && c != '4' && c != '5') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }

    /**
     * 功能：读取键盘输入的一个字符
     * @return 一个字符
     */
    public static char readChar() {
        String str = readKeyBoard(1, false);//就是一个字符
        return str.charAt(0);
    }
    /**
     * 功能：读取键盘输入的一个字符，如果直接按回车，则返回指定的默认值；否则返回输入的那个字符
     * @param defaultValue 指定的默认值
     * @return 默认值或输入的字符
     */

    public static char readChar(char defaultValue) {
        String str = readKeyBoard(1, true);//要么是空字符串，要么是一个字符
        return (str.length() == 0) ? defaultValue : str.charAt(0);
    }

    /**
     * 功能：读取键盘输入的整型，长度小于2位
     * @return 整数
     */
    public static int readInt() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, false);//一个整数，长度<=10位
            try {
                n = Integer.parseInt(str);//将字符串转换成整数
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }
    /**
     * 功能：读取键盘输入的 整数或默认值，如果直接回车，则返回默认值，否则返回输入的整数
     * @param defaultValue 指定的默认值
     * @return 整数或默认值
     */
    public static int readInt(int defaultValue) {
        int n;
        for (; ; ) {
            String str = readKeyBoard(10, true);
            if (str.equals("")) {
                return defaultValue;
            }

            //异常处理...
            try {
                n = Integer.parseInt(str);
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串
     * @param limit 限制的长度
     * @return 指定长度的字符串
     */

    public static String readString(int limit) {
        return readKeyBoard(limit, false);
    }

    /**
     * 功能：读取键盘输入的指定长度的字符串或默认值，如果直接回车，返回默认值，否则返回字符串
     * @param limit 限制的长度
     * @param defaultValue 指定的默认值
     * @return 指定长度的字符串
     */

    public static String readString(int limit, String defaultValue) {
        String str = readKeyBoard(limit, true);
        return str.equals("")? defaultValue : str;
    }


    /**
     * 功能：读取键盘输入的确认选项，Y或N
     * 将小的功能，封装到一个方法中.
     * @return Y或N
     */
    public static char readConfirmSelection() {
        System.out.println("请输入你的选择(Y/N): 请小心选择");
        char c;
        for (; ; ) {//无限循环
            //在这里，将接受到字符，转成了大写字母
            //y => Y n=>N
            String str = readKeyBoard(1, false).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

    /**
     * 功能： 读取一个字符串
     * @param limit 读取的长度
     * @param blankReturn 如果为true ,表示 可以读空字符串。
     * 					  如果为false表示 不能读空字符串。
     *
     *	如果输入为空，或者输入大于limit的长度，就会提示重新输入。
     * @return
     */
    private static String readKeyBoard(int limit, boolean blankReturn) {

        //定义了字符串
        String line = "";

        //scanner.hasNextLine() 判断有没有下一行
        while (scanner.hasNextLine()) {
            line = scanner.nextLine();//读取这一行

            //如果line.length=0, 即用户没有输入任何内容，直接回车
            if (line.length() == 0) {
                if (blankReturn) return line;//如果blankReturn=true,可以返回空串
                else continue; //如果blankReturn=false,不接受空串，必须输入内容
            }

            //如果用户输入的内容大于了 limit，就提示重写输入
            //如果用户如的内容 >0 <= limit ,我就接受
            if (line.length() < 1 || line.length() > limit) {
                System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");
                continue;
            }
            break;
        }

        return line;
    }
}
```