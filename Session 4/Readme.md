

## 4.1.1. Function Fundamentals  
  
A function is a reusable block of code that performs a specific task.   
### a) Basic Syntax  
  
The basic syntax of a C++ function is:  
  
```C++  
void print(int x){
	cout << "HELLO";
}

int print(int x) {
	return x;
}
```  
### b) Function Type vs. Signature  
  
Functions have both a type and a signature, and it's important to know the difference.  
  
- Function Type: Defined by the return type and the parameter list. The name is not part of the type.  
  
  - For `int add(int a, int b);`  
      - the type is `int(int, int)`.  
      - This describes a function that takes two `int`s and returns an `int`.  
  
- Function Signature: Defined by the function name and the parameter list.  
  - In C++, the return type is not part of the signature.   
- The signature is what the compiler uses to distinguish between **overloaded** functions.  
  
  - `void print(int);` and `void print(double);` have _different signatures_ (`print(int)` vs. `print(double)`).  
  
  - `void print(int);` and `char print(int);` have the **same signature** and will cause a compiler error.  
  
  
### c) The Role of `void`  
  
`void` is a type specifier, not a signature itself. It means "nothing" or "no type"  
- As a return type, it means the function returns no value.  
---  
  
## 4.1.2. Passing Parameters  
How you pass data to a function is one of the most important performance considerations in C++.  
  
### a) Pass by Value  
  
- A copy of the argument is made. - Changes inside the function do not affect the original.  
  
```C++  

void add(const int& A[], int size) { 

}  

int main() {  
    int a = 10; // aaa1
    add(a);
    // 'a' is STILL 10 here!
}  
```  
  
### b) Pass by Reference (`&`)  
  
- The function receives a direct alias to the original variable.  
- No copy is made, so changes **do** affect the original.  
  
```C++  

void add(int &x) { // x is an alias for 'a'  
    x++;
}  

int main() {  
    int a = 10;
    add(a);
    cout << a; // 11
}  
```  

  ![[Pasted image 20250717101240.png]]
  
- **CP Tip:**  
  - Use when you need to **modify** the original argument or to **avoid copying** a large data structure.  
  
What if I do not want to edit the value of the original variale,  
and also do not want to consume a redundunt memory?  



### c) Pass by `const` Reference (`const &`)  
  
This is the best of both worlds: no copy is made, but the function is forbidden from modifying the original variable.  
  
```C++  
long long sum(int size, const int& arr[]) {  
    // arr[0]++;
    // COMPILE ERROR! Cannot modify a const reference.
    
    long long total = 0;  
    for (int &x : arr) {        
	    total += x;
	}    
	 
	return total;  
}  
```  
  
// Note  
// this is another way to write a for loop  
// it's called range-based for loop (for-each loop).  
  
```C++  
for (declaration : range) {  
// loop body  
}  
```  
- range: The container you want to iterate over (in your case, the array arr).  
- declaration: Declares a variable that will hold a copy of each element from the range, one at a time, for each iteration of the loop.  
- to avoid making copy for each element use the reference symbol '&'  
  
- 💡 CP Golden Rule:  
  - Always pass large objects (`string`, `vector`, `map`, `set`, custom structs) by `const` reference** if you do not need to modify them. This gives you high performance with safety.  
  
  
---  

### d) Default argument
![[cpp-default-parameters.png]]

## 4.1.3 Tips, Tricks.  
  
### Helper Functions are Your Best Friend  
Don't write monolithic code in the`main` funtcion. 
Instead. Break logic into small, testable helper functions. It makes debugging 10x easier.  
  
### Use `inline` for Tiny Functions  
  
For very short, frequently called functions, `inline` is used to suggest that the compiler eliminate the overhead of calling a small function by pasting its code directly into the call site.  
  
  
```C++  
inline int max(int a, int b) {  
    return a > b ? a : b;
}  
  
int x = 10, y = 20;  
int biggest = max(x, y); // Function call  
  
int x = 10, y = 20;  
// The call to max(x, y) is replaced by the function's body  
int biggest = (x > y ? x : y);  
  
```  
  
  
### Avoid Function-like Macros  
Never use `#define` to create function-like macros. They perform blind text substitution and are a famous source of bugs.  
  
