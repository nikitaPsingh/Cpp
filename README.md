# C++ Interview Preparation

A comprehensive guide to preparing for C++ technical interviews.

---

## What is C++?

C++ is a **general-purpose, compiled, statically typed, object-oriented programming language** 
It supports multiple programming paradigms:

- Procedural Programming: A program is divided into functions (procedures) that perform specific tasks step by step.
- Object-Oriented Programming: The program is organized around objects instead of functions.
- Generic Programming (Templates): Code that works with multiple data types without rewriting the same logic.
- Functional Programming (Lambdas): Instead of creating a separate function we create it on spot.

---

## Applications of C++

C++ is widely used in:

- Operating Systems
- Game Development
- Embedded Systems
- High Performance Computing
- Browsers
- Databases
- Compilers
- Financial Software
- Robotics
- Competitive Programming

---

# Structure of a C++ Program

### `#include <iostream>`

A **preprocessor directive** that includes the input-output stream library.

- A preprocessor is a program that runs before the compiler.
- Copies everything from the iostream library to this file before compiling.
- iostream is a header file that contains definition for cout, cin, cerr, clog.
---

### `using namespace std;`

The C++ Standard Library is inside the `std` namespace.
Without it:

```cpp
std::cout << "Hello";
```

With it:

```cpp
using namespace std;

cout << "Hello";
```

Namespaces prevent naming conflicts between different libraries.

### NOTE
- We shouldn't usig namespace in large projects because it imports all names from the Standard Library into the global namespace, increasing the risk of name collisions.
- The `<<` operator is called the **stream insertion operator**.

# Compilation Process

Every C++ program goes through four stages.

```
Source Code
     │
     ▼
Preprocessor
     │
     ▼
Compiler
     │
     ▼
Assembler
     │
     ▼
Linker
     │
     ▼
Executable Program
```

1. Preprocessor: Processes directives such as #include, #define...

2. Compiler: Converts C++ source code into Assembly Language.

3. Assembler: Converts Assembly Language into Machine Code using an assembler.

4. Linker: Links object files with required libraries.->Produces the executable program.

---

### Interview Question

**What is the role of the linker?**

The linker combines object files and libraries into one executable file.

---

# Tokens in C++

A token is the smallest meaningful unit of a program.

Example:

```cpp
int age = 20;
```

Tokens:

```
int
age
=
20
;
```

---

## Types of Tokens

- Keywords
- Identifiers
- Constants
- Operators
- Separators
- String Literals

---

# Keywords

Keywords are reserved words having predefined meanings.

Examples:

```cpp
int
float
char
double
class
public
private
virtual
const
return
```

Keywords **cannot** be used as variable names.

Invalid:

```cpp
int class = 5;
```

---

# Identifiers

Identifiers are names created by programmers.

Examples:

```cpp
age
salary
studentName
totalMarks
```

## Rules

✔ Can contain letters

✔ Digits

✔ Underscore

✔ Cannot start with a digit

✔ Cannot contain spaces

✔ Cannot be a keyword

### Valid

```cpp
student1
_total
marksObtained
```

### Invalid

```cpp
1student
my marks
class
```

---

# Comments

Comments improve code readability.

## Single-line Comment

```cpp
// This is a comment
```

## Multi-line Comment

```cpp
/*
This
is
a
multi-line
comment
*/
```

---

# Statements

A statement is a complete instruction.

Example:

```cpp
int a = 5;

a++;

cout << a;
```

---

# Blocks

A block is a group of statements enclosed within braces.

```cpp
{
    int x = 5;
    cout << x;
}
```

Variables declared inside a block have block scope.

---

# Frequently Asked Interview Questions

## 1. Why is C++ faster than Java?

Because C++ is compiled directly into machine code while Java runs on the JVM using bytecode.

---

## 2. Why is C++ called a middle-level language?

Because it supports both:

- High-level programming
- Low-level memory manipulation

---

## 3. Difference between C and C++

| C | C++ |
|---|---|
| Procedural | Multi-Paradigm |
| No Classes | Supports Classes |
| No Inheritance | Supports Inheritance |
| No Polymorphism | Supports Polymorphism |
| Uses `malloc()` | Uses `new` |

---

## 4. Why is C++ called Object-Oriented?

Because it supports:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

---

# Common Beginner Mistakes

- Forgetting semicolons
- Misspelling keywords
- Using variables without initialization
- Confusing `=` with `==`
- Forgetting required header files

---

# Practice Questions

1. What is C++?
2. Why is C++ called a multi-paradigm language?
3. Explain the compilation process.
4. What is a namespace?
5. What are tokens?
6. Differentiate keywords and identifiers.
7. Explain the role of the linker.
8. What does `return 0;` do?
9. Explain the structure of a C++ program.
10. Why is `using namespace std;` discouraged in large projects?

---

# Summary

By the end of this chapter, you should understand:

- ✔ What C++ is
- ✔ Features of C++
- ✔ Program structure
- ✔ Compilation process
- ✔ Namespaces
- ✔ Tokens
- ✔ Keywords
- ✔ Identifiers
- ✔ Statements
- ✔ Blocks
- ✔ Common interview questions

---

**Next Chapter:** Variables, Data Types, Constants, Memory Layout, Type Modifiers, Literals, Variable Scope, Initialization, and Interview Questions.
