---
layout:     post
title:      "JavaScript学习笔记"
subtitle:   " JavaScript，通常缩写为 JS，是一种高级的，不进行预编译的，从上到下逐行执行的编程语言。 "
date:       2019-07-28 11:50:46
header-img: ""
author:     "Jerry"
catalog: true
tags:
    - 前端
---

JavaScript 是一门基于原型、函数先行的语言，是一门多范式的语言，它支持面向对象编程，命令式编程，以及函数式编程。它提供语法来操控文本、数组、日期以及正则表达式等，不支持 I/O，比如网络、存储和图形等，但这些都可以由它的宿主环境提供支持。
<!-- more -->

# 基础

## 高级运算符

+ **求余** x = y % 2
+ **累加** 让 a = 5
- c = a++, 结果: c = 5 和 a = 6
- c = ++a, 结果: c = 6 和 a = 6

## JavaScript 的组成
**ECMAScript**：JavaScript 的语法标准。
**DOM**：JavaScript 操作网页上的元素的 API。
**BOM**：JavaScript 操作浏览器的部分功能的 API。

## 变量
- **动态类型**
JavaScript 是一种“动态类型语言”，这意味着不同于其他一些语言(如 C、Java)，你不需要指定变量将包含什么数据类型（例如 number 或 string）,通通用 var 关键字声明就是了。

## 数组
### 操作数组
- 获取数组长度
   使用`length`方法获取
- 利用分隔符将字符串转化为数组
 使用`split("x")`方法
 例如：`"1:2:3:4".split(":")    // returns ["1", "2", "3", "4"]`
 - 将数组转化为字符串
 使用`join("x")`方法
 例如：`["1", "2", "3", "4"].join(":"); // returns "1:2:3:4"`
 >注：我们同样可以使用 toString() 方法将数组转换为字符串，但是 join() 方法可以指定不同的分隔符，而 toString() 方法只能是逗号。

 - 添加数组项
 使用`push()`方法
 - 删除数组项
 使用`pop()`删除数组最后一个元素

 >unshift() 和 shift() 从功能上与 push() 和 pop() 完全相同，只是它们分别作用于数组的开始，而不是结尾。

## 字符串
### 操作字符串
- 连接字符串  
 通过 “+” 连接字符串
- 字符串转换
 1. 通过 toString 方法把数字转换成字符串
 ```javascript
 var myNum = 123;
var myString = myNum.toString();
typeof myString;
 ```
数值类型的 toString() ,可以携带一个参数,输出对应进制的值。比如：
```javascript
var num = 16;
console.log(num.toString());  //"16" 默认是10进制
console.log(num.toString(10));//"16"
console.log(num.toString(2)); //"10000"
console.log(num.toString(8)); //"20"
console.log(num.toString(16));//"10"
```
>注：因为有的值没有 toString() 方法，所以需要用 String(),比如 null 和 undefined。


2. 通过 `Number `对象把传递给它的字符串类型的数字转换为数字。
```javascript
var myString = '123';
var myNum = Number(myString);
typeof myNum;
```
3. `parseInt() `把字符串转换成整数。

```javascript
var num1 = parseInt("12.3abc");  
num1; //返回 12，如果第一个字符是数字会解析知道遇到非数字结束,只取整，不是约等于

var num2 = parseInt("abc123");  
num2; //返回 NaN，如果第一个字符不是数字或者符号就返回 NaN

var num3 = parseInt(""); 
num3;       // 空字符串返回 NaN，但是 Number("")返回 0

var num4 = parseInt("520");
num4;      //返回 520

var num5 = parseInt("0xA"); 
num5;  //返回 10
```
4. `parseFloat()`把字符串转换成浮点数。写法和`parseInt()`相似，主要有以下几个不同点：
- `parseFloat`不支持第二个参数，只能解析 10 进制数
- 如果解析的内容里只有整数，解析成整数


