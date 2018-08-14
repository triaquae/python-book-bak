#### 1. 问：为什么程序需要权限控制？
答：生活中的权限限制，① 看灾难片电影《2012》中富人和权贵有权登上诺亚方舟，穷苦老百姓只有等着灾难的来临；② 屌丝们，有没有想过为什么那些长得漂亮身材好的姑娘在你身边不存在呢？因为有钱人和漂亮姑娘都是珍贵稀有的，稀有的人在一起玩耍和解锁各种姿势。而你，无权拥有他们，只能自己玩自己了。  

程序开发时的权限控制，对于不同用户使用系统时候就应该有不同的功能，如：

  - 普通员工
  - 部门主管
  - 总监
  - 总裁

所以，只要有不同角色的人员来使用系统，那么就肯定需要权限系统。

#### 2. 问：为什么要开发权限组件？

答：假设你今年25岁，从今天开始写代码到80岁，每年写5个项目，那么你的一生就会写275个项目，保守估计其中应该有150+个都需要用到权限控制，为了以后不再重复的写代码，所以就开发一个权限组件以便之后55年的岁月中使用。 亲，不要太较真哦，你觉得程序员能到80岁么，哈哈哈哈哈哈哈

偷偷告诉你：老程序员开发速度快，其中一个原因是经验丰富，另外一个就是他自己保留了很多组件，新系统开发时，只需把组件拼凑起来基本就可以完成。

#### 3. 问：web开发中权限指的是什么？

答：web程序是通过 url 的切换来查看不同的页面（功能），所以权限指的其实就是URL，对url控制就是对权限的控制。

结论：一个人有多少个权限就取决于他有多少个URL的访问权限。

### 权限表结构设计：第一版

问答环节中已得出权限就是URL的结论，那么就可以开始设计表结构了。

  - 一个用户可以有多个权限。
  - 一个权限可以分配给多个用户

你设计的表结构大概会是这个样子：

