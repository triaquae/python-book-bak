# 函数

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

```
function add3(x,y){
  return x+y;
}

var sum = add3(4,5)
alert(sum)
```