- 在字符串中查找子字符串并提取它
1. 使用`indexof("x")`方法
最详细的写法是**str.indexOf(searchValue, fromIndex);**
str 指的是我们需要查的较长的字符串，searchValue 表示我们指定的较小的字符串，fromIndex 表示调用该方法的字符串中开始查找的位置，是一个可选的任意整数值，也可以不写，默认是 0 表示从头开始查，fromIndex < 0 和 fromIndex = 0 是一样的效果，表示从头开始查找整个字符串。
```javascript
"Blue Sky".indexOf("Blue");     // returns  0
"Blue Sky".indexOf("", 0);      // returns  0
```
2. 使用`slice(strat，end)`方法
第一个参数 start 是开始提取的字符位置，第二个参数 end 是提取的最后一个字符的后一个位置。
例如：`"Blue Sky".slice(0,3); // returns "Blu"`
还可以省略第一个参数  
`"Blue Sky".slice(2); // returns "ue Sky"`
- 转换大小写
字符串方法 `toLowerCase()` 和` toUpperCase()` 字符串并将所有字符分别转换为小写或大写。
- 替换字符串
使用`replace()`方法
```javascript
var string = "I like study";
string.replace("study","sleep"); // returns "I like sleep"
```
## 函数

### 函数声明和函数表达式的区别
- 函数声明
```javascript
//此处的代码执行没有问题，JavaScript解析器首先会把当前作用域的函数声明提前到整个作用域的最前面。
    f(2,3);
    function f(a,b) {
        console.log(a+b);
    }
```
- 函数表达式
```javascript
//报错：f is not a function
//这是因为函数表达式，如同定义其它基本类型的变量一样，只在执行到某一句时也会对其进行解析

    f(2,3);
    var f = function(a,b){
    console.log(a+b);
    }
```

### 在 JavaScript 中没有重载

```javascript
function f(a,b) {
       return a + b;
}
function f(a,b,c) {
       return a + b + c;
}
var result = f(5,6); 
result;// returns NaN
```
上述代码中三个参数的 f 把两个参数的 f 覆盖，调用的是三个参数的 f，最后执行结果为 NaN。而不是其他语言中的 5。
### 匿名函数
匿名函数就是没有命名的函数，一般用在绑定事件的时候。
```javascript
var myButton = document.querySelector('button');

myButton.onclick = function() {
  alert('hello');
}
```
>注：将匿名函数分配为变量的值，也就是我们前面所讲的函数表达式创建函数。一般来说，创建功能，我们使用函数声明来创建函数。使用匿名函数来运行负载的代码以响应事件触发（如点击按钮） ，使用事件处理程序。
>

### 自调用函数
匿名函数不能通过直接调用来执行，因此可以通过匿名函数的自调用的方式来执行。
```javascript
(function () {
  alert('hello');
})();
```
### 输入函数
`prompt("请输入")`
### 输出函数
`document.write()`

## 对象
什么是对象？男朋友？女朋友？这是你以为的对象？当然这可能是我们大多数人生活中对于对象最直观的理解。

而在 JavaScript 中所有事物都是对象：字符串，数组，日期等等。我们甚至可以自己创建对象，将相关的函数和变量封装打包成便捷的数据容器。另外值得注意的是 JavaScript 是一门基于对象的语言。

在 JavaScript 中对象是拥有属性和方法的数据。
### 属性和方法
属性是与对象相关的值，也可以理解为特征。方法是能够在对象上执行的动作，也可以理解为行为。

举个例子：一辆汽车就是现实生活中的对象，它的名字，它的颜色，它的价格等特征就是汽车对象的属性。它能够启动，驾驶，加速，刹车等行为就是汽车对象的方法。

### JSON
- JSON 是一种纯数据格式,它只包含属性,没有方法。
- JSON 的属性必须通过双引号引起来。
- JSON 要求有两头的 { } 来使其合法。

尽管 JSON 是 JavaScript 的一个子集，但 JSON 是独立于语言的文本格式，并且采用了类似于 C 语言家族的一些习惯。

JSON 数据格式与语言无关，脱胎于 JavaScript，但当前很多编程语言都支持 JSON 格式数据的生成和解析。

### 内置对象

#### Array对象
常用属性
- length  获取数组长度

