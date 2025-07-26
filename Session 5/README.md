# 🧠 Recursion – Agenda

### 📌 1. What is Recursion & Why Use It?
- **What**: A function solving a problem by calling itself with smaller inputs.
- **Why**: Elegant for problems with recursive structure (e.g., trees, fractals).
- **Loop vs. Recursion**: Loops iterate; recursion divides and conquers.

### 📚 2. Call Stack & Stack Memory
- Visualize how the **call stack** tracks function calls.
- Understand stack frames: parameters, variables, return addresses.
- Recursion tree and stack trace examples for clarity.

### 🔁 3. Single-Way Recursion
- Print `"Hello, Recursion"` N times.
- Print numbers: 1 to N vs. N to 1.
- Classic problems:
  - Factorial
  - Sum of first N numbers
- Practice problems:
  - 🧱 **Pyramid Problem** ([Codeforces G](https://codeforces.com/group/MWSDmqGsZm/contest/223339/problem/G))
  - 🔢 **Print Digits** ([Codeforces D](https://codeforces.com/group/MWSDmqGsZm/contest/223339/problem/D))

### 🔀 4. Multi-Way Recursion
- **Paths Problem**: Count ways to reach N by adding 1 or 2 at each step.
- 🌀 **Fibonacci Series**: Recursive computation and its challenges.
- Practice problems
  - 🌳 **B. Tavas and SaDDas** ([Codeforces Round 299 (Div. 2)](https://codeforces.com/problemset/problem/535/B))

### 🧩 5. Practice & Debugging
- Master base cases and recursive cases.
- Avoid pitfalls: stack overflow, missing base cases.
- Live problem-solving and recursion tracing tips.

---

## 📚 What is a Stack?

A **stack** is a **Last-In-First-Out (LIFO)** data structure, like a stack of plates: you add (push) to the top and remove (pop) from the top. In C++, the **call stack** manages function calls by storing **stack frames** containing:
- Function parameters
- Local variables
- Return address (where to resume after the function ends)

### Key Operations
- **Push**: Adds a stack frame at a **lower memory address** (stack grows downward).
- **Pop**: Removes the top frame, returning control to the caller.

### Stack in Action
Consider this C++ program:

```cpp
#include <iostream>
using namespace std;

void say_bye() {
    cout << "Goodbye!" << endl;
}

void greet() {
    cout << "Hello!" << endl;
    say_bye();
}

int main() {
    greet();
    return 0;
}
```

#### Stack Visualization
The stack grows **downward** (lower memory addresses). Each frame is labeled with `[top]` for the current frame.

1. **main() Called**
```
+----------------------+
| main()             | [top] (0x1000)
+----------------------+
```

2. **main() Calls greet()**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| greet()            | [top] (0x0FF0)
+----------------------+
```

3. **greet() Calls say_bye()**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| greet()            | (0x0FF0)
+----------------------+
| say_bye()          | [top] (0x0FE0)
+----------------------+
```

4. **say_bye() Completes, Pops**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| greet()            | [top] (0x0FF0)
+----------------------+
```

5. **greet() Completes, Pops**
```
+----------------------+
| main()             | [top] (0x1000)
+----------------------+
```

6. **main() Completes, Stack Empty**
```
+----------------------+
| [empty]            |
+----------------------+
```

### Key Notes
- The stack is managed by the C++ runtime.
- **Stack overflow**: Too many frames (e.g., deep recursion) crash the program.
- Stack grows **downward** in most systems.

---

## 🔄 Recursion in C++: A Deep Dive

**Recursion** is when a function calls itself to solve a smaller version of the problem. It needs:
1. **Base Case**: Stops recursion to prevent infinite calls.
2. **Recursive Case**: Calls the function with modified inputs.

Each recursive call adds a stack frame. The stack grows until the base case is reached, then **unwinds** as frames pop, resolving the computation.

### Example 1: Factorial
Compute \( n! = n \times (n-1) \times \dots \times 1 \). Example: \( 5! = 120 \).

#### Code
```cpp
#include <iostream>
using namespace std;

unsigned long long factorial(int n) {
    if (n < 0) return 0; // Edge case
    if (n == 0 || n == 1) return 1; // Base case
    return n * factorial(n - 1); // Recursive case
}

int main() {
    int n = 5;
    cout << "Factorial of " << n << ": " << factorial(n) << endl;
    return 0;
}
```

#### Recursion Tree
```
factorial(5)
├── 5 * factorial(4)
│   ├── 4 * factorial(3)
│   │   ├── 3 * factorial(2)
│   │   │   ├── 2 * factorial(1)
│   │   │   │   └── 1 (base case)
│   │   │   └── 2
│   │   └── 6
│   └── 24
└── 120
```

#### Stack Visualization
1. **factorial(5) Pushed**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| factorial(5)       | [top] (0x0FF0)
+----------------------+
```

2. **Down to factorial(1)**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| factorial(5)       | (0x0FF0)
+----------------------+
| factorial(4)       | (0x0FE0)
+----------------------+
| factorial(3)       | (0x0FD0)
+----------------------+
| factorial(2)       | (0x0FC0)
+----------------------+
| factorial(1)       | [top] (0x0FB0)
+----------------------+
```

3. **Unwinding (factorial(1) Returns 1)**
- Pops frames, computes: \( 2 \times 1 = 2 \), \( 3 \times 2 = 6 \), \( 4 \times 6 = 24 \), \( 5 \times 24 = 120 \).
- Final stack:
```
+----------------------+
| main()             | [top] (0x1000)
+----------------------+
```

### Example 2: Fibonacci
Fibonacci: \( F(n) = F(n-1) + F(n-2) \), with \( F(0) = 0 \), \( F(1) = 1 \). Example: \( F(5) = 5 \).

#### Code
```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n < 0) return 0; // Edge case
    if (n <= 1) return n; // Base case
    return fibonacci(n - 1) + fibonacci(n - 2); // Recursive case
}

int main() {
    int n = 5;
    cout << "Fibonacci(" << n << "): " << fibonacci(n) << endl;
    return 0;
}
```

#### Recursion Tree (Simplified)
```
fibonacci(5)
├── fibonacci(4)
│   ├── fibonacci(3)
│   │   ├── fibonacci(2)
│   │   │   ├── fibonacci(1) → 1
│   │   │   ├── fibonacci(0) → 0
│   │   │   └── 1
│   │   ├── fibonacci(1) → 1
│   │   └── 2
│   ├── fibonacci(2)
│   │   ├── fibonacci(1) → 1
│   │   ├── fibonacci(0) → 0
│   │   └── 1
│   └── 3
├── fibonacci(3)
│   ├── fibonacci(2)
│   │   ├── fibonacci(1) → 1
│   │   ├── fibonacci(0) → 0
│   │   └── 1
│   ├── fibonacci(1) → 1
│   └── 2
└── 5
```

#### Stack Visualization (Left Branch)
1. **fibonacci(5) to fibonacci(2)**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| fibonacci(5)       | (0x0FF0)
+----------------------+
| fibonacci(4)       | (0x0FE0)
+----------------------+
| fibonacci(3)       | (0x0FD0)
+----------------------+
| fibonacci(2)       | [top] (0x0FC0)
+----------------------+
```

2. **Base Cases and Unwinding**
- `fibonacci(2)` calls `fibonacci(1)` (returns 1) and `fibonacci(0)` (returns 0), computes \( 1 + 0 = 1 \).
- Stack unwinds, resolving up to \( F(5) = 3 + 2 = 5 \).

### Example 3: Print 1 to N
Print numbers from 1 to N recursively.

#### Code
```cpp
#include <iostream>
using namespace std;

void print_1_to_n(int n) {
    if (n < 1) return; // Edge case
    print_1_to_n(n - 1); // Recursive case
    cout << n << " "; // Print after recursion (ascending)
}

int main() {
    int n = 5;
    print_1_to_n(n); // Outputs: 1 2 3 4 5
    cout << endl;
    return 0;
}
```

#### Why It Works
- Recursive calls go to `n-1`, hitting base case (`n < 1`).
- Prints occur during unwinding, giving 1 to N order.

#### Stack Visualization
For `n = 3`:
1. **Push to print_1_to_n(1)**
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| print_1_to_n(3)    | (0x0FF0)
+----------------------+
| print_1_to_n(2)    | (0x0FE0)
+----------------------+
| print_1_to_n(1)    | [top] (0x0FD0)
+----------------------+
```

2. **Unwinding**
- `print_1_to_n(1)` prints 1, pops.
- `print_1_to_n(2)` prints 2, pops.
- `print_1_to_n(3)` prints 3, pops.
- Output: `1 2 3`.

---

## ⚠️ Stack Overflow: The Dark Side of Recursion

A **stack overflow** occurs when the call stack runs out of memory due to excessive frames.

### Causes
1. **Missing Base Case**:
```cpp
void bad_recursion(int n) {
    bad_recursion(n + 1); // Infinite recursion
}
```
- Stack grows forever:
```
+----------------------+
| main()             | (0x1000)
+----------------------+
| bad_recursion(1)   | (0x0FF0)
+----------------------+
| bad_recursion(2)   | (0x0FE0)
+----------------------+
| ...                | [top]
+----------------------+
```

2. **Deep Recursion**: Large inputs (e.g., `fibonacci(50)`) create too many frames.

### Prevention
- **Define Base Cases**: Ensure recursion stops (e.g., `n <= 1` for Fibonacci).
- **Tail Recursion**: Place recursive calls as the last operation (C++ may not optimize, but it’s good practice).
  ```cpp
  unsigned long long factorial_tail(int n, unsigned long long acc = 1) {
      if (n <= 1) return acc;
      return factorial_tail(n - 1, n * acc);
  }
  ```
- **Iterative Alternatives**: Use loops for large inputs.
- **Increase Stack Size** (rare): Compiler-specific, e.g., `-fstack-limit` (not portable).
- **Memoization**: Cache results for multi-way recursion (e.g., Fibonacci):
  ```cpp
  #include <iostream>
  #include <vector>
  using namespace std;

  vector<long long> memo(100, -1); // Initialize with -1

  long long fibonacci_memo(int n) {
      if (n < 0) return 0;
      if (n <= 1) return n;
      if (memo[n] != -1) return memo[n];
      memo[n] = fibonacci_memo(n - 1) + fibonacci_memo(n - 2);
      return memo[n];
  }

  int main() {
      cout << "Fibonacci(10): " << fibonacci_memo(10) << endl; // Outputs 55
      return 0;
  }
  ```

---

## 🛠️ Debugging Recursion

1. **Trace with Print Statements**:
   - Add `cout` to log function calls and parameters.
   ```cpp
   void print_1_to_n(int n) {
       cout << "Entering n=" << n << endl;
       if (n < 1) return;
       print_1_to_n(n - 1);
       cout << "Printing n=" << n << endl;
   }
   ```

2. **Use Visualizers**:
   - [Python Tutor](https://pythontutor.com/) supports C++: Step through code to see stack frames.
   - [C++ Insight](https://cppinsights.io/) for understanding compiler transformations.

3. **Check Base Cases**:
   - Ensure all paths hit a base case.
   - Test edge cases (e.g., `n = 0`, negative inputs).

4. **Monitor Stack Depth**:
   - For large inputs, estimate stack size (each frame ~1-10 KB).
   - Switch to iterative solutions if depth exceeds ~1000 frames.

---

## 🧩 Practice Problems

1. **New Problem: Sum of Digits**
   - Compute the sum of digits of a number recursively.
   ```cpp
   #include <iostream>
   using namespace std;

   int sum_digits(int n) {
       if (n < 10) return n; // Base case: single digit
       return (n % 10) + sum_digits(n / 10); // Recursive case
   }

   int main() {
       int n = 123;
       cout << "Sum of digits of " << n << ": " << sum_digits(n) << endl; // Outputs 6
       return 0;
   }
   ```

---

## 📚 Resources
- **Articles**:
  - [GeeksforGeeks: Recursion](https://www.geeksforgeeks.org/introduction-to-recursion-data-structure-and-algorithm-tutorials/)
  - [GeeksforGeeks: Stack Data Structure](https://www.geeksforgeeks.org/stack-data-structure/)
  - [Programiz: C++ Recursion](https://www.programiz.com/cpp-programming/recursion)
- **Visualizers**:
  - [Python Tutor](https://pythontutor.com/) (C++ supported)
  - [VisuAlgo](https://visualgo.net/en/recursion) (general recursion concepts)
- **Books**:
  - "Introduction to Algorithms" by Cormen et al. (Chapter on Recursion)
  - "C++ Programming Language" by Stroustrup (for advanced insights)
---

## 🎯 Key Takeaways
- **Stack**: LIFO structure managing function calls via push/pop.
- **Recursion**: Solves problems by breaking them into smaller subproblems.
- **Base Case**: Critical to stop recursion and prevent stack overflow.
- **Optimization**: Use memoization or iteration for efficiency.
- **Debugging**: Trace with prints or visualizers to understand stack behavior.

Start coding, trace the stack, and conquer recursion! 🚀
