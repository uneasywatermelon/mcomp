# SimpleScript to C Translator

This is a Python-based compiler (`mcomp.py`) that translates a small, simple scripting language (called "SimpleScript") into C code, ready for compilation into an executable.

---

## ✨ Basic Features

### ✅ Variables

Supports **type inference** — just declare a variable and assign a value. **Do not change the variable's type** after declaration.

**Examples:**
simplescript x = 15 s = "Yes"
These become C variables with inferred types:
c int x = 15; char* s = "Yes";
---

### ✅ Printing

Supports printing **strings and variables**, space-separated. Automatically adds a newline.

This is compiled to a `printf(...)` statement in C.

The compiler:
- Looks up variable types.
- Inserts appropriate format specifiers (`%d` for int, `%s` for string, etc.).
- Appends variables in order.

**Examples:**
simplescript x = 14 print x
C output:
c printf("%d\n", x);
More examples:
simplescript print "Hello" "world" print "hello world" x = 14 print "hello" x
C output:
c printf("Hello world\n"); printf("hello world\n"); printf("hello %d\n", x);
simplescript s = "Hello World" print s
C output:
c printf("%s\n", s);
---

### ✅ For Loops

Loops using a number, variable, or a parenthesized C-style expression.

**Syntax:**
simplescript for {expression} print ... end
#### 🔹 Static Number:
simplescript for 50 print "Hello" end
C output:
c for (int __i = 0; __i < 50; __i++) { printf("Hello\n"); }
#### 🔹 Variable Count:
simplescript x = 15 for x print "Hello" end
C output:
c int x = 15; for (int __i = 0; __i < x; __i++) { printf("Hello\n"); }
#### 🔹 Expressions (wrapped in parentheses):
simplescript x = 15 y = 4 for (x * y) print "Hello" end
C output:
c int x = 15; int y = 4; for (int __i = 0; __i < (x * y); __i++) { printf("Hello\n"); }
> **Note:** Expression inside `for` is inserted *directly into C*. It must be valid C math.

---

### ✅ Comments

Any line starting with `#` is treated as a **comment** and ignored by the compiler.
simplescript # This is a comment x = 5 # print "This won't show"
---

## 🛠 How to Use

### Step 1: Write your script

Create a file, e.g., `myscript.txt`, with your SimpleScript code.

Example:
simplescript x = 10 print "Repeating" x "times" for x print "Hello" end
---

### Step 2: Compile with `mcomp.py`

Run the translator:
bash python3 mcomp.py myscript.txt
This generates a C file: `__out.c`

---

### Step 3: Compile the C Code

Use your preferred compiler (like `gcc`) to compile:
bash gcc __out.c -o myprogram
Run your program:
bash ./myprogram
---

## 🧠 Notes

- You cannot change a variable’s type once declared.
- All variables must be declared before use in loops or print statements.
- Complex math inside `for` loops must be **valid C** syntax.
- String literals should be in quotes.
- The `print` command automatically appends a newline.
- No `if` statements or functions — this is a minimal translator.

---

## 📁 Example Script
simplescript x = 3 s = "Hi!" print "Message:" for x print s end
Compiles to:
c int x = 3; char* s = "Hi!"; printf("Message:\n"); for (int __i = 0; __i < x; __i++) { printf("%s\n", s); }
---

## ✅ Summary

- 🚀 Simple syntax
- 🌀 Translates directly to C
- 🧱 Supports variables, printing, and for-loops
- 🔧 Easy to compile and run

Enjoy writing and compiling your own mini-scripts into C executables!
