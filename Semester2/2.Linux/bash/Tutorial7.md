## Exercise 1. A simple if statement 
```bash
#!/bin/bash
echo -n "Are you a full-time student?"
read choice
if [ $choice = Y ]
then
    echo "Please go to Building J"
else
    echo "Please go to Building A"
fi
```

## Ex 2. Nested if statements 
```bash
#!/bin/bash
if [ $# = 1 ]
then
   if [ -f  $1 ]
   then
        echo –n “The owner and last update time for $1 is “
        ls -l $1 | tr –s ’ ’ | cut –d’ ’ -f3,8
   else
        echo “$1 is not an ordinary file”
   fi
else
   echo “Please enter one argument, a file name.”
fi
```
## Ex 3. case statements 
```bash
#!/bin/bash
read -p "Enter A, B, or C: " letter
case $letter in
    A)
        echo "You entered A"
        ;;
    B)
        echo "You entered B"
        ;;
    C)
        echo "You entered C"
        ;;
    *)
        echo "You did not enter A, B, or C"
        ;;
esac
```
## Ex 4. for..in statements 
```bash
#!/bin/bash
echo “You can see the following animals in our zoo: “
for animal in `cat animalList`
do
   echo $animal
done
```
```bash
#!/bin/bash
echo “The things I like to do include:”
for myHobbies in read, ski, “collect stamps”, run
do
     echo $myHobbies
done
```
## Ex 5. C-like for loops
```bash
#!/bin/bash
# Examples using the C-style for loop
echo; echo Example 1
for (( x=0; $x<5; x=$x+1 ))
do
    echo -n $x" "
done
 
echo; echo Example 2
let x=0
while [ $x < 5 ]; then
do
    echo –n $x” “
    let x=$x+1
done
 
echo; echo Example 3
for (( y=25; $y > 0; y-- ))
do
    echo -n $y" "
done
 
echo; echo Example 4
for (( z=23; $z >= 0; z=$z-2 ))
do
    echo -n $z" "
done
```

## Ex 6. while loops with nested if statements
```bash
#!/bin/bash
# Purpose: Demonstrate the OR operator
repeat=yes
input=yes
while [ $repeat = yes ]
do
    echo "What is your name?"
    read name
    if [ $name = "Ellen" -o $name = "ellen" -o $name = "ELLEN" ]
    then
        echo "Hello, $name"
    else
        echo "Hello, $name. You are not Ellen"
    fi
    echo "Again? (To stop, type: no)  "
    read input
    if [ $input = no ]
    then
        repeat=no
    fi
done
```
```bash
#!/bin/bash
# since we are making an assignment which will always 
# evaluate to true, we have created an endless loop
while [ repeat=y ]
do
    echo "What is your name?"
    read name
    if [ $name = "Ellen" -o $name = "ellen" -o $name = "ELLEN" ]
    then
        echo "Hello, $name"
    else
        echo "Hello, $name. You are not Ellen"
    fi
    read -p "Again? (Type c to continue, followed by Enter)  " input
# when the user selects c to continue, the continue command will
# start the next iteration of the loop. Otherwise, the break command
# will execute and exit the loop.
    if [ $input = c ]
    then
        continue
    fi
    break
done
```

