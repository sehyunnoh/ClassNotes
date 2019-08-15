## 1.
- PATH : A colon-delimited list of directories
        directories to search for executable files
- PWD : The path of current working directory 
- PS1 : The primary shell prompt
        PS1 is one of the prompts available in Linux/Unix
- HOME : The path of home directory

## 2.
```bash
var1=foo
var2=bar
a) echo '$var1 $var2' 
$var1 $var2
b) echo $var1 $var2
bar
c) There should be no whitespace before or after =, so var1 = foo should be changed to var1=foo
```

## 3
```bash
num1=5
num2=7
echo $(( num1 + num2 ))
echo "sum of $num1 + $num2 is $(($num1+$num2))"
# 12
```

## 4
```bash
#!/bin/bash
for x in a b c d e
do
        echo $x
done
#  만약 $가 빠지면 x만 5번 찍힘 (세로로)
```

## 5
> - shift: Shift positional parameters to the left by n.
> - it shifts the positional parameters(such as arguments passed to a bash script) to the left, putting each parameter in a lower position
> [shift](https://ss64.com/bash/shift.html)

## 6
```bash
cat=fluffy
a) echo $cat
fluffy
b) cat "$cat"
cat: fluffy: No such file or directory
c) cat '$cat'
cat: '$cat': No such file or directory
d) echo \$cat
$cat

echo "$cat"
fluffy
echo '$cat'
$cat
```

## 7
```bash
#!/bin/bash
echo "line 1: $0, $9, and $#"
echo "line 2: $1 $2 $2" or $*.

./7.sh c h e c k m a r k

line 1: ./7.sh, k, and 9
line 2: c h h or c h e c k m a r k.
```

## 8
```bash
#!/bin/bash
while [ $# -gt 0 ]
do
   let multi=$multi*$1
   shift
done
echo "Multiple is $multi"
```

## 9
```bash
#!/bin/bash
clear
echo "Menu"
echo "   d: Display today's date and time"
echo "   e: Display environment variables"
echo "   s: Show how file space is used by user's files"
echo "   p: Display detailed information about ALL processes"
echo "   u: View file system usage"
echo -n "Choose one of the options:"
read choice
case $choice in
        [Dd]) date ;;
        [Ee]) env ;;
        [Ss]) echo $(stat -f /) ;;
        [Pp]) ps aux ;;
        [Uu]) df ;;
esac
```
---

## 1 
> - A regular expression is a special text string for describing a search pattern.
> - It refers to a set of rules for specifying patterns, often used in search and replace operations

## 2
> - grep '^411' file

## 3
> - grep '411$' file

## 3
> - sed 's/supervisor/employee/g' supervisor > employees

## 4
```txt
dogs bone
The quick brown fox jumps over the lazy dog
('The quick brown fox jumps over the lazy dog')
(dogssssss)
```
```bash
grep -E 'dogs*[^a-zA-Z]{2,3}' somefile
# $('The quick brown fox jumps over the lazy dog')
```

## 5
```txt
A3b7x9
L6M 4L9
The code is a1b2c3.
d9d9d9d9d9d9d
l337
```
```bash
grep -E '[a-z][0-9]{3}' files
# l337
```

## 6
```console
filename.674535 directory.12345  file1+3e1234  mine  nineteen.19119

ls ?i?e*.*
filename.674535  directory.12345  nineteen.19119
```

## 7
```text
filename.674535
file1+3e1234
directory.12345
mine
nineteen.19119
+333-888-4545
9i
```
```console
grep -E '[+-][0-9]{1,5}.[0-9]*' files

file1+3e1234
+333-888-4545
```

## 8
```bash
sed -E 's/[0-9]{4}-[0-9]{2}-[0-9]{2}/December 2,1908?/g'



-------



   
   