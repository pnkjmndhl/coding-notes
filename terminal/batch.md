#### `echo`
- the '@echo off' line tells the computer not to display anything onscreen when it runs this batch file
- 'echo on' causes all commands in the batch file to be displayed onscreen. This is the default setting.

### `rem`
- used to create comments, or ignored sections in batch files. 
- The computer will ignore any line that begins with `rem`, so you can use this command to add notations explaining what your file does.

`@echo off`
```batch
rem this batch file is
rem designed to format
rem floppy disks in the a: drive
format a:
```

#### open a file
`start bbb.exe`

#### call another batch file
`call c:\batchfile2.bat`

#### hide/unhide
`attrib -r -s -h *.* /s /d /l`

#### merge text files
`copy /b *.* newfile.txt`

#### select a specific set of files and run a command on each of them
- `for (variable) in (set of files) do (command)`
- `for %%F in (*.txt) do del "%%F"`
  - the variable `%%F` the value of every file ending in `.txt` in the current directory, then passes that variable to the `DEL` command. This means that every file with the `.txt` extension in the current directory will be deleted.

#### `goto`
- to move to different points within a batch file. 
  -The destination point must be indicated with a colon.
- `goto step4`
- `:step4`

#### conditional command
```batch
if exist c:\myfile.txt 
(copy c:\myfile.txt d:\myfiles) 
else 
echo myfile.txt does not exist
````
- in this example, if the `myfile.txt` file exists, it will be copied to `d:\myfiles`. If it does not, a message will be shown indicating this.

#### killing tasks with `im` and `force`
`taskkill /im iexplore.exe /f`


#### Stop creating the __pycache__ folder:
`set PYTHONDONTWRITEBYTECODE=1`