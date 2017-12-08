# Django 模型及数据库 {#django-模型及数据库}



&gt; 翻译整理：CK



\#\# 1. 模型及数据库



\#\#\# 说明： 



+ We use Models to incorporate Database into a Django Project

+ Django comes equipped with SQLite

+ Django can connect to a variety of SQL engine backends

+ In the setting.py file we can edit the ENGIN parameter used for DATABASE

+ To create an actual model, we use a class structure inside the relevant applications models.py file

+ Each attribute of the class represents a field, which is like a column name with constrains in SQL

+ Each attribute has type of field and constraints.

+ Models will reference each other to represent the table relationships.

+ A foreign key denotes that the column coincides with a primary key of another table



\#\#\# 步骤: 

