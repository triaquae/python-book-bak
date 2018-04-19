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

# 2、模态框

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
* &lt;div class="modal-header"&gt;
  ，modal-header 是为模态窗口的头部定义样式的类。
* **class="close"**，close 是一个 CSS class，用于为模态窗口的关闭按钮设置样式。
* **data-dismiss="modal"**，是一个自定义的 HTML5 data 属性。在这里它被用于关闭模态窗口。
* **class="modal-body"**，是 Bootstrap CSS 的一个 CSS class，用于为模态窗口的主体设置样式。
* **class="modal-footer"**，是 Bootstrap CSS 的一个 CSS class，用于为模态窗口的底部设置样式。
* **data-toggle="modal"**，HTML5 自定义的 data 属性 data-toggle 用于打开模态窗口。

#### 通过js控制模态框弹出

```html
    <body>
        <div class="container">
            <div class="row">
                <div class="col-md-4">
                    <div class="panel panel-success">
                        <div class="panel-heading">
                            <div class="panel-title">

                            </div>

                        </div>
                        <div class="panel-body">
                            <h2>创建模态框</h2>
                            <!-- 按钮触发模态框 -->
                            <button class="btn btn-primary btn-lg" data-toggle="modal" id="delete">删除</button>
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
                        </div>
                    </div>
                </div>
            </div>

        </div>

        <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
        <script src="https://cdn.bootcss.com/jquery/1.12.4/jquery.min.js"></script>
        <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
        <script src="https://cdn.bootcss.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
        <script type="text/javascript">
            $(function(){
                //通过jquery控制模态框弹出
                $('#delete').click(function(){
                    $('#myModal').modal({
                        keyboard:false
                    })
                })

            })
        </script>
    </body>
```

# 3、滚动监听

```html
<nav id="navbar-example" class="navbar navbar-default navbar-static" role="navigation">
    <div class="container-fluid">
        <div class="navbar-header">
            <button class="navbar-toggle" type="button" data-toggle="collapse" data-target=".bs-js-navbar-scrollspy">
            <span class="sr-only">切换导航</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
        </button>
            <a class="navbar-brand" href="#">luffy</a>
        </div>
        <div class="collapse navbar-collapse bs-js-navbar-scrollspy">
            <ul class="nav navbar-nav">
                <li>
                    <a href="#ios">iOS</a>
                </li>
                <li>
                    <a href="#svn">SVN</a>
                </li>
                <li class="dropdown">
                    <a href="#" id="navbarDrop1" class="dropdown-toggle" data-toggle="dropdown">Java
                        <b class="caret"></b>
                    </a>
                    <ul class="dropdown-menu" role="menu" aria-labelledby="navbarDrop1">
                        <li>
                            <a href="#jmeter" tabindex="-1">jmeter</a>
                        </li>
                        <li>
                            <a href="#ejb" tabindex="-1">ejb</a>
                        </li>
                        <li class="divider"></li>
                        <li>
                            <a href="#spring" tabindex="-1">spring</a>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</nav>
<div data-spy="scroll" data-target="#navbar-example" data-offset="0" style="height:200px;overflow:auto; position: relative;">
    <h4 id="ios">iOS</h4>
    <p>iOS 是一个由苹果公司开发和发布的手机操作系统。最初是于 2007 年首次发布 iPhone、iPod Touch 和 Apple TV。iOS 派生自 OS X，它们共享 Darwin 基础。OS X 操作系统是用在苹果电脑上，iOS 是苹果的移动版本。
    </p>
    <h4 id="svn">SVN</h4>
    <p>Apache Subversion，通常缩写为 SVN，是一款开源的版本控制系统软件。Subversion 由 CollabNet 公司在 2000 年创建。但是现在它已经发展为 Apache Software Foundation 的一个项目，因此拥有丰富的开发人员和用户社区。
    </p>
    <h4 id="jmeter">jMeter</h4>
    <p>jMeter 是一款开源的测试软件。它是 100% 纯 Java 应用程序，用于负载和性能测试。
    </p>
    <h4 id="ejb">EJB</h4>
    <p>Enterprise Java Beans（EJB）是一个创建高度可扩展性和强大企业级应用程序的开发架构，部署在兼容应用程序服务器（比如 JBOSS、Web Logic 等）的 J2EE 上。
    </p>
    <h4 id="spring">Spring</h4>
    <p>Spring 框架是一个开源的 Java 平台，为快速开发功能强大的 Java 应用程序提供了完备的基础设施支持。
    </p>
    <p>Spring 框架最初是由 Rod Johnson 编写的，在 2003 年 6 月首次发布于 Apache 2.0 许可证下。
    </p>

</div>
```

通过javascript 调用滚动监听，选取要监听的元素，然后调用.scrollspy\(\)函数

```javascript
$('.navbar-header').scrollspy('.bs-js-navbar-scrollspy')
```

像后面还介绍了：  
   0. 手风琴效果  
 data-toggle="collapse" 添加到您想要展开或折叠的组件的链接上。

href 或 data-target 属性添加到父组件，它的值是子组件的 id。

data-parent 属性把折叠面板（accordion）的 id 添加到要展开或折叠的组件的链接2

1. 弹出框

2. 警告框

3. 轮播

      **通过 data 属性**：使用 data 属性可以很容易控制轮播（Carousel）的位置。

* 属性**data-slide**接受关键字prev或next，用来改变幻灯片相对于当前位置的位置
* 使用**data-slide-to**来向轮播传递一个原始滑动索引，**data-slide-to="2" **将把滑块移动到一个特定的索引，索引从 0 开始计数。
* **data-ride="carousel"**属性用于标记轮播在页面加载时就开始动画播放

上面是常用Bootstrap插件，相关代码都在Bootstrap的官网上。大家自行copy一定要演示

