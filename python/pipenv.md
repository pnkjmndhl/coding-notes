#### Introduction
- single command line tool that helps you manage your Python dependencies, and makes it easy to create and share your work
- uses `Pipfile` to declare your dependencies
- uses `Pipfile.lock` to lock down to specific version
- makes it easy to reproduce your builds
- crates virtualenv for your project, isolates your dependencies from the system python installation, which makes it easy to switch between different projects, and run multiple versions of python at the same time
- makes your python development workflow much more efficient


#### installation
-command propmt
`python -m pip install pipenv`


#### activating
- `python -m pipenv shell`
    - this creates a pip file


#### installing multiple packages
- `pipenv install django djangorestframework django-rest-knox`
  - adds to the `pipfile` file