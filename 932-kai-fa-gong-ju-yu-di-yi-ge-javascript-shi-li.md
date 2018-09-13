# 本节内容

* ### [JS的引入方式](#js的引入方式 "JS的引入方式")
* ### [注释](#注释)
* ### [调试语句](/注释)
* ### [变量的声明](/变量的声明)
* ### [变量的命名规范](/变量的命名规范)
* ### [基本数据类型](/基本数据类型)
* ### [复杂\(引用\)数据类型](/复杂%28引用%29数据类型)
* ### [运算符](/运算符)
* ### [数据类型转换](/数据类型转换)
* ### [流程控制](/流程控制)
* ### [常用内置对象\(复杂数据类型\)（重点）](/常用内置对象%28复杂数据类型%29（重点）)
* ### [函数（重点）](/函数（重点）)
* ### [伪数组arguments](/伪数组arguments)
* ### [对象Object\(重点\)](/对象Object%28重点%29)
* ### [Date日期对象](/Date日期对象)
* ### [JSON\(重点\)](/JSON%28重点%29)

前端常用开发工具：sublime、visual Studio Code、HBuilder、Webstorm。

那么大家使用的PCharm跟WebStorm是JetBrains公司推出的编辑工具，开发阶段建议使用。

#### JS的引入方式

* 内接式

```html
<script type="text/javascript">

</script>
```

* 外接式

```html
<!--相当于引入了某个模块-->
<script type="text/javascript" src = './index.js'></script>
```

#### 注释

```单行注释的快捷键ctrl+/.多行注释的快捷键是ctrl+shift+/\`\`\`
#### 调试语句

- alert(''); 弹出警告框
- console.log('');  控制台输出



#### 变量的声明

在js中使用var关键字 进行变量的声明,注意 分号作为一句代码的结束符

```javascript
var a = 100;
```

* 定义变量：var就是一个**关键字**，用来定义变量。所谓关键字，就是有特殊功能的小词语。关键字后面一定要有空格隔开。
* 变量的赋值：等号表示**赋值**，将等号右边的值，赋给左边的变量。
* 变量名：我们可以给变量任意的取名字。

变量要先定义，才能使用。比如，我们不设置变量，直接输出：

```html
 <script type="text/javascript">
        console.log(a);
  </script>
```

控制台将会报错：

![img](https://images2018.cnblogs.com/blog/1364810/201805/1364810-20180526102920462-1087853951.png)

正确写法：

```javascript
var a; //先定义
a = 100; // 后赋值

//也可以直接定义变量+赋值
var a = 100;
```

#### 变量的命名规范

变量名有命名规范：只能由**英语字母、数字、下划线、美元符号$**构成，且不能以数字开头，并且不能是JavaScript保留字。

下列的单词叫做保留字，就是说不允许当做变量名，不用记：

```javascript
bstract、boolean、byte、char、class、const、debugger、double、enum、export、extends、final、float、goto
implements、import、int、interface、long、native、package、private、protected、public、short、static、super、synchronized、throws、transient、volatile
```

#### 基本数据类型

##### 数值类型:number

如果一个变量中，存放了数字，那么这个变量就是数值型的

```javascript
    var a = 100;            //定义了一个变量a，并且赋值100
    console.log(typeof a);  //输出a变量的类型 使用typeof函数 检测变量a的数据类型
    //特殊情况
    var b = 5/0;
    console.log(b); //Infinity 无限大
    console.log(typeof b); //number 类型
