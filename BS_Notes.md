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

Decision Making 

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
$a -lt $b    $a < $b
$a -gt $b    $a > $b
$a -le $b    $a <= $b
$a -ge $b    $a >= $b
$a -eq $b    $a is equal to $b
$a -ne $b    $a is not equal to $b
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

