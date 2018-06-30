### 10.1 用户认证
#### 一、auth模块

```py
from django.contrib import auth
```

django.contrib.auth中提供了许多方法，这里主要介绍其中的三个：

1.1 、authenticate()     
提供了用户认证，即验证用户名以及密码是否正确,一般需要username  password两个关键字参数  
如果认证信息有效，会返回一个  User  对象。authenticate()会在User 对象上设置一个属性标识那种认证后端认证了该用户，且该信息在后面的登录过程中是需要的。当我们试图登陆一个从数据库中直接取出来不经过authenticate()的User对象会报错的！！  

```py
user = authenticate(username='someone',password='somepassword')
```

1.2 、login(HttpRequest, user)　　  
该函数接受一个HttpRequest对象，以及一个认证了的User对象  
此函数使用django的session框架给某个已认证的用户附加上session id等信息。  

```py
from django.contrib.auth import authenticate, login

def my_view(request):
  username = request.POST['username']
  password = request.POST['password']
  user = authenticate(username=username, password=password)
  if user is not None:
    login(request, user)
    # Redirect to a success page.
    ...
  else:
    # Return an 'invalid login' error message.
    ...
```

1.3 、logout(request) 注销用户

```py
from django.contrib.auth import logout

def logout_view(request):
  logout(request)
  # Redirect to a success page.
```

该函数接受一个HttpRequest对象，无返回值。当调用该函数时，当前请求的session信息会全部清除。该用户即使没有登录，使用该函数也不会报错。

#### 二、User对象
User 对象属性：username， password（必填项）password用哈希算法保存到数据库  
2.1 、user对象的 is_authenticated()  
如果是真正的 User 对象，返回值恒为 True 。 用于检查用户是否已经通过了认证。  
通过认证并不意味着用户拥有任何权限，甚至也不检查该用户是否处于激活状态，这只是表明用户成功的通过了认证。 这个方法很重要, 在后台用request.user.is_authenticated()判断用户是否已经登录，如果true则可以向前台展示request.user.name  
要求：  
1  用户登陆后才能访问某些页面，  
2  如果用户没有登录就访问该页面的话直接跳到登录页面  
3  用户在跳转的登陆界面中完成登陆后，自动访问跳转到之前访问的地址  

方法1:

```py
def my_view(request):
  if not request.user.is_authenticated():
    return redirect('%s?next=%s' % (settings.LOGIN_URL, request.path))
```

方法2:  
django已经为我们设计好了一个用于此种情况的装饰器：login_requierd()  

```py
from django.contrib.auth.decorators import login_required

@login_required
def my_view(request):
  ...
```

若用户没有登录，则会跳转到django默认的 登录URL '/accounts/login/ ' (这个值可以在settings文件中通过LOGIN_URL进行修改)。并传递  当前访问url的绝对路径 (登陆成功后，会重定向到该路径)。

2.2 、创建用户

使用 create_user 辅助函数创建用户:

```py
from django.contrib.auth.models import User
user = User.objects.create_user（username='',password='',email=''）
```

2.3 、check_password(passwd)  
用户需要修改密码的时候 首先要让他输入原来的密码 ，如果给定的字符串通过了密码检查，返回 True  

2.4 、修改密码  
使用 set_password() 来修改密码  

```py
user = User.objects.get(username='')
user.set_password(password='')
user.save　
```

2.5 、简单示例  
注册：  

```py
def sign_up(request):

    state = None
    if request.method == 'POST':

        password = request.POST.get('password', '')
        repeat_password = request.POST.get('repeat_password', '')
        email=request.POST.get('email', '')
        username = request.POST.get('username', '')
        if User.objects.filter(username=username):
                state = 'user_exist'
        else:
                new_user = User.objects.create_user(username=username, password=password,email=email)
                new_user.save()

                return redirect('/book/')
    content = {
        'state': state,
        'user': None,
    }
    return render(request, 'sign_up.html', content)　　
```

修改密码：

```py
@login_required
def set_password(request):
    user = request.user
    state = None
    if request.method == 'POST':
        old_password = request.POST.get('old_password', '')
        new_password = request.POST.get('new_password', '')
        repeat_password = request.POST.get('repeat_password', '')
        if user.check_password(old_password):
            if not new_password:
                state = 'empty'
            elif new_password != repeat_password:
                state = 'repeat_error'
            else:
                user.set_password(new_password)
                user.save()
                return redirect("/log_in/")
        else:
            state = 'password_error'
    content = {
        'user': user,
        'state': state,
    }
    return render(request, 'set_password.html', content)
```