![](https://hcdn1.luffycity.com/data/python-book/1201/01.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/02.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/03.png)  

现在，此时此刻是不是觉得自己设计出的表结构棒棒哒！！！

**But**，无论是是否承认，你还是too young too native，因为老汉腚眼一看就有问题....

问题：假设 “老男孩”和“Alex” 这俩货都是老板，老板的权限一定是非常多。那么试想，如果给这俩货分配权限时需要在【用户权限关系表中】添加好多条数据。假设再次需要对老板的权限进行修改时，又需要在【用户权限关系表】中找到这俩人所有的数据进行更新，太他妈烦了吧！！！ 类似的，如果给其他相同角色的人来分配权限时，必然会非常繁琐。


### 权限表结构设计：第二版

聪明机智的一定在上述的表述中看出了写门道，如果对用户进行角色的划分，然后对角色进行权限的分配，这不就迎刃而解了么。

  - 一个人可以有多个角色。
  - 一个角色可以有多个人。
  - 一个角色可以有多个权限。
  - 一个权限可以分配给多个角色。

表结构设计：

![](https://hcdn1.luffycity.com/data/python-book/1201/04.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/05.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/06.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/07.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/08.png)  

 这次调整之后，由原来的【基于用户的权限控制】转换成【基于角色的权限控制】，以后再进行分配权限时只需要给指定角色分配一次权限，给众多用户再次分配指定角色即可。

 models.py示例

 ```py
 from django.db import models


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name
 ```

 小伙子，告诉你一个事实，不经意间，你居然设计出了一个经典的权限访问控制系统：rbac（Role-Based Access Control）基于角色的权限访问控制。你这么优秀，为什么不来老男孩IT教育？路飞学城也行呀！ 哈哈哈哈。

注意：现在的设计还不是最终版，但之后的设计都是在此版本基础上扩增的，为了让大家能够更好的理解，我们暂且再此基础上继续开发，直到遇到无法满足的情况，再进行整改。

源码示例: <a href='https://hcdn1.luffycity.com/data/python-book/1201/luffy_permission（示例一）.zip'>点击下载</a>

### 客户管理之权限控制

学习知识最好的方式就是试错，坑踩多了那么学到的知识自然而然就多了，所以接下里下来我们用《客户管理》系统为示例，提出功能并实现，并且随着功能越来越多，一点点来找出问题，并解决问题。

目录结构：

```py
luffy_permission/
├── db.sqlite3
├── luffy_permission
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
├── rbac            # 权限组件，便于以后应用到其他系统
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── templates
└── web            # 客户管理业务
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    └── views.py
```

rbac/models.py

```py
from django.db import models


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name
```

web/models.py

```py
from django.db import models


class Customer(models.Model):
    """
    客户表
    """
    name = models.CharField(verbose_name='姓名', max_length=32)
    age = models.CharField(verbose_name='年龄', max_length=32)
    email = models.EmailField(verbose_name='邮箱', max_length=32)
    company = models.CharField(verbose_name='公司', max_length=32)


class Payment(models.Model):
    """
    付费记录
    """
    customer = models.ForeignKey(verbose_name='关联客户', to='Customer')
    money = models.IntegerField(verbose_name='付费金额')
    create_time = models.DateTimeField(verbose_name='付费时间', auto_now_add=True)
```

《客户管理》系统截图：基本增删改查和Excel导入源码下载：

![](https://hcdn1.luffycity.com/data/python-book/1201/09.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/10.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/11.png)  

以上简易版客户管理系统中的URL有：

客户管理
- 客户列表：/customer/list/
- 添加客户：/customer/add/
- 删除客户：/customer/list/(?P<cid>\d+)/
- 修改客户：/customer/edit/(?P<cid>\d+)/
- 批量导入：/customer/import/
- 下载模板：/customer/tpl/

账单管理

- 账单列表：/payment/list/
- 添加账单：/payment/add/
- 删除账单：/payment/del/(?P<pid>\d+)/
- 修改账单：/payment/edit/<?P<pid>\d+/

那么接下来，我们就在权限组件中录入相关信息：

- 录入权限
- 创建用户
- 创建角色
- 用户分配角色
- 角色分配权限


这么一来，用户登录时，就可以根据自己的【用户】找到所有的角色，再根据角色找到所有的权限，再将权限信息放入session，以后每次访问时候需要先去session检查是否有权访问。

已录入权限数据源码下载：

含用户登录权限源码下载：

含用户登录权限源码下载：

至此，基本的权限控制已经完成，基本流程为：

- 用户登录，获取权限信息并放入session
- 用户访问，在中间件从session中获取用户权限信息，并进行权限验证。

所有示例中的账户信息：

 ```py
 账户一：
     用户名：alex
        密码：123

 账户二：
     用户名：wupeiqi
        密码：123
 ```

### 客户管理之动态“一级”菜单


上述过程中的菜单是在程序中定义好的，无法根据用户权限进行动态配置。

那么，接下来我们来完成一个 “单级菜单”的功能：

```py
from django.db import models


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    icon = models.CharField(verbose_name='图标', max_length=32, null=True, blank=True, help_text='菜单才设置图标')
    is_menu = models.BooleanField(verbose_name='是否是菜单', default=False)

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name
```

 这样可以开发出一个单级菜单的示例：

![](https://hcdn1.luffycity.com/data/python-book/1201/12.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/13.png)  

 示例源码下载：

### 客户管理之动态“二级”菜单

对于功能比较少的应用程序 “一级菜单” 基本可以满足需求，但是功能多的程序就需要 “二级菜单” 了，并且访问时候需要默认选中指定菜单。

表结构

```py
from django.db import models


class Menu(models.Model):
    """
    菜单
    """
    title = models.CharField(verbose_name='菜单', max_length=32)
    icon = models.CharField(verbose_name='图标', max_length=32)

    def __str__(self):
        return self.title


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    menu = models.ForeignKey(verbose_name='菜单', to='Menu', null=True, blank=True, help_text='null表示非菜单')

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name
```

示例效果：
![](https://hcdn1.luffycity.com/data/python-book/1201/14.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/15.png)  

示例源码下载：

### 客户管理之默认展开非菜单URL

由于很多URL都是不能作为菜单，所以当点击该类功能时，是无法默认展开菜单的，如：

- 删除
- 修改
- ...

![](https://hcdn1.luffycity.com/data/python-book/1201/16.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/17.png)  

此类页面只能通过菜单页面二次点击才能跳转，此时也应该为他们默认展开原菜单。

```py
from django.db import models


class Menu(models.Model):
    """
    菜单
    """
    title = models.CharField(verbose_name='菜单', max_length=32)
    icon = models.CharField(verbose_name='图标', max_length=32)

    def __str__(self):
        return self.title


class Permission(models.Model):
    """
    权限表
    """
    title = models.CharField(verbose_name='标题', max_length=32)
    url = models.CharField(verbose_name='含正则的URL', max_length=128)

    pid = models.ForeignKey(verbose_name='默认选中权限', to='Permission', related_name='ps', null=True, blank=True,
                            help_text="对于无法作为菜单的URL，可以为其选择一个可以作为菜单的权限，那么访问时，则默认选中此权限",
                            limit_choices_to={'menu__isnull': False})

    menu = models.ForeignKey(verbose_name='菜单', to='Menu', null=True, blank=True, help_text='null表示非菜单')

    def __str__(self):
        return self.title


class Role(models.Model):
    """
    角色
    """
    title = models.CharField(verbose_name='角色名称', max_length=32)
    permissions = models.ManyToManyField(verbose_name='拥有的所有权限', to='Permission', blank=True)

    def __str__(self):
        return self.title


class UserInfo(models.Model):
    """
    用户表
    """
    name = models.CharField(verbose_name='用户名', max_length=32)
    password = models.CharField(verbose_name='密码', max_length=64)
    email = models.CharField(verbose_name='邮箱', max_length=32)
    roles = models.ManyToManyField(verbose_name='拥有的所有角色', to='Role', blank=True)

    def __str__(self):
        return self.name
```

功能完成后的示例如下：

![](https://hcdn1.luffycity.com/data/python-book/1201/18.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/19.png)  

示例源码下载：

### 客户管理之访问路径导航
如果想要保留放的地址，那么就可以通过在权限配置中获取此功能，示例如下：

![](https://hcdn1.luffycity.com/data/python-book/1201/20.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/21.png)  

示例源码下载：

### 客户管理之 权限粒度控制按钮级别

不同用户登录系统时候，根据权限不同来控制是否限制指定按钮，如：

![](https://hcdn1.luffycity.com/data/python-book/1201/22.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/23.png)  

示例源码下载：

### 客户管理之 编辑权限和分配权限
给用户进行权限的分配。

![](https://hcdn1.luffycity.com/data/python-book/1201/24.png)  

![](https://hcdn1.luffycity.com/data/python-book/1201/25.png)  

示例源码下载：
