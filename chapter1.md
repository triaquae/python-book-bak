* # python基础

* GitBook allows you to organize your book into chapters, each chapter is stored in a separate file like this one.

![](/assets/技能图谱设计图.png)





```py
def hosts_status(request):

    hosts_data_serializer = serializer.StatusSerializer(request,REDIS_OBJ)
    hosts_data = hosts_data_serializer.by_hosts()

    return HttpResponse(json.dumps(hosts_data))
```



