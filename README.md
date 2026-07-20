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

## Structure of a C++ Program

### `#include <iostream>`

A **preprocessor directive** that includes the input-output stream library.

- A preprocessor is a program that runs before the compiler.
- Copies everything from the iostream library to this file before compiling.
- iostream is a header file that contains definition for cout, cin, cerr, clog.

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

## Compilation Process

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

3. Compiler: Converts C++ source code into Assembly Language.
   - Assembly language is human readable.

5. Assembler: Converts Assembly Language into Machine Code(0s and 1s) using an assembler.

6. Linker: Links object files(our code) with required libraries.->Produces the executable program.
   - The linker combines object files and libraries into one executable file.

## Tokens in C++

A token is the smallest meaningful unit of a program.

### Types of Tokens

``` int age = 20; ```
- Keywords: Reserved words with predefined meanings. (int, float, return, if, while, for, class, public, private, virtual, const) -> int
- Identifiers: Names given by the programmer. -> age
- Constants -> 20
- Operators -> =
- Separators -> ;
- String Literals: Sequence of characters in "". -> "Yo"
- Statements: An instruction executed by the program. Basically each line in a code.
- Block: Group of statments in braces({})
