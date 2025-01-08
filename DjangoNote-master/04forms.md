### Django Forms

### Form
Form is web elment that allow user to input and submit data to server. For e.g. login form, registration form, contact form etc.

### GET Vs POST
- GET: Used in getting[Fetching] data from server. Data is visible in URL.
- POST: Used in sending data to server. Data is hidden from URL. To send sensitive data like password, use POST.

### Django Forms
A form in Django is a Python class that helps you to create HTML forms. It is used to:
- Collect user data [login, registration, contact form, feedback form]
- Validate user data 
- Save data to database or process data further

### How to Create Django Form
1. Create a new file forms.py in your app directory
2. Import forms from django
3. Create a class that inherits from forms.Form or forms.ModelForm
4. Define fields in the form
5. Use form in views.py

### Example: Feedback Form
1. Create a new file forms.py in your app directory
```python
from django import forms

class FeedbackForm(forms.Form):
    name = forms.CharField(max_length=100, label='Your Name')
    email = forms.EmailField(label='Your Email')
    phone = forms.CharField(max_length=15, label='Your Phone')
    message = forms.CharField(widget=forms.Textarea, label='Your Message')
```
Here CharField means text input, EmailField means email input, Textarea means textarea input.

2. Use form in views.py
```python
from django.shortcuts import render
from .forms import FeedbackForm

def feedback(request):
    form = FeedbackForm()
    return render(request, 'feedback.html', {'form': form})
```

3. Create a template feedback.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feedback Form</title>
</head>
<body>
    <h1>Feedback Form</h1>
    <form method="POST">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

4. Add URL in urls.py
```python
from django.urls import path
from . import views

urlpatterns = [
    path('feedback/', views.feedback, name='feedback'),
]
```
5. Add URL in main urls.py
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('feedbackapp.urls')),
]
```

### Make Migration and Create Superuser
1. Make migration
```bash
python manage.py makemigrations
```

2. Apply migration
```bash
python manage.py migrate
```

3. Create superuser
```bash
python manage.py createsuperuser
```

### How to Process Form Data
1. In views.py
```python
from django.shortcuts import render

def feedback(request):
    form = FeedbackForm()
    if request.method == 'POST':
        form = FeedbackForm(request.POST)
        if form.is_valid():
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            phone = form.cleaned_data['phone']
            message = form.cleaned_data['message']
            print(name, email, phone, message)
    return render(request, 'feedback.html', {'form': form})
```

### Form Validation
- Django form validation is done using is_valid() method.

### Save Form Data to Database
1. Create a model in models.py
```python
from django.db import models

class Feedback(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    phone = models.CharField(max_length=15)
    message = models.TextField()
```

2. Make migration and apply migration
```bash
python manage.py makemigrations
python manage.py migrate
```

3. Save form data to database
```python
from django.shortcuts import render
from .forms import FeedbackForm
from .models import Feedback

def feedback(request):
    form = FeedbackForm()
    if request.method == 'POST':
        form = FeedbackForm(request.POST)
        if form.is_valid():
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            phone = form.cleaned_data['phone']
            message = form.cleaned_data['message']
            Feedback.objects.create(name=name, email=email, phone=phone, message=message)
    return render(request, 'feedback.html', {'form': form})
```

### Show Success Message 
```python
from django.shortcuts import render


def feedback(request):
    form = FeedbackForm()
    if request.method == 'POST':
        form = FeedbackForm(request.POST)
        if form.is_valid():
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            phone = form.cleaned_data['phone']
            message = form.cleaned_data['message']
            Feedback.objects.create(name=name, email=email, phone=phone, message=message)
            return render(request, 'success.html')
    return render(request, 'feedback.html', {'form': form})
```

### Show Success Message HTML 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Success</title>
</head>
<body>
    <h1>Thank You</h1>
    <p>Your feedback has been submitted successfully.</p>
</body>
</html>
```

### Register Model in Admin
1. In admin.py
```python
from django.contrib import admin
from .models import Feedback

admin.site.register(Feedback)
```
