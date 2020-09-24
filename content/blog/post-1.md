---
title: "Django models"
date: 2020-06-12
image: "images/blog/post-5.jpg"
description: "This is meta description."
draft: false
---

**Introduction**

In this tutorial, we will create the Django models that define the fields and behaviors of the Blog application data that we will be storing. These models map the data from your Django application to the database. It’s what Django uses to generate the database tables via their object relational mapping (ORM) API called "models".

Django models are the base thing of any django project.The main purpose of django models are to save the user data in to any database(sqlite3,MongoDB,Oracle,PostgreSQL etc)


Generally we give specific field names to the django models examples are:
+ first_name

+ last_name

+ email

+ mobile_number

+ adress

+ country

+ created_date

+ picture & many more..

Above is the basic things we give to a model.py file. For validation we have to use decorators and inbuilt django features.


**Creating an Application**

*Install Python 3.6.8*

*Install Virtualenv (using latestpip)*


Creating a folder `project`

``` python

manas@dell:~$ mkdir ManasBlog
manas@dell:~$ cd ManasBlog

```
After moving inside the project directory we have create virtualenv for our project.


``` python

manas@dell:~$ virtualenv -p python3 venv

```

Its time to install django in our virtualenv i.e venv. Install any one according to your choice.


``` python

manas@dell:~$ pip install django | pip install django==2.2

```

As we installed Django by using pip its time to create our django project and for that we have to type following command.

Note: Below commant will create the following tree where we can configure settings.py and urls.py according to our requirements.

``` python

manas@dell:~$ django-admin startproject blog

```

``` text

blog
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py

```

After this we have to create an application as we know django is all about applications. So moving on use below command to create an application.


``` python

manas@dell:~$ python manage.py startapp blogapp

```

Noew open ManasBlog folder in any IDE's and you will see the tree like below.

``` text

ManasBlog
|-blog
├── blogapp
│   ├── admin.py
│   ├── apps.py
│   ├── __init__.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── db.sqlite3
├── manage.py
├── mysite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── venv
│   └── ...


```
After creating an application, we should aware Django that it should use it. We do that in the file blog/settings.py -- open it in your code editor. We need to find `INSTALLED_APPS` and add a line containing `'blogapp.apps.BlogConfig'`, just above ( ] ). So the final product should look like this:


blog/settings.py

``` python

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog.apps.BlogConfig',
]

```

Its time to create a model for our blog so that it will store the data in to the database when we do operations. So now open models.py file which will be in our app that is **blogapp**.



``` python
from django.conf import settings
from django.db import models
from django-utils import timezone

first_name = models.CharField(max_length=100)
last_name = models.CharField(max_length=100)
title = models.CharField(max_length=100)
email = models.EmailField(max_length=100)
location = models.CharField(max_length=100)
image = models.FileField()
mobile = models.BigIntegerField()
date_of_birth = models.DateTimeField(blank=True)
publish_date = models.DateTimeField(blank=True,null=True)

def publish(self):
    self.published_date = timezone.now()
    self.save()

def __str__(self):
    return self.first_name  #manasblog
```

Its looks confusing right but don't worry my friend everything will gonna be chakachak. So now open ternminal and go our project directory and do the following.

``` python
manas@dell:~$cd ManasBlog
manas@dell:~/ManasBlog$ source venv/bin/activate
(venv) manas@dell:~/ManasBlog$ cd blog
(venv) manas@dell:~/ManasBlog/blog$ python manage.py makemigrations
(venv) manas@dell:~/ManasBlog/blog$ python manage.py migrate
```

Dont worry i will tell you the reason of using makemigrations and migrate

>Makemigrations will collect the data from models.py and it will store in migrations folder by creating 0001_initial.py (Note: For each change in models file it will create a migration file).

``` python
(venv) manas@dell:~/ManasBlog/blog$ python manage.py makemigrations
Migrations for 'blog':
  blog/migrations/0001_initial.py:
  - Create model Post
```

>Migrate will take the data from 0001_initial.py folder and it will create a table in our database.

``` python
(venv) manas@dell:~/ManasBlog/blog$ python manage.py makemigrations
Operations to perform:
  Apply all migrations: blogapp
Running migrations:
  Applying blog.0001_initial... OK
```


Our post created and the data is stored in database. I used default django database i.e sqlite3 but you can use other database like mysql,PostgreSQL,MongoDB.


Plese ping me to my mail iammanas24@gmail.com for any queries and inspire me to do more. Thank you  !