常用方法
- `concat()方法`用于连接两个或多个数组，并返回结果。栗子:
```javascript
var a = [1,2,3];
var b = [4,5,6];
var c =["one","two","three"];
console.log(a.concat(b,c)); //打印结果为：[1, 2, 3, 4, 5, 6, "one", "two", "three"]
```
- `join()方法`将数组转换成字符串
- `pop()方法`删除并返回数组的最后一个元素
- `push()方法`向数组的末尾添加一个或更多元素，并返回新的长度。
- `everse() 方法`颠倒数组的顺序。
- `shift() 方法`删除并返回数组的第一个元素。
- `unshift() 方法`向数组的开头添加一个或更多元素，并返回新的长度。
- `slice() 方法`从某个已有的数组返回选定的元素。
```javascript
x.slice(start,end);
//strat 值是必需的，规定从何处开始选取。
//end 值可选，规定从何处结束选取，如果没有设置，默认为从 start 开始选取到数组后面的所有元素。
```
- `splice(start,deleteCount,options) 方法`删除或替换当前数组的某些项目。
>start 值是必需的，规定删除或替换项目的位置
deleteCount 值是必需的，规定要删除的项目数量，如果设置为 0，则不会删除项目。
options 值是可选的，规定要替换的新项目
和 slice() 方法不同的是 splice() 方法会修改数组。

```javascript
var a = [1,2,3,4,5,6];
a.splice(2,2,"abc");
a; // 最终 a 数组变成了[1, 2, "abc", 5, 6]
```
- `toString() 方法`把数组转换为字符串，并返回结果。
- `sort()方法`排序
`array.sort(sortfunction)`
两个小例子
```javascript
var arr3 = [1,22,44,6,55,5,2,4,66];
    document.write(arr3 + "<br />");
    document.write(arr3.sort() + "<br />" + "<br />");
输出
//1,22,44,6,55,5,2,4,66
//1,2,22,4,44,5,55,6,66
 function sortNum1(a,b){
        return a - b;//从小到大排序
      }
      var arr4 = [1,22,44,6,55,5,2,4,66];
      document.write(arr4 + "<br />");
      document.write(arr4.sort(sortNum1) + "<br />" + "<br />");
输出
//1,22,44,6,55,5,2,4,66
//1,2,4,5,6,22,44,55,66
```
显然是回调函数做的手脚，那么原理是什么呢？
回调函数的参数要有两个：第一个参数的元素肯定在第二个参数的元素前面!!!

这个方法的排序是看回调函数的返回值：

 - 如果返回值大于 0，则位置互换。
 - 如果返回值小于 0，则位置不变。

#### String对象
常用属性：length。获取字符串的长度。
常用方法
- `charAt(index)方法`获取指定位置处字符。
```javascript
var str = "Hello world!";
document.write(str.charAt(2));
//以上代码输出为 l
```
- `charCodeAt(index) 方法`获取指定位置处字符的 Unicode 编码。
```javascript
var str = "Hello world!";
document.write(str.charCodeAt(2));
//以上代码输出为 l08
```
- concat() 方法，连接字符串,等效于 “+”，“+” 更常用。与数组中的 concat() 方法相似。
- slice() 方法，提取字符串的片断，并在新的字符串中返回被提取的部分（字符串章节有详细介绍，这里不过多的赘述，下面的类似情况同样处理）。
- indexOf() 方法，检索字符串。
- toString() 方法，返回字符串。
- toLowerCase() 方法，把字符串转换为小写。
- toUpperCase() 方法，把字符串转换为大写。
- replace() 方法，替换字符串中的某部分。
- split() 方法，把字符串分割为字符串数组。
#### Date对象
- Date()：返回当日的日期和时间。（输出是中国标准时间）
- getDate()：从 Date 对象返回一个月中的某一天 (1 ~ 31)。
- getDay()：从 Date 对象返回一周中的某一天 (0 ~ 6)。
- getMonth():从 Date 对象返回月份 (0 ~ 11)。
- getFullYear():从 Date 对象以四位数字返回年份。
- getHours():返回 Date 对象的小时 (0 ~ 23)。
- getMinutes():返回 Date 对象的分钟 (0 ~ 59)。
- getSeconds():返回 Date 对象的秒数 (0 ~ 59)。
- getMilliseconds():返回 Date 对象的毫秒(0 ~ 999)。