```

ps:**在JavaScript中，只要是数，就是数值型\(number\)的**。无论整浮、浮点数（即小数）、无论大小、无论正负，都是number类型的。

##### 字符串类型:string

```javascript
var a = "abcde";
var b = "路飞";
var c = "123123";
var d = "哈哈哈哈哈";
var e = "";     //空字符串
```

###### 连字符和+号的区别

键盘上的`+`可能是连字符，也可能是数字的加号。如下：

```javascript
console.log("我" + "爱" + "你");   //连字符，把三个独立的汉字，连接在一起了
console.log("我+爱+你");           //原样输出
console.log(1+2+3);             //输出6
```

**总结**：如果加号两边**都是**数值，此时是加。否则，就是连字符（用来连接字符串）。

##### 布尔类型：boolean

```javascript
var isShow = false;
console.log(typeof b1);
```

##### 空对象：null

```javascript
var c1 = null;//空对象. object
console.log(typeof c1);
```

##### 未定义：undefined

```javascript
var d1;
//表示变量未定义
console.log(typeof d1);
```

#### 复杂（引用）数据类型

##### Function

##### Object

##### Arrary

##### String

##### Date

后面课程讲解

#### 运算符

##### 赋值运算符

以var x = 12,y=5来演示示例

![](/assets/chapter10/02.png)

##### 算数运算符

var a = 5,b=2;

![](/assets/chapter10/03.png)

##### 比较运算符

var x = 5;

![](/assets/chapter10/04.png)

#### 数据类型转换

##### 将number类型转换成string类型

###### 隐式转换

```javascript
var n1 = 123;
var n2 = '123';
var n3 = n1+n2;
// 隐式转换
console.log(typeof n3);
```

###### 强制转换

```javascript
// 强制类型转换String(),toString()
var str1 = String(n1);
console.log(typeof str1);

var num = 234;
console.log(num.toString())
```

##### 将string类型转换成number类型

```javascript
var  stringNum = '789.123wadjhkd';
var num2 =  Number(stringNum);
console.log(num2); //NaN  Not a Number 但是一个number类型

// parseInt()可以解析一个字符串 并且返回一个整数
console.log(parseInt(stringNum))； //789
console.log(parseFloat(stringNum)); //789.123
```

##### 任何的数据类型都可以转换为boolean类型

```javascript
var b1 = '123'; //true
var b2 = 0; //false
var b3 = -123 //true
var b4 = Infinity; //true
var b5 = NaN; //false
var b6; //false
var b7 = null; //false
//使用Boolean(变量) 来查看当前变量的真假
```

#### 流程控制

##### if

```javascript
var age = 20;
if(age>18){
    //{}相当于作用域
    console.log('可以去会所');
}
alert('alex'); //下面的代码照样执行
```

##### if-else

```javascript
var age = 20;
if(age>18){
    //{}相当于作用域
    console.log('可以去会所');
}else{
    console.log('好好学js,年纪够了再去会所');
}
alert('alex'); //下面的代码照样执行
```

##### if-else if -else

```javascript
var age = 18;
if(age==18){
    //{}相当于作用域
    console.log('可以去会所');
}else if(age==30){
    console.log('该娶媳妇了！！');
}else{
    console.log('随便你了')
}
alert('alex'); //下面的代码照样执行
```

##### 逻辑与&&、 逻辑或\|\|

```javascript
//1.模拟  如果总分 >400 并且数学成绩 >89分 被清华大学录入
//逻辑与&& 两个条件都成立的时候 才成立
if(sum>400 && math>90){
    console.log('清华大学录入成功')
}else{
    alert('高考失利')
}
```

```javascript
//2.模拟 如果总分>400 或者你英语大于85 被复旦大学录入
//逻辑或  只有有一个条件成立的时候 才成立
if(sum>500 || english>85){
    alert('被复旦大学录入')
}else{
    alert('高考又失利了')
}
```

##### switch 语句

```javascript
var gameScore = 'better';

switch(gameScore){

//case表示一个条件 满足这个条件就会走进来 遇到break跳出。break终止循环。如果某个条件中不写 break，那么直到该程序遇到下一个break停止
    case 'good':
    console.log('玩的很好')
    //break表示退出
    break;
    case  'better':
    console.log('玩的老牛逼了')
    break;
    case 'best':
    console.log('恭喜你 吃鸡成功')
    break;

    default:
    console.log('很遗憾')

}
//注意：switch相当于if语句 但是玩switch的小心case穿透
```

##### while循环

给大家总结了循环三步走，任何语言的循环离不开这三步：

1. 初始化循环变量
2. 判断循环条件
3. 更新循环变量

```javascript
// 例子：打印 1~9之间的数
var i = 1; //初始化循环变量

while(i<=9){ //判断循环条件
    console.log(i);
    i = i+1; //更新循环条件
}
```

练习：将1~100所有是2的倍数在控制台打印。使用while循环

```javascript
var i = 1;
while(i <= 100){
    if(i%2==0){
        console.log(i);
    }
    i +=1;
}
```

##### do-while循环

用途不大：就是先做一次 ，上来再循环

```javascript
//不管有没有满足while中的条件do里面的代码都会走一次
var i = 3;//初始化循环变量
do{

    console.log(i)
    i++;//更新循环条件

}while (i<10) //判断循环条件
```

##### for循环

for循环遍历列表是最常用的对数据的操作，在js中希望大家熟练使用for循环的书写方式

```javascript
//输出1~10之间的数
for(var i = 1;i<=10;i++){
     console.log(i)
 }
