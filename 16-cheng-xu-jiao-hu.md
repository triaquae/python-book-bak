## 本节重点：

* 让学生掌握如果让程序读取用户输入

> **本节时长需控制在25分钟之内**



## 读取用户输入

```py
name = input("What is your name?")

print("Hello " + name )
```

执行脚本就会发现，程序会等待你输入姓名后再往下继续走。

可以让用户输入多个信息，如下 

```py
name = input("What is your name?")
age = input("How old are you?")
hometown = input("Where is your hometown?")

print("Hello ",name , "your are ", age , "years old, you came from",hometown)
```

执行输出

```bash
What is your name?Alex Li
How old are you?22
Where is your hometown?ShanDong
Hello  Alex Li your are  22 years old, you came from ShanDong
```



> 为避免学生蒙逼，py2.7 的raw\_input 以后再补充



