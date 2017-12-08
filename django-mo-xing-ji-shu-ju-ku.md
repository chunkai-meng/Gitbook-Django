# Django 模型及数据库

> 翻译整理：CK

## 1. 模型及数据库

### 说明：

* We use Models to incorporate Database into a Django Project
* Django comes equipped with SQLite
* Django can connect to a variety of SQL engine backends
* In the setting.py file we can edit the ENGIN parameter used for DATABASE
* To create an actual model, we use a class structure inside the relevant applications models.py file
* Each attribute of the class represents a field, which is like a column name with constrains in SQL
* Each attribute has type of field and constraints.
* Models will reference each other to represent the table relationships.
* A foreign key denotes that the column coincides with a primary key of another table

### 步骤:

## 2. Django Admin

* 在setting.py中注册 app: first\_app

  ```
  INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'first_app',
  ]
  ```

* 添加model（数据表），atrribute（字段），字段类型，约束及外键

\`\`\`  
from django.db import models

# Create your models here.

class Topic\(models.Model\):  
    top\_name = models.CharField\(max\_length=246, unique=True\)

```
def __str__(self):
    return self.top_name
```

class Webpage\(models.Model\):  
    topic = models.ForeignKey\(Topic, on\_delete=models.CASCADE\)  
    name = models.CharField\(max\_length=264, unique=True\)  
    url = models.URLField\(unique=True\)

```
def __str__(self):
    return self.name
```

class AccessRecord\(models.Model\):  
    name = models.ForeignKey\(Webpage,on\_delete=models.CASCADE\)  
    date = models.DateField\(unique=True\)

```
def __str__(self):
    return str(self.date)
```

```
+ 移植
```

root@38c80f8e29c3:/code\# python manage.py migrate  
Operations to perform:  
  Apply all migrations: admin, auth, contenttypes, sessions  
Running migrations:  
  Applying contenttypes.0001\_initial... OK  
  Applying auth.0001\_initial... OK  
  Applying admin.0001\_initial... OK  
  Applying admin.0002\_logentry\_remove\_auto\_add... OK  
  Applying contenttypes.0002\_remove\_content\_type\_name... OK  
  Applying auth.0002\_alter\_permission\_name\_max\_length... OK  
  Applying auth.0003\_alter\_user\_email\_max\_length... OK  
  Applying auth.0004\_alter\_user\_username\_opts... OK  
  Applying auth.0005\_alter\_user\_last\_login\_null... OK  
  Applying auth.0006\_require\_contenttypes\_0002... OK  
  Applying auth.0007\_alter\_validators\_add\_error\_messages... OK  
  Applying auth.0008\_alter\_user\_username\_max\_length... OK  
  Applying sessions.0001\_initial... OK

```

```

root@38c80f8e29c3:/code\# python manage.py makemigrations first\_app  
Migrations for 'first\_app':  
  first\_app/migrations/0001\_initial.py

* Create model AccessRecord
* Create model Topic
* Create model Webpage
* Add field name to accessrecor

\`\`\`

```
root@38c80f8e29c3:/code# python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, first_app, sessions
Running migrations:
  Applying first_app.0001_initial... OK
```

* 在对应app的admin.py中注册admin将要管理的模块：

  ```
  from django.contrib import admin
  from first_app.models import AccessRecord, Topic, Webpage
  # Register your models here.
  admin.site.register(AccessRecord)
  admin.site.register(Topic)
  admin.site.register(Webpage)
  ```

* 创建超级用户：（“root@38c80f8e29c3:/code” 说明当前主机是容器）

  ```
  root@38c80f8e29c3:/code# python manage.py createsuperuser
  Username (leave blank to use 'root'): ck
  Email address: willxxx@gmail.com
  Password:
  Password (again):
  Superuser created successfully.
  ```

* 填充伪数据  
  \`\`\`python  
  import os

  # Configure settings for project

  # Need to run this before calling models from application!

  os.environ.setdefault\('DJANGO\_SETTINGS\_MODULE','first\_project.settings'\)

import django

# Import settings

django.setup\(\)

import random  
from first\_app.models import Topic,Webpage,AccessRecord  
from faker import Faker

fakegen = Faker\(\)  
topics = \['Search','Social','Marketplace','News','Games'\]

def add\_topic\(\):  
    t = Topic.objects.get\_or\_create\(top\_name=random.choice\(topics\)\)\[0\]  
    t.save\(\)  
    return t

def populate\(N=5\):  
    '''  
    Create N Entries of Dates Accessed  
    '''

```
for entry in range(N):

    # Get Topic for Entry
    top = add_topic()

    # Create Fake Data for entry
    fake_url = fakegen.url()
    fake_date = fakegen.date()
    fake_name = fakegen.company()

    # Create new Webpage Entry
    webpg = Webpage.objects.get_or_create(topic=top,url=fake_url,name=fake_name)[0]

    # Create Fake Access Record for that page
    # Could add more of these if you wanted...
    accRec = AccessRecord.objects.get_or_create(name=webpg,date=fake_date)[0]
```

if **name** == '**main**':  
    print\("Populating the databases...Please Wait"\)  
    populate\(20\)  
    print\('Populating Complete'\)

```
+ 执行populate_first_app.py
```

root@c271100f853b:/code\# python populate\_first\_app.py  
Populating the databases...Please Wait  
Populating Complete  
\`\`\`

## Django MVC



