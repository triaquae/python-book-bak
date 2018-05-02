### 标签嵌套规则

块元素可以包含内联元素或某些块元素，但内联元素却不能包含块元素，它只能包含其它的内联元素，例如：

`<div><div></div><h1></h1><p><p></div>` ✔️

`<a href=”#”><span></span></a>`  ✔️

`<span><div></div></span>` ❌

 块级元素不能放在p标签里面，比如

`<p><ol><li></li></ol></p>` ❌

`<p><div></div></p>`  ❌ 

有几个特殊的块级元素只能包含内嵌元素，不能再包含块级元素，这几个特殊的标签是：

```
h1、h2、h3、h4、h5、h6、p
```

1. li元素可以嵌入ul，ol，div等标签

```html
    <ul>
        <li>
            <ul>
                <li>
                    <div>

                    </div>
                </li>
                <li>
                    <ol>
                        <li></li>
                        <li></li>
                        <li></li>
                        <li></li>
                    </ol>
                </li>
            </ul>
        </li>
    </ul>
```



