## 定义

bytes类型是指一堆字节的集合，在python中以b开头的字符串都是bytes类型

```py
b'\xe5\xb0\x8f\xe7\x8c\xbf\xe5\x9c\x88' #b开头的都代表是bytes类型，是以16进制来显示的，2个16进制代表一个字节。 utf-8是3个字节代表一个中文，所以以上正好是9个字节
```

## Bytes类型的作用

计算机只能存储2进制， 我们的字符、图片、视频、音乐等想存到硬盘上，也必须以正确的方式编码成2进制后再存。

* 对于文字，我们可以以gbk编码，也可以以utf-8、ASCII编码。

* 对于图片，必须编码成PNG,JPEG等格式

* 对于音乐，必须编码成MP3,WAV等 

在python中， 数据转成2进制后不是直接以0101010的形式表示的，而是用一种叫bytes\(字节\)的类型来表示，人类不可读。字符串转成bytes后长成这个样子

```py
>>> s = "小猿圈"
>>> s.encode("utf-8")  # 以utf-8编码 
b'\xe5\xb0\x8f\xe7\x8c\xbf\xe5\x9c\x88' #b开头的都代表是bytes类型，是以16进制来显示的，2个16进制代表一个字节。 utf-8是3个字节代表一个中文，所以以上正好是9个字节
```

在python中，字符串必须编码成bytes后才能存到硬盘上。 唉，你说，我之前学的文件操作时也没有把字符串编码后再存呀， 哈，那是python默认帮你干了这个事，在python3中文件存储的默认编码是utf-8.

当然你可以自行改变文件的默认编码，但意味着你存的数据

```py
f = open(file="encode_test",encoding="gbk",mode="w")
```

这样，你写入的数据就是按gbk编码的了。

## 以二进制模式操作文件

当然，在打开文件时如果你不想让open这个对象帮你自动编码，你也可以直接往文件里存入bytes数据。

```py
f = open(file="encode_test",mode="wb") # wb以2进制模式打开文件
s = "自学编程，谁不上小猿圈".encode("utf-8")  # 自行编码
print(s )
f.write(s)
f.close()
```

```
#以下是print(s)的输出
b'\xe8\x87\xaa\xe5\xad\xa6\xe7\xbc\x96\xe7\xa8\x8b\xef\xbc\x8c\xe8\xb0\x81\xe4\xb8\x8d\xe4\xb8\x8a\xe5\xb0\x8f\xe7\x8c\xbf\xe5\x9c\x88'
```

2进制模式打开文件有

* wb 二进制创建

* rb 二进制读

* ab 二进制追加



