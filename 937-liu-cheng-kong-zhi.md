# 数据类型转换

其实这个概念我就详细介绍了，我们的数据类型有很多，在某个页面中展示的数据类型也不同，比如说电话号码我就要求number的类型，而输入姓名的时候就要求string类型的。那么在适当的情况下我们可以将数据类型进行转换。python中比如说int\('12'\) 转换成数值类型的。那么javascript中如何转换的呢？

### 1.将数值类型转换成字符串类型

```js
var n1 = 123;
var n2 = '123';
var n3 = n1+n2;
// 隐式转换
console.log(typeof n3);
```

```js
// 强制类型转换String(),toString()
var str1 = String(n1);
console.log(typeof str1);

var num = 234;
console.log(num.toString())
```

### 2.将字符串类型转换成数值类型

```js
var  stringNum = '789.123wadjhkd';
var num2 =  Number(stringNum);
console.log(num2)

// parseInt()可以解析一个字符串 并且返回一个整数
console.log(parseInt(stringNum))
console.log(parseFloat(stringNum));
```

### 3.任何数据类型都可以转换为boolean类型

```js
var b1 = '123';
var b2 = 0;
var b3 = -123

var b4 = Infinity; 
var b5 = NaN;

var b6; //undefined
var b7 = null;

// 非0既真
console.log(Boolean(b7))
```



