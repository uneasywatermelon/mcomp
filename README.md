Here is a Python project that translates a simple syntax to C for further compilation into an executable

Basic Functionalities:

VARIABLES:

supports type inference, but dont change the type of a variable in your script.

# x = 15

# s = "Yes"



PRINTING:

takes arguments separated by spaces. automatically adds a newline. (just feeds arguments into a printf.

variable support: supports variables by looking into dictionary of declared variables, where a variable name is associated with a variable type.

(this works because variable types will not change throughout the program).

program then puts the associated printf symbol (int = %d, string = %s) in order of which you provided the arguments, then afterwords cites variable name.

example:

# x = 14

# print x

this puts printf("%d \n", x);

more examples:

# print "Hello" "world"

# print "hello world"

# x = 14

# print "hello" x

outputs:

Hello world

hello world

hello 14

# s = "Hello World"

# print s

outputs:

Hello World



FOR LOOPS:

can provide any numerical argument, and the loop will run that many times. only works on nonnegative integers.

ex:

# for 50

#   print "Hello"

# end

prints "Hello" 50 times, newline after every print.

# x = 15

# y = 7

you can add integer variables as the argument.

# for x

#   print y

# end


if you want math to be involved to decide the number of times it should iterate, use parenthesis like as follows:

# x = 15

# y = 4

# for (x * y)

#   print "Hello"

# end

this loop prints "Hello" 60 times. (15 X 4).

the reason this works is because the parenthesized argument is just directly deposited into a for loop in C. So any math operations that you use in the for's argument must be valid operations in C.

Comments can be written with "#" symbol at the start of the line, then the program will ignore that line.


HOW TO RUN PROGRAM:

make text file containing simple code in this made up language.

run "python3 mcomp.py {your_script_name}".

a new "__out.c" file should be automatically generated in the directory you ran the program in.

compile "__out.c" with gcc or your favorite C compiler.

run and enjoy your new executable.
