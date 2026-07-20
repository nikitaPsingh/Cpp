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
- We shouldn't use namespace in large projects because it imports all names from the Standard Library into the global namespace, increasing the risk of name collisions.
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

2. Compiler: Converts C++ source code into Assembly Language.
   - Assembly language is human readable.

3. Assembler: Converts Assembly Language into Machine Code(0s and 1s) using an assembler.

4. Linker: Links object files(our code) with required libraries.->Produces the executable program.
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

# Templates

A blueprint for creating functions or classes that can operate with any data type.

2 types of templates:

##1. Function Templates

Allows a single function to work with multiple data types.

Syntax
```cpp
template <typename T>
return_type function_name(parameters)
{
    // code
}
```
or
```cpp
template <class T>
```

Example
```cpp
#include <iostream>
using namespace std;

template <typename T>
T add(T a, T b)
{
     return a + b;
}

int main(){
     cout << add(5, 10) << endl; // or add<int>(5, 7(;
     cout << add(2.5, 3.7) << endl; // or add<double>(2.5, 4.8);

     return 0;
}
```
Output
```
15
6.2
```

Explanation
- add(5, 10) -> compiler generates int add(int a, int b)
- add(2.5, 3.7) -> compiler generates double add(double a, double b)

This is called **template instantiation**.

### Multiple Template Parameters
Templates can have more than one type.

```cpp
template<typename T, typename U>
void display(T a, U b)
{
    cout << a << " " << b;
}
```

Usage
```cpp
display(10,3.14);

display("Age",25);
```

### Non-Type Template Parameters
Templates can also take constant values

```cpp
template<typename T, int size>
class Array
{
    T arr[size];
};
```

Usage
```cpp
Array<int,10> obj;
```
- T is a type parameter
- 10 is a non type template parameter
  
##2. Class Templates
Templates can also create generic classes.

Example
```cpp
#include <iostream>
using namespace std;

template<typename T>
class Calculator
{
    T a, b;

public:

    Calculator(T x, T y)
    {
        a = x;
        b = y;
    }

    T add()
    {
        return a + b;
    }
};

int main()
{
    Calculator<int> c1(10,20);

    cout << c1.add();

    Calculator<double> c2(5.5,3.2);

    cout << c2.add();
}

// Output
// 10
// 8.7
```

Before templates, generic code often used void*. void* is a universal pointer. It is a generic pointer type that can hold the memory address of any data type. This is C style programming.

## Template Instantiation
The compiler generates actual functions or classes only when they are used.

```cpp
template<typename T>
T square(T x)
{
    return x*x;
}
```

Calling
```cpp
square(5);
```

generates
```cpp
int square(int x)
```

Calling 
```cpp
square(2.5);
```

generates
```cpp
double square(double x)
```

## Template Specialization
Sometimes the generic implementation is not suitable for a particular type.

Generic Template
```cpp
template<typename T>
void print(T value)
{
    cout << value;
}
```

Specialization for char*
```cpp
template<>
void print<char*>(char* value)
{
    cout << "String: " << value;
}
```

Usage
```cpp
print(10);

print("Hello");
```

Output
```
10

String: Hello
```


