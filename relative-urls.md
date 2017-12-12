# Django Relative URLs

> 内容来源：[Python and Django Full Stack Web Developer Bootcamp](https://www.udemy.com/python-and-django-full-stack-web-developer-bootcamp/learn/v4/overview)

> 翻译整理：CK

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