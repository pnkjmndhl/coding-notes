## 1. Introduction
- [1. Introduction](#1-introduction)
  - [helpful keyboard shortcuts:](#helpful-keyboard-shortcuts)
    - [tab completion](#tab-completion)
    - [common  commands:](#common--commands)
    - [wild Cards:](#wild-cards)
- [2. File Folders Permissions](#2-file-folders-permissions)
  - [explore and navigate](#explore-and-navigate)
  - [list](#list)
    - [Create and remove files:](#create-and-remove-files)
    - [copy, move, and delete file and directories](#copy-move-and-delete-file-and-directories)
    - [find](#find)
- [3. User Roles and Permissions](#3-user-roles-and-permissions)
    - [normal user vs super user (root)](#normal-user-vs-super-user-root)
    - [if you need to do lot of works on root folder](#if-you-need-to-do-lot-of-works-on-root-folder)
    - [file premissions](#file-premissions)
    - [change the permissions of a file](#change-the-permissions-of-a-file)
    - [change ownership of file](#change-ownership-of-file)
- [4. touch, pip, grep, sed and ping](#4-touch-pip-grep-sed-and-ping)
    - [touch](#touch)
    - [using pipes](#using-pipes)
    - [grep](#grep)
    - [sed](#sed)
      - [ping](#ping)
- [5. Scripts:](#5-scripts)
  - [general](#general)
  - [echo](#echo)
  - [working with variables:](#working-with-variables)
  - [adding attributes to variables (I,r,l,u)](#adding-attributes-to-variables-irlu)
  - [common variables:](#common-variables)
  - [command substitution:](#command-substitution)
  - [arithmetic operations: `$(( expression ))`](#arithmetic-operations--expression-)
  - [comparison operation: `[[ expression ]]`](#comparison-operation--expression-)
  - [string manipulation:](#string-manipulation)
  - [date:](#date)
  - [working with arrays:](#working-with-arrays)
  - [Reading and writing file:](#reading-and-writing-file)
- [bash functions:](#bash-functions)
  - [working with arguments:](#working-with-arguments)
  - [getting input during execution](#getting-input-during-execution)
  - [ensuring a response:](#ensuring-a-response)
- [6. System info](#6-system-info)
    - [find out linux distribution](#find-out-linux-distribution)
    - [find disk and system information](#find-disk-and-system-information)
    - [install and update software](#install-and-update-software)
- [7. Miscellaneous](#7-miscellaneous)
  - [diff and cut](#diff-and-cut)
    - [Using diff files to patch](#using-diff-files-to-patch)
  - [extracting tar files](#extracting-tar-files)
  - [extracting zip files](#extracting-zip-files)
  - [stdin, stdout, stderr, and output redirection](#stdin-stdout-stderr-and-output-redirection)
    - [example: create a new file and add contents and append to an existing file](#example-create-a-new-file-and-add-contents-and-append-to-an-existing-file)
  - [`.bashrc`](#bashrc)

bash: Bourne Again Shell

### helpful keyboard shortcuts:
#### tab completion
- `Ctrl A`: beginning of line
- `Ctrl E`: End of line (^ = ctrl)
- `Ctrl + Shift + C` : Copy
- `Ctrl + Shift + V` : Paste

#### common  commands:
- `pwd` prints working directory
- `ls` lists the files and folders in current working directory
- `man` manual (forward: f, backward: b, q: exit)
- `mkdir` make a directory
- `rmdir` delete a directory
- `cd` change directory
- `cp - v` verbose copy
- `cat`  concatenate / see inside a file

- `~`  home directory
- `..`  parent directory
- `.`  current directory

#### wild Cards:
- `*` any number of characters
- `?` one character

## 2. File Folders Permissions

### explore and navigate
`pwd`  prints the working directory
`cd Exercise/ Files`  for space in name of folder, use escape character '/'
`ls -R`  look recursively
`cd ..`  the two dots represents the parent directory of the current directory
`cd ../../../COSC505`  go 3 levels back and goto folder COSC505
`cd -`  go back to a folder
`cd ~`  goto the home folder

### list
`ls [-l|-h]` `-l`with details `-h` human readable

#### Create and remove files:
- `mkdir new_folder` 
- `mkdir COSC505/C++/newfolder`  # makes a folder in the path specified
- `mkdir COSC505/C++/new1 COSC/C++/new2 COSC505/C++/new`  # creates 3 folder inside C++
- `mkdir -p COSC505/C++/new1/subdir/subsubdir`  # creates subsubdir inside newly created subdir

- `rmdir COSC505/C++/new1/`  # in order to remove a folder, it has to be empty
- `rmdir -- COSC505/C++/new1/`

#### copy, move, and delete file and directories
- `cp poems.txt poems2.txt`
- `cp simple_data.txt departments/hr/employee\ info/`
- `mv poems2.txt departments/marketing`  # move and rename
- `mv poems2.txt departments/marketing/literature.txt`  # renamed
- `mv ../poems2.txt .`  # moved
- `rm poems?.txt`  # removes poemsx.txt, not poems.txt, Remember: no trashcan or recyclebin
- `rm -r departments/customerservice/`  # deletes recursively

#### find
- `find . -name "poe*"` finds all files that starts with poe
- `find . -name "*d*"` finds everything that has d in it

## 3. User Roles and Permissions

#### normal user vs super user (root)
normal user can be temporarily super user to get root power using sudo (super user do)
- `su Pankaj` switch user to Pankaj user
- `sudo - k`  # to give up the privileges

#### if you need to do lot of works on root folder
- `su root`  # switch user to root, now $ changes to # (reminds you of the root privileges)

#### file premissions
- user group others
- `rwx`
- `read`  # see but not modify
- `write`  # modify but not read
- `execute`  # run without loading it to another program

#### change the permissions of a file
- `chmod 775` # octal
   - `7:111`
   - `6:110`
   - `4:100`

- `chmod u + rwx`  # symbolic
  - u user, g group, o others, a all
  - r read, w write, x execute
  - + add, - remove, = make equal

- `./executable.sh` to run a executable file

#### change ownership of file
`sudo chown root c++` changes the ownership of c++ folder to root, also chgrp


## 4. touch, pip, grep, sed and ping
#### touch
- `touch {apple,ball,cat}`  creates 3 files with these names, no spaces
- `touch file_{1..1000}`  creates 1000 files, file_1, file_2, file_3
- `echo {1..10}` 1 2 3 4 5 6 7 8 9 10
- `touch file_{01...1000}` with 0 padding

- `echo {1..10..2}`  1 3 5 7 9
- `echo {A..z}`  A B C ... x y z
- `echo {w..d..2}`  w u s q o m k i g e

#### using pipes
- `ls - 1 | wc`  pipes and counts the total number of words (newlines, words, characters)
- `ls | more`  list the files page by page

#### grep
- `grep "sc" 1.txt` # the search term is highlighted
- `grep - i break-in auth.log awk {'print $12'}` prints the 12th word from the letter specified, `-i` case insensitive

#### sed


##### ping
`ping website.com`

## 5. Scripts:

### general
- `#!/bin/bash` shebang and path to the bash executable
- `#` comment
- `bash ls.sh` to run the script
- `./ls.sh` to run an executable code
- `ls.sh` if the file is exactly on the path environment variable 

### echo
- special characters should always be escaped using backslash
- `echo $ddd` to access ddd variable
- `echo ddd` prints exactly
- `echo 'ddd'` even if it has variable inside, it comes out literally
- `echo "ddd"` middle ground ??

### working with variables:
- `a=3`
- `e="hello dd"` no spaces (important)

### adding attributes to variables (I,r,l,u)
- `declare -i d=123` d is an integer
- `declare -r e=456` e is read-only
- `declare -l f="LolCats"` f is lolcats
- `declare -u f = "dfd"` f is DFD

### common variables:
- `echo $PWD` returns current directory
- `echo $MACHTYPE` returns machine type
- `echo $HOSTNAME` returns system name
- `echo $BASH_VERSION` returns version of bash
- `echo $SECONDS` returns the number of seconds the bash session has run
- `echo $0` contains the name of the script

### command substitution:
- `d = $(pwd)` d would be string with present working directory
- `echo $d`

### arithmetic operations: `$(( expression ))`
- `d=2`
- `e = $((d+2))`
- `echo $e`

### comparison operation: `[[ expression ]]`

```sh
[["cat" == "cat"]]
echo $? 
```

```sh
[["cat" == "dog"]]
echo $?
```
lt `gt` `le` `ge` `eq` `ne` for integers
```sh
[[ 20 -gt 100 ]]  
echo $?
``` 


### string manipulation:
- `a="hello"`
- `b="world"`
- `echo $a$b`
- `echo $(#a) #?`

### date:
- `date + "%d-%m-%Y"`
- `printf "Name:\t %s\nID:\t%04d\n" "Sxott" "12"`

### working with arrays:
- `a=()`
- `b=("apple" "banana" "cherry")`
- `echo ${b[2]}`
- `b[5] = "kiwi"`
- `b[@] # get all elements`

### Reading and writing file:
- `echo "some text" > file.txt`
- `echo "some text" >> file.txt` apend to the file

## bash functions:
```sh
function greet {
             echo "Hi, $1"
     }
greet pankaj 
```

### working with arguments:
`echo $1`

``` sh
for i in $@ #for array of arguments
do
     echo $i
done
echo "There are $# arguments"
```

### getting input during execution

- `echo "what is your name?"`
- `read name`
- `echo "What is your password?"`
- `read -s pass  # secret`
- `read -p "What's your favorite animal?" animal`
- `echo name: $name, pass $pass, animal: $animal`

### ensuring a response:
``` sh
if [$# -lt 3 ]; then
        echo "Not enough arguments"
else
         echo "username: " $1
         echo "UserID : $2"
         echo "Favorite Number: $3"
fi 
```

## 6. System info

#### find out linux distribution
- `cat /etc/*-release | head -n 3 >> 5.txt`
```
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
DISTRIB_CODENAME=xenial
```
`uname -a` alternatively


#### find disk and system information
- `free -h`
- `cat /proc/cpuinfo`
- `df -h`

#### install and update software
- `sudo dpkg -i <debfilename>`
- 


## 7. Miscellaneous

### diff and cut
`diff <(sort filename.txt) <(sort filename2.txt)`

`cut -c-7 <(diff <(sort filename.txt) <(sort filename2.txt))`

`git diff HEAD <filename>` See difference between committed and working

#### Using diff files to patch
- `Diff -u file1 file2 > difference.diff` 
- `Patch file2 < difference.diff`

### extracting tar files
- `tar -cvf ../Bash mynewtar.tar`  compress, verbose to a file, Bash in parent directory
- `tar -xf mynewtar.tar`  extract

### extracting zip files
- `unzip '*.zip'`  or `unzip \*.zip`
### stdin, stdout, stderr, and output redirection
- 3 standard streams in unix-like systems 

|streams |type |description|shortcut|
|---|---|---|---|
|`stdin`| standard input | receive input from keyboard	| 0 |
|`stdout`| standard output | normal output, eg. text on screen	| 1 |
|`stderr` | standard error | like `stdout` but for error messages | 2 |

- eg.
  - `ls <folder-name> > newfile.txt` prints the output of the ls command to a file
  - `ls <folder-name> > newfile1.txt` prints the error to the file

#### example: create a new file and add contents and append to an existing file
`cat auth.log | grep "input_auth_request" | awk '{print $9}' | sort -u >>users.txt`


### `.bashrc`
- file located at `~` is a script that runs everytime a new terminal is opened
- for windows
  - `%UserProfile%\Documents\WindowsPowerShell\profile.ps1`