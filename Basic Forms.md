# Django MTV

> 内容来源：[Python and Django Full Stack Web Developer Bootcamp](https://www.udemy.com/python-and-django-full-stack-web-developer-bootcamp/learn/v4/overview)
> 翻译整理：CK

## 1. 优点：

+ 快速生成 HTML 表单
在first_app目录中创建 forms.py

```
from django import forms

class FormName(forms.Form):
    name = forms.CharField()
    email = forms.EmailField()
    text = forms.CharField(widget=forms.Textarea)

```


+ 校验数据并转换成Python数据结构
+ 替Models创建表单式样
+ 快速从form更新models
+ 隐藏字段