```

课堂练习：输入1~100之间所有数之和

```javascript
var sum = 0;
for(var j = 1;j<=100;j++){
    sum = sum+j
}
console.log(sum);
```

##### for循环嵌套的练习

document.write\('_'\); 往浏览器文档中写_

```javascript
for(var i=1;i<=3;i++){

 　　for(var j=0;j<6;j++){
        document.write('*')
    }

   document.write('<br>')
 }
```

小作业：

1.在浏览器中输出直角三角形

```html
*  
** 
***
****
*****
******
```

代码：

```javascript
for(var i=1;i<=6;i++){ //控制的行数
   for(var j=1;j<=i;j++){ //控制的*
      　　document.write("*")；
   }

     document.write('<br>')；
}
```

2.在浏览器中输出 等腰三角形

```html
          *  
        ***  
        ***** 
       ******* 
      ********* 
     ***********
```

代码：

```javascript
    for(var i=1;i<=6;i++){ //控制行数，一共显示6行 记得换行document.write('<br>');

        //控制我们的空格数
        for(var s=i;s<6;s++){
            document.write('&nbsp;');
        }
        //控制每行的输出*数
        for(var j=1;j<=2*i-1;j++){
            document.write('*');
        }
        document.write('<br>');

   }
```

#### 常用内置对象（复杂数据类型）

所谓内置对象就是ECMAScript提供出来的一些对象，我们知道对象都是有相应的属性和方法,jie'xi'lai

##### 数组Array

###### 字面量方式创建（推荐大家使用这种方式，简单粗暴）

```javascript
var colors = ['red','green','yellow'];
```

###### 使用构造函数（后面会讲）的方式创建 使用new关键词对构造函数进行创建对象,构造函数与后面的面向对象有关系

```javascript
var colors = new Array();
//通过下标进行赋值
colors[0] = 'red';
colors[1] = 'green';
colors[2] = 'yellow';
console.log(colors);
```

###### 数组的常用方法

![](/assets/chapter10/05.png)

* 数组的合并 concat\(\)

```javascript
var north = ['北京','山东','天津'];
var south = ['东莞','深圳','上海'];

var newCity = north.concat(south);
console.log(newCity)
```

* join\(\) 将数组中元素使用指定的字符串连接起来，它会形成一个新的字符串

```javascript
var score = [98,78,76,100,0];
var str = score.join('|');
console.log(str);//"98|78|76|100|0"
```

* slice\(start,end\); 返回数组的一段记录，顾头不顾尾

```javascript
var arr = ['张三','李四','王文','赵六'];
var newArr  = arr.slice(1,3);
console.log(newArr);//["李四", "王文"]
```

* pop 移除数组的最后一个元素

```javascript
var arr = ['张三','李四','王文','赵六'];
arr.pop();
console.log(arr);//["张三", "李四"，"王文"]
```

* push\(\) 向数组最后添加一个元素

```javascript
var arr = ['张三','李四','王文','赵六'];
arr.push('小马哥');
console.log(arr);//["张三", "李四"，"王文"，"赵六"，"小马哥"]
```

* reverse\(\) 翻转数组

```javascript
var names = ['alex','xiaoma','tanhuang','angle'];
//4.反转数组
names.reverse();
console.log(names);
```

* sort对数组排序

```javascript
var names = ['alex','xiaoma','tanhuang','abngel'];
names.sort();
console.log(names)；// ["alex", "angle", "tanhuang", "xiaoma"]
```

* 判断是否为数组：isArray\(\)

```
 布尔类型值 = Array.isArray(被检测的值) ;
