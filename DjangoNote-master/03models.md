### Django Models
A model in Django is a Python Class that represent database table. Each attribute in the model represent field in that table.

### How Models Work
- Django use ORM [Object Relational Mapping], which allows you to interact with database using python code instead of SQL.
- Models Define Structure of database, Django automatically create SQL to create database tables and interact with data.

### How To Create
Lets suppose we just create blog app in our project. Go to 'yourappname/models.py' and paste the code:
```python
from django.db import models

# Create your models here.
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

### Migration
- Migratons is Django way of applying change to database schea. 
- When you define or update model, you create migration to reflect those changes in the database.

### Create Migration
```bash
python manage.py makemigrations
```
This will generate migration file in your apps migration directory.

### Apply Migration
- To apply the migration and update in database run:
```bash
python manage.py migrate
```
This will automaticaly create necessary database table based on your model defination.

### Register Mode To Admin Site
Go to admin.py in your app directory.
```python
from django.contrib import admin
from .models import Post

# Register your models here.
admin.site.register(Post)
```

### Create Superuser
To create superuser use this command:
```bash
python manage.py createsuperuser
```
Now enter username, password, email and open
http://127.0.0.1:8000/admin/
- Enter your username and password
- Now you can add, update, delete, view post.


### Django ORM
Django ORM allows youu to interfact with database using Python Code. To start:
Type
```bash
python manage.py shell
```

### Create a New Post
```python
from blog.models import Post
post = Post.objects.create(title="Hello", content="From Terminal")
print(post)
```
### View Post
- All
```python
from blog.models import Post
posts = Post.objects.all()
```
- Single Post
```python
from blog.models import Post
post = Post.objects.get(id=1)
```

### Update
```python
from blog.models import Post
post = Post.objects.get(id=1)
post.title = "My New Title"
post.save()
```

### Delete
```python
from blog.models import Post
post = Post.objects.get(id=3)
post.delete()
```

### QuerySet Method and Filters
```python
from blog.models import Post
postsasc= Post.objects.all().order_by('created_at') # Asc
postsdesc= Post.objects.all().order_by('-created_at') #Desc
first_five_post= Post.objects.all().[:5]
count = Post.objects().all().count()
```

### How to Add Image In Models
```python
from django.db import models

# Create your models here.
class Blog(models.Model):
    title = models.CharField(max_length=100)
    description = models.TextField()
    date = models.DateField(auto_now_add=True)
    updated = models.DateField(auto_now=True)
    image = models.ImageField(upload_to='blog/images/') # Add this line

    def __str__(self):
        return self.title
```

In post.html
```html
 <img height="500" width="700" src="{{blog.image.url}}" alt="{{blog.title}}">
```

In your setting.py in project directory
```python
import os
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

In your app urls.py
```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

or 

```python
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```


