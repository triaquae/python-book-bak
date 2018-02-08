### 表示代码的标签

表示简短的单行代码可以使用`<code>`标签，如果是带有缩进的大段代码就要使用`<pre>`标签了。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        单行代码：
        <code>
            print("Hello world!")
        </code>
        代码块：
        <pre>
            while True:
            age = input("猜猜看啊:").strip()
            try:
                age = int(age)
                if age > 100 or age < 100:
                    print("不对!")
                else:
                    print("对了!")
                    break
            except ValueError:
                print("别捣乱!")            
        </pre>
    </body>
</html>
```
我们来看一下页面的效果：

![代码标签的效果](/assets/chapter9/html/HTML_12.png)