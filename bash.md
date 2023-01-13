# Bash Scripts:

## general
- `#!/bin/bash` shebang and path to the bash executable
- `#` comment
- `bash ls.sh` to run the script
- `./ls.sh` to run an executable code
- `ls.sh` if the file is exactly on the path environment variable

## echo
- special characters should always be escaped using backslash
- `echo $ddd` to access ddd variable
- `echo ddd` prints exactly
- `echo 'ddd'` even if it has variable inside, it comes out literally
- 'echo "ddd"' middle ground ??

## working with variables:
- `a=3`
- `e="hello dd"` no spaces (important)

## adding attributes to variables (I,r,l,u)
- `declare -i d=123` d is an integer
- `declare -r e=456` e is read-only
- `declare -l f="LolCats"` f is lolcats
- `declare -u f = "dfd"` f is DFD

## common variables:
- `echo $PWD` returns current directory
- `echo $MACHTYPE` returns machine type
- `echo $HOSTNAME` returns system name
- `echo $BASH_VERSION` returns version of bash
- `echo $SECONDS` returns the number of seconds the bash session has run
- `echo $0` contains the name of the script

## command substitution:
- `d = $(pwd)` d would be string with present working directory
- `echo $d`

## arithmetic operations: `$(( expression ))`
- `d=2`
- `e = $((d+2))
- echo $e

## comparison operation: `[[ expression ]]`
- `[["cat" == "cat"]]`
- `echo $?`
- '[["cat" == "dog"]]'
- `echo $?`
- '[[ 20 -gt 100 ]]'  lt gt le ge eq ne for integers
- `echo $?`

## string manipulation:
- `a="hello"`
- `b="world"`
- `echo $a$b`
- `echo $(#a) #?`

## date:
- `date + "%d-%m-%Y"`
- `printf "Name:\t %s\nID:\t%04d\n" "Sxott" "12"`

## working with arrays:
- `a=()`
- `b=("apple" "banana" "cherry")`
- `echo ${b[2]}`
- `b[5] = "kiwi"`
- `b[@] # get all elements`

## Reading and writing file:
- `echo "some text" > file.txt`
- `echo "some text" >> file.txt` apend to the file

# bash functions:
```function greet {
             echo "Hi, $1"
     }
greet pankaj```

## working with arguments:
`echo $1`

```
for i in $@ #for array of arguments
do
     echo $i
done
echo "There are $# arguments"```

## getting input during execution

- `echo "what is your name?"`
- `read name`
- `echo "What is your password?"`
- `read -s pass  # secret`
- `read -p "What's your favorite animal?" animal`
- `echo name: $name, pass $pass, animal: $animal`

# ensuring a response:
```
if [$# -lt 3 ]; then
        echo "Not enough arguments"
else
         echo "username: " $1
         echo "UserID : $2"
         echo "Favorite Number: $3"
fi```
