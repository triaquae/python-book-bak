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



