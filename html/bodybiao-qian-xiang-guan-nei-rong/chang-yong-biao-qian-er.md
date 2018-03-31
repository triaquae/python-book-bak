### 表格标签 table
表格由` <table>` 标签来定义。每个表格均有若干行（由 `<tr>` 标签定义），每行被分割为若干单元格（由` <td> `标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等 
![](/assets/chapter9/html/table.png)

```
<div class="table">
        <table>
            <!--表格头-->
            <thead>
                <!--表格行-->
                <tr>
                    <!--表格列，【注意】这里使用的是th-->
                    <th></th>
                </tr>
            </thead>
            <!--表格主体-->
            <tbody>
                <!--表格行-->
                <tr>
                    <!--表格列，【注意】这里使用的是td-->
                    <td></td>
                </tr>
                <tr>
                    <td></td>
                </tr>
            </tbody>
            <!--表格底部-->
            <tfoot>
                <tr>
                    <td></td>
                </tr>
            </tfoot>
        </table>
</div>
```
表格行和列的合并
```
rowspan 合并行(竖着合并)
colspan 合并列(横着合并)
```
```html
<body>
    <div class="table">
        <table border="1" cellspacing="0">
            <!--表格头-->
            <thead>
                <!--表格行-->
                <tr>
                    <!--表格列，【注意】这里使用的是th-->
                    <th></th>
                    <th>星期一</th>
                    <th>星期二</th>
                    <th>星期三</th>
                    <th>星期四</th>
                    <th>星期五</th>
                </tr>
            </thead>
            <!--表格主体-->
            <tbody>
                <!--表格行-->
                <tr>
                	<td rowspan="3">上午</td>
                    <!--表格列，【注意】这里使用的是td-->
                    <td>语文</td>
                    <td>数学</td>
                    <td>英文</td>
                    <td>生物</td>
                    <td>化学</td>
                </tr>
                <tr>
                    <!--表格列，【注意】这里使用的是td-->
                    <td>语文</td>
                    <td>数学</td>
                    <td>英文</td>
                    <td>生物</td>
                    <td>化学</td>
                </tr>
                <tr>
                    <!--表格列，【注意】这里使用的是td-->
                    <td>语文</td>
                    <td>数学</td>
                    <td>英文</td>
                    <td>生物</td>
                    <td>化学</td>
                </tr>
                <tr>
                	<td rowspan ="2">下午</td>
                    <!--表格列，【注意】这里使用的是td-->
                    <td>语文</td>
                    <td>数学</td>
                    <td>英文</td>
                    <td>生物</td>
                    <td>化学</td>
                </tr>
                <tr>
                    <!--表格列，【注意】这里使用的是td-->
                    <td>语文</td>
                    <td>数学</td>
                    <td>英文</td>
                    <td>生物</td>
                    <td>化学</td>
                </tr>
            </tbody>
            <!--表格底部-->
            <tfoot>
                <tr>
                    <td colspan="6">课程表</td>
                </tr>
            </tfoot>
        </table>
    </div>
</body>
```

### 表单标签 form
表单是一个包含表单元素的区域
表单元素是允许用户在表单中输入内容，比如：文本域(textarea)、输入框(input)、单选框（）

### 表单的作用
表单用于显示、手机信息，并将信息提交给服务器
语法：
```
<form>允许出现表单控件</form>
```

