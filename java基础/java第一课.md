### 什么是程序

程序：计算机执行***某些操作***或解决***某个问题***而编写的一系列==有序指令集合==。

### Java 诞生

第一个版本诞生在1995年，java的创始人是 James Gosling

### Java 重要特点

1. Java语言是***面向对象***的(oop)

2. Java语言是健壮的。Java的强类型机制、异常处理、垃圾的自动收集等是Java程序健壮性的重要保证。

3. Java语言是***跨平台***性的。

4. Java语言是***解释型***的。
   解释性语言: javascript，PHP java

   编译性语言: c/c++
   **区别是:** 解释性语言，编译后的代码，不能直接被机器执行,需要解释器来执行,编译性语言编译后的代码，可以直接被机器执行，c/c++

### Java 运行机制及运行过程

Java核心机制 - ***Java虛拟机*** [ ==Jvm== java virtual machine ]

1. JVM是一个虚拟的计算机，具有指令集并使用不同的存储区域。负责执行指令管理数据、内存、寄存器，***包含在 ==JDK==*** 中
2. 对于不同的平台，有不同的虚拟机。
3. Java虚拟机机制屏蔽了底层运行平台的差别，实现了“一次编译，到处运行“

### 什么是 JDK ，JRE

1. **JDK 基本介绍**（开发者）

   JDK的全称(Java Development Kit ==Java开发工具包==)

   ***JDK=JRE + java的开发工具 [java,javac,javadoc,javap等]***

   JDK是提供给Java开发人员使用的，其中包含了java的开发工具，也包括了JRE.所以安装了JDK，就不用在单独安装JRE了。

2. **JRE 基本介绍** （使用者）
   JRE(ava Runtime EnvironmentJava运行环境)

   ***JRE= JVM + Java的核心类库[类]***

   包括Java虛拟机(JVM Java Virtual Machine)和Java程序所需的核心类库等，如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。 

### 什么是编译

1. 有了java**源文件**（.java），通过编译器将其编译成JVM可以识别的**字节码文件**（.class）
2. 在该源文件目录下，通过javac编译工具对Hello.java文件进行编译。
3. 如果程序没有错误，没有任何提示，但在当前目录下会出现一个Hello.class文件，
   该文件称为字节码文件，也是可以执行的java的程序。

### 什么是运行

- 什么是运行
  1. 有了可执行的java程序(Hello.class字节码文件)
  2. 通过运行工具java.exe对字节码文件进行执行,本质就是.class装载到jvm 机执行
- java程序开发注意事项
  对修改后的Hello.iava源文件需要重新编译，生成新的class文件后，再进行执行,才能生效