## HTML表格

有些时候我们为了更形象地在HTML页面上展示一系列数据的时候，会使用表格展示数据。

那如何在HTML页面上定义表格呢？

HTML中使用`table`标签来定义表格，通常`table`还会分为`thead`(表头)和`tbody`(表格内容)两部分。
你看表格中的数据都是分很多行，每一行又会有很多列。
在`thead`和`tbody`中都用`tr`表示一行，在`thead`中用`th`表示一列，用`tbody`中用`td`表示一列。

我们来动手自己写一个表格。

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>名称</th>
                    <th>价格</th>
                    <th>库存</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>苹果</td>
                    <td>9.99</td>
                    <td>100</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>香蕉</td>
                    <td>11.99</td>
                    <td>80</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>芒果</td>
                    <td>14.99</td>
                    <td>160</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```
看一下效果：
![表格默认效果](/assets/chapter9/html/HTML_18.png)

这样的表格默认是不显示边框，我们可以通过为表格设置边框属性让表格显示边框。

在`table`标签中通过设置`border="1"`为表格设置一个宽度为1像素的边框：

```html
<!DOCTYPE HTML>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>路飞学城</title>
    </head>
    <body>
        <table border="1">
            <thead>
                <tr>
                    <th>#</th>
                    <th>名称</th>
                    <th>价格</th>
                    <th>库存</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>苹果</td>
                    <td>9.99</td>
                    <td>100</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>香蕉</td>
                    <td>11.99</td>
                    <td>80</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>芒果</td>
                    <td>14.99</td>
                    <td>160</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```
设置了边框的表格效果：

![代表框的表格](/assets/chapter9/html/HTML_19.png)