```

##### 字符串string

![](/assets/chapter10/06.png)

* chartAt\(\) 返回指定索引的位置的字符

```javascript
var str = 'alex';
var charset = str.charAt(1);
console.log(charset);//l
```

* concat 返回字符串值，表示两个或多个字符串的拼接

```javascript
var str1 = 'al';
var str2  = 'ex';
console.log(str1.concat(str2,str2));//alexex
```

* replace\(a,b\) 将字符串a替换成字符串b

```javascript
var a = '1234567755';
var newStr = a.replace("4567","****");
console.log(newStr);//123****755
```

* indexof\(\) 查找字符的下标，如果找到返回字符串的下标，找不到则返回-1 。跟seach\(\)方法用法一样

```javascript
var str = 'alex';
console.log(str.indexOf('e'));//2
console.log(str.indexOf('p'));//-1
```

* slice\(start，end\) 左闭右开 分割字符串

```javascript
var str = '小马哥';
console.log(str.slice(1,2));//马
```

* split\('a',1\) 以字符串a分割字符串，并返回新的数组。如果第二个参数没写，表示返回整个数组，如果定义了个数，则返回数组的最大长度

```javascript
var  str =  '我的天呢,a是嘛,你在说什么呢?a哈哈哈';
console.log(str.split('a'));//["我的天呢,", "是嘛,你在说什么呢?", "哈哈哈"]
```

* substr\(statr,end\) 左闭右开

```javascript
var  str =  '我的天呢,a是嘛,你在说什么呢?a哈哈哈';
console.log(str.substr(0,4));//我的天呢
```

* toLowerCase\(\)转小写

```javascript
var str = 'XIAOMAGE';
console.log(str.toLowerCase())；//xiaomage
```

* toUpperCase\(\)转大写

```javascript
var str = 'xiaomage';
console.log(str.toUpperCase());//XIAOMAGE
```

特别：

```javascript
//1.将number类型转换成字符串类型
var num = 132.32522;
var numStr = num.toString()
console.log(typeof numStr)
//四舍五入
var newNum = num.toFixed(2)
console.log(newNum)
```

##### Math内置对象

![](/assets/chapter10/07.png)

* Math.ceil\(\) 向上取整，'天花板函数'

```javascript
var x = 1.234;
//天花板函数  表示大于等于 x，并且与它最接近的整数是2
var a = Math.ceil(x);
console.log(a);//2
```

* Math.floor 向下取整，'地板函数'

```javascript
var x = 1.234;
// 小于等于 x，并且与它最接近的整数 1
var b = Math.floor(x);
console.log(b);//1
```

* 求两个数的最大值和最小值

```javascript
//求 两个数的最大值 最小值
console.log(Math.max(2,5));//5
console.log(Math.min(2,5));//2
```

* 随机数 Math.random\(\)

```javascript
var ran = Math.random();
console.log(ran);[0,1)
```

如果让你取100-200之间的随机数，怎么做？

背过公式：min - max之间的随机数： min+Math.random\(\)\*\(max-min\);

#### 函数

函数：就是把将一些语句进行封装，然后通过调用的形式，执行这些语句。

函数的作用：

* 解决大量的重复性的语句
* 简化编程，让编程模块化

```python
# python 中声明函数
def add(x,y):
    return x+y

# 调用函数
print(add(1,2))
```

```javascript
//js中声明函数
function add(x,y){
    return x+y;
}
//js中调用函数
console.log(add(1,2));
```

解释如下：

* function：是一个关键字。中文是“函数”、“功能”。
* 函数名字：命名规定和变量的命名规定一样。只能是字母、数字、下划线、美元符号，不能以数字开头。
* 参数：后面有一对小括号，里面是放参数用的。
* 大括号里面，是这个函数的语句。

#### 伪数组 arguments

arguments代表的是实参。有个讲究的地方是：arguments**只在函数中使用**。

```javascript
    fn(2,4);
    fn(2,4,6);
    fn(2,4,6,8);

    function fn(a,b,c) {
        console.log(arguments);
        console.log(fn.length);         //获取形参的个数
        console.log(arguments.length);  //获取实参的个数

        console.log("----------------");
    }
```

结果：

![](/assets/chapter10/08.png)

（2）之所以说arguments是伪数组，是因为：**arguments可以修改元素，但不能改变数组的长短**。举例：

```javascript
    fn(2,4);
    fn(2,4,6);
    fn(2,4,6,8);

    function fn(a,b) {
        arguments[0] = 99;  //将实参的第一个数改为99
        arguments.push(8);  //此方法不通过，因为无法增加元素
    }
```

清空数组的几种方式：

```javascript
   var array = [1,2,3,4,5,6];
    array.splice(0);      //方式1：删除数组中所有项目
    array.length = 0;     //方式2：length属性可以赋值，在其它语言中length是只读
    array = [];           //方式3：推荐
