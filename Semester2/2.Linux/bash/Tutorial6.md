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

echo "That DOG is called $DOG" # That DOG is called
echo "The value of PI is $PI"  # The value of PI is 3.14159
echo "My cat's name is $CAT"   # My cat's name is Spot

x=7;
y=13;

z=x+y;
echo "z equals $z" # z equals x+y

z=$x+$y;
echo "z equals $z" # z equals 7+13
echo "z equal $((x+y))" # z equals 20
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
echo “The average pay is $1000” # The average pay is 000
echo The average pay is \$1000  # The average pay is $1000
echo ‘The average pay is $1000’ # The average pay is 000
echo “The PATH is $PATH. The current directory is `pwd`”
mydir=`pwd`; echo $mydir # /home/nohs
size=`wc –c < foo.txt`; echo $size
message=You\ didn’t\ enter\ the\.; echo $message # You didn’t enter the.
dirListing=`ls -l`
echo $dirListing     # unquoted
echo "$dirListing"   # quoted
```

## 6. Operators
```bash
let x=14+5+4*8; echo $x  # 51
let y=(14+5)+4*8; echo $y # 51
let z=(14+5+4)*8; echo $z # 184

let A=1
let B=2
let sum=$A+$B 
echo "A=$A, B=$B, sum=$sum" # A=1, B=2, sum=3
```
---
- n1 -eq n2	true if integers n1 and n2 are equal
- n1 -ne n2	true if integers n1 and n2 are not equal
- n1 -gt n2	true if integer n1 is greater than integer n2
- n1 -ge n2	true if integer n1 is greater than or equal to integer n2
- n1 -lt n2	true if integer n1 is less than integer n2
- n1 -le n2	true if integer n1 is less than or equal to integer n2
- -r	true if it exists and is readable
- -w	true if it exists and is writable
- -x	true if it exists and is executable
- -f	true if it exists and is a regular file
- -d	true if it exists and is a directory
- -h or -L	true if it exists and is a symbolic link
- -c	true if it exists and is a character special file (i.e. the special device is accessed one character at a time)
- -b	true if it exists and is a block special file (i.e. the device is accessed in blocks of data)
- -p	true if it exists and is a named pipe (fifo)
- -u	true if it exists and is setuid (i.e. has the set-user-id bit set, s or S in the third bit)
- -g	true if it exists and is setgid (i.e. has the set-group-id bit set, s or S in the sixth bit)
- -k	true if it exists and the sticky bit is set (a t in bit 9)
- -s	true if it exists and is greater than zero in size
---

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
expr 7 + 3 # 10
expr 7+3 # 7+3
expr 7 * 3 # expr: syntax error
expr 7\*3 # 7*3 
expr 7 \* 3 # 21 
expr 7 \* \( 3 + 1 \) # 28
expr 7 = 3 # 0
expr 7 \* \( 3 + 1 \) \| 222 # 28
expr 7 = 3 \| 222 # 222
expr length "Linux is a great operating system" # 33
expr substr "Linux is a great operating system" 7 13 # is a great op
expr index "Linux is a great operating system" "x" # 5
```

## 9. Shell Variables - positional parameters
---
- $#	Number of arguments on the command line (number of positional parameters)
- $-	Options supplied to the shell
- $?	Exit value of the last command executed
- \$$	Process number of the current process
- $!	Process number of the last command done in background
- $n	Argument on the command line, where n is from 1 through 9, reading left to right, that is $1, $2, $3, $4, $5, $6, $7, $8, and $9, holding the value of the 1st, 2nd, 3rd, 4th, 5th, 6th, 7th, 8th, and 9th argument, respectively.
- $0	The name of the current shell or program (the first token)
- $*	All arguments on the command line (“$1 $2 … $9”)
- \$@	All arguments on the command line, each separately quoted (“$” “$2” … “$9”)
---
```bash
unset DOG
readonly DOG

x=7
y=13
z=x+y
echo "$z"
z=$x+$y
echo "$z"

env
printenv
echo $TERM
echo $SHELL
echo $PATH
export PATH=$PATH:/new/dir 

MYPROMPT=$PS1
echo $MYPROMPT


set A B C
echo $1 $2 $3

echo “the first argument is $1”
echo “the second is $2”
echo the number off arguments is $#

```