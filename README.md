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
#
# Create a html file in templates with name  index.html 
#
# Create static ( Just name ),( we store here html file ) folder in project root folder