```

#### 对象Object

1.使用Object或对象字面量创建对象

2.工厂模式创建对象

3.构造函数模式创建对象

4.原型模式创建对象

##### 使用Object或字面量方式创建对象

JS中最基本创建对象的方式：

```javascript
var student = new Object();
student.name = "easy";
student.age = "20";
```

这样，一个student对象就创建完毕，拥有2个属性`name`以及`age`，分别赋值为`"easy"`和`20`。

如果你嫌这种方法有一种封装性不良的感觉。来一个对象字面量方式创建对象。

```javascript
var sutdent = {
  name : "easy",
  age : 20
};
```

这样看起来似乎就完美了。但是马上我们就会发现一个十分尖锐的问题：当我们要创建同类的student1，student2，…，studentn时，我们不得不将以上的代码重复n次....

```javascript
var sutdent1 = {
  name : "easy1",
  age : 20
};

var sutdent2 = {
  name : "easy2",
  age : 20
};

...

var sutdentn = {
  name : "easyn",
  age : 20
};
```

有个提问？能不能像工厂车间那样，有一个车床就不断生产出对象呢？我们看”工厂模式”。

##### 工厂模式创建对象

JS中没有类的概念，那么我们不妨就使用一种函数将以上对象创建过程封装起来以便于重复调用，同时可以给出特定接口来初始化对象

```javascript
function createStudent(name, age) {
  var obj = new Object();
  obj.name = name;
  obj.age = age;
  return obj;
}

var student1 = createStudent("easy1", 20);
var student2 = createStudent("easy2", 20);
...
var studentn = createStudent("easyn", 20);
```

这样一来我们就可以通过createStudent函数源源不断地”生产”对象了。看起来已经高枕无忧了，但贪婪的人类总有不满足于现状的天性：我们不仅希望”产品”的生产可以像工厂车间一般源源不断，我们还想知道生产的产品究竟是哪一种类型的。

比如说，我们同时又定义了”生产”水果对象的createFruit\(\)函数：

```javascript
function createFruit(name, color) {
  var obj = new Object();
  obj.name = name;
  obj.color = color;
  return obj;
}

var v1 = createStudent("easy1", 20);
var v2 = createFruit("apple", "green");
```

对于以上代码创建的对象v1、v2，我们用instanceof操作符去检测，他们统统都是Object类型。我们的当然不满足于此，我们希望v1是Student类型的，而v2是Fruit类型的。为了实现这个目标，我们可以用自定义构造函数的方法来创建对象

##### 构造函数模式创建对象

在上面创建Object这样的原生对象的时候，我们就使用过其构造函数：

```
var obj = new Object();
```

在创建原生数组Array类型对象时也使用过其构造函数：

```
var arr = new Array(10);  //构造一个初始长度为10的数组对象
```

在进行自定义构造函数创建对象之前，我们首先了解一下`构造函数`和`普通函数`有什么区别。

1、实际上并不存在创建构造函数的特殊语法，其与普通函数唯一的区别在于调用方法。对于任意函数，使用new操作符调用，那么它就是构造函数；不使用new操作符调用，那么它就是普通函数。

2、按照惯例，我们约定构造函数名以大写字母开头，普通函数以小写字母开头，这样有利于显性区分二者。例如上面的new Array\(\)，new Object\(\)。

3、使用new操作符调用构造函数时，会经历\(1\)创建一个新对象；\(2\)将构造函数作用域赋给新对象（使this指向该新对象）；\(3\)执行构造函数代码；\(4\)返回新对象；4个阶段。

ok，了解了`构造函数`和`普通函数`的区别之后，我们使用构造函数将`工厂模式`的函数重写，并添加一个方法属性：

```javascript
function Student(name, age) {
  this.name = name;
  this.age = age;
  this.alertName = function(){
    alert(this.name)
  };
}

function Fruit(name, color) {
  this.name = name;
  this.color = color;
  this.alertName = function(){
    alert(this.name)
  };
}
```

这样我们再分别创建Student和Fruit的对象：

```javascript
var v1 = new Student("easy", 20);
var v2 = new Fruit("apple", "green");
```

这时我们再来用instanceof操作符来检测以上对象类型就可以区分出Student以及Fruit了：

```javascript
alert(v1 instanceof Student);  //true
alert(v2 instanceof Student);  //false
alert(v1 instanceof Fruit);  //false
alert(v2 instanceof Fruit);  //true

