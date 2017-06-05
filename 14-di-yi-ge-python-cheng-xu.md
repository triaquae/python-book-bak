## 本节重点：

* 让学生掌握Python代码的2种执行方式

> **本节时长需控制在10分钟之内**

## 文件执行

1. 用notepad++创建一个文件，输入以下代码
2. ```py
   print("Hello World!")
   print("Python好简单呀，我要学好挣大钱！")
   ```
3. 保存为HelloWorld.py , 注意要强调.py后缀名的作用
4. 进入cmd命令行，执行python HelloWorld.py, 看结果 （注意要解释文件名前面加python 的原因是要把代码交给python解释器去解释执行）

## 交互器执行

演示在python交互器下 ，输出hello world ！

> 要强调python交互器是主要用来对代码进行调试用的

## 精通各种语言的Hello World

C++

```cpp
#include <iostream>
 int main(void)
 {
  std::cout<<"Hello world";
 }
```

C

```c
#include <stdio.h>
int main(void)
{
printf("\nhello world!");
return 0;
}
```

JAVA

```java
public class HelloWorld{
  // 程序的入口
  public static void main(String args[]){
    // 向控制台输出信息
    System.out.println("Hello World!");
  }
}
```

PHP

```php
<?php  
             echo "hello world!";  
?>
```

Ruby

```
 puts "Hello world."
```

GO

```go
package main

import "fmt"

func main(){

    fmt.Printf("Hello World!\n God Bless You!");

}
```



