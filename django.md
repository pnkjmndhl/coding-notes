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
- `django-admin startproject [name-of-project] .`
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
- `python manage.py makemigrations [name-of-app]`
    - create the migrations (generate the SQL commands)
    - `python manage.py migrate` runs the migrations (executes SQL commands)
- `python manage.py runserver`
    -start's django's development server at default port 8080

#### creating a new app
- `django manage.py start-app [name-of-app]`
    - everytime you install an app, you need to add it to `INSTALLED_APPS` in `settings.py`

### migrations
- generates scripts to change database structure
- adding a new model, adding a new field, changing a field
- first migration
    - creates tables for the models that are defined
    - `python manage.py makemigrations`

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