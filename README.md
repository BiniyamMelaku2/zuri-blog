# zuri-blog
## Django Models - Building A Blog Application With Django 

## Resources

-[Building A Blog Application With Django](https://djangocentral.com/building-a-blog-application-with-django/)

-[How to Create a Blog Application Using Django](https://pythonsansar.com/how-create-blog-application-using-django/)

-[Django timezone.now](https://stackoverflow.com/questions/10783864/django-1-4-timezone-now-vs-datetime-datetime-now)

## Create virtual env 

> $ python3 -m venv venv

## activate virtual env

> $ source venv/bin/activate


## Install Django on venn

> (venv) $ sudo pip3 install Django

## Create a Django project

> $ django-admin startproject I4G000675LXH

## create a Django app

> $ sudo python3 manage.py startapp blog

## Add the blog app to the main_projects INSTALLED_APPS. open your settings.py file
```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog'
]
```

## Create a new model in the `blog` app called `Post`. It should have the following fields:

Database Models.py
```
from django.db import models
from django.contrib.auth.models import User
from django.utils import timezone


STATUS = (
    (0,"Draft"),
    (1,"Publish")
)

class Post(models.Model):
    title = models.CharField(max_length=200, unique=True)
    text = models.TextField()
    author = models.ForeignKey(User, on_delete= models.CASCADE,related_name='blog_posts')
    created_date = models.DateTimeField(auto_now_add=True)
    published_date = models.DateTimeField(default=timezone.now)
    
 
    status = models.IntegerField(choices=STATUS, default=0)

    class Meta:
        ordering = ['-created_date']

    def __str__(self):
        return self.title
```

## migrate the change into our database.
```
(django) $ sudo python3 manage.py makemigrations
Migrations for 'blog':
  blog/migrations/0001_initial.py
    - Create model Post

(django) $ sudo python3 manage.py migrate

  Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
```

## Creating An Administration Site

> (django) $ sudo python3 manage.py createsuperuser

> (django) $ sudo python3 manage.py runserver

## Adding Models To The Administration Site

Open the blog/admin.py file

```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```