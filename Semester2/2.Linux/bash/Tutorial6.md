## 1. Programming with bash shell
``` bash
#!/bin/sh
# Program name: myVeryFirst.sh
# Author name: Put your name here
# Date created: Date the file was first created
# Date updated: Date the file was last modified
# Description: 
#   A short description of what the purpose of  
#   the program is. This script print a couple 
#   of strings to the terminal window.
echo “Hello, you have successfully run your first script.”
echo “Congratulations!”
 ~$ bash ./myFirstScript.sh
 ~$ chmod 751 myFirstScript.sh
 ~$ ./myFirstScript.sh
```

## 2. Working With Variables
```bash
# test
echo "test"

DOG="Barky"
PI=3.14159
CAT="Spot"

unset DOG
readonly DOG

echo "That DOG is called $DOG"
echo "The value of PI is $PI"
echo "My cat's name is $CAT"

x=7;
y=13;

z=x+y;
echo "z equals $z"

z=$x+$y;
echo "z equals $z"
echo "z equal $((x+y))"
```

## 3. Explore Environment Variables
```bash
env
printenv
echo $TERM
echo $SHELL
echo $PATH
export PATH=$PATH:/new/dir
```

## 4. Personalize your prompt
```bash
echo PS1
export PS1="[\t \j] "
export PS1="[\d][\u@\h \w] : "
export PS1="{\!} "
export PS1="\[\033[1;35m\]\u@\h\[\033[0m\] "
PS1="\[\033[1;35m\]\u\[\033[0m\] \[\033[1;34m\]\w\[\033[0m\] "
export PS1
export PS1="\[\033[1;44m\]$USER is in \w\[\033[0m\] "
```

## 5. Working with Quotes
```bash
echo “The average pay is $1000”
echo The average pay is \$1000
echo ‘The average pay is $1000’
echo “The PATH is $PATH. The current directory is `pwd`”
mydir=`pwd`; echo $mydir
size=`wc –c < foo.txt`; echo $size
message=You\ didn’t\ enter\ the\ filename.; echo $message
dirListing=`ls -l`
echo $dirListing     # unquoted
echo "$dirListing"   # quoted
```

## 6. Operators
```bash
let x=14+5+4*8; echo $x
let y=(14+5)+4*8; echo $y
let z=(14+5+4)*8; echo $z

let A=1
let B=2
let sum=$A+$B 
echo "A=$A, B=$B, sum=$sum"
```

## 7. Conditional statements and test Command
```bash
number=20; value=10; name="Linux"
test $number -eq 20; echo $?
test $number -lt $value; echo $?
test $name = "Linux"; echo $?
test $name = "linux"; echo $?
touch testFile
test -x testFile; echo $?
test -r testFile; echo $?
test -d testFile; echo $?
test -s testFile; echo $?
test -w testFile; echo $?
test -f testFile; echo $?
```

## 8. Using expr to evaluate
```bash 
expr 7 + 3
expr 7+3
expr 7 * 3
expr 7\*3
expr 7 \* 3
expr 7 \* \( 3 + 1 \)
expr 7 = 3
expr 7 \* \( 3 + 1 \) \| 222
expr 7 = 3 \| 222
expr length "Linux is a great operating system"
expr substr "Linux is a great operating system" 7 13
expr index "Linux is a great operating system" "x"
```

## 9. Shell Variables - positional parameters
```bash
set A B C
echo $1 $2 $3

echo “the first argument is $1”
echo “the second is $2”
echo the number off arguments is $#
```