# Django VS ASP.Net Core

> 本文基于个人学习 ASP.Net Core 以及 Django 的经验总结，有不对的地方求指教！
> 作者：CK

## ModelForm VS ViewModel
区别可能在于 ModelForm 可以根据 Model 快速生成自定义的 Form，Form 校验，以及存储表单到数据库。
ViewMode，则用于将不同Model的或者同一个Model中的部分field 合成一个Model对象，
它不对应数据库中的一个具体table，而是为了便于Contrller处理数据并传给View去展示。

## MTV VS MVC

+ Django 基于MTV: Model Template View
Controller 用的是 MVC 不知道是不是仅仅叫法的不同，
大体来看 ASP.Net Core 的 Controller 可以对应 Django 的 View
+ 视图和模板
    - ASP.NET Core 的Views 是一个文件夹，所有的 HTML 文件存储在其中，其 template 也是 html 文件，不过存在 Views/share 目录下.
    - Django 的 View 是 Python 文件，每个方法对应一个 Action， 其template 也是 html 文件，存储在 根目录的 template 下，并在 setting.py 中用变量设定 template 目录的位置。
