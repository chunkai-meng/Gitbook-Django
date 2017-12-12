# Django ModelForm

> 内容来源：[Python and Django Full Stack Web Developer Bootcamp](https://www.udemy.com/python-and-django-full-stack-web-developer-bootcamp/learn/v4/overview)

> 翻译整理：CK

**ModelForm 有点类似 ASP.Net Core 中的 ViewModel 的功能**
区别可能在于 ModelForm 可以根据 Model 快速生成自定义的 Form，Form 校验，以及存储表单到数据库。
ViewMode，则用于将不同Model的或者同一个Model中的部分field 合成一个Model对象，
它不对应数据库中的一个具体table，而是为了便于Contrller处理数据并传给View去展示。

