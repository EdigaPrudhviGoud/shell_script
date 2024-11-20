1.Read a user input and print:
echo "What is your name?"
read name
echo "$name"

Syntax:
read variable_name
readonly variable_name
unset variable_name
__________________________________
Special Variables:
$0 ->The filename of the current script.
$n ->These variables correspond to the arguments with which a script was invoked. Here n is a positive decimal number corresponding to the position of an argument (the first argument is $1, the second argument is $2, and so on).	
$# ->The number of arguments supplied to a script.
$* ->All the arguments are double quoted. If a script receives two arguments, $* is equivalent to $1 $2.
$@ ->All the arguments are individually double quoted. If a script receives two arguments, $@ is equivalent to $1 $2.
$? ->The exit status of the last command executed.   ----> 0 =successful , non-zeero=failure
$$ ->The process number of the current shell. For shell scripts, this is the process ID under which they are executing.
$! ->The process number of the last background command.

Note:Both the parameters specify the command-line arguments. However, the "$*" special parameter takes the entire list as one argument with spaces between and the "$@" special parameter takes the entire list and separates it into separate arguments.

Examples:
$./test.sh Zara Ali

#!/bin/sh
echo "File Name: $0"
echo "First Parameter : $1"
echo "Second Parameter : $2"
echo "Quoted Values: $@"
echo "Quoted Values: $*"
echo "Total Number of Parameters : $#"

Arithmetic operations:
Bourne shell didn't originally have any mechanism to perform simple arithmetic operations but it uses external programs, either awk or expr.
#!/bin/sh
val=`expr 10 + 12`
echo "Total value : $val"

Note:There must be spaces between operators and expressions. For example, 2+2 is not correct; it should be written as 2 + 2.
The complete expression should be enclosed between ‘ ‘, called the backtick.
[ $a == $b ] is correct whereas, [$a==$b] is incorrect.

Relational Operators:
-eq -> equals to
-ne -> not equals to
-gt
-lt
-ge
-le

Boolean Operators
!
-o -> logical or operator
-a -> logical and operator

String Operators
=
!=
-z -> 	Checks if the given string operand size is zero; if it is zero length, then it returns true.
-n
str

File Test Operators
Operator Description	Example
-b file	Checks if file is a block special file; if yes, then the condition becomes true.	[ -b $file ] is false.
-c file	Checks if file is a character special file; if yes, then the condition becomes true.	[ -c $file ] is false.
-d file	Checks if file is a directory; if yes, then the condition becomes true.	[ -d $file ] is not true.
-f file	Checks if file is an ordinary file as opposed to a directory or special file; if yes, then the condition becomes true.	[ -f $file ] is true.
-g file	Checks if file has its set group ID (SGID) bit set; if yes, then the condition becomes true.	[ -g $file ] is false.
-k file	Checks if file has its sticky bit set; if yes, then the condition becomes true.	[ -k $file ] is false.
-p file	Checks if file is a named pipe; if yes, then the condition becomes true.	[ -p $file ] is false.
-t file	Checks if file descriptor is open and associated with a terminal; if yes, then the condition becomes true.	[ -t $file ] is false.
-u file	Checks if file has its Set User ID (SUID) bit set; if yes, then the condition becomes true.	[ -u $file ] is false.
-r file	Checks if file is readable; if yes, then the condition becomes true.	[ -r $file ] is true.
-w file	Checks if file is writable; if yes, then the condition becomes true.	[ -w $file ] is true.
-x file	Checks if file is executable; if yes, then the condition becomes true.	[ -x $file ] is true.
-s file	Checks if file has size greater than 0; if yes, then condition becomes true.	[ -s $file ] is true.
-e file	Checks if file exists; is true even if file is a directory but exists.	[ -e $file ] is true.
---------------------------------------------------------------------------------------------------------------------------------------

if...fi statement
if...else...fi statement
if...elif...else...fi statement

case word in
   pattern1)
      Statement(s) to be executed if pattern1 matches
      ;;
   pattern2)
      Statement(s) to be executed if pattern2 matches
      ;;
   pattern3)
      Statement(s) to be executed if pattern3 matches
      ;;
   *)
     Default condition to be executed
     ;;
esac
---------------------------------------------------------------------------------------------------------------
Ex1:
#!/bin/sh
FRUIT="kiwi"
case "$FRUIT" in
   "apple") echo "Apple pie is quite tasty." 
   ;;
   "banana") echo "I like banana nut bread." 
   ;;
   "kiwi") echo "New Zealand is famous for kiwi." 
   ;;
esac
------------------------------------------------------------------------------------------------------------------------
Ex2:
#!/bin/sh

option="${1}" 
case ${option} in 
   -f) FILE="${2}" 
      echo "File name is $FILE"
      ;; 
   -d) DIR="${2}" 
      echo "Dir name is $DIR"
      ;; 
   *)  
      echo "`basename ${0}`:usage: [-f file] | [-d directory]" 
      exit 1 # Command to come out of the program with status 1
      ;; 
esac 

Outputs:
$./test.sh
test.sh: usage: [ -f filename ] | [ -d directory ]
$ ./test.sh -f index.htm
File name is index.htm
$ ./test.sh -d unix
Dir name is unix
------------------------------------------------------------------------------------------------------------------------
Loops:
1.While
while command1 ; # this is loop1, the outer loop
do
   Statement(s) to be executed if command1 is true

   while command2 ; # this is loop2, the inner loop
   do
      Statement(s) to be executed if command2 is true
   done

   Statement(s) to be executed if command1 is true
done

2.for
for var in word1 word2 ... wordN
do
   Statement(s) to be executed for every word.
done

ex:
for FILE in $HOME/.bash*
do
   echo $FILE
done

o/p:
/root/.bash_history
/root/.bash_logout
/root/.bash_profile
/root/.bashrc
--------------------------------------------------------
select var in word1 word2 ... wordN
do
   Statement(s) to be executed for every word.
done
