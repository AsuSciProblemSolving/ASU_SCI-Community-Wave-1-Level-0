# Algorithm Complexity Analysis Guide (C++ Examples)

_Reference: [A Gentle Introduction to Algorithm Complexity Analysis](https://discrete.gr/complexity/)_

## Table of Contents

1. Introduction
2. Asymptotic Behavior
3. Big O Notation
4. Big Theta Notation
5. Average Case Analysis
6. Comparing Functions with Limits
7. Recurrence Relations
8. Methods for Solving Recurrences
## Introduction

**Problem solving** in computer science is fundamentally about _pattern recognition_: identifying recurring structures, behaviors, or computational patterns in problems. Complexity analysis provides a formal language to compare, classify, and reason about the efficiency of different solutions — especially as input sizes grow.

---

## Asymptotic Behavior

Analyzing an algorithm's performance as input size grows large gives us critical insight into its scalability. This is called studying the **asymptotic behavior** of the algorithm.

-> what we are interest in is the **Tail behavior"**

### Why Do We Drop Constants? "Addressing behavior"

- because we are concerned with the rate of growth and how the algorithm will behave on large input sizes.
- Constants reflect micro-level differences, like hardware or language quirks, which are dwarfed by input size for large `n`
- Example: If an algorithm takes `6n + 4` steps, for sufficiently large `n`, the 4 becomes negligible, simplifying to `Θ(n)`

### Why Do We Drop Lower-Order Terms?

- When multiple terms exist (e.g., `n³ + 10n² + 25n`), the term with the highest degree dominates for large inputs
- This allows us to ignore lesser terms: `n³ + 10n² + 25n` becomes `Θ(n³)`

---

## Big O Notation (O(g(n)))

**Big O** provides an **upper bound** on the growth rate of an algorithm's runtime or space usage.
![[Pasted image 20250816223739.png]]
```c++
// 5

int a[n];
for (int i =0; i<n; i++) {
	cin >> a[i];
}

for (int i =0; i<n; i++) {
	for(int j=0; j<n; j++) {
		a[i] += 5;
	}
}


runtinme = O(n^2)
```

### Key Properties

- **Upper Bound:** The algorithm will not be slower than this, for large `n`
- **Worst-Case:** Unless specified, Big O typically refers to the worst-case scenario

### Loose vs. Tight Upper Bounds

#### Loose Upper Bound

A bound that is not tight; e.g., saying linear search is `O(n²)` is correct but not useful, as it's actually `O(n)`.

#### Tight Upper Bound

The smallest possible function class that accurately bounds the runtime from above. For linear search, the tight bound is `O(n)`.

### C++ Example: Linear Search - O(n)

```cpp
bool exists(const vector<int>& A, int value) {
    for (int i = 0; i < A.size(); ++i) {
        if (A[i] == value) return true;
    }
    return false;
}
```

**Analysis:** In the worst case (when the value doesn't exist), every element is checked — `O(n)`.

---

## Big Theta Notation (Θ(g(n)))

**Big Theta** gives a _tight bound_ — both upper and lower — meaning the algorithm always takes this order of time.

### C++ Example: Constant Time - Θ(1)

```cpp
int add_first_two(const vector<int>& a) {
    return a[0] + a[1];
}
```

**Analysis:** Regardless of input size, only a fixed number of steps are executed.

---

## Average Case Analysis

The average case considers _expected_ runtime, usually assuming a probabilistic distribution over possible inputs. This is important when worst-case performance is rare but analyzing it is essential for understanding real-world efficiency.

### When to Use Average Case

- When worst-case scenarios are unlikely in practice
- When input has known probabilistic properties
- When making practical performance predictions

---

## Comparing Functions with Limits


To determine which function grows faster, compute:

```
lim (n→∞) f(n)/g(n)
```

### Interpretation

- **Limit = 0:** `f(n)` grows slower than `g(n)`
- **Limit = constant:** They grow at the same rate
- **Limit = ∞:** `f(n)` grows faster than `g(n)`

### Example

Compare `f(n) = n` and `g(n) = n²`:

```
lim (n→∞) n^2/n = lim (n→∞) n/1 = ∞;
```

Therefore, `n` grows slower than `n²`.

---

## Recurrence Relations

Many divide-and-conquer and recursive algorithms have runtimes described by **recurrence relations**: equations that define a function in terms of itself with smaller inputs.

### What Does "Solving a Recurrence" Mean?

- Finding a closed-form (non-recursive) expression for the function
- This allows us to determine the asymptotic runtime

### Classic Example: Merge Sort

```
T(n) = 2T(n/2) + cn
```

**Solution:** `T(n) = O(n log n)`

---

## Methods for Solving Recurrences

### 1. Master Theorem

For recurrences of the form `T(n) = aT(n/b) + f(n)`:

- Compare `f(n)` with `n^(log_b(a))`
- Apply one of three cases to determine the solution

### 2. Recursion Tree Method

- Draw the sequence of recursive calls as a tree
- Compute the work done at each level
- Sum over all levels to get total work
- Visualizes how work splits and accumulates

### 3. Substitution Method

- Guess the solution based on pattern recognition
- Prove the guess using mathematical induction

#### Example: Substitution Method

Given `T(n) = 2T(n/2) + n`, guess `T(n) ≤ cn log n`:

**Base case:** Verify for small values of `n`

**Inductive step:**

```
T(n) = 2T(n/2) + n
     ≤ 2c(n/2)log(n/2) + n
     = cn(log n - log 2) + n
     = cn log n - cn + n
     ≤ cn log n  (for c ≥ 1)
```

---

## Common Complexity Classes

| Notation   | Name         | Example             |
| ---------- | ------------ | ------------------- |
| O(1)       | Constant     | Array access        |
| O(log n)   | Logarithmic  | Binary search       |
| O(n)       | Linear       | Linear search       |
| O(n log n) | Linearithmic | Merge sort          |
| O(n²)      | Quadratic    | Bubble sort         |
| O(2ⁿ)      | Exponential  | Recursive Fibonacci |

---

## Conclusion

### Key Takeaways

- **Constants and lower-order terms** are dropped to focus on meaningful long-term efficiency
- **Big O** provides an upper bound, while **Big Theta** gives a tight bound
- **Limits** help compare growth rates of different functions
- **Recurrence relations** are essential for analyzing recursive algorithms
- **Master theorem, recursion tree, and substitution** are standard tools for solving recurrences

### Best Practices

1. Always consider the worst-case scenario unless specified otherwise
2. Use the tightest bounds possible for meaningful analysis
3. Understand the practical implications of theoretical bounds
4. Consider average-case analysis for real-world performance prediction

---

For more details and tutorial walkthroughs, see [A Gentle Introduction to Algorithm Complexity Analysis](https://discrete.gr/complexity/)_
