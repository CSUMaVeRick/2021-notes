# Django笔记

## 如何开始

创建项目

```django
django-admin startproject mysite
```

测试站点，先cd到文件夹

```django
py manage.py runserver
```

创建应用

```django
py manage.py startapp app_name
```

告知django，哪个应用发生了迁移

```django
py manage.py makemigration app_name
```



为应用建表，数据库迁移

```django
py manage.py migrate
```

创建管理员

```django
py manage.py createsuperuser
```

## 数据库ORM

**对象关系映射**Object Relational Mapping：用于实现面向对象编程语言里不同类型系统的数据之间的转换。在业务逻辑层和数据库层之间充当了桥梁的作用。

ORM 是通过使用描述对象和数据库之间的映射的元数据，将程序中的对象自动持久化到数据库中。

使用 ORM 的好处：

- 提高开发效率。
- 不同数据库可以平滑切换。

使用 ORM 的缺点：

- ORM 代码转换为 SQL 语句时，需要花费一定的时间，执行效率会有所降低。
- 长期写 ORM 代码，会降低编写 SQL 语句的能力。

ORM 解析过程:

1. ORM 会将 Python 代码转换成为 SQL 语句。
2. SQL 语句通过所使用数据库对应的第三方库传送到数据库服务端。
3. 在数据库中执行 SQL 语句并将结果返回。

<img src="C:\Downloads\beiyong\ormdb.jpg" alt="ormdb" style="zoom: 67%;" />

## 数据库配置

由于ORM可操作的对象最高级是表，所以我们必须首先完成建立数据库的工作，选择utf8作为编码方式。语句为`create database <数据库名> default charset=utf8;`。

接下来要在项目所在目录中的`settings.py`找到`DataBase`配置项，修改信息，格式如下：

```python
DATABASES = { 
    '<应用名>': 
    { 
        'ENGINE': 'django.db.backends.<数据库引擎>',
        'NAME': '<数据库名>',
        'HOST': '127.0.0.1', # 数据库地址，本机 ip 地址 127.0.0.1 
        'PORT': 3306, # 端口 
        'USER': 'root',  # 数据库用户名
        'PASSWORD': '123456', # 数据库密码
    }  
}
```

然后在与 settings.py 同级目录下的` __init__.py `中引入模块和进行配置。