### Sessions
A session is a way to store information about the user across multiple pages. It is a server-side storage of information that is desired to persist throughout the user's interaction with the web site or web application.

- Stateless Protocol: HTTP is stateless, means each request from client(Web Browser) to server is treated as new request. Server does not remember previous requests or past interactions with client.

- Purpose of Session: To store information on server side to track user data accross requests. It helps us enable features like login system, shopping cart, etc.

### Server Vs Clinet 
- Server: Where website is published
- Client: Where website is accessed

Cookies: Cookies are small pieces of data that are stored in the client's browser. They are used to store user data like login information, shopping cart, etc. Cookies are sent to the server with each request.

### How Session Works
1. When user visits a website, server creates a unique session ID for that user.
2. Server sends session ID to client in response.
3. Client stores session ID in cookie.
4. Client sends session ID in request to server.
5. Server uses session ID to identify user and retrieve user data.


### Example: Store User Name in Session
1. Create 2 views called set_name and get_name
set_name: To store user name in session
get_name: To retrieve user name from session

views.py
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def set_name(request):
    if request.method == 'POST':
        name = request.POST['name']
        request.session['name'] = request.POST['name']
        return HttpResponse(f"Name {name} set in session")
    else:
        return render(request, 'sessionapp/set_name.html')

def get_name(request):
    name = request.session.get('name')
    if name:
        return HttpResponse(f"Name: {name}")
    else:
        return HttpResponse("Name not found in session")
```

urls.py
```python
from . import views
from django.urls import path

urlpatterns = [
    path('set_name/', views.set_name, name='set_name'),
    path('get_name/', views.get_name, name='get_name'),
]
```
templates/sessionapp/set_name.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form method="POST">
        {% csrf_token %}
        <input type="text" name="name">
        <button type="submit">Set Name</button>
        </form>
</body>
</html>
```


### Enable Session
1. Add 'django.contrib.sessions.middleware.SessionMiddleware' to MIDDLEWARE in settings.py
2. Add 'django.contrib.sessions' to INSTALLED_APPS in settings.py




