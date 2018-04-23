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

```js
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

```js
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

### 3.构造函数模式创建对象

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

了解了`构造函数`和`普通函数`的区别之后，我们使用构造函数将`工厂模式`的函数重写，并添加一个方法属性：

```
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

```
var v1 = new Student("easy", 20);
var v2 = new Fruit("apple", "green");
```

这时我们再来用instanceof操作符来检测以上对象类型就可以区分出Student以及Fruit了：

```
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

```js
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

在调用stu1.alert\(\)时，this对象才被绑定到stu1上。

我们通过将alertName\(\)函数定义为全局函数，这样对象中的alertName属性则被设置为指向该全局函数的指针。由此stu1和stu2共享了该全局函数，解决了内存浪费的问题。

但是，通过全局函数的方式解决对象内部共享的问题，终究不像一个好的解决方法。如果这样定义的全局函数多了，我们想要将自定义对象封装的初衷便几乎无法实现了。更好的方案是通过原型对象模式来解决。

### 4.原型的模式创建对象



原型链甚至原型继承，是整个JS中最难的一部分也是最不好理解的一部分，在这里由于我们课程定位的原因，如果对js有兴趣的同学，可以去查阅一下相关JS原型的一些知识点。更加有助于你以后前端JS的面试。

```
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



