#### Introduction
- single command line tool that helps you manage your Python dependencies, and makes it easy to create and share your work
- uses `Pipfile` to declare your dependencies
- uses `Pipfile.lock` to lock down to specific version
- makes it easy to reproduce your builds
- creates virtualenv for your project, isolates your dependencies from the system python installation, which makes it easy to switch between different projects, and run multiple versions of python at the same time


#### installation
-command prompt
`python -m pip install pipenv`
- add pipenv path to the environment variables
  - usually this path: `C:\Users\<username>\AppData\Local\Programs\Python\Python311\Scripts\pipenv.exe`

#### activating
- `python -m pipenv shell`
    - this creates a pip file
- after activating the environment, you should be able to run `pipenv` without intials `python -m`

#### installing multiple packages
- if you install packages using pip, the packages would not be tracked using piplock file
- `pipenv install django djangorestframework django-rest-knox`
  - adds to the `pipfile` file

#### deleting packages
- `pipenv clean` to delete a package that is not being tracked by pipenv


#### exiting a pipenv environment
- `pipenv exit`


#### syncing the dependencies
- `pipenv sync`


#### generating requirements.txt file
- `pipenv requirements`


#### activating existing pipenv
- `pipenv 