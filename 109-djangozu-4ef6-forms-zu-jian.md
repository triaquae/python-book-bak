### 9.1 forms组件
校验字段功能  
针对一个实例：注册用户讲解。  
模型：models.py  

```py
class UserInfo(models.Model):
    name=models.CharField(max_length=32)
    pwd=models.CharField(max_length=32)
    email=models.EmailField()
    tel=models.CharField(max_length=32)
```

模板: register.html:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<form action="" method="post">
    {% csrf_token %} 
    <div>
        <label for="user">用户名</label>
        <p><input type="text" name="name" id="name"></p>
    </div>
    <div>
        <label for="pwd">密码</label>
        <p><input type="password" name="pwd" id="pwd"></p>
    </div>
    <div>
        <label for="r_pwd">确认密码</label>
        <p><input type="password" name="r_pwd" id="r_pwd"></p>
    </div>
     <div>
        <label for="email">邮箱</label>
        <p><input type="text" name="email" id="email"></p>
    </div>
    <input type="submit">
</form>

</body>
</html>
```

视图函数：register

```py
# forms组件
from django.forms import widgets

wid_01=widgets.TextInput(attrs={"class":"form-control"})
wid_02=widgets.PasswordInput(attrs={"class":"form-control"})

class UserForm(forms.Form):
    name=forms.CharField(max_length=32,
                         widget=wid_01
                         )
    pwd=forms.CharField(max_length=32,widget=wid_02)
    r_pwd=forms.CharField(max_length=32,widget=wid_02)
    email=forms.EmailField(widget=wid_01)
    tel=forms.CharField(max_length=32,widget=wid_01)

def register(request):

    if request.method=="POST":
        form=UserForm(request.POST)
        if form.is_valid():
            print(form.cleaned_data)       # 所有干净的字段以及对应的值
        else:
            print(form.cleaned_data)       #
            print(form.errors)             # ErrorDict : {"校验错误的字段":["错误信息",]}
            print(form.errors.get("name")) # ErrorList ["错误信息",]
        return HttpResponse("OK")
    form=UserForm()
    return render(request,"register.html",locals())
```

### 9.2 渲染标签功能
渲染方式1  

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
   <!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
    <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>
<h3>注册页面</h3>
<div class="container">
    <div class="row">
        <div class="col-md-6 col-lg-offset-3">

                <form action="" method="post">
                    {% csrf_token %}
                    <div>
                        <label for="">用户名</label>
                        {{ form.name }}
                    </div>
                    <div>
                        <label for="">密码</label>
                        {{ form.pwd }}
                    </div>
                    <div>
                        <label for="">确认密码</label>
                        {{ form.r_pwd }}
                    </div>
                    <div>
                        <label for=""> 邮箱</label>
                        {{ form.email }}
                    </div>

                    <input type="submit" class="btn btn-default pull-right">
                </form>
        </div>
    </div>
</div>
</body>
</html>
```

渲染方式2

```html
<form action="" method="post">
                    {% csrf_token %}

                    {% for field in form %}
                        <div>
                            <label for="">{{ field.label }}</label>
                            {{ field }}
                        </div>
                    {% endfor %}
                    <input type="submit" class="btn btn-default pull-right">

</form>
```

渲染方式3

```py
<form action="" method="post">
    {% csrf_token %}

    {{ form.as_p }}
    <input type="submit" class="btn btn-default pull-right">

</form>
```

### 9.3 显示错误与重置输入信息功能
视图  

```py
def register(request):

    if request.method=="POST":
        form=UserForm(request.POST)
        if form.is_valid():
            print(form.cleaned_data)       # 所有干净的字段以及对应的值
        else:
            print(form.cleaned_data)       #
            print(form.errors)             # ErrorDict : {"校验错误的字段":["错误信息",]}
            print(form.errors.get("name")) # ErrorList ["错误信息",]
        return render(request,"register.html",locals())
    form=UserForm()
    return render(request,"register.html",locals())
```

模板

```html
<form action="" method="post" novalidate>
    {% csrf_token %}

    {% for field in form %}
        <div>
            <label for="">{{ field.label }}</label>
            {{ field }} <span class="pull-right" style="color: red">{{ field.errors.0 }}</span>
        </div>
    {% endfor %}
    <input type="submit" class="btn btn-default">

</form>
```

### 9.4 局部钩子与全局钩子
模板

```py
# forms组件
from django.forms import widgets

wid_01=widgets.TextInput(attrs={"class":"form-control"})
wid_02=widgets.PasswordInput(attrs={"class":"form-control"})

from django.core.exceptions import ValidationError
class UserForm(forms.Form):
    name=forms.CharField(max_length=32,
                         widget=wid_01
                         )
    pwd=forms.CharField(max_length=32,widget=wid_02)
    r_pwd=forms.CharField(max_length=32,widget=wid_02)
    email=forms.EmailField(widget=wid_01)
    tel=forms.CharField(max_length=32,widget=wid_01)

    # 局部钩子
    def clean_name(self):
        val=self.cleaned_data.get("name")
        if not val.isdigit():
            return val
        else:
            raise ValidationError("用户名不能是纯数字!")

    # 全局钩子

    def clean(self):
        pwd=self.cleaned_data.get("pwd")
        r_pwd=self.cleaned_data.get("r_pwd")

        if pwd==r_pwd:
            return self.cleaned_data
        else:
            raise ValidationError('两次密码不一致!')

def register(request):

    if request.method=="POST":
        form=UserForm(request.POST)
        if form.is_valid():
            print(form.cleaned_data)       # 所有干净的字段以及对应的值
        else:
            clean_error=form.errors.get("__all__")

        return render(request,"register.html",locals())
    form=UserForm()
    return render(request,"register.html",locals())
```

视图

```html
<form action="" method="post" novalidate>
            {% csrf_token %}

            {% for field in form %}
                <div>
                    <label for="">{{ field.label }}</label>
                    {{ field }}
                    <span class="pull-right" style="color: red">
                          {% if field.label == 'R pwd' %}
                          <span>{{ clean_error.0 }}</span>
                          {% endif %}
                          {{ field.errors.0 }}
                    </span>
                </div>
            {% endfor %}
            <input type="submit" class="btn btn-default">

</form>
```
