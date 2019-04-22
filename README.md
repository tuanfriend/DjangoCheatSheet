Django Project Cheat Sheet
==============

Step-by-step guide:
--------------

A Django Virtual Environment **It is a little bit different for Mac User and Windows User**

**Mac users**
```
> virtualenv -p python3 djangoPy3Env
> source djangoPy3Env/bin/activate
(djangoPy3Env)> pip install Django==1.10
```
**Windows users**
```
> virtualenv djangoPy3Env
> call djangoPy3Env\Scripts\activate
(djangoPy3Env)> pip install Django==1.10
```

Create a new Django project, first **navigate** to where you want the project to be saved.
```
django-admin startproject your_project_name_here
```

Next, we'll manually create a folder for our project's apps:
```
(djangoPy3Env) django_intro> cd your_project_name_here
(djangoPy3Env) your_project_name_here> mkdir apps
```

Next, we need to ensure that our Django app can see our apps folder
```
(djangoPy3Env) your_project_name_here> cd apps
(djangoPy3Env) apps> touch __init__.py
            OR
(djangoPy3Env) apps> nul>__init__.py
```

Since we've already navigated to the apps folder, we'll use the CLI again to create a Django app, with a name of our choosing: **The apps in a project CANNOT have the same name as the project.**
```
(djangoPy3Env) apps> python ../manage.py startapp your_app_name_here
```

Navigate into the newly created app folder and create an empty file called urls.py.
```
(djangoPy3Env) apps> cd app_name
(djangoPy3Env) your_app_name_here> touch urls.py	// Mac users
                    OR
(djangoPy3Env) your_app_name_here> nul>urls.py	// Windows command prompt users; ignore Access Denied warning
```

In the text editor, find the settings.py file. It should be in a folder with the same name as our project. Find the variable INSTALLED_APPS, and let's add our newly created app:
**your_project_name_here/your_project_name_here/settings.py**

```
INSTALLED_APPS = [
       'apps.your_app_name_here', # added this line. Don't forget the comma!!
       'django.contrib.admin',
       'django.contrib.auth',
       'django.contrib.contenttypes',
       'django.contrib.sessions',
       'django.contrib.messages',
       'django.contrib.staticfiles',
   ]    # the trailing comma after the last item in a list, tuple, or dictionary is commonly accepted in Python
```

For these next few steps, we are creating the route "/" to be associated with a specific function. 
**your_project_name_here/your_project_name_here/urls.py**
```
from django.conf.urls import url, include	# added an import!
# from django.contrib import admin              # comment out, or just delete
urlpatterns = [
    url(r'^', include('apps.your_app_name_here.urls')),	# use your app_name here
    # url(r'^admin/', admin.sites.urls)         # comment out, or just delete
]
```

Then, in our app, for every route we want to add, we'll do the following:

In the app level urls.py file, add a URL pattern:

**your_project_name_here/apps/your_app_name_here/urls.py**
```
from django.conf.urls import url
from . import views
                    
urlpatterns = [
    url(r'^$', views.index),
]
```

And then actually put a function called index in our app's views.py file:
**your_project_name_here/apps/your_app_name_here/views.py**
```
from django.shortcuts import render, HttpResponse
def index(request):
    return HttpResponse("this is the equivalent of @app.route('/')!")
```

Let's run our app again and check it out at **localhost:8000/**. Whew. We've done it!
```
(djangoPy3Env) your_project_name_here> python manage.py runserver
```

**Note: Do not manually change the name of any of your folders after creation!**


**------------- Bonus command Migrations and Shell ----------------**
To do this, (basically the equivalent of forward engineering in MySQL Workbench), we are going to run a couple of commands from the terminal.
```
  > python manage.py makemigrations
  > python manage.py migrate
```

Command go to shell
To use the shell, we'll run the following command in our terminal from our project's root directory (where our manage.py file is located):
```
> python manage.py shell
```

You're done almost command in Django Python! Thank you to Tuan for take time do it. :D Have fun Ninja Dojo!!!
