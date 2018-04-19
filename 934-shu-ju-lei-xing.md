# javascript中的数据类型

数据类型包括：基本数据类型和引用数据类型

基本数据类型指的是简单的数据段，引用数据类型指的是有多个值构成的对象。

当我们把变量赋值给一个变量时，解析器首先要确认的就是这个值是基本类型值还是引用类型值

## 1.基本数据类型

* number

```
var a = 123;
//typeof 检查当前变量是什么数据类型
console.log(typeof a)
//特殊情况
var a1 = 5/0;
console.log(typeof e1) //Infinity 无限大. number类型
```

* string

```
var str  = '123'
console.log(typeof str)
```

* boolean

```
var b1 = false;
console.log(typeof b1)
```

* null

```
var c1 = null;//空对象. object
console.log(c1)
```

* undefined

```
var d1;
//表示变量未定义
console.log(typeof d1)
```

## 2.引用数据类型

* Function
* Object
* Arrray
* String
* Date

后面课程会讲解。



