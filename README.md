SimpleScript to C Translator
This is a Python-based compiler (mcomp.py) that translates a small, simple scripting language (called "SimpleScript") into C code, ready for compilation into an executable.

✨ Basic Features
✅ Variables
Supports type inference — just declare a variable and assign a value. Do not change the variable's type after declaration.

Examples:

text
x = 15
s = "Yes"
These become C variables with inferred types:

c
int x = 15;
char* s = "Yes";
✅ Printing
Supports printing strings, numbers, and variables, space-separated. Automatically adds a newline at the end.

The compiler:

Detects string literals (in quotes) and inserts them directly

Detects numbers and inserts them directly

Looks up variable types and inserts appropriate format specifiers (%d for int, %s for string)

Automatically adds spaces between printed items

Appends variables in order after the format string

Important: Each printed item is followed by a space in the output.

Examples:

text
x = 14
print x
C output:

c
printf("%d \n", x);
text
print "Hello" "world"
C output:

c
printf("Hello world \n");
text
print "hello world"
x = 14
print "hello" x
C output:

c
printf("hello world \n");
printf("hello %d \n", x);
text
s = "Hello World"
print s
C output:

c
printf("%s \n", s);
✅ For Loops
Loops using a number, variable, or a parenthesized C-style expression.

Syntax:

text
for {expression}
  print ...
end
🔹 Static Number:
text
for 50
  print "Hello"
end
C output:

c
for (int __i = 0; __i < 50; __i++) {
  printf("Hello \n");
}
🔹 Variable Count:
text
x = 15
for x
  print "Hello"
end
C output:

c
int x = 15;
for (int __i = 0; __i < x; __i++) {
  printf("Hello \n");
}
🔹 Expressions (wrapped in parentheses):
text
x = 15
y = 4
for (x * y)
  print "Hello"
end
C output:

c
int x = 15;
int y = 4;
for (int __i = 0; __i < (x * y); __i++) {
  printf("Hello \n");
}
🔹 Infinite Loop:
text
for
  print "forever"
end
C output:

c
while (1) {
  printf("forever \n");
}
Note: Expression inside for is inserted directly into C. It must be valid C math.

✅ Comments
Any line starting with # is treated as a comment and ignored by the compiler.

text
# This is a comment
x = 5  # This part is NOT a comment - will cause error!
print "Hello"  # This will also cause error!
Important: Comments must be on their own line. Inline comments are not supported.

🛠 How to Use
Step 1: Write your script
Create a file, e.g., myscript.txt, with your SimpleScript code.

Example:

text
x = 10
print "Repeating" x "times"
for x
  print "Hello"
end
Step 2: Compile with mcomp.py
Run the translator:

bash
python3 mcomp.py myscript.txt
This generates a C file: __out.c

Step 3: Compile the C Code
Use your preferred compiler (like gcc) to compile:

bash
gcc __out.c -o myprogram
Run your program:

bash
./myprogram
⚠️ Important Notes & Limitations
Variables must be declared before use in loops or print statements

Type safety: You cannot change a variable's type once declared

No inline comments: Comments must be on separate lines starting with #

Spaces in print: Each printed item is automatically followed by a space

Parenthesis required: Complex math in for loops must be wrapped in parentheses

String literals must be in double quotes

No if statements or functions — this is a minimal translator

Variable names should be valid C identifiers

All generated C code is on a single line (minified)

📁 Complete Example Script
text
x = 3
s = "Hi!"
print "Message:"
for x
  print s
end
Compiles to:

c
#include <stdio.h>
int main() {int x = 3;char* s = "Hi!";printf("Message: \n");for (int __i = 0; __i < x; __i++) {printf("%s \n", s);}return 0;}
Which formats to:

c
#include <stdio.h>
int main() {
  int x = 3;
  char* s = "Hi!";
  printf("Message: \n");
  for (int __i = 0; __i < x; __i++) {
    printf("%s \n", s);
  }
  return 0;
}
✅ Summary
🚀 Simple syntax inspired by Python

🌀 Translates directly to compilable C code

🧱 Supports variables, printing with automatic spacing, and for-loops

🔧 Easy compilation workflow

📝 Space-separated print output

🔄 Flexible for loops with C expression support

Enjoy writing and compiling your own mini-scripts into C executables!
