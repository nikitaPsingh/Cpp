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

# Pointers
A pointer is a variable whose job is to store the memory address of another variable.
### Example

```cpp
int x = 10;
int* ptr = &x;
```
**NOTE**
- x is a named variable.
- ptr stores the address of x.
```
x -> 20 (Value)
&x -> 1000 (Address of x)
ptr -> 1000 (Stores the address)
*ptr -> 20 (Value stored at that address)
```

```cpp
int* ptr = new int(10);
```
- new int(10) → Creates an integer in memory, initializes it with 10, and returns its address.
- int* ptr → Creates a pointer that can store the address of an int.
- ptr = new int(10) → Stores the returned address in ptr.

**NOTE**
- There is no variable named x.
- **new allocates memory in heap and returns its address**
- The only way to access it is through ptr.
  
# Smart Pointers
A class template that behaves like a pointer but automatically manages memory allocation and deallocation.

Normal Pointer
```
int*
```

Smart Pointer
```
<unique_ptr>int
```

### Example

Instead of 
```cpp
int* ptr = new int(10);

delete ptr;
```

it becomes
```cpp
unique_ptr<int> ptr(new int(10));
```
- unique_ptr → class template provided by C++ standard library
- unique_ptr<int> → class (created from the template)
- p → object of the class unique_ptr<int>
- Inside p → a raw pointer (int*) that points to heap memory

## Types of Smart Pointer

## 1. unique_ptr (one owner)
Only ONE pointer can own the object.

```cpp
#include <memory>

int main()
{
    std::unique_ptr<int> ptr(new int(10));
}
```

Copy is not allowed
```cpp
unique_ptr<int> p1(new int(10));

unique_ptr<int> p2 = p1;
```
Because in this case, we now have two pointers that own(it's their responsibility to delete that object) the object but we will be deleting only one of them which will cause memory leak.

Instead
```cpp
unique_ptr<int> p2 = std::move(p1);
```
### Access Object
```cpp
unique_ptr<int> p(new int(5));

cout << *p;

//output 5
```
means
"Go to the object that p points to and give me its value."

**Member access**
```cpp
class Car
{
public:
    void drive(){}
};

unique_ptr<Car> c(new Car());

c->drive();
```

### make unique
Instead of 
```cpp
unique_ptr<Car> c(new Car());
```
Use
```cpp
auto c = make_unique<Car>();
```

## 2. shared_ptr (many owner)
Two pointers own the same object.
```cpp
auto p1 = make_shared<int>(10);

auto p2 = p1;
```
Even if you destroy one pointer the object will still remain

## 3. weak_ptr (Observer, No Ownership)
A weak_ptr observes an object managed by shared_ptr but does not increase the reference count.
```cpp
shared_ptr<int> p = make_shared<int>(5);

weak_ptr<int> w = p;
```
To break cyclic references created by shared_ptrs and avoid memory leaks.

### Access weak ptr
This is wrong
```cpp
*w;
```
Insted
```cpp
if (auto temp = w.lock())
{
    cout << *temp;
}
```
lock() tries to create a temporary shared_ptr. If the object has already been destroyed, it returns an empty shared_ptr.

# enum (Enumerations)
An enum is an user defined data type. It contains a fixed list of constants.

```cpp
enum EnumName
{
    value1,
    value2,
    value3
};
```

Example
```cpp
#include <iostream>
using namespace std;

enum Color
{
    Red,
    Green,
    Blue
};

int main()
{
    Color c = Green; // Creating variables and assigning values

    if(c == Green)
    {
        cout << "Green selected";
    }

     cout << c; // outputs 2
}

// Output: Green selected
```
**NOTE**
cout << c print an integer because that is how the compiler stores the integers. Here it stores Red, Green and Blue as 0, 1 and 2 respectively,

### Assign your own values

```cpp
enum ErrorCode
{
    Success = 200,
    NotFound = 404,
    ServerError = 500
};
```

### Mixed values

```cpp
enum Numbers
{
    A = 5,
    B,
    C,
    D = 20,
    E
};
```

Compiler gives
```cpp
A = 5
B = 6
C = 7
D = 20
E = 21
```

### Converting enum to int
```cpp
Color c = Green;

cout << (int)c;

or

cout << static_cast<int>(c);
```
Output
```
1
```
**NOTE**
We need not convert enum to int in Old enum but in the new one(enum class), we need to convert it explicitly if needed.
### Converting int to enum
```cpp
Color c = static_cast<Color>(2);
```
Now
```
c == blue
```

## enum class (Scoped enums)

Problem:
```cpp
enum Color
{
    Red,
    Green
};

enum Fruit
{
    Apple,
    Mango
};

Color c = Red;
Fruit f = Apple;

if(c == f)
```
This compiles in older cpp because both of them have equal integer values but comparing a Fruit to a Color makes no sense.

Another Problem:
```cpp
enum Color
{
    Red
};

enum Traffic
{
    Red
};
```
Gives an error because both Red are in the same scope.

Solution: enum class
```cpp
enum class Color
{
    Red,
    Green,
    Blue
};
```

Example
```cpp
#include <iostream>
using namespace std;

enum class TrafficLight
{
    Red,
    Yellow,
    Green
};

int main()
{
    TrafficLight light = TrafficLight::Green;

    if(light == TrafficLight::Green)
    {
        cout << "Go";
    }
}
```

# Casting
Converting one data type to another.

## Types of Casting

## 1. Implicit Casting (Automatic)
Compiler does it

Example
```cpp
char ch = 'A';

int x = ch;
```
Output
```
65
```
'A' -> ASCII -> 65

## 2. Ezplicit Casting (Manual)

Example
```cpp
double x = 5.8;

int y = (int)x;
```
Output
```
5
```
Better
```cpp
int y = static_cast<int>(x);
```

**NOTE**
```cpp
int a = 5;
int b = 2;

double c = a / b;
```
Output is 2, not 2.5 because 5/2(both are integers). Integer division happens first and rhen it is converted to a double.

Correct
```cpp
double c = (double)a / b;
```

## Types of Casts in C++
There are four C++ casting operators.
```
static_cast
dynamic_cast
const_cast
reinterpret_cast
```

## 1. static_cast
Used for safe and well-defined conversions.
#### int-> double
```cpp
int x = 5;

double y = static_cast<double>(x);

//Output: 5->5.0
```

#### double -> int
```cpp
double x = 5.9;

int y = static_cast<int>(x);

//Output: 5
```

#### float -> int
```cpp
float f = 7.8f;

int x = static_cast<int>(f);

//Output: 7
```

#### char -> int
```cpp
char ch = 'A';

int x = static_cast<int>(ch);

//Output: 65
```

#### int -> char
```cpp
int x = 66;

char ch = static_cast<char>(x);

cout << ch;

//Output: B
```

## static_cast in OOP
### Upcasting
Upcasting is the process of converting a derived class pointer/reference to a base class pointer/reference. 
Example
```cpp
class Animal
{
public:
    void eat()
    {
        cout << "Eating";
    }
};

class Dog : public Animal
{
public:
    void bark()
    {
        cout << "Barking";
    }
};
```
Create a dog
```cpp
Dog d;
```
Now
```cpp
Animal* ptr = &d;
```
or
```cpp
Animal* ptr = static_cast<Animal*>(&d);
```
This is upcasting. The compiler automatically converts Dog* to Animal*.

##### **NOTE**
ptr->eat() is correct. ptr->bark() is wrong. Because compiler only ptr is an Animal*. Even though the object is actually a Dog, the pointer's type controls what members are directly accessible.

### Downcasting
Downcasting is the process of converting a base class pointer/reference to a derived class pointer/reference.

Upcasting
```cpp
Dog* → Animal*
```
Downcasting
```cpp
Animal* → Dog*
```

Suppose
```cpp
Dog d;
Animal* ptr = &d; //Upcasting
```

- ptr is an Animal*, Now to go back to Dog*:
```cpp
Dog* dogPtr = static_cast<Dog*>(ptr);
```

Works only if the object is actually a Dog. If it was 'Animal a', it would have been an undefined behaviour(since it is not checked by static_cast at runtime, so use dynamic_cast):
  
Unsafe Example
```cpp
Animal a;

Animal* ptr = &a;

Dog* dogPtr = static_cast<Dog*>(ptr);

dogPtr->bark();   // ❌ Undefined behavior
```
To solve this we have dynamic_cast.

## 2. dynamic_cast
Used with polymorphism. It's the safest cast for base and derived classes.
Example
```cpp
class Animal
{
public:
    virtual void speak() {}
};

class Dog : public Animal
{
};
```
Now
```cpp
Animal* ptr = new Dog();
```
Convert
```cpp
Dog* d = dynamic_cast<Dog*>(ptr);
```
If successful (object is a Dog)
```cpp
d != nullptr
```
If not (oject is not a Dog)
```cpp
nullptr
```
Example 1
```cpp
Animal* ptr = new Animal();

Dog* d = dynamic_cast<Dog*>(ptr);

if(d == nullptr)
    cout << "Failed";
```
It checks the object's type at runtime(which is Animal and not Dog) so d becomes nullptr.

Example 2(succeeds)
```cpp
Animal* ptr = new Dog();

Dog* d = dynamic_cast<Dog*>(ptr);
```

## 3. const_cast
Removes or adds const
```cpp
const int x = 10;

x = 20; //error
```
This variable 'x' cannot be modified.

```cpp
const int x = 10;

const int* ptr = &x;

*ptr = 20; //error
```
ptr points to a const int. Modifying *ptr gives an error because we are trying to modify a const object.

Syntax
```cpp
const_cast<new_type>(expression)
```
Example
```cpp
const int x = 10;

const int* p = &x; //pointer

*p = 20; //error

int* q = const_cast<int*>(p); //remove const qualifier from the pointer type
```
Now 
```cpp
*q
```
This compiles, but it is undefined behaviour because x is originally declared const. We have removed const from the pointer only. It does not make the object writable.

Safe Example
```cpp
int x = 10;

const int* p = &x;

int* q = const_cast<int*>(p);

*q = 20;

cout << x; //output: 20
```
 **USE**:
Interfacing with older APIs that incorrectly take a non-const pointer even though they don't modify the data.

## 4. reinterpret_cast
Tells the compiler
```
"Treat these bits as another type"
```
Example
```cpp
int x = 65;

int* p = &x;

char* c = reinterpret_cast<char*>(p);
```

This converts int pointer to char pointer. No data conversion happens. It is not safe at all.

# Virtual Destructor

## Destructor
A special function that is automatically called when an object is destroyed.

Example
```cpp
class Animal
{
public:
    ~Animal()
    {
        cout << "Animal destroyed\n";
    }
};

int main()
{
Animal a;
}
```
Output 
```
Animal destroyed
```

When main() ends, the object dies, so the destructor runs.

## Virtual Destructor
A virtual destructor is a destructor declared with the virtual keyword in a base class.

### Why do we need it?
If a derived object is deleted using a base class pointer, the base class destructor must be virtual. Otherwise, only the base destructor is called, and the derived destructor is skipped, which can cause resource leaks.

### Without Virtual Destructor
```cpp
#include <iostream>
using namespace std;

class Animal
{
public:
    ~Animal()
    {
        cout << "Animal destroyed\n";
    }
};

class Dog : public Animal
{
public:
    ~Dog()
    {
        cout << "Dog destroyed\n";
    }
};

int main()
{
    Animal* ptr = new Dog();

    delete ptr;
}
```
Output
```
Animal destoryed
```
Dog's destructor is not called.

### With Virtual Destructor
```cpp
#include <iostream>
using namespace std;

class Animal
{
public:
    virtual ~Animal()
    {
        cout << "Animal destroyed\n";
    }
};

class Dog : public Animal
{
public:
    ~Dog()
    {
        cout << "Dog destroyed\n";
    }
};

int main()
{
    Animal* ptr = new Dog();

    delete ptr;
}
```
Output
```
Dog destroyed
Animal destroyed
```

**NOTE**
- virtual enables runtime polymorphism for destructors.
- Without a virtual destructor, deleting a derived object through a base pointer results in undefined behavior.
- With a virtual destructor, the derived destructor executes first, followed by the base destructor.
- Constructors cannot be virtual, but destructors can.

# Rule of Three

For a Class to manage a resource(dynamically allocated memory), we need the following three special functions
1. Destructor
2. Copy Constructor
3. Copy Assignment Operator

## Why?
The compiler performs a **shallow copy** by default.

```cpp
Student s1;
Student s2 = s1;
```

Compiler does:

```cpp
s2.age = s1.age;   // Copies the pointer (address), not the data
```

Result:

- 2 pointers
- 1 heap object

Both objects point to the same memory, so when both destructors call `delete`, it causes **double deletion (undefined behavior).**

## Solution: Deep Copy
Instead of copying the pointer, allocate new memory and copy the value.

```cpp
age = new int(*other.age);
```

Now each object owns its own memory.

## The Three Functions

### 1. Destructor
Frees the owned resource.

```cpp
~Student()
{
    delete age;
}
```

### 2. Copy Constructor
Called when creating a new object from another object.

```cpp
Student(const Student& other)
{
    age = new int(*other.age);
}
```

### 3. Copy Assignment Operator
Called when assigning one existing object to another.

```cpp
Student& operator=(const Student& other)
{
    if (this != &other) //Using '&' gives its address. &oother means address of s1.
    {
        delete age;
        age = new int(*other.age);
    }
    return *this;
}
```
'this' is a special pointer automatically provided by C++. It points to the object that called the function.

Here,
```cpp
s2.operator=(s1)
```
means
```
this---->s2 (same as s2.age)
other---->s1
```

Execution:

1. Check this != &other (avoid self-assignment).
2. Delete s2's old heap memory.
3. Read the value from s1's heap (*other.age).
4. Allocate new heap memory with that value (new int(...)).
5. Make s2.age point to the new memory.
6. Return *this (i.e., s2) so expressions like s3 = s2 = s1; work correctly.

## NOTE

- **Shallow Copy:** Copies the pointer (address).
- **Deep Copy:** Copies the actual data into new memory.
- Use the **Rule of Three** whenever a class directly manages resources (e.g., `new`/`delete`).

> **Destroy → Copy → Assign**
>
> If you implement one, you usually need all three.

# Rule of Five C++
If your class manages a resource (heap memory, file, socket, mutex, etc.) and you define any one of these five special member functions, you should usually define all five.
1. Destructor
2. Copy Constructor
3. Copy Assignment Operator
4. Move Constructor
5. Move Assignment Operator

C++11 introduced move semantics, so two more functions were added.

Before C++11, copying was the only way to transfer objects. But later, we got to move semantics. 

Instead of copying the resource, we cansimply transfer **ownership**.

## Move Constructor
Instead of copying, it steals the resource.

Example
```cpp
Student(Student&& other)
{
    age = other.age;

    other.age = nullptr;
}
```

- Student&&: This is an **rvalue reference**. It means "I am receiving a temporary object whose resources can be taken."

## Move Assignment Operator
Suppose
```cpp
Student s1(10);
Student s2(20);

s2 = std::move(s1);
```
s2 already owns memory, we must first free it.

Implementation
```cpp
Student& operator=(Student&& other)
{
    if(this != &other)
    {
        delete age;

        age = other.age;

        other.age = nullptr;
    }

    return *this;
}
```
Ownership transferred. No copying.

### Complete Example
```cpp
class Student
{
    int* age;

public:

    Student(int a)
    {
        age = new int(a);
    }

    ~Student()
    {
        delete age;
    }

    Student(const Student& other)
    {
        age = new int(*other.age);
    }

    Student& operator=(const Student& other)
    {
        if(this != &other)
        {
            delete age;
            age = new int(*other.age);
        }

        return *this;
    }

    Student(Student&& other)
    {
        age = other.age;
        other.age = nullptr;
    }

    Student& operator=(Student&& other)
    {
        if(this != &other)
        {
            delete age;

            age = other.age;

            other.age = nullptr;
        }

        return *this;
    }
};
```

## std::move()
It simply tells the compiler:

"Treat this object as one whose resources may be moved from."
```cpp
Student s1(20);

Student s2 = std::move(s1);
```
std::move(s1) converts s1 into an rvalue reference, allowing the move constructor to be selected. The actual transfer of ownership happens inside the move constructor, not inside std::move().

## When are these functions called?
- **Creating a new object** → Constructor / Copy Constructor / Move Constructor
- **Assigning to an existing object** → Copy Assignment / Move Assignment

| Code | Function Called |
|------|-----------------|
| `Student s1(20);` | Constructor |
| `Student s2 = s1;` | Copy Constructor |
| `Student s3 = std::move(s1);` | Move Constructor |
| `s2 = s1;` | Copy Assignment Operator |
| `s2 = std::move(s1);` | Move Assignment Operator |

