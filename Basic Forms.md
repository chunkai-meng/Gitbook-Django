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
        
3. **校验数据**

    ```py
    from django import forms
    # 导入django.core 的 validators包
    from django.core import validators

    # 自定义校验方法
    def check_for_z(value):
        if value[0].lower() != 'z':
            raise forms.ValidationError("Name NEEDS TO START WITH Z")

    class FormName(forms.Form):
        # 校验器是一个列表，可以有多个校验器（validator）
        name = forms.CharField(validators=[check_for_z,])
        email = forms.EmailField()
        text = forms.CharField(widget=forms.Textarea)
        # 在form 中添加一个隐藏的input 字段
        botcatcher = forms.CharField(required=False,
                                     widget=forms.HiddenInput,
                                    validators=[validators.MaxLengthValidator(10)])
        
    ```    

4. **映射URL**
    编辑：urls.py
    ```py
    url(r'^form/', views.form_name_view, name='form')
    ```
4. **替Models创建表单式样**
    编辑 templates/first_app/form_name_view.html
    ```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Form Name View</title>
    <!-- 添加bootstrap -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
  </head>
  <body>
    <div class="container">
      <form method="post" >
        <!-- 将表单拆分成多个项 -->
        {{ form.as_p }}
        <!-- 防止跨站点伪造请求 -->
        {% csrf_token %}
        <input type="submit" class="btn btn-primary" name="" value="Submit">
      </form>
    </div>
  </body>
</html>
    ```

5. **快速从form更新models**

6. **隐藏字段**