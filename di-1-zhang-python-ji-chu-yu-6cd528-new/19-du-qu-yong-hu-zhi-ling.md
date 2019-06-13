若你的程序要接收用户指令，可以用input语法：

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

结果输出

```
What is your name?Alex Li
How old are you?22
Where is your hometown?ShanDong
Hello  Alex Li your are  22 years old, you came from ShanDong
```



> 注意，input\(\)方法接收的只是字符串，即使你输入的是数字，它也会按字符串处理

  


