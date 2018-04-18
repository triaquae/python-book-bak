# 1、下拉菜单

```html
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
    <li role="separator" class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

**aria-haspopup** :true表示点击的时候会出现菜单或是浮动元素； false表示没有pop-up效果。

**aria-expanded**:表示展开状态。默认为undefined, 表示当前展开状态未知。其它可选值：true表示元素是展开的；false表示元素不是展开的

**aria-labelledby**：当想要的标签文本已在其他元素中存在时，可以使用aria-labelledby，并将其值为所有读取的元素的id。如下：

当ul获取到焦点时，屏幕阅读器是会读：“选择您的职位”

**data-toggle**: 表示什么事件类型发生

# 2.模态框

```html
<h2>创建模态框</h2>
<!-- 按钮触发模态框 -->
<button class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">删除</button>
<!-- 模态框（Modal） -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
<div class="modal-dialog">
    <div class="modal-content">
        <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
            <h4 class="modal-title" id="myModalLabel">是否删除</h4>
        </div>
        <div class="modal-body">你确定要删除吗？</div>
        <div class="modal-footer">
            <button type="button" class="btn btn-default" data-dismiss="modal">关闭</button>
            <button type="button" class="btn btn-danger">确定</button>
        </div>
    </div>
    <!-- /.modal-content -->
</div>
<!-- /.modal -->
</div>
```



在模态框中需要注意两点：

* 1. 第一是**.modal**，用来把 &lt;div&gt;的内容识别为模态框。
  2. 第二是**.fade    **class。当模态框被切换时，它会引起内容淡入淡出。
* **aria-labelledby="myModalLabel"**
  ，该属性引用模态框的标题。
* 属性
  **aria-hidden="true"**
  用于保持模态窗口不可见，直到触发器被触发为止（比如点击在相关的按钮上）。
* &lt;
  div class="modal-header"
  &gt;
  ，modal-header 是为模态窗口的头部定义样式的类。
* **class="close"**
  ，close 是一个 CSS class，用于为模态窗口的关闭按钮设置样式。
* **data-dismiss="modal"**
  ，是一个自定义的 HTML5 data 属性。在这里它被用于关闭模态窗口。
* **class="modal-body"**
  ，是 Bootstrap CSS 的一个 CSS class，用于为模态窗口的主体设置样式。
* **class="modal-footer"**
  ，是 Bootstrap CSS 的一个 CSS class，用于为模态窗口的底部设置样式。
* **data-toggle="modal"**
  ，HTML5 自定义的 data 属性 data-toggle 用于打开模态窗口。



