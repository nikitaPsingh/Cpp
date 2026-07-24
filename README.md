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


## Constructor Initializer List

A **constructor initializer list** is a special syntax used to **initialize data members and base classes before the constructor body executes**.

### Syntax

```cpp
ClassName(parameters)
    : member1(value1), member2(value2)
{
    // Constructor body
}
```

The part after the colon (`:`) is called the **constructor initializer list**.

### Without Initializer List

```cpp
class Student
{
    int age;

public:
    Student(int a)
    {
        age = a;
    }
};
```

```text
Create age (default initialization)
      ↓
Assign age = a
```

---

### With Initializer List

```cpp
class Student
{
    int age;

public:
    Student(int a)
        : age(a)
    {
    }
};
```
```text
Create age with value a (age is directly initialialized with 'a'
```

No extra assignment is performed.

# Templates

A blueprint for creating functions or classes that can operate with any data type.

2 types of templates:

## 1. Function Templates

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

#### NOTE
```cpp
template<typename T>
T add(T a,T b)
{
    return a+b;
}

add(5,4.5);
```
Results into an error. Use Multiple Template.
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
  
## 2. Class Templates
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
- For classes you must specify the type:
```cpp
Box<int> obj(10);
```
If not specified, default: int
- Before templates, generic code often used void*. void* is a universal pointer. It is a generic pointer type that can hold the memory address of any data type. This is C style programming.

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

Example:
```cpp
#include <iostream>
using namespace std;

// Generic Template
template<typename T>
class Printer
{
public:

    void print()
    {
        cout<<"Generic Printer"<<endl;
    }
};

// Specialization
template<>
class Printer<char>
{
public:

    void print()
    {
        cout<<"Character Printer"<<endl;
    }
};

int main()
{
    Printer<int> p1;

    Printer<double> p2;

    Printer<char> p3;

    p1.print();

    p2.print();

    p3.print();
}
```

Output:
```
Generic Printer

Generic Printer

Character Printer
```
## Template Inheritance

### 1. Class template inherits from another class template (mixins)

Syntax
```cpp
template <typename T>
class Base
{
public:
    void display()
    {
        cout << "Base class" << endl;
    }
};

template <typename T>
class Derived : public Base<T>
{
public:
    void show()
    {
        cout << "Derived class" << endl;
    }
};
```

Example
```cpp
#include <iostream>
using namespace std;

template <typename T>
class Base
{
protected:
    T data;

public:
    Base(T x)
    {
        data = x;
    }

    void display()
    {
        cout << "Data = " << data << endl;
    }
};

template <typename T>
class Derived : public Base<T>
{
public:
    Derived(T x) : Base<T>(x) // Before constructing Derived call Base<T>'s constructor. ':Base<T>' is the 'Derived<T>' constructor's initializer list.
    {
    }

    void square()
    {
        cout << "Square = " << this->data * this->data << endl;
    }
};

int main()
{
    Derived<int> obj(5);

    obj.display();
    obj.square();

    return 0;
}
```

Output 
```
Data = 5
Square = 25
```

### 2. Class Template Inheriting from Normal class
```cpp
#include <iostream>
using namespace std;

class Person
{
public:
    void introduce()
    {
        cout << "I am a person." << endl;
    }
};

template <typename T>
class Student : public Person
{
    T marks;

public:
    Student(T m)
    {
        marks = m;
    }

    void showMarks()
    {
        cout << "Marks = " << marks << endl;
    }
};

int main()
{
    Student<float> s(89.5);

    s.introduce();
    s.showMarks();
}
```
Output
```
I am a person.
Marks = 89.5
```

### 3. Normal Class Inheriting from Template Class
```cpp
template <typename T>
class Base
{
public:
    T value;

    Base(T v)
    {
        value = v;
    }
};

class Derived : public Base<int>
{
public:
    Derived(int x) : Base<int>(x)
    {
    }

    void print()
    {
        cout << value << endl;
    }
};

int main()
{
    Derived obj(20);
    obj.print();
}
```

Output
```
20
```

## Template Type Deduction in C++

Template type deduction is the process where the compiler automatically determines the template type based on the function argument.

### Example 1

```cpp
func(10);
```

- `10` is of type `int`
- **Deduced type:** `T = int`

### Example 2

```cpp
std::string s = "Hello";
func(s);
```

- `s` is of type `std::string`
- **Deduced type:** `T = std::string`

### Example 3

```cpp
func("Hello");
```
- `"Hello"` is of type `const char[6]`
- When passed by value, it decays to `const char*`

**Deduced type:**

```cpp
T = const char*
```

> **Note:** String literals are **not** `std::string`; they are character arrays that usually decay to pointers.
