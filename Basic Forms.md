# DJANGO FORM

> 内容来源：[Python and Django Full Stack Web Developer Bootcamp](https://www.udemy.com/python-and-django-full-stack-web-developer-bootcamp/learn/v4/overview)
> 翻译整理：CK

## 步骤：

1. **快速生成 HTML 表单**

    在first_app目录中创建 forms.py
    
    ```py
    from django import forms
    
    class FormName(forms.Form):
        name = forms.CharField()
        email = forms.EmailField()
        text = forms.CharField(widget=forms.Textarea)
    ```


2. **校验数据并转换成Python数据结构**
    
    在 views.py 中添加
    ```py
    from . import forms
    
    #... 
    
    def form_name_view(request):
    form = forms.FormName()

    if request.method == 'POST':
        form = forms.FormName(request.POST)

        if form.is_valid():
            print("VALIDATION SUCCESS!")
            print(form.cleaned_data['name'])
            print(form.cleaned_data['email'])
            print(form.cleaned_data['text'])

    return render(request, 'first_app/form_name_view.html', {'form': form})
    ```
    `form_name_view` 负责在client 请求网页（GET：默认）的时候提供 form 表单，
    也可在client 提交（POST）的时候处理提交上来的内容。
        
+ **校验数据**
    - 隐藏字段
    - 校验

+ **替Models创建表单式样**
+ **快速从form更新models**
+ **隐藏字段**