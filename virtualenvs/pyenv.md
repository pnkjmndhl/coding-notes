### installation
- all you need is download `pyenv-win` and add it to environment variables
<!-- - Use this [link](https://github.com/pyenv-win/pyenv-win) for windows -->
- using git (make pyenv only available for a user),
    ```
    git clone https://github.com/pyenv-win/pyenv-win.git %USERPROFILE%\.pyenv
    ```
- using git (make pyenv available for all users)
    ```
    git clone https://github.com/pyenv-win/pyenv-win.git C:\pyenv
    ```
<!-- - or, use this command in powershell
    ```ps
    Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
    ``` -->

### adding pyenv to environment variables
- add both `bin` and `shims` to system environment variables
- create a new variable `PYENV` and add path, for example, `C:\Users\<user>\.pyenv` on system variables
- add to `Path`
    ```
    %PYENV%\pyenv-win\bin;
    %PYENV%\pyenv-win\shims;
    ```



### activating an environment
```
pyenv install 3.9.0
```


### listing the installed versions
```
pyenv versions
```
### setting up global and local variables
```bat
pyenv global 3.11.0
pyenv local 3.9.0
pyenv global system  //use back the system's python
```

### asking pyenv for different versions of python
```
pyenv shell 3.11.0
pyenv shell 3.9.0
```

### removing existing environments from path
Please remove `C:\Users\pdh\AppData\Local\Microsoft\WindowsApps\` from PATH for pyenv to work properly.
remove python from "execution alisas"


