# BASH SCRIPTING

```bash
#!/bin/bash
```

 This path, tells the operating system that this file is a set of commands to be fed into the interpreter indicated. 

Note that if the path given at the **"sha-bang"** is incorrect, then an error message e.g. "Command not found.",

```bash
ps | grep $$
  91194 pts/6    00:00:00 bash

```

It show the current shell using with type with bash 

```bash
/bin/bash
```

This show the full execution path of the shell interpreter

```bash
echo 'Goodbye, World!
```

## **Variables**

```bash
PRICE_PER_APPLE=5
MyFirstLetters=ABC
greeting='Hello        world!'
```

A backslash "\" is used to escape special character meaning

```bash
PRICE_PER_APPLE=5
echo "The price of an Apple today is: \$HK $PRICE_PER_APPLE"
```

```bash
MyFirstLetters=ABC
echo "The first 10 letters in the alphabet are: ${MyFirstLetters}DEFGHIJ"

greeting='Hello        world!'
echo $greeting" now with spaces: $greeting"
```

```bash
FILELIST=`ls`
FileWithTimeStamp=/tmp/my-dir/file_$(/bin/date +%Y-%m-%d).txt
```

```bash
date -d "Dec 11, 2025" +%A
Thursday

/bin/date +%Y-%m-%d
2025-12-11

/bin/date +%A
Thursday
```

```bash
/bin/date -d "Jan 1, 2025" +%A
Wednesday
```

## Passing Arguments to the Script

```bash
#!/bin/bash
function File {
	echo $#
}

if [ ! $# -lt 1 ]; then 
	File $*
	exit 0
fi

bash test.sh Shell is fun 
```

output

```bash
3
```

## Arrays

```bash
my_array=(apple banana "Fruit Basket" orange)
new_array[2]=apricot
```

