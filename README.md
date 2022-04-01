# -首个Django练手项目-
项目的创建和使用

## 安装Django并创建项目

### pip安装django
pip3 install Django -i https://pypi.tuna.tsinghua.edu.cn/simple

### 创建项目
django-admin startproject project-name

### 切换到创建的项目
cd project-name

## 创建和MYSQL的连接

### 进入_init_.py初始化pymysql插件
import pymysql
pymysql.install_as_MySQLdb()

### 进入setting.py修改数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': '127.0.0.1',
        'PORT': '3306'
    }
}

### 向数据库写入数据表
python manage.py migrate

### 创建root账户
python manage.py createsuperuser

### 启动项目
python manage.py runserver

## 创建html目录和文件

### 创建polls目录
python manage.py startapp polls

### 在mysite目录的主路由文件urls.py中定义路径指向polls目录的路由文件urls.py
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('polls/',include("polls.urls"))
]

### 定义HTML页面文件的指向(以views.py为例),注意:所有的html页面需要通过setting中的模板定义
from django.shortcuts import render

def toLogin_view(request):
    return render(request,'login.html')
    

### 配置polls目录下的子路由文件urls.py
from . import views
from django.urls import path

urlpatterns = [
    path('',views.toLogin_view)
]


### 在setting.py中的templates中定义模板页面(先往polls目录创建templates模板目录),在INSTALLED_APPS中定义路径
#### templates
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR,'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
#### INSTALLED_APPS
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls'
]
