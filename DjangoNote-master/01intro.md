### Introduction
**Django** is a **high-level Python web framework** that encourages rapid development and clean, pragmatic design. It helps you build secure and maintainable websites quickly, so you can focus on writing your app without needing to reinvent the wheel. 🛠️

## Why Use Django? 🤔

### Advantages ✅

- **Fast Development**: Get your web application up and running quickly! ⏩
- **Secure**: Protects against common security threats by default. 🔒
- **Scalable**: Handles high traffic and large amounts of data gracefully. 📈
- **Versatile**: Suitable for all types of projects, from simple to complex. 🧩

### Built-In Features (Batteries Included) 🔋

- **Admin Interface**: Automatically generated admin panel to manage your site.
- **ORM**: Object-Relational Mapping to interact with databases easily.
- **Templating Engine**: For dynamic HTML generation.
- **Form Handling**: Simplifies form rendering and validation.
- **Authentication**: User authentication system ready to go.

## Real-World Examples 🌐

Websites that use Django:

- **Instagram** 📸
- **Pinterest** 📌
- **Mozilla** 🦊
- **Khalti** 💰
- **National Geographic** 🌍

---


## Understanding Django's Architecture 🏗️

Django follows the **MVT (Model-View-Template)** architectural pattern:

1. **Model**: Defines the data structure; it's the database layer. 🗄️
2. **View**: Contains the logic that interacts with the model and renders a response. 🧠
3. **Template**: Deals with the presentation layer; how data is displayed to the user. 🎨

![MVT Architecture](https://simpleisbetterthancomplex.com/media/2016/08/diagram-01.png)

---

## Key Principles 🎯

- **DRY (Don't Repeat Yourself)**: Encourages reusability and clean code. ♻️
- **Convention over Configuration**: Makes decisions for you, so you can focus on your app. 📋
- **Pluggable Apps**: Easy to integrate third-party apps or create reusable ones. 🔌

---

## Alternatives to Django 🛣️

While Django is powerful, it's good to know other frameworks:

1. **Flask** 🧪
   - Lightweight and minimalistic.
   - Requires more configuration.
2. **Laravel** 🧙‍♂️
   - PHP framework with elegant syntax.
3. **Ruby on Rails** 💎
   - Based on Ruby, focuses on convention over configuration.

---
## Getting Started 🏁

### Prerequisites 📋

1. **Python** 🐍
   - Make sure Python is installed on your system.
2. **Virtual Environment** 🌐
   - Isolates your project dependencies.
3. **VS Code** 💻
   - A powerful code editor.

**Optional:**

- **Chrome Extension for Django** 🧩
   - Enhances your development experience.

## Setting Up Your Environment 🌳
### Install Virtualenv
virtualenv
```bash
pip install virtualenv
```
To create virutal env
```bash
virtualenv myenv
```
Activate using bash
```bash
source myenv/Scripts/activate
```

```bash
pip install Django
```

3. Vs Code

Optional
- Chrome Extension For Django


### How to Create First Project
Go to virtual env and run this command.
```bash
django-admin startproject myweekroutine
```
### Run Project
```bash
python manage.py runserver 
```

### Run on Different Port
```bash
python manage.py runserver 8181
```


### Project File Structure
**manage.py** - A utility for interacting with Django project from command.

### Inside myproject
**settings.py** - Setting files for your project.
**urls.py** - Define URL routing for project.
**__init__.py** - Marks this directory as python package.
**asgi.py** Configuration for ASGI [Asynchronous Server Gateway Interface]
- **wsgi.py** - Configuration for WSGI [Web Server GateWay Interface]
-- **db.sqlite** - Default SQlite database


### Django App
Django app is web application that does one thing. For e.g. blog, ecommerce, forum, etc.
- Django project can contain multiple apps.
- Apps are reusable

### How to Create Django App
```bash
python manage.py startapp <appname>
```
```bash
python manage.py startapp myapp
```

### Project Vs App
- **Project** is overall configuration that ties multiple apps together.

- **App** is independent module/feature of project.


### URL
Define URL routing for project.
- https://technologychannel.org/ - Root URL
- https://technologychannel.org/about/ - About URL

### Views
Logic for handling request and returning response. It can be function or class.

### Inside App
**__init__.py** - Marks this directory as python package.
**admin.py** - Register models to apprear on Django admin interface.
**apps.py** - Contain the configuration for app.
**models.py** - Define Database models.
**tests.py** - Used to write unit test for app.
**views.py** - Logic for handling request and returning response.
**migrations/**- Contains migration files for database changes.



### Connect App to Project
- Open settings.py and find INSTALLED_APPS list.
- Add your new app to the list.
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
]
```

### How to Define Views
To define views first you need to import:
```python
from django.http import HttpResponse
```

```python
def index(request):
    return HttpResponse("<h1> Welcome to My Website </h1>")

def contact(request):
    return HttpResponse("<h1>Welcome to Contact Page</h1>")
```

### After Define views What to do?
Create file called `urls.py` and add urls.
```python
from . import views
from django.urls import path

urlpatterns = [
    path('',views.index,name='homepage'),
    path('contact',views.contact,name='contactpage'),
]
```

### Define App Views To Project
First go to project's `urls.py` and add the code:
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('myapp.urls')) # Add this
]
```
### Run Project
```bash
python manage.py runserver 
```


### Steps To Do While Create New Project
1. Create virtualenv
```bash
virtualenv myenv
```
2. Activate virtualenv
- On Windows [Bash]
```bash
source myenv/Scripts/activate
```
- On Mac
```bash
source myenv/bin/activate
```

3. Install Django
```
pip install django
```
4. Create Django Project
```bash
django-admin startproject myproject
```
5. Open Project on Vs Code and Activate Virtual Env
6. Create App
```bash
python manage.py startapp myapp
```
7. Register App
```python
INSTALLED_APPS = [
    'myapp',
]
```
8. Define Views in App
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.

def index(request):
    return HttpResponse("<h1> Welcome to My Website </h1>")

def contact(request):
    return HttpResponse("<h1>Welcome to Contact Page</h1>")

```
9. Create `urls.py` file in app directory and create urls.
```python
from . import views
from django.urls import path

urlpatterns = [
    path('',views.index,name='homepage'),
    path('contact',views.contact,name='contactpage'),
]
```

10. Define App views to project
First go to project's `urls.py` and add the code:
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('myapp.urls')) # Add this
]
```
11.  Run Project
```bash
python manage.py runserver 
```