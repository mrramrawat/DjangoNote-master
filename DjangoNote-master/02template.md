### Django Templates
Template is a text file that define the structure of that file, such as html page. In Django Template are used to generate dynamic HTML by injecting data to placehoders.

### Why Use Templates?
- To Seprate Presntation Logic From business logic.
- Template allows us to dynamically generate content based on data pass from view.

### Template Variables
- Template Variable {{variable}}
- Template Tags {{% %}} [Loop or Condition]


### How to Display HTML In Django
- First create one folder named "templates" in your app directory
- Inside templates folder create another folder "your app name"
- Put your html file inside that templates/"your app name" folder.
- For e.g index.html
- To show html page use following code:
```python
# app views.py
from django.shortcuts import render

def index(request):
    return render(request, 'htmlapp/index.html')
``` 

We use DTL [Django Template Language]. 
### Pass Data To Templates
1. Suppose this is HTML file called index.html on 
htmlapp/index.html
```html
<!DOCTYPE html>
<head>
    <title>{{title}}</title>
</head>
<body>
    <h1>Welcome to {{webname}} Website</h1>
</body>
</html>
```
2. Now We need to pass title and webname for this. You can use following code in views.
```python
def index(request):
    context = {
        'title': 'Bishworaj Poudel',
        'webname': 'BRPS'
    }
    return render(request, 'htmlapp/index.html',context=context)

```

### Use Loop
For e.g we have list of 10 names. We need to display all name in html list.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{title}}</title>
</head>
<body>
    <h1>Welcome to {{webname}} Website</h1>
    <h2>My New Students</h2>
    <li>
        {% for name in names %}
        <ul>{{name}}</ul>
        {% endfor %}
    </li>
</body>
</html>
```

```python
def index(request):
    context = {
        'title': 'Bishworaj Poudel',
        'webname': 'BRPS',
        'names': ["Sita", "Ram", "Gita", "Hari"],
    }
    return render(request, 'htmlapp/index.html',context=context)
```




### Use Template Inheritance
It allows us to define base template and extend it on child templates. First create base.html on templates/"your app name" folder
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}{% endblock title %}</title>
</head>
<body>
    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
        <div class="container-fluid">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" href="index.html" >Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="service.html">Services</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="about.html">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="contact.html">Contact</a>
            </li>
          </ul>
        </div>
      </nav>

      {% block content %}{% endblock content %}
</body>
</html>
```

index.html code
```html
{% extends "htmlapp/base.html" %}

{% block title %}Homepage{% endblock title %}


{% block content %}
<h1>Welcome to {{webname}} Website</h1>
<h2>My New Students</h2>
<li>
    {% for name in names %}
    <ul>{{name}}</ul>
    {% endfor %}
</li>
{% endblock content %}
```
service.html code
```html
{% extends "htmlapp/base.html" %}

{% block title %}Service{% endblock title %}


{% block content %}
<h1>Welcome to Service</h1>
{% endblock content %}
```


### Include Static Files
You can load css, js and images as static file in django. For that follow the step.
1. Create static folder in your app directory.
2. Inside your static folder create folder with appname
3. Inside your <appname> folder create folder css and js
4. Inside css folder place your css there and inside js folder 
place your js there.
5. Use that css and js, or images in your project or html template.
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Website</title>
    <link rel="stylesheet" href="{% static 'brpapp/css/style.css' %}">
</head>
<body>
    <h1>My Website</h1>


    <script src="{% static 'brpapp/js/scripts.js' %}"></script>
</body>
</html>
```


### How to Add Images
Place your images to folder static/<yourappname>/images. Use following code in templates.
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Website</title>
    <link rel="stylesheet" href="{% static 'brpapp/css/style.css' %}">
</head>
<body>
    <h1>My Website</h1>
    
    <img src="{% static 'brpapp/images/brp.jpg' %}" alt="My Photo">
    <script src="{% static 'brpapp/js/scripts.js' %}"></script>
</body>
</html>
```

### Filter
1. {{value|capfirst}} : Capitalizes first letter of text.
2. {{value|lower}}: Lower Case for text 
3. {{value|upper}}: Upper Case for text 
4. {{value|length}}: Find the length of text 
5. {{value|title}}: Convert it to title case
6. {{value|wordcount}}: Convert it to title case

