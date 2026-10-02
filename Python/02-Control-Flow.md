# 02 - Control Flow in Python

> **Control flow** decides *which* lines of code run, *how many times* they run, and *in what order*.
> Without it, a program just runs top to bottom, one line after another.

---

## Table of Contents

1. [Indentation Rules](#1-indentation-rules)
2. [Conditional Statements](#2-conditional-statements)
3. [Comparison and Logical Operators](#3-comparison-and-logical-operators)
4. [Truthy and Falsy Values](#4-truthy-and-falsy-values)
5. [Ternary (Conditional) Expression](#5-ternary-conditional-expression)
6. [match-case (Python 3.10+)](#6-match-case-python-310)
7. [Loops](#7-loops)
8. [Loop Control Statements](#8-loop-control-statements)
9. [Loop `else` Clause](#9-loop-else-clause)
10. [Nested Loops](#10-nested-loops)
11. [Useful Loop Helpers](#11-useful-loop-helpers)
12. [Common Mistakes](#12-common-mistakes)
13. [Practice Problems](#13-practice-problems)
14. [Quick Cheat Sheet](#14-quick-cheat-sheet)

---

## 1. Indentation Rules

Python uses **indentation** (not curly braces) to define a block of code.

```python
if True:
    print("Inside the block")   # indented = belongs to the if
print("Outside the block")      # not indented = outside
```

- Standard is **4 spaces** per level (PEP 8).
- Do not mix tabs and spaces.
- A block starts after a colon `:`.
- Wrong indentation raises `IndentationError`.

---

## 2. Conditional Statements

### 2.1 `if`

Runs a block only when the condition is `True`.

```python
age = 20
if age >= 18:
    print("You are an adult")
```

### 2.2 `if - else`

```python
num = 7
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### 2.3 `if - elif - else`

Checks conditions **in order**; the first `True` one runs and the rest are skipped.

```python
marks = 82

if marks >= 90:
    grade = "A+"
elif marks >= 80:
    grade = "A"
elif marks >= 70:
    grade = "B"
elif marks >= 60:
    grade = "C"
else:
    grade = "F"

print(grade)   # A
```

### 2.4 Nested `if`

An `if` inside another `if`.

```python
age = 25
has_id = True

if age >= 18:
    if has_id:
        print("Entry allowed")
    else:
        print("ID required")
else:
    print("Underage")
```

Often cleaner with a logical operator:

```python
if age >= 18 and has_id:
    print("Entry allowed")
```

### 2.5 Chained Comparisons

Python lets you chain comparisons naturally.

```python
x = 15
if 10 < x < 20:
    print("x is between 10 and 20")
```

---

## 3. Comparison and Logical Operators

### Comparison Operators

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `4 <= 3` | `False` |

### Logical Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `and` | `True` if **both** are True | `age > 18 and age < 60` |
| `or` | `True` if **at least one** is True | `day == "Sat" or day == "Sun"` |
| `not` | Reverses the result | `not is_raining` |

**Truth table**

| A | B | A and B | A or B |
|---|---|---------|--------|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

### Short-Circuit Evaluation

- `and` stops at the first `False`.
- `or` stops at the first `True`.

```python
x = 0
if x != 0 and 10 / x > 1:   # 10 / x is never evaluated, so no ZeroDivisionError
    print("ok")
```

### Membership and Identity Operators

```python
fruits = ["apple", "banana"]
print("apple" in fruits)        # True
print("mango" not in fruits)    # True

a = None
print(a is None)                # True  (use `is` for None checks)
```

> `==` compares **values**, `is` compares **identity** (same object in memory).

---

## 4. Truthy and Falsy Values

Every object in Python has a boolean value.

**Falsy values** (treated as `False`):

- `False`, `None`
- `0`, `0.0`, `0j`
- `""` (empty string)
- `[]`, `()`, `{}`, `set()` (empty collections)
- `range(0)`

**Everything else is truthy.**

```python
name = ""
if not name:
    print("Name is empty")

items = [1, 2, 3]
if items:
    print("List has elements")
```

Check with `bool()`:

```python
print(bool(0))        # False
print(bool("hello"))  # True
print(bool([]))       # False
```

---

## 5. Ternary (Conditional) Expression

A one-line `if-else` that **returns a value**.

**Syntax:** `value_if_true if condition else value_if_false`

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)   # Adult
```

Use it only for simple cases. For complex logic, a normal `if` block is more readable.

---

## 6. match-case (Python 3.10+)

Python's version of a `switch` statement, but more powerful (structural pattern matching).

```python
command = "start"

match command:
    case "start":
        print("Starting...")
    case "stop":
        print("Stopping...")
    case "pause" | "hold":        # OR pattern
        print("Pausing...")
    case _:                        # default (wildcard)
        print("Unknown command")
```

Matching with conditions and sequences:

```python
point = (0, 5)

match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"On the Y axis at {y}")
    case (x, 0):
        print(f"On the X axis at {x}")
    case _:
        print("Somewhere else")
```

> Check your version with `python --version`. On older versions, use `if-elif-else`.

---

## 7. Loops

A loop repeats a block of code.

### 7.1 `for` Loop

Iterates over any **iterable** (list, tuple, string, dict, set, range, etc.).

```python
for fruit in ["apple", "banana", "cherry"]:
    print(fruit)
```

Looping over a string:

```python
for ch in "Python":
    print(ch)
```

Looping over a dictionary:

```python
student = {"name": "Aman", "age": 21}

for key in student:                 # keys
    print(key)

for value in student.values():      # values
    print(value)

for key, value in student.items():  # both
    print(key, value)
```

### 7.2 `range()`

Generates a sequence of numbers.

| Form | Meaning | Output |
|------|---------|--------|
| `range(5)` | 0 up to 4 | 0, 1, 2, 3, 4 |
| `range(2, 6)` | 2 up to 5 | 2, 3, 4, 5 |
| `range(0, 10, 2)` | step of 2 | 0, 2, 4, 6, 8 |
| `range(10, 0, -1)` | countdown | 10, 9, ..., 1 |

```python
for i in range(1, 6):
    print(i)
```

> The **stop** value is **excluded**. `range` is lazy, so it does not build the whole list in memory.

### 7.3 `while` Loop

Repeats **as long as** the condition is `True`.

```python
count = 1
while count <= 5:
    print(count)
    count += 1
```

**Always make sure the condition eventually becomes False**, or you get an infinite loop.

Intentional infinite loop with `break`:

```python
while True:
    answer = input("Type 'quit' to exit: ")
    if answer == "quit":
        break
```

### 7.4 `for` vs `while`

| `for` | `while` |
|-------|---------|
| Number of iterations is known / fixed by a sequence | Number of iterations is unknown |
| Iterates over an iterable | Runs until a condition becomes False |
| Less risk of infinite loops | Easy to create infinite loops by mistake |
| Example: process every item in a list | Example: keep asking until input is valid |

---

## 8. Loop Control Statements

### `break`: exit the loop immediately

```python
for i in range(1, 10):
    if i == 5:
        break
    print(i)
# 1 2 3 4
```

### `continue`: skip the rest of this iteration

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
# 1 2 4 5
```

### `pass`: do nothing (placeholder)

```python
for i in range(5):
    pass   # to be implemented later

if True:
    pass   # empty block is not allowed in Python, so we use pass
```

| Statement | Effect |
|-----------|--------|
| `break` | Terminates the entire loop |
| `continue` | Jumps to the next iteration |
| `pass` | No operation, just fills a block |

---

## 9. Loop `else` Clause

A unique Python feature. The `else` block runs **only if the loop finished without hitting `break`**.

```python
for n in range(2, 6):
    if n == 7:
        print("Found 7")
        break
else:
    print("7 was not found")   # runs, because there was no break
```

**Classic use: checking for a prime number**

```python
num = 29

for i in range(2, int(num ** 0.5) + 1):
    if num % i == 0:
        print(f"{num} is not prime")
        break
else:
    print(f"{num} is prime")
```

Works with `while` loops too.

---

## 10. Nested Loops

A loop inside another loop. The inner loop completes fully for **each** iteration of the outer loop.

```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i * j}")
    print("---")
```

**Pattern printing**

```python
# Right triangle
for i in range(1, 6):
    print("*" * i)
```

Output:

```
*
**
***
****
*****
```

```python
# Same thing using nested loops
for i in range(1, 6):
    for j in range(i):
        print("*", end="")
    print()
```

> `end=""` stops `print` from adding a newline.

> `break` and `continue` only affect the **innermost** loop they are in.

---

## 11. Useful Loop Helpers

### `enumerate()`: get index and value

```python
colors = ["red", "green", "blue"]

for index, color in enumerate(colors):
    print(index, color)

for index, color in enumerate(colors, start=1):   # start counting from 1
    print(index, color)
```

### `zip()`: loop over multiple iterables together

```python
names = ["Aman", "Riya", "Karan"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

`zip` stops at the shortest iterable.

### `reversed()` and `sorted()`

```python
for x in reversed([1, 2, 3]):
    print(x)            # 3 2 1

for x in sorted([3, 1, 2]):
    print(x)            # 1 2 3
```

### List Comprehension (preview)

A compact way to build a list with a loop (covered in more detail in Data Structures).  
**List comprehension** is a simple and shorter way to create a new list by using a `for` loop in a single line.  

```python
squares = [x ** 2 for x in range(1, 6)]
print(squares)   # [1, 4, 9, 16, 25]

evens = [x for x in range(10) if x % 2 == 0]
print(evens)     # [0, 2, 4, 6, 8]
```

---

## 12. Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Using `=` instead of `==` in a condition | `=` assigns, `==` compares | `if x == 5:` |
| Forgetting the colon `:` | `SyntaxError` | `if x > 5:` |
| Wrong indentation | `IndentationError` or wrong logic | Use consistent 4 spaces |
| Infinite `while` loop | Condition never becomes False | Update the loop variable |
| Off-by-one with `range()` | Stop value is excluded | `range(1, n + 1)` to include `n` |
| Modifying a list while looping over it | Skips items / unexpected results | Loop over a copy: `for x in lst[:]` |
| Using `is` to compare numbers or strings | Identity vs equality confusion | Use `==` for values |
| Checking `if x == True` | Verbose and fragile | Just write `if x:` |

---

## 13. Practice Problems

**Beginner**

1. Check whether a number is positive, negative, or zero.
2. Check whether a year is a leap year.
3. Print numbers from 1 to 20 that are divisible by 3.
4. Print the multiplication table of any number.
5. Find the sum of the first `n` natural numbers.

**Intermediate**

6. Print the Fibonacci series up to `n` terms.
7. Check whether a number is a palindrome.
8. Count the vowels in a string.
9. Print the factorial of a number.
10. FizzBuzz: print 1 to 50; multiples of 3 print "Fizz", multiples of 5 print "Buzz", multiples of both print "FizzBuzz".

**Pattern and Logic**

11. Print an inverted right triangle of stars.
12. Print a pyramid pattern.
13. Number guessing game using a `while` loop and `break`.
14. Simple calculator using `match-case`.
15. Check whether a number is an Armstrong number.

<details>
<summary>Sample solution: Leap Year (#2)</summary>

```python
year = int(input("Enter a year: "))

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print("Leap year")
else:
    print("Not a leap year")
```

</details>

<details>
<summary>Sample solution: FizzBuzz (#10)</summary>

```python
for i in range(1, 51):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

</details>

---

## 14. Quick Cheat Sheet

```python
# Conditionals
if cond1:
    ...
elif cond2:
    ...
else:
    ...

# Ternary
result = a if cond else b

# match-case (3.10+)
match value:
    case 1:
        ...
    case _:
        ...

# for loop
for item in iterable:
    ...

# range
range(stop)
range(start, stop)
range(start, stop, step)

# while loop
while cond:
    ...

# Loop control
break       # exit loop
continue    # next iteration
pass        # placeholder

# Loop else
for x in seq:
    ...
else:
    ...     # runs if no break happened

# Helpers
enumerate(seq, start=0)
zip(a, b)
reversed(seq)
sorted(seq)
```

---

### Key Takeaways

- Python uses **indentation** to define blocks.
- `elif` chains stop at the **first** matching condition.
- Use `for` when iterating over a known sequence, `while` when the repeat count is unknown.
- `break` exits, `continue` skips, `pass` does nothing.
- A loop's `else` runs only when **no `break`** occurred.
- Prefer `enumerate()` and `zip()` over manual index handling.

---
