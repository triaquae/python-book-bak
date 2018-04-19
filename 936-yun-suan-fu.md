# 运算符

js中的运算符跟python中的运算符有点类似，但也有不同。所谓运算,在数学上，是一种行为，通过已知量的可能的组合，获得新的量。

### 1.赋值运算符

以var x = 12,y=5来演示示例

| 运算符 | 例子 | 等同于 | 运算结果 |
| :---: | :---: | :---: | :---: |
| = | x=y |  | x=5 |
| += | x+=y | x=x+y | x=17 |
| -= | x-=y | x=x-y | x=7 |
| \*= | x\*=y | x=x\*y | x=60 |
| /= | x/=y | x=x/y | x=2 |
| %= | x%=y | x=x%y | x=2 |

### 2.算数运算符

var a = 5,b=2

| 运算符 | 描述 | 例子 | 运算结果 |
| :--- | :--- | :--- | :--- |
| + | 加法 | var c = a+b | c =  7 |
| - | 减法 | var c = a-b | c = 3 |
| \* | 乘法 | var c = a\*b | c = 10 |
| / | 除法 | var c = a/b | c = 2.5 |
| % | 取余 | var c = a%b | c = 1 |
| ++ | 自增 | var x= a++ | x = 6,a = 6 |
|  |  | var x  = ++a | x = 5,a = 6 |
| -- | 自减 | var x = a-- | x = 4,y = 4 |
|  |  | var x = --a | x = 5,y= 4 |

### 3.比较运算符

var x = 5;

| 运算符 | 描述 | 比较 | 返回值 |
| :---: | :---: | :---: | :---: |
| == | 等于 | x==8,x==5 | false,true |
| === | 等同于（值和类型均相等） | x===5,x==='5' | true,false |
| != | 不等于 | x!='8' | true |
| !== | 不等同与（值和类型有一个不相等，或两个都不相等） | x!==5,x!=='5' | true,false |
| &gt; | 大于 | x&gt;8 | false |
| &lt; | 小于 | x&lt;8 | true |
| &gt;= | 大于等于 | x&gt;=8 | false |
| &lt;= | 小于等于 | x&lt;=8 | true |

### 4.特殊情况

 字符串拼接+字符串运算 特殊情况。python中有拼接字符串中更简便的办法，其实在js中也有，大家可以百度引擎搜索es6模板字符串。（扩展）

```js
var  firstName  = '星';
var lastName = 'Li';
var name = '伊拉克';
var am = '美军';
// 字符串拼接
var str = "2003年3月20日,"+name+"战争爆发，以美军为主的联合部队仅用20多天就击溃了萨达姆的军队。这是继十多年前的海湾战争后，"+am+"又一次取得的大规模压倒性军事胜利。"
var fullStr = str;
console.log(fullStr)

var fullName = firstName +" "+ lastName;
console.log(fullName)
```

```js
// 不能对字符串进行+运算 只能拼接
var a1 = '1';
var a2 = '2';
console.log(a1-a2) //12
```

```js
var b1 = 'one';
var b2  = 'two';

// NaN. ==== not a number 是number类型
console.log(typeof(b1*b2))
```



