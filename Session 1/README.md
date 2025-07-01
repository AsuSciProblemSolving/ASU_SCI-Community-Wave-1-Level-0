# Session 1 (Data Types & Conditions)

# 🚀 Introduction to C++

- **C++**: Performance programming language that supports both procedural and object-oriented paradigms.
- Developed as an extension of the C language.
- Supports low-level memory manipulation for system-level programming.

---

## 🌍 Where C++ is used

- System/software development (OS, device drivers)
- Game development (e.g., Unreal Engine)
- Embedded systems
- Real-time systems
- High-performance apps (databases, finance)
- GUI apps (e.g., Qt framework)

---

## 🛠 Why many languages are implemented using C++

- Performance: Compiled to machine code, very fast.
- Memory control: Fine-grained control.
- Mature ecosystem: Libraries, tools, community.
- Cross-platform: Works across Windows, Linux, macOS.

> Examples:
> - Rust (initial stages) — some compiler parts used to be in C++.
> - Python (CPython): mostly in C, but alternative implementations (IronPython, Jython) use C++ or Java.

---

## ⚙️ Brief history of C++ compilers

1. Started as "C with Classes" by Bjarne Stroustrup.
2. First compiler (Cfront): written in C, transpiled C++ → C.
3. Became self-hosted: compiler written in C++ itself → bootstrapping.
4. Now:
   - GCC: C & C++.
   - Clang/LLVM: mostly C++.
   - MSVC: C++.

> "Like building a house using scaffolding, then living in the house and removing the scaffolding."

---

## 📦 Basic Structure of a C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, world!" << endl;
    return 0;
}
```
## Explain The Structure of a C++ Program

1. ```#include <iostream>```
    - Includes the standard input/output library.
    - Think of it as importing a toolbox with cout, cin.

2. ```using namespace std;```
    - cout and cin live inside the std namespace.
    - Instead of writing std::cout, you can just write cout.

3.  ```int main()```
    - Starting point of every C++ program.
    - Returns an integer to the OS.

4.  ```return 0;```
    - Tells the OS the program ended successfully.
    - success, other numbers = different error codes.


---
## 🗃️ Data Types in C++

In C++, **data types** define the type and size of data that can be stored in a variable.  
Think of variables as boxes, and data types as the labels that say what kind of item each box can hold.



## 📦 Common data types

| Type        | What it stores                       | Example values    |
|------------:|-------------------------------------:|-----------------:|
| `int`      | Whole numbers                        | 5, 100, -7       |
| `float`    | Decimal numbers (single precision)   | 3.14, -0.5       |
| `double`   | Decimal numbers (double precision)   | 3.141592, -0.001 |
| `char`     | Single character                     | 'A', 'z', '0'    |
| `string`   | Sequence of characters (text)        | "Hello", "C++"   |
| `bool`     | Boolean values (true / false)        | true, false      |
| `long long`| Very large whole numbers             | 2e18, -1000000   |

---

## ✏️ Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int age = 21;
    float pi = 3.14f;
    double bigPi = 3.1415926535;
    char initial = 'A';
    string name = "Alice";
    bool isStudent = true;
    long long bigNumber = 123456789012345;

    cout << "Name: " << name << endl;
    cout << "Initial: " << initial << endl;
    cout << "Age: " << age << endl;
    cout << "Pi: " << pi << endl;
    cout << "Big Pi: " << bigPi << endl;
    cout << "Is Student: " << isStudent << endl;
    cout << "Big Number: " << bigNumber << endl;

    return 0;
}

```

# ✅ Conditions in C++ (Summary)

Conditions let your program decide what to do based on data or logic.

Here are the most common types of conditions in C++:

---

## 🧩 1. `if` statement
- Checks a single condition.
- Runs code only if the condition is true.
```cpp
#include <iostream>
using namespace std;
int main() {
    int age = 20;

    if (age >= 18) {
        cout << "You can enter." << endl;
    }

    return 0;
}
```
---

## 🔀 2. `if...else`
- Checks a single condition.
- If true → run one block of code.
- If false → run a different block.
```cpp
#include <iostream>
using namespace std;
int main() {
    int age = 16;

    if (age >= 18) {
        cout << "Welcome!" << endl;
    } else {
        cout << "Sorry, you're too young." << endl;
    }

    return 0;
}
```
---

## 🌱 3. `if...else if...else`
- Checks multiple conditions in order.
- Runs the block for the first condition that is true.
- If none are true → runs the `else` block.
```cpp
#include <iostream>
using namespace std;
int main() {
    int grade = 85;

    if (grade >= 90) {
        cout << "A" << endl;
    } else if (grade >= 80) {
        cout << "B" << endl;
    } else if (grade >= 70) {
        cout << "C" << endl;
    } else {
        cout << "Try harder!" << endl;
    }

    return 0;
}