alert(v1 instanceof Object);  //true 任何对象均继承自Object
alert(v2 instanceof Object);  //true 任何对象均继承自Object
```

这样我们就解决了`工厂模式`无法区分对象类型的尴尬。那么使用构造方法来创建对象是否已经完美了呢？使用构造器函数通常在js中我们来创建对象。

我们会发现Student和Fruit对象中共有同样的方法，当我们进行调用的时候这无疑是内存的消耗。

我们完全可以在执行该函数的时候再这样做，办法是将对象方法移到构造函数外部：

```javascript
function Student(name, age) {
  this.name = name;
  this.age = age;
  this.alertName = alertName;
}

function alertName() {
  alert(this.name);
}

var stu1 = new Student("easy1", 20);
var stu2 = new Student("easy2", 20);
```

在调用stu1.alertName\(\)时，this对象才被绑定到stu1上。

我们通过将alertName\(\)函数定义为全局函数，这样对象中的alertName属性则被设置为指向该全局函数的指针。由此stu1和stu2共享了该全局函数，解决了内存浪费的问题

但是，通过全局函数的方式解决对象内部共享的问题，终究不像一个好的解决方法。如果这样定义的全局函数多了，我们想要将自定义对象封装的初衷便几乎无法实现了。更好的方案是通过原型对象模式来解决。

##### 原型的模式创建对象

原型链甚至原型继承，是整个JS中最难的一部分也是最不好理解的一部分，在这里由于我们课程定位的原因，如果对js有兴趣的同学，可以去查阅一下相关JS原型的一些知识点。

```javascript
function Student() {
    this.name = 'easy';
    this.age = 20;
}


Student.prototype.alertName = function(){
    alert(this.name);
};

var stu1 = new Student();
var stu2 = new Student();

stu1.alertName();  //easy
stu2.alertName();  //easy

alert(stu1.alertName == stu2.alertName);  //true 二者共享同一函数
```

#### Date日期对象

创建日期对象只有构造函数一种方式，使用new关键字

```javascript
//创建了一个date对象
var myDate = new Date();
```

![](/assets/chapter10/09.png)

```javascript
//返回本地时间
console.log(myDate().toLocalString());
```

#### JSON

##### 概念简介

JSON\(JavaScript Object Notation\) 是一种轻量级的数据交换格式，采用完全独立于语言的文本格式，是理想的数据交换格式。同时，JSON是 JavaScript 原生格式，这意味着在 JavaScript 中处理 JSON数据不须要任何特殊的 API 或工具包。

在JSON中，有两种结构：对象和数组。

* 对象

```json
var packJSON= {"name":"alex", "password":"123"};
```

一个对象以“{”开始，“}”结束，“key/value”之间运用 “,”分隔。

* 数组

```json
var packJSON = [{"name":"alex", "password":"123"}, {"name":"wusir", "password":"456"}];
```

数组是值的有序集合。一个数组以“\[”开始，“\]”结束。值之间运用 “,”分隔。

##### JSON对象和JSON字符串转换

在数据传输过程中，JSON是以字符串的形式传递的，而JS操作的是JSON对象，所以，JSON对象和JSON字符串之间的相互转换是关键。例如：

* JSON字符串:

```javascript
var jsonStr ='{"name":"alex", "password":"123"}' ;
```

* JSON对象：

```javascript
var jsonObj = {"name":"alex", "password":"123"};
```

1. JSON字符串转换JSON对象

```javascript
var jsonObject= jQuery.parseJSON(jsonstr);
```

1. JSON对象转化JSON字符串

```javascript
var jsonstr =JSON.stringify(jsonObject );
```

##### 遍历JSON对象和JSON数组

1. 遍历JSON对象代码如下：

```javascript
var packAlex  = {"name":"alex", "password":"123"} ;

for(var k in packAlex ){//遍历packAlex 对象的每个key/value对,k为key
   alert(k + " " + packAlex[k]);
}
```

1. 遍历JSON数组代码如下

```javascript
var packAlex = [{"name":"alex", "password":"123"}, {"name":"wusir", "password":"456"}];

for(var i in packAlex){//遍历packJson 数组时，i为索引
   alert(packAlex[i].name + " " + packAlex[i].password);
}
```