```C++  
// BAD - Don't do this!  
#define SQR(x) x * x  
  
// SQR(a + b) becomes a + b * a + b, which is WRONG!  
  
// GOOD - Use an inline function  
template<typename T>  
inline T sqr(T x) {  
    return x * x;
}  
```  
  
# Pointers  in C++ 

## 4.2.1. The Core Concept
  
A **pointer** is simply a variable that stores the **memory address** of another variable.  

### Key Operators  
  
1.  **Declaration (`*`)**: Declares a pointer variable.  
    `int* ptr;`
2.  **Address-of (`&`)**: Gets the memory address of a variable.  
    `ptr = &my_variable;`
3.  **De-reference (`*`)**: Accesses the value stored at the memory address the pointer is holding.  
    `cout << *ptr;`  
### Basic Example  
  
```js  
#include <iostream>  
  
int main() {  
    int score = 95;      // A regular integer variable.    
    int* score_ptr;      // A pointer that can hold the address of an integer.  
    score_ptr = &score;  // Store the memory address of 'score' in 'score_ptr'.  
    // Print the addresses and values
    std::cout << "Value of score: " << score << std::endl;
    // Prints the address
    std::cout << "Address of score (&score): " << &score << std::endl;
    std::cout << "Value of score_ptr: " << score_ptr << std::endl;
    
    // Use the dereference operator (*) to get the value at the address  
    std::cout << "Value at score_ptr (*score_ptr): " << *score_ptr << std::endl;  
    // We can also modify the original variable through the pointer
	*score_ptr = 100
	std::cout << "New value of score: " << score << std::endl; // Prints 100  
    return 0;
}  
````  
  
-----  
  
## 4.2.2. Pointers and Arrays  
  
This is a fundamental relationship in C++. The name of an array acts as a pointer to its first element.  
  
```cpp  
int arr[5] = {10, 20, 30, 40, 50};  
  
// Both lines below point to the first element (10)  
int* ptr = arr;  
int* ptr2 = &arr[0];  
```  
  
You can use **pointer arithmetic** to navigate the array. This is often faster than index-based access.  
  
```cpp  
#include <iostream>  
  
int main() {  
    int arr[5] = {10, 20, 30, 40, 50};    
    int* ptr = arr;  
    // Iterate through the array using pointer arithmetic
        for (int i = 0; i < 5; ++i) {
        // *(ptr + i) is equivalent to arr[i]
        std::cout << "Value: " << *(ptr + i) << std::endl;
        }
    return 0;
}
```  
  
**CP Tip 🚀:** Using pointers to iterate over arrays can be slightly more performant in tight loops, as it can be closer to how the machine accesses memory.  
  
-----  
  
## 4.2.3. Dynamic Memory Allocation (`new` and `delete`)  
  
Sometimes you don't know the size of an array or object at compile time. Dynamic memory allocation lets you request memory from the operating system on the **heap** at runtime.  
  
* `new`: Allocates memory.  
* `delete`: De-allocates memory to prevent **memory leaks**.  
  
### Single Variable  

```cpp  
// Allocate an integer on the heap  
int* p = new int;  
*p = 25;  
  

delete p;  
p = nullptr; // Good practice to nullify the pointer after deleting  
```  
  
### Arrays  
  
Allocating and de-allocating arrays has a special syntax (`delete[]`).  
  
```cpp  
int size;  
std::cout << "Enter array size: ";  
std::cin >> size;  
  
// Allocate an array of 'size' integers on the heap  
int* my_array = new int[size];  
  
// ... use the array ...  
my_array[0] = 5;  
  
// CRUCIAL: Use delete[] for arrays  
delete[] my_array;  
my_array = nullptr;
```
  
  **Warning:** Forgetting `delete` or using `delete` instead of `delete[]` are common and serious bugs.  
  
-----  
  
## 4.2.4. Key Use Cases  
  
### a) Passing Pointers to Functions  
  
This allows a function to modify the original data. It's an alternative to pass-by-reference.  
  
```cpp  
void triple(int* num) {  
    if (num != nullptr) { // Always check for nullptr!
        *num = *num * 3;
    }
}  
  
