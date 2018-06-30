#
## 12.1 Django的分页器（paginator）
view

```py
from django.shortcuts import render,HttpResponse
# Create your views here.
from app01.models import *
from django.core.paginator import Paginator, EmptyPage, PageNotAnInteger
def index(request):
'''
批量导入数据:

Booklist=[]
for i in range(100):
Booklist.append(Book(title="book"+str(i),price=30+i*i))
Book.objects.bulk_create(Booklist)
'''

'''
分页器的使用:

book_list=Book.objects.all()

paginator = Paginator(book_list, 10)

print("count:",paginator.count) #数据总数
print("num_pages",paginator.num_pages) #总页数
print("page_range",paginator.page_range) #页码的列表

page1=paginator.page(1) #第1页的page对象
for i in page1: #遍历第1页的所有数据对象
print(i)

print(page1.object_list) #第1页的所有数据

page2=paginator.page(2)

print(page2.has_next()) #是否有下一页
print(page2.next_page_number()) #下一页的页码
print(page2.has_previous()) #是否有上一页
print(page2.previous_page_number()) #上一页的页码

# 抛错
#page=paginator.page(12) # error:EmptyPage

#page=paginator.page("z") # error:PageNotAnInteger
'''

book_list=Book.objects.all()

paginator = Paginator(book_list, 10)
page = request.GET.get('page',1)
currentPage=int(page)

try:
print(page)
book_list = paginator.page(page)
except PageNotAnInteger:
book_list = paginator.page(1)
except EmptyPage:
book_list = paginator.page(paginator.num_pages)

return render(request,"index.html",{"book_list":book_list,"paginator":paginator,"currentPage":currentPage})
```

index.html:

```py
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/3.3.7/css/bootstrap.min.css"
    integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>

<div class="container">

    <h4>分页器</h4>
    <ul>

        {% for book in book_list %}
             <li>{{ book.title }} -----{{ book.price }}</li>
        {% endfor %}

     </ul>
    <ul class="pagination" id="pager">

                 {% if book_list.has_previous %}
                    <li class="previous"><a href="/index/?page={{ book_list.previous_page_number }}">上一页</a></li>
                 {% else %}
                    <li class="previous disabled"><a href="#">上一页</a></li>
                 {% endif %}
                 {% for num in paginator.page_range %}

                     {% if num == currentPage %}
                       <li class="item active"><a href="/index/?page={{ num }}">{{ num }}</a></li>
                     {% else %}
                       <li class="item"><a href="/index/?page={{ num }}">{{ num }}</a></li>

                     {% endif %}
                 {% endfor %}

                 {% if book_list.has_next %}
                    <li class="next"><a href="/index/?page={{ book_list.next_page_number }}">下一页</a></li>
                 {% else %}
                    <li class="next disabled"><a href="#">下一页</a></li>
                 {% endif %}

            </ul>
</div>

</body>
</html>
```

扩展

```py
def index(request):

    book_list=Book.objects.all()
    paginator = Paginator(book_list, 15)
    page = request.GET.get('page',1)
    currentPage=int(page)

    #  如果页数十分多时，换另外一种显示方式
    if paginator.num_pages>11:
        if currentPage-5<1:
            pageRange=range(1,11)
        elif currentPage+5>paginator.num_pages:
            pageRange=range(currentPage-5,paginator.num_pages+1)
        else:
            pageRange=range(currentPage-5,currentPage+5)
    else:
        pageRange=paginator.page_range
    try:
        print(page)
        book_list = paginator.page(page)
    except PageNotAnInteger:
        book_list = paginator.page(1)
    except EmptyPage:
        book_list = paginator.page(paginator.num_pages)

    return render(request,"index.html",locals())
```
