## 1.
- PATH
- PWD
- PS1
- HOME

## 2.
```bash
echo '$var1 $var2' 
# $var1 $var2
echo $var1 $var2
# bar
var1=foo
var2=bar
echo $var1 $var2
```

## 3
```bash
num1=5
num2=7
echo $(( num1 + num2 ))
# 12
```

## 4
```bash
#!/bin/bash
for x in a b c d e
do
        echo $x
done
```

## 5
> shift: Shift positional parameters to the left by n.
> [shift](https://ss64.com/bash/shift.html)

## 6
```bash
cat=fluffy
echo $cat
# fluffy
cat "$cat"
# cat: fluffy: No such file or directory
cat '$cat'
# cat: '$cat': No such file or directory
echo \$cat
# $cat
echo "$cat"
# fluffy
echo '$cat'
# $cat
```

## 7
```bash
#!/bin/bash
echo "line 1:$0,$9,and $#"
echo "line 2:$1 $2 $2" or $*.

./7.sh c h e c k m a r k

# line 1:./7.sh,k,and 9
# line 2:c h h or c h e c k m a r k.
```

## 8
```bash
#!/bin/bash
read -p "write arbitrary number: " number
echo $number

./8.sh
# write arbitrary number: 10
# 10
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
shopt -s nocasematch
case $choice in
        d)
                date
                ;;
        e)
                printenv
                ;;
        s)
                du
                ;;
        p)
                ps
                ;;
        u)
                df
                ;;
esac
```
---

## 1 
> A regular expression is a special text string for describing a search pattern.

## 2

## 3

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
1337
```
```bash
grep -E '[a-z][0-9]{3}' files
#
```

## 6
```console
directory.12345  file1+3e1234  filename.674535  mine  nineteen.19119

ls ?i?e*.*
directory.12345  filename.674535  nineteen.19119
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



-------



   
   