The total number of elements in the array is referenced by ${#my_array[@]}

```bash
my_array=(apple banana "Fruit Basket" orange)
echo  ${#my_array[@]} 
```

The array elements can be accessed with their numeric index. The index of the first element is 0

```bash
my_array=(apple banana "Fruit Basket" orange)
echo ${#my_array[@]} 
my_array[4] = "carrot"
echo ${#my_array[@]}
echo ${my_array[${#my_array[@]}-1]}
```

## Basic Operator

```bash
A=3
B=$((100 * $A + 5)) # 305

A=3
B=$((100 * A + 5)) # 305
```

```bash
#!/bin/bash

COST_PINEAPPLE=50

COST_BANANA=4

COST_WATERMELON=23

COST_BASKET=1

TOTAL=$(($COST_PINEAPPLE + $COST_BANANA + $COST_WATERMELON + $COST_BASKET))

echo "Total Cost is $TOTAL"
```

## Basic String Operation

```bash
String="this is a String"
echo ${#String}
```

Index 

```bash
STRING="this is a string"
SUBSTRING="hat"
expr index "$STRING" "$SUBSTRING" #2
```

Substring Extraction

```bash
STRING="this is a string"
POS=1
LEN=3
echo ${STRING:POS:LEN} #his
```

```bash
STRING="this is a string"
echo ${STRING:1} #this is a string
echo ${STRING:12}  #ring
```

Simple data extraction example

```bash
#Code to extract the First name from the data
DATARECORD="last=Clifford,first=John Doe,state=CA"
COMMA1=`expr index "$DATARECORD" ","`
CHOPFIELD1=${DATARECORD:COMMA1}
COMMA2=`expr index "$CHOPFIELD" ","`
LENGTH=`expr "$COMMA2" - 6 - 1
FIRSTNAME=${CHOPFIELD1:6:LENGTH}
echo $FIRSTNAME
```

Substring Replacement

```bash
STRING="to be or not to be"
```

Replace first occurence of substring with replacement

```bash
STRING="to be or not to be"
echo ${STRING[@]/be/eat}  #to eat or not to be
```

Replacement all occurrences of substring

```bash
STRING="to be or not to be"
echo ${STRING[@]//be/eat}  #to eat or not to eat
```

Delete all occurrences of substring (replace with empty string)

```bash
STRING="to be or not to be"
echo ${STRING[@]// not/}  #to be or to be
```

Replace occurrence of substring if all the beginning of $String

```bash
STRING="to be or not to be"
echo ${STRING[@]/#to be/eat now}  #eat now or not to be
```

Replace occurrence of substring if at the end of $STRING

```bash
STRING="to be or not to be"
echo ${STRING[@]/%be/eat}  # to be or not to eat
```

Replace occurrence of substring with shell command output

```bash
STRING="to be or not to be"
echo ${STRING[@]/%be/be on $(date +%Y-%m-%d)}  # to be or not to be on 2025-12-12
```

Example

```bash
#!/bin/bash

BUFFETT="Life is like a snowball. The important thing is finding wet snow and a really long hill."

    # write your code here
    ISAY=$BUFFETT
    change1=${ISAY[@]/snow/foot}
    change2=${change1[@]//snow/}
    change3=${change2[@]/finding/getting}
    loc=`expr index "$change3" 'w'`
    ISAY=${change3::$loc+2}

# Test code - do not modify
echo "Warren Buffett said:"
echo $BUFFETT
echo "and I say:"
echo "$ISAY"
```

output

```bash
Warren Buffett said:
Life is like a snowball. The important thing is finding wet snow and a really long hill.
and I say:
Life is like a football. The important thing is getting wet

```

## Decision Making

```bash
NAME="John"
if [ "$NAME" = "John" ]; then
		echo "True - my name is indeed John"
fi
```

```bash
NAME="Bill"
if [ "$NAME" = "John" ]; then
		echo "True - my name is indeed John"
fi
else 
	echo "False"
	echo "You must mistaken me for $NAME"
fi
```

```bash
NAME="George"
if [ "$NAME" = "John" ]; then 
	echo "John Lennon"
elif [ "$NAME" = "George" ]; then
	echo "George Harrison"
else 
	echo "This leaves us with Paul and Ringo"
```

Types of numeric comparisons

```bash
comparison    Evaluated to true when
$a -lt $b    #$a < $b
$a -gt $b    #$a > $b
$a -le $b    #$a <= $b
$a -ge $b    #$a >= $b
$a -eq $b    #$a is equal to $b
$a -ne $b    #$a is not equal to $b
```

Types of string comparison

```bash
comparison    Evaluated to true when
"$a" = "$b"     $a is the same as $b
"$a" == "$b"    $a is the same as $b
"$a" != "$b"    $a is different from $b
-z "$a"         $a is empty
```

Logical Combination

```bash
if [[ $VAR_A[0] -eq 1 && ($VAR_B = "bee" || $VAR_T = "tee") ]] ; then
		command...
fi
```

Case Structure

```bash
case "$variable" in 
			"$variable1" )
				command...
			;;
			"$variable2" )
				command..
			;;
esac
		
```

Simple case Bash Structure

```bash
mycase=1
case $mycase in 
		1) echo "Selected Bash";;
		2) echo "Selected Java";;
		3) echo "Selected Python";;
esac
```

## LOOPS

bash for loop

```bash
for arg in [list] ; do 
	command..
done
```

```bash
#loop for array number
NAMES=(Joe Jenny Sara Tony)
for N in ${NAMES[@]} ; do 
		exho "My name is $N"
done

for f in test.sh /etc/localtime; do
  if [ -e "$f" ]; then  # if exist
    echo "File is: $f"
  fi
done
```

bash while loop

```bash
while [ condition ] do 
		command..
done
```

```bash
COUNT=4
while [ $COUNT -gt 0 ]; do 
	echo "Value of count is: $COUNT"
	COUNT=$((COUNT-1))
done
```

bash until loop

```bash
unitl [ condition ]; do
	command...
done
```

```bash
COUNT=1
until [ $COUNT -gt 5 ]; do
	echo "Value of count is: $COUNT"
	COUNT=$((COUNT + 1))
done
```

break and continue

```bash
#Print out 0,1,2,3,4
COUNT=0
while [ $COUNT -ge 0 ]; do 
	echo "Value of COUNT is: $COUNT"
	COUNT=$((COUNT + 1))
	if [ $COUNT -ge 5 ]; then
		break
	fi 
done

#Print out only odd numbers - 1,3,5,7,9
COUNT=0
while [ $COUNT -ge 0 ]; do 
	echo "Value of COUNT is: $COUNT"
	COUNT=$((COUNT + 1))
	if [ $((COUNT % 2)) == 0 ]; then
		continue;
	fi 
done

```

## ARRAY-COMPARISON

```bash
array=(23 45 34 1 3 2)

#To refer to a particular value (e.g. : to refer 3rd value)
echo ${array[2]}

#To refer to all the array values
echo ${array[@]}

#To evaluate the number of elements in an array
echo ${#array[@]}
```

```bash
a=(3 5 8 10 6) 
b=(6 5 4 12) 
c=(14 7 5 7)
	#comparison of first two arrays a and b
for x in "${a[@]}"; do
  for y in "${b[@]}"; do
    [ "$x" == "$y" ] && z+=("$x")
  done
done

for i in "${c[@]}"; do
  for k in "${z[@]}"; do
    [ "$i" == "$k" ] && j+=("$i")
  done
done

echo "${j[@]}" # 5
```

## SHELL FUNCTION

```bash
function function_name {
	command...
}
```

```bash
function function_B {
	echo "Function B."
}

funcction function_A {
	echo "$1"
}

function adder {
	echo "$(($1 + $2))"
}

function_A "Function A."
function_B
addr 12 56
```

## SPECIAL FUNCTION

```bash
#!/bin/bash
echo "Scipt Name: $0"
functuon func {
		i=0
		for var in "$@"
			((i++))
			echo "The \$${i} argument is: ${var}"
		done
		echo "Total count of arguments: $#"
}

func We are argument
```

```bash
func() {
		echo " ---- \"\$*\""
		for ARG in "$*"
		do 
			echo $ARG   # We are argument
		done
		
		echo "--- \"\$@\""
    for ARG in "$@"
    do
        echo $ARG  # We\nare\nargument\n
    done
}
func We are argument
```

## BASH TRAP CMD

```bash
trap "echo Booh!;exit" 2 15 
echo "it's going to run until you hit Ctrl+Z"
echo "hit Ctrl+C to be blown away!"

while true        
do
    sleep 60       
done
```

## FILE TESTING

use “-e” to test if the file exist 

```bash
#!/bin/bash
filename="sample.md"
if [ -e "$filename" ]; then
	echo "$filename exists as a file"
fi
```

use “-d” to test if the directory exist 

```bash
#!/bin/bash 
dir_name="test_dir"
if [ -d "$dir_name" ]; then
	echo "$dir_name exists as a directory"
fi
```

use “-r” to test if file has read permission for the user running the script/test

```bash
#!/bin/bash
filename="sample.md"
if [ ! -f "$filename" ]; then 
	touch "$filename"
fi
if [ -r "$filename" -a -w "$filename" -a -x "$filename" ]; then
	echo "you are allowed to read, write, execute $filename"
else
	echo "you are not allowed to read $filename"
fi
```

## INPUT PARAMETER PARSING

```bash
#script.sh -f sample.md -o output.md -v
while getopts "f:vo" option; do
	case "$option" in 
		f) filename=$OPTARG ;;
		o) output=$OPTARG ;;
		v) verbose=true ;;
		*) echo "Invalid option"; exit 1
	esac
done

echo "Filename: $filename"

if [ "$verbose" = true ] ; then
	echo "Verbose mode is ON"
else 
	echo "Verbose mode in OFF"
fi
```

## PIPELINES

```bash
command1 | command2
```

```bash
ls / | wc -l

ls / | head

ls / | grep
```

```bash
#!/bin/bash
cat /proc/cpuinfo | grep processor | wc -l 
```
