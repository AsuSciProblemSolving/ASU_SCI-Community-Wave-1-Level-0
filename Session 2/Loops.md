# 🚀 Introduction to Loops

Loops are control structures in programming that allow a block of code to be executed repeatedly based on a condition. This is essential for automating repetitive tasks and writing efficient, readable code.

---

## 🔁 Types of Loops & Syntax

### ➤ `for` Loop

The `for` loop is used when the number of iterations is known beforehand.

**Syntax:**

```cpp
for(initialization; condition; update) {
    // code to execute
}
```

**Example:**

```cpp
for(int i = 1; i <= 5; i++) {
    cout << i << " ";
}
// Output: 1 2 3 4 5
```

---

### ➤ `while` Loop

The `while` loop checks the condition before executing the loop body. It’s used when the number of iterations is not known.

**Syntax:**

```cpp
while(condition) {
    // code to execute
}
```

**Example:**

```cpp
int i = 1;
while(i <= 5) {
    cout << i << " ";
    i++;
}
// Output: 1 2 3 4 5
```

---

### ➤ `do-while` Loop

The `do-while` loop guarantees at least one execution before checking the condition.

**Syntax:**

```cpp
do {
    // code to execute
} while(condition);
```

**Example:**

```cpp
int i = 1;
do {
    cout << i << " ";
    i++;
} while(i <= 5);
// Output: 1 2 3 4 5
```

---

## ⚙️ Loop Control Statements

- **`break`**: Immediately exits the loop.
- **`continue`**: Skips the current iteration and proceeds with the next.

**Example with `break`:**

```cpp
for(int i = 1; i <= 10; i++) {
    if(i == 5) break;
    cout << i << " ";
}
// Output: 1 2 3 4
```

**Example with `continue`:**

```cpp
for(int i = 1; i <= 5; i++) {
    if(i == 3) continue;
    cout << i << " ";
}
// Output: 1 2 4 5
```

---

## 🧮 Variable Scope in Loops

Variables declared inside a loop exist only within that loop. Redeclaring outside will not conflict with loop-scoped variables.

```cpp
for(int i = 0; i < 3; i++) {
    int x = i * 2;
    cout << x << " ";
}
```

---

## 🔂 Nested Loops

A loop inside another loop. Commonly used in matrix problems or pattern printing.

**Example:**

```cpp
for(int i = 1; i <= 3; i++) {
    for(int j = 1; j <= 3; j++) {
        cout << "(" << i << "," << j << ") ";
    }
}
```

🔗 [Practice Problem](https://vjudge.net/problem/Gym-479619I)

---

## ➕ Increment Operators in Loops

### `x++` vs `++x`

- `x++`: Returns current value, then increments.
- `++x`: Increments first, then returns new value.

**Example:**

```cpp
int x = 5;
while(x++ < 7) { // Uses x first, then increments
    cout << x << " ";
}
// Output: 6 7 8

x = 5;
while(++x < 7) { // Increments first, then checks
    cout << x << " ";
}
// Output: 6 7
```

---

## 💻 Loop Challenges

Here are common challenges to strengthen your understanding:

1. **Print numbers from 1 to N**
2. **Sum of even numbers between 1 and N**
3. **Find sum, max, and min from user input**
4. **Factorial of a number**
   ```cpp
   int fact = 1;
   for(int i = 1; i <= n; i++) fact *= i;
   ```
5. **Reverse digits of a number**
6. **Check if a number is prime**
7. **Print numbers divisible by X from 1 to N**
8. **Sum of numbers between A and B**
9. **Palindrome number checker**
10. **Given range [L,R], count (a,b) pairs such that a \* b = K**

---

## 📝 Notes

- Practice different loop patterns to improve your logic-building skills.
- Loop challenges are often used in coding interviews and competitive programming.

---
