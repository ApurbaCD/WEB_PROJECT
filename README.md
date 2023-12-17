# To create Virtual Environment to install Django in Ubuntu
#### If you dont have venv then install it sudo apt install python3-venv
#### To create environment  python3 -m venv my_env
##### Activate the environment source my_env/bin/activate
Deactivate the environment deactivate 
Install django python3 -m pip install Django
If you want to install django specifiq version python3 -m pip install Django==3.2
Create A project django-admin startproject mysite

```
{
  "version": 2,
  "builds": [
    {
      "src": "projectname/wsgi.py",
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
