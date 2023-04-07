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


#### `python -m pipenv shell`
  - activating when no pipfile is present
  - this creates a new pip file


#### `pipenv install <packagename1> <packagename2> <packagename3>`
  - installs multiple packages
  - adds to pipfile

#### `pipenv lock -r`
  - see what's installed in the pipenv package

#### `pipenv uninstall <packagename1> <packagename2> <packagename3>`
  - uninstalls a package


### `pipenv install -r ./requirements.txt`
  - installs from requrements.txt


### `pipenv check` 
  - checks vulnerabilities, if you find any, edit the piplock file and rerun `pipenv install`


### `exit`
  - exit from a pipenv


### `pipenv run python`
  - runs the python from the virtual environment
  - see the location using `sys.executable`