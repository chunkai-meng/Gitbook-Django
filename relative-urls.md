# Django Relative URLs

> 内容来源：[Python and Django Full Stack Web Developer Bootcamp](https://www.udemy.com/python-and-django-full-stack-web-developer-bootcamp/learn/v4/overview)

> 翻译整理：CK

相对 URL 重点在以下三个文件：

**Views 基本没有变化**
```
from django.shortcuts import render

# Create your views here.


def index(request):
    return render(request, 'basic_app/index.html')


def other(request):
    return render(request, 'basic_app/other.html')

```

**在 urls.py 中添加 app_name**
```
from django.conf.urls import url
from . import views

app_name = 'basic_app'
urlpatterns = [
    url(r'^$', views.index, name='index'),
    url(r'^other', views.other, name='other'),
]
```

**templates/app/index.html 中将超链接地址写成template tag的形式**
_注： app名:url名， url名在 urls.py中定义_
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Index</title>
  </head>
  <body>
    <h1>Welcome to Basic APP</h1>
    <h2>This is index.html</h2>
    <a href="{% url 'basic_app:other' %}">Other Page</a>
    <a href="{% url 'admin:index' %}">Admin Page</a>
    <a href="{% url 'index' %}">LINK TO INDEX</a>
  </body>
</html>

```