```
---

## 🧪 4. Nested `if`
- An `if` statement inside another `if` (or inside `else`).
- Lets you add extra checks depending on earlier conditions.
```cpp
#include <iostream>
using namespace std;
int main() {
    int age = 20;
    bool hasTicket = true;

    if (age >= 18) {
        if (hasTicket) {
            cout << "You can enter the event." << endl;
        } else {
            cout << "You need a ticket to enter." << endl;
        }
    } else {
        cout << "You are too young." << endl;
    }

    return 0;
}
```
---

## ✏️ 5. Ternary operator (shorthand condition)
- Quick one-line way to choose between two values.
- Syntax: `condition ? value_if_true : value_if_false;`
```cpp
#include <iostream>
using namespace std;
int main() {
    int age = 20;
    string status = (age >= 18) ? "Adult" : "Minor";

    cout << "Status: " << status << endl;

    return 0;
}
```
---

## 📝 Summary
- Use `if` for simple checks.
- Use `if...else` for either/or logic.
- Use `if...else if...else` for multiple choices.
- Use nested `if` for complex, multi-level decisions.
- Use the ternary operator for simple, single-variable decisions in one line.

> 💡 Conditions make your programs dynamic and responsive to data!



---
## ⚠️ Common Problems Beginners Face in C++

Even experienced developers sometimes fall into these traps!  
Here’s a list of common mistakes beginners often make in C++ — explained with examples and tips to avoid them.


## Overflow & Underflow

When numbers go beyond the limits of their data type.

### 🔧 1) Integer Overflow

```cpp
#include <iostream>
#include <limits>
using namespace std;

int main() {
    int a = INT_MAX; // largest possible int: 2147483647
    int b = 1;
    int sum = a + b;

    cout << "a: " << a << endl;
    cout << "b: " << b << endl;
    cout << "a + b: " << sum << endl; // unexpected negative value!
    return 0;
}
```

### 🔧 2) Integer Underflow

``` cpp
#include <iostream>
#include <limits>
using namespace std;

int main() {
    int a = INT_MIN; // smallest value an int can hold
    int b = 1;
    int result = a - b;

    cout << "a: " << a << endl;
    cout << "b: " << b << endl;
    cout << "a - b: " << result << endl; // unexpected result
    return 0;
}
```

#### Tips to avoid overflow/underflow:
 - Use long long or unsigned if you expect very large numbers.

- Think carefully before doing operations near type limits.

- For critical applications, use libraries like BigInteger.

---
### 🔧3) Forgetting to initialize variables 
``` cpp
int x;
cout << x << endl; // prints garbage value!
```

#### Tip to avoid it 
 - Always initialize variables, e.g., int x = 0;.
---

### 🧠 4) Using = instead of == in conditions

``` cpp
int age = 18;
if (age = 21) { // wrong! assigns 21 to age
    cout << "You are 21!" << endl;
}
```

---

## 📚 Resources to Learn More

### 📖 Official & Reference
- [C++ Reference (cppreference.com)](https://en.cppreference.com/)
- [ISO C++ official website](https://isocpp.org/)

### 🎓 Free Tutorials
- [GeeksforGeeks – C++ Programming Language](https://www.geeksforgeeks.org/c-plus-plus/) – explanations, articles, and problems.
- [LearnCpp.com](https://www.learncpp.com/) – very beginner-friendly, step-by-step.
- [C++ Tutorial on Programiz](https://www.programiz.com/cpp-programming)
- [Codecademy: Learn C++ (free parts)](https://www.codecademy.com/learn/learn-c-plus-plus)

### 🎥 YouTube Playlists
- [C++ Programming for Beginners (freeCodeCamp)](https://www.youtube.com/watch?v=vLnPwxZdW4Y)

---