#### Math对象
常用属性：
* E ：返回常数 e (2.718281828...)。
* LN2 ：返回 2 的自然对数 (ln 2)。
* LN10 ：返回 10 的自然对数 (ln 10)。
* LOG2E ：返回以 2 为底的 e 的对数 (log2e)。
* LOG10E ：返回以 10 为底的 e 的对数 (log10e)。
* PI ：返回π（3.1415926535...)。
* SQRT1_2 ：返回 1/2 的平方根。
* SQRT2 ：返回 2 的平方根。

常用方法
- abs(x) ：返回 x 的绝对值。
- round(x) ：返回 x 四舍五入后的值。
- sqrt(x) ：返回 x 的平方根。
- ceil(x) ：返回大于等于 x 的最小整数。
- floor(x) ：返回小于等于 x 的最大整数。
- sin(x) ：返回 x 的正弦。
- cos(x) ：返回 x 的余弦。
- tan(x) ：返回 x 的正切。
- acos(x) ：返回 x 的反余弦值（余弦值等于 x 的角度），用弧度表示。
- asin(x) ：返回 x 的反正弦值。
- atan(x) ：返回 x 的反正切值。
- exp(x) ：返回 e 的 x 次幂 (e^x)。
- pow(n, m) ：返回 n 的 m 次幂 (nm)。
- log(x) ：返回 x 的自然对数 (ln x)。
- max(a, b) ：返回 a, b 中较大的数。
- min(a, b) ：返回 a, b 中较小的数。
- random() ：返回大于 0 小于 1 的一个随机数。

### 创建对象
**通过对象字面量来创建**
```javascript
var student = {
  name: 'zhangsan',
  age: 18,
  gender : 'male',
  sayHi: function () {
    console.log("hi,my name is "+this.name);
  }
}; 
```
**通过 new Object() 创建对象**
```js
var student = new Object();
  student.name = 'zhangsan',
  student.age = 18,
  student.gender = 'male',
  student.sayHi = function () {
    console.log("hi,my name is "+this.name);
  }
```

**通过函数创建**
```js
function createStudent(name, age, gender) {
  var student = new Object();
  student.name = name;
  student.age = age;
  student.gender = gender;
  student.sayHi = function(){
    console.log("hi,my name is "+this.name);
  }
  return student;
}
var s1 = createStudent('zhangsan', 18, 'male');
```
构造函数
```js
function Student(name,age,gender){
  this.name = name;
  this.age = age;
  this.gender = gender;
  this.sayHi = function(){
       console.log("hi,my name is "+this.name);
  }
}
var s1 = new Student('zhangsan', 18, 'male');
```
补充：
**new关键字**
构造函数，是一种特殊的函数。主要用来在创建对象时初始化对象，即为对象成员变量赋初始值，总与 new 运算符一起使用在创建对象的语句中。这里有需要特别注意的几点：

- 构造函数用于创建一类对象，首字母要大写。
- 内部使用 this 关键字给对象添加成员。
- 使用 new 关键字调用对象构造函数。

**this关键字**
this到底指向什么？
其实很简单：**谁调用this，它就是谁**
- 函数在定义的时候 this 是不确定的，只有在调用的时候才可以确定
- 一般函数直接执行，内部 this 指向全局 window。
- 函数作为一个对象的方法，被该对象所调用，那么 this 指向的是该对象。
- 构造函数中的 this，始终是 new 的当前对象。

### 遍历属性
通过 for...in 语句用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）
```js
 <script>
            var student = {
                name: 'zhangsan',
                age: 18,
                gender: 'male'
            };
            for(var key in student) {
                console.log(key);
                console.log(student[key]);
            }
   </script>
```
>注：key 是一个变量,这个变量中存储的是该对象的所有的属性的名字。

### 删除对象的属性
使用`delete`删除
```js
var student = {
  name: 'zhangsan',
  age: 18,
  gender: 'male'
};
student.name; // "zhangsan"
delete student.name;
```








