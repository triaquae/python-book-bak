# 流程控制

### 1.if 、if-else、if-else if-else

```js
var ji  = 20;
if(ji >= 20){
    console.log('恭喜你，吃鸡成功，大吉大利')
}
alert('alex');//下面的代码还会执行
```

```
var ji  = 20;
if(ji>=20){
    console.log('恭喜你，吃鸡成功，大吉大利')
}else{
    console.log('很遗憾 下次继续努力')

}
```

```js
if (true) {
   //执行操作
}else if(true){
    //满足条件执行            
}else if(true){
   //满足条件执行        
}else{
  //满足条件执行
}
```

```
注意：浏览器解析代码的顺序 是从上往下执行，从左往右
```

### 2.逻辑与&&、逻辑或\|\|

```js
//1.模拟  如果总分 >400 并且数学成绩 >89分 被清华大学录入
//逻辑与&& 两个条件都成立的时候 才成立
if(sum>400 && math>90){
    console.log('清华大学录入成功')
}else{
    alert('高考失利')
}
```

```js
//2.模拟 如果总分>400 或者你英语大于85 被复旦大学录入
//逻辑或  只有有一个条件成立的时候 才成立
if(sum>500 || english>85){
    alert('被复旦大学录入')
}else{
    alert('高考又失利了')
}
```

### 3.switch

```js
var gameScore = 'good1111';



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
```

### 4.while循环

循环三步走：

1.初始化循环变量

2.判断循环条件

3.更新循环变量

```js
var i = 1; //初始化循环变量

while(i<=9){ //判断循环条件
    console.log(i);
    i = i+1; //更新循环条件
}
```

练习：将1-100所有是2的倍数在控制台中打印。使用while循环

### 5.do\_while

```js
//不管有没有满足while中的条件do里面的代码都会走一次
var i = 3;//初始化循环变量
do{

    console.log(i)
    i++;//更新循环条件

}while (i<10) //判断循环条件
```

### 6.for循环

```js
for(var i = 1;i<=10;i++){
     console.log(i)
 }
```

课堂练习：

1-100之间所有的偶数

```js
for(var i = 1;i<=100;i++){
    if(i%2==0){
        //是偶数
        console.log(i)
    }
}
```

1-100之间所有数之和

```js
var sum = 0;
for(var j = 1;j<=100;j++){
    sum = sum+j
}
console.log(sum)
```

课下练习：

* 使用\*打印直角三角形

* 使用\*打印等边三角形

* 有兴趣的同学在这里我们结合前面的html+css+部分js就可以做个计算器了

![](/jquery/计算器.png)





