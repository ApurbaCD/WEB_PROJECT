# To create Virtual Environment to install Django in Ubuntu
#### If you dont have venv then install it : sudo apt install python3-venv
#### To create environment :  python3 -m venv my_env
##### Activate the environment source my_env/bin/activate
#### Everytime Activate the environment to work in the environment . Activate in same folder .  
#### Deactivate the environment deactivate 
#### Install django : python3 -m pip install Django
#### If you want to install django specifiq version : python3 -m pip install Django==3.2
#### Create A project : django-admin startproject mysite
#### Create A apps    : python manage.py startapp polls 
# To deploy Your Django app in Vercel
## create vercel.json file of your project directory and paste this line of code and change projectname your actaul project name:

```
{
  "version": 2,
  "builds": [
    {
      "src": "projectname/wsgi.py", #change project_name into actual project name 
      "use": "@vercel/python",
      "config": { "maxLambdaSize": "15mb", "runtime": "python3.11" }
    },
    {
      "src": "build_files.sh",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "staticfiles_build"
      }
    }
  ],
  "routes": [
    {
      "src": "/static/(.*)",
      "dest": "/static/$1"
    },
    {
      "src": "/(.*)",
      "dest": "projectname/wsgi.py"
    }
  ]
}
# change projectname your actual projectname

```
# Create templates ( Just name ),( we store here html file ) folder in project root folder
#### Change in urls.py in mysite
```
urlpatterns = [
    path('admin/', admin.site.urls),
    path("",include("Poll.urls")),
]
```
# Change in TEMPLATES in  settings.py of mysite : 
#### 'DIRS': [BASE_DIR / "templates"],

# Create urls.py in polls 

# Create a html file in templates with name  index.html

# In view.py add the html file 
```
from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse


def index(request):
    return render(request,"index.html")

```

# In urls.py add the index function (while lies in views.py)
```
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```


# Create static file index.css ( Just name ),( we store here html file ) folder in project root folder

# Add the index.css file in index.html by adding  avobe code :
```
{% load static %}
//in head 
    <link rel="stylesheet" href="{%static 'index.css'%}">

```

# To create requirements.txt run this :  pip freeze > requirements.txt.

# Create a file name build_files.sh in your project directory and paste this line of code
```
# build_files.sh
pip install -r requirements.txt
python3.9 manage.py collectstatic
#here you must be give python3.9

```

# Modify setting.py-------

#### import os in import section
### ALLOWED_HOSTS = ['127.0.0.1', '.vercel.app', '.now.sh']

#### If you don't have install postgresql please Comment Database setion of setting.py
```
DATABASES = {
    # 'default': {
    #     'ENGINE': 'django.db.backends.sqlite3',
    #     'NAME': BASE_DIR / 'db.sqlite3',
    # }
}
```
### Below the STATIC_URL = 'static/' paste this lines of code:
```
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)
STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles_build','static')

```

# Modify urls.py-------

### Import section add these line code:
```
from django.conf import settings
from django.conf.urls.static import static

```
# Modify in wsgi.py

### Add this at the end

```
app=application

```
## Now Push Your code in Github and Create a account in vercel.com with github.com

# Installed Postgresql Database in ubuntu
### Just go to the postges website and copy and pase the command to install postgres shell and pgadmin4 .
#### To Show psql version psql --version.
#### Navigate back to the Postgres shell and run the following commands consecutively sudo -i -u postgres.
#### To interact with the database server run  psql.
#### To create Database user & password run this  CREATE USER username WITH PASSWORD 'password';.
#### To create a database run this CREATE DATABASE db_name;  or createdb db_name .
#### To delete a database run this DROP DATABASE db_name;.
#### To see list of db here \l.
#### To connect db run \c db_name.


## Install postgresql in Django

#### To install postgresql in virstual environment run pip install psycopg2-binary.
#### To change requirement.txt file run pip freeze > requirements.txt.
#### Now Change in setting.py DATABASE section
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'database_name',
        'USER': 'user_name_of_psql',
        'PASSWORD': 'password_pf_psql',
        'HOST': 'localhost',
        'PORT': 5432
    }
}

```
### To migrate database run python3 manage.py migrate.
### If You face Error :
```
django.db.migrations.exceptions.MigrationSchemaMissing: Unable to create the django_migrations table (permission denied for schema public
LINE 1: CREATE TABLE "django_migrations"

```
### Go your psql shell and GRANT the the databse to userGRANT ALL ON DATABASE mydb TO myuser; and ALTER DATABASE my_db OWNER TO myuser;.
