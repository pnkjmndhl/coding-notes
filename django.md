### notes
- free and open-source framework for building web apps with python
- less time, less code
- eg. youtube, instagram, spotify, dropbox use django
- comes with lot of features out of the box, "batteries-included"
- huge community

### how web works
- any website has 2 components
- frontend
    - loaded in the web browser in the client machine
    - user sees and interacts with
- backend
    - runs in a web server and is responsible for processing, validating business roles and so on
- client vs server
- client (react, angular, vue)
- server (django, express, flask) 


### setting up
#### installing
- `python -m venv .venv`
- `python -m pip install Django`
#### create a django project
- `django-admin startproject <name-of-project> .`
    - `manage.py` is a commandline administrative utility
    - a subfolder named `name-of-project` is created with following files
        - `__init.py__` is an empty file that tells python that this folder is a python package
        - `asgi.py` is an entry point for ASGI-compatible web servers to serve the project, leave as is, provides hooks for production web servers
        - `settings.py` contains all settings for the project (modify as you work)
            - location of templates
            - which database to use
            - dont change `__file__` to `'__file__'` (default is not wrong)
        - `urls.py` is a TOC for the project (modify as you work)
            - all the searched urls (at front end) come here
            - from project's `url.py` the request is directed to app's `url.py`
        - `wsgy.py` is an entry for WSGI-compatible web serve to serve the project, leave as is, provides hooks for production web server

#### creating a new app (components of an app)
- `python manage.py startapp <name-of-app>`
    - everytime you install an app, you need to add it to `INSTALLED_APPS` in `settings.py`

### migrations
- generates scripts to change database structure
- adding a new model, adding a new field, changing a field
- first migration
    - creates tables for the models that are defined
    - `python manage.py makemigrations [name-of-app]`
      - creates a list of SQL commands
    - `python manage.py migrate [name-of-app]`
      - runs the migrations (executes the commands)

### working with models
- always register newly created models in `admin.py`
```py
from .models import <model-name>
admin.site.register(<model-name>)
```

### creating the server
- `python manage.py runserver`
    - start's django's development server at default port 8080

### adding static folder (make these changes)
- `settings.py`
    - `STATIC_URL` is a URL where the user can access the static files from the brower. The default is `http://127.0.0.1:8000/static/`
    - `STATIC_ROOT` is the absolute path to the directory where your django application will serve your static files from. When your run `collectstatic`, it will find static files from all apps and copy them to this directory
        ```py 
        STATIC_URL = 'static/' 
        STATIC_ROOT = os.path.join(BASE_DIR, 'static')
        ```
    - `STATICFILES_DIRS` is an additional folder where `collectstatic` command looks and copies to `STATIC_ROOT`
    - more on `STATICFILES_STORAGE` and `STATICFILES_FINDER`
- management commands
    - `python manage.py collectstatic`
        - copies all static files from each apps and copies to `STATIC_ROOT`
        - !doesnot recopy once files are deleted  
    - `findstatic`
        - see where a file comes from

### adding a superuser
- `python manage.py createsuperuser`
    - you'll be prompted to enter userame, email and password for a superuser
    - use `http://localhost:8000/admin` in your web browser to access the admin page


### creating and updating models
- a model is a table/fomat in your database
- adding to a model
  - `ModelName(parameter1= parameter1, parameter2=parameter2, ...).save()`

##### notes:
dont put static files on the `STATIC_ROOT` directory. Instead use `STATICFILES_DIRS`

#### difference between webserver and development server
-   development server 
    - available at localhost, runs on local machine
    - intended for local development and testing
- web server
    - available at an IP address or domain
    - runs on a remote server like a cloud server such as google cloud, heroku, digital ocean
    - intended for production for real users


#### creating custom commands in Django
- create these folders inside you app `[app-name]/management/<command-name.py>`
- template for the `command-name.py` file
```py
from django.core.management.base import BaseCommand, CommandError
class Command(BaseCommand):
    help = "Command to print a text"
    def handle(self, *args, **options):
    try:
        # write your codes here
        print("Hello World") 
    except Exception as e:
        raise CommandError(e)
```
- running commands using `shell` (only works in linux terminal)
- `python manage.py shell < path/to/script.py`

#### working with views
- views are functions in `views.py` that can be run using url of the server
- add the path to the `urls.py` file
    ```py
    from django.urls import path
    from . import views
    urlpatterns = [
        path('', views.[function-name], name = 'getdata'),
    ]
    ```
- define `function-name` function to the `views.py` file
    ```py
    from django.http import HttpResponse
    def getdata(request):
        return HttpResponse("Hello World")
    ```


#### periodically running codes on the server using cron job
- `python -m pip install django-crontab`
- add `django_crontab` on `settings.py`
    ```py
    INSTALLED_APPS = [
        ...,
        'django_crontab',
    ]
    ```
-  create `path/to/file/filename.py` file that you want to run periodically
-  add the file to `settings.py`
    ```py
    CRONJOBS = [
        ('*/2 * * * *', '<app-name>.cron.<function-name>')
    ]
    ```
   - the syntax for the cron job
        | field #|  meaning     |allowed values|
        |----|------------------|------------|
        | 1  |    minute        | 0-59      |
        | 2  |      hour        |0-23        |  
        | 3  |    day of month  |1-31           |
        | 4  |   month          | 1-12 or simply names|
        | 5  |  day of week     |  0-7 (0/7->Sun, or simply names)|
   - multiple in same category could be separated by `,`
   - `*/5` every that unit
 - add/remove/show all defined `CRONJOBS` to `crontab`
   - `python manage.py crontab add/remove/show`
 - run django server


#### periodically running codes on the server using celery and redis
- `pip install celery redis`
- configure celery
  - add the following code to `settings.py` to configure celery to use redis as the message broker
    ```py
    import os
    from celery import Celery

    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'yourproject.settings')

    app = Celery('yourproject')
    app.config_from_object('django.conf:settings', namespace='CELERY')
    app.autodiscover_tasks()
    ```


### working with templates
