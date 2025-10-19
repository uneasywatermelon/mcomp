# Lamg → C Translator

This project is a Python-based translator (`mcomp.py`) that converts a minimal, toy scripting language — **Lamg** — into **C source code**, which can then be compiled into an executable.

---

## ✨ Overview

Lamg is designed to be extremely lightweight — a teaching and experimentation tool that mirrors how a basic compiler might parse and emit code.

Currently, the language supports:

- ✅ Variable declarations (strings and numbers)
- ✅ Printing literals and variables
- ✅ Simple `for` loops
- ✅ Comments
- 🚧 (Planned) Arrays and math initialization support

---

## ✅ Variables

Lamg uses **implicit typing** at declaration: you assign a value, and the compiler infers whether it’s a number (`int`) or a string (`char*`).  

Once declared, a variable’s type **cannot change**.

**Examples:**

```lamg
x = 15
s = "Yes"
Translated C output:

c
Copy code
int x = 15;
char* s = "Yes";
💡 Notes:

Numbers can be plain digits (15) or parenthesized C-style expressions, e.g. (x * 3) — they are inserted directly into the C output.

Strings must be in double quotes (" ").

✅ Printing
print outputs a sequence of values — either string literals, numeric literals, or previously declared variables. Arguments are separated by spaces, and a space is added after every token, followed by a newline (\n).

This results in a printf(...) call with the correct C format specifiers depending on the variable types.

Examples:

lamg
Copy code
print "Hello"
C output:

c
Copy code
printf("Hello \n");
lamg
Copy code
x = 42
print "Value is" x
C output:

c
Copy code
printf("Value is %d \n", x);
lamg
Copy code
s = "Hi"
x = 3
print "Message:" s x
C output:

c
Copy code
printf("Message: %s %d \n", s, x);
Printing Rules
String literals must be enclosed in quotes ("...").

Numeric literals and variables are both allowed.

Each item in a print command is separated by a space in the final output.

A newline (\n) is always added automatically at the end.

✅ For Loops
Loops are introduced with for, followed by:

a number (e.g. for 5)

a variable (e.g. for x)

or a C-style expression in parentheses (e.g. for (x * 2))

Each for must be closed with an end statement.

Examples:

lamg
Copy code
for 3
  print "Hello"
end
C output:

c
Copy code
for (int __i = 0; __i < 3; __i++) {
    printf("Hello \n");
}
lamg
Copy code
x = 5
for x
  print "Hi"
end
C output:

c
Copy code
int x = 5;
for (int __i = 0; __i < x; __i++) {
    printf("Hi \n");
}
lamg
Copy code
x = 2
y = 4
for (x * y)
  print "Hello"
end
C output:

c
Copy code
int x = 2;
int y = 4;
for (int __i = 0; __i < (x * y); __i++) {
    printf("Hello \n");
}
Loop Notes
The argument to for is inserted directly into the C code.

If parentheses are used, the content is treated as a raw C expression.

Every for block must end with end.

✅ Comments
Any line starting with # is treated as a comment and ignored during compilation.

Example:

lamg
Copy code
# This is a comment
x = 5
# print "This will not appear"
print x
C output:

c
Copy code
int x = 5;
printf("%d \n", x);
🛠 How to Use
Step 1: Write your script
Create a file, e.g., myscript.txt, with your Lamg code:

lamg
Copy code
x = 10
print "Repeating" x "times"
for x
  print "Hello"
end
Step 2: Compile with mcomp.py
Run the translator:

bash
Copy code
python3 mcomp.py myscript.txt
This generates a C file: __out.c.

Step 3: Compile the C Code
Use your preferred compiler (like gcc) to compile:

bash
Copy code
gcc __out.c -o myprogram
Run your program:

bash
Copy code
./myprogram
🧠 Notes
You cannot change a variable’s type once declared.

Variables must be declared before they’re used in a print or for.

Expressions inside parentheses are treated as raw C code.

Strings must always use double quotes.

The print command automatically appends a newline.

The translator’s spacing in printf output is literal — it includes a space after each argument.

Error messages are basic; this project’s main goal is educational clarity, not strict robustness.

📁 Example Script
lamg
Copy code
x = 3
s = "Hi!"
print "Message:"
for x
  print s
end
C output:

c
Copy code
int x = 3;
char* s = "Hi!";
printf("Message: \n");
for (int __i = 0; __i < x; __i++) {
    printf("%s \n", s);
}
✅ Summary
🚀 Easy, minimal language

🌀 Translates directly into working C code

🧱 Supports variables, printing, and for-loops

🔧 Ready for compilation with gcc or any C compiler

Enjoy experimenting with Lamg, and see how high-level syntax maps directly into real compiled C programs!