int main() {  
    int val = 10;
    triple(&val); // Pass the address of val
    // val is now 30
    std::cout << val << std::endl;
    return 0;
}  
```  
  
### b) Data Structures (additional)  
  
Pointers are the backbone of nearly all complex data structures. They link individual nodes together.  
  
```cpp  
// A node for a Linked List or a Binary Tree  
struct Node {  
    int data;
    Node* next; // Pointer to the next node in the list
};  
```  
  
### c) Common Pitfalls to Avoid  
  
1.  **Null Pointer De-reference**: Accessing a pointer that is `nullptr`. This causes a crash. **Always check if a pointer is `nullptr` before using it.**  
2.  **Dangling Pointers**: A pointer that holds the address of memory that has already been deallocated (`delete`d). Using it leads to undefined behavior.  
3.  **Memory Leaks**: Forgetting to `delete` memory allocated with `new`. The program loses the ability to access that memory, but it remains allocated until the program terminates.  
  
In short, pointers offer great power at the cost of greater responsibility. Use them for performance-critical code and for building custom data structures.  



# We need to talk about the Memory 
## The Stack 🥞

Think of the stack as an organized group of books one above the other. It follows a strict **Last-In, First-Out (LIFO)** rule.

- **What it's for:** Storing **local variables** (variables declared inside functions), function parameters, and managing the sequence of function calls.
    
- **How it works:** When you call a function, a block of memory (a "stack frame") is pushed onto the top of the stack for its local variables. When the function returns, its frame is automatically popped off, and all its variables are destroyed.
    
- **Key Features:**
    
    - **Automatic:** Memory management is handled for you. You don't use `new` or `delete`.
        
    - **Fast:** Pushing and popping from the stack is extremely fast.
        
    - **Limited Size:** The stack is relatively small. If you have too many nested function calls (deep recursion) or declare a massive local array, you'll get a **stack overflow** error.
        

```C++
void myFunction() {
    int y = 20; // 'y' is created on the stack when myFunction is called.
    // When this function ends, 'y' is automatically destroyed.
}

int main() {
    int x = 10; // 'x' is created on the main() stack frame.
    myFunction();
    // At this point, 'y' no longer exists.
    return 0;
}
```

---

## The Heap 📦

Think of the heap as a large, open warehouse of memory. You can request chunks of any size, but you are responsible for tracking them and cleaning up afterward.

- **What it's for:** **Dynamic memory allocation**. This is for data whose size isn't known at compile time or whose lifetime must extend beyond the function that created it. You access this memory using pointers.
    
- **How it works:** You explicitly request memory using the `new` keyword. The system finds a free block in the heap and returns a pointer to it. You **must** return this memory using the `delete` keyword.
    
- **Key Features:**
    
    - **Manual:** You are in full control of allocation (`new`) and de-allocation (`delete`).
        
    - **Slower:** Allocation can be slower because the system needs to find a suitable block of memory.
        
    - **Large Size:** The heap is much larger than the stack, so it's perfect for large objects or data structures.
        
    - **Responsibility:** Forgetting to `delete` memory causes a **memory leak**, where the memory remains reserved but inaccessible until the program ends.
        


```C++
void createItem() {
    // Request an integer from the heap. 'p' is a local pointer on the stack.
    int* p = new int;
    *p = 50;
    // ...
    // If we don't 'delete p' here, the memory for the integer 50 is leaked
    // when the function ends and the pointer 'p' is destroyed.
    delete p; // We must manually free the memory. 🗑️
}
```

---

## Stack vs. Heap: Summary

| Feature          | Stack                                 | Heap                                       |
| ---------------- | ------------------------------------- | ------------------------------------------ |
| **Lifecycle**    | Automatic (managed by function scope) | Manual (managed by `new` and `delete`)     |
| **Speed**        | Very Fast                             | Slower                                     |
| **Size**         | Small and fixed                       | Large and flexible                         |
| **Used For**     | Local variables, function calls       | Dynamic objects, shared data, large arrays |
| **Accessed Via** | Variable name directly                | Pointers                                   |
|                  |                                       |                                            |