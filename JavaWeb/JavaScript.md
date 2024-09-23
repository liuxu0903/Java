# 一 什么是 JavaScript?



- JavaScript (简称: JS) 是一门跨平台、面向对象的脚本语言 (**脚本语言**是不需要编译，直接通过浏览器的解释就可以运行)。是用来控制网页行为的，它能使网页可交互。
- JavaScript 和 Java 是完全不同的语言，不论是概念还是设计。但是基础语法类似。
- JavaScript 在1995 年由 Brendan Eich 发明，并于1997 年成为 ECMA 标准。
- ECMAScript6(ES6) 是最新的 JavaScript 版本(发布于2015年)。

# JS 引入方式

1. **内部脚本**: 将 JS 代码定义在 HTML 页面中。

   - JavaScript 代码必须位于`<script></script>`标签之间。

   - 在HTML文档中，可以在任意地方，放置任意数量的`<script>`。

   - 一般会把脚本置于`<body>`元素的底部，可改善显示速度。

     ```html
     <script>
     	alert("Hello javaScript")
     </script>
     ```

2. **外部脚本:** 将 JS 代码定义在外部 JS 文件中，然后引入到 HTML 页面中。

   - 外部 JS 文件中，只包含 JS 代码，不包含`<script>`标签。

   - `<script>` 标签不能自闭合。

     上述例子更改为：

     ```javascript
     <script src= "js/demo.js"></script>
     ```

     ```javascript
     alert("Hello javaScript")
     ```

     

# JS 基础语法

1. **书写语法**

   - 区分大小写: 与 Java 一样，变量名、函数名以及其他一切东西都是区分大小写的。
   - 每行结尾的分号可有可无
   - 注释:
     单行注释: `// 注释内容`
     多行注释: `/* 注释内容 */` 
   - 大括号表示代码块

2. **输出语句**

   - 使用 `window.alert()` 写入警告框
   - 使用 `document.write()` 写入 HTML 输出
   - 使用 `console.log()` 写入浏览器控制台

3. **变量**

   - JavaScript 中用 **var 关键字** (variable 的缩写) 来声明变量。

   - JavaScript 是一门弱类型语言，变量可以存放不同类型的值。

     - 特点1：var 作用于比较大，是全局变量。

       （**let 是局部变量，不能重复定义**）(**const 是常量，不能被改变**)

     - 特点2：**var 可以重复定义**的，后面定义的会把前面定义的覆盖。

     ```javascript
     var a = 20;
     
     a = "张三";
     ```

   - 变量名需要遵循如下规则：

     - 组成字符可以是任何字母、数字、下划线 (_) 或美元符号 ($)
     - 数字不能开头
     - 建议使用驼峰命名

4. **数据类型、运算符、流程控制语句**

   

