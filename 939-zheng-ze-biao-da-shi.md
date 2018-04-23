# 普通函数

在javascript中,函数是一等公民,函数在javascript是一个数据类型,而非像C\#或其他描述性语言那样仅仅作为一个模块来使用.

一.函数调用形式

函数调用形式是最常见的形式,也是最好理解的形式。所谓函数形式就是一般声明函数后直接调用。例如：

```js
//1.js中的函数的声明  记得：有函数的声明 就一定有调用
function add(){
  alert("函数被调用了")；
  alert(this);//当前的this指向了window
//执行的一些操作
}

//2.函数的执行
add()；
```

或者下面的声明函数和调用函数的方式

```js
var add = function(){
    alert('函数被调用了')；
}
add()
```

声明函数式带形式参数

```js
function add3(x,y){
  return x+y;
}

var sum = add3(4,5)
alert(sum)
```

# 创建对象的几种常用方式

1.使用Object或对象字面量创建对象

2.工厂模式创建对象

3.构造函数模式创建对象

4.原型模式创建对象

### 1.使用Object或对象字面量创建对象

JS中最基本创建对象的方式：

```js
var student = new Object();
student.name = "easy";
student.age = "20";
```

这样，一个student对象就创建完毕，拥有2个属性`name`以及`age`，分别赋值为`"easy"`和`20`。

如果你嫌这种方法有一种封装性不良的感觉。来一个对象字面量方式创建对象

```js
var sutdent = {
  name : "easy",
  age : 20
};
```

这样看起来似乎就完美了。但是马上我们就会发现一个十分尖锐的问题：当我们要创建同类的student1，student2，…，studentn时，我们不得不将以上的代码重复n次....



```
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

能不能像**工厂车间**那样，有一个**车床就不断生产出对象**呢？我们看”**工厂模式**”。



### 2.工厂模式创建对象

JS中没有类的概念，那么我们不妨就使用一种函数将以上对象创建过程封装起来以便于重复调用，同时可以给出特定接口来初始化对象

```
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







使用构造器函数通常在js中我们来创建对象。

特点：

* 函数名首字母要大写
* 构造函数不需要returen
* 为对象添加成员变量：this.name = ‘alex’

```js
var Stu = function(){
    this.name = '武sir';
    this.age = 18;
    this.fav = function(){
       console.log('泡妹子')
    }
}
//创建这个对象
var s = new Stu();
console.log(s);

var s1 = new Stu();
console.log(s1);
```

分析上面代码：

```
1、程序在执行到这一句的时候，不会执行函数体，因此 JavaScript 的解释器并不知道这个函数的内容
2、接下来执行 new 关键字，创建对象，解释器开辟内存，得到对象的引用，将新对象的引用交给函数
3、紧接着执行函数，将传过来的对象引用交给 this。也就是说，在构造方法中，this 就是刚刚被 new 创建出来的对象
4、然后为 this 添加成员，也就是为对象添加成员
5、最后函数结束，返回 this，将 this 交给左边的变量。
分析过构造函数的执行以后，可以得到，构造函数中的 this 就是当前对象。
```



