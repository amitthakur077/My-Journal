# 01. Python Basics

> Fundamental concepts required to get started with Python.

## Table of Contents

1. [Introduction to Python](#1-introduction-to-python)
2. [Syntax](#2-syntax)
3. [Variables](#3-variables)
4. [Data Types](#4-data-types)
5. [Type Conversion](#5-type-conversion)
6. [Input and Output](#6-input-and-output)
7. [Operators](#7-operators)
8. [Keywords and Identifiers](#8-keywords-and-identifiers)
9. [Quick Revision](#9-quick-revision)

---

## 1. Introduction to Python

Python is a **high-level, interpreted, general-purpose programming language** created by **Guido van Rossum** and first released in **1991**. It is famous for its clean, readable syntax that looks close to plain English.

### Key Features

| Feature | Meaning |
|---------|---------|
| Easy to read and write | Less boilerplate than Java or C++ |
| Interpreted | Code runs line by line, with no separate compile step |
| Dynamically typed | No need to declare variable types |
| Cross-platform | Runs on Windows, macOS and Linux |
| Large ecosystem | Libraries for web, data science, AI/ML, automation and more |

### Where is Python used?

- Web development (Django, Flask, FastAPI)
- Data science and analysis (pandas, NumPy)
- Machine learning and AI (TensorFlow, PyTorch)
- Automation and scripting
- Game development, cybersecurity, and more

### Your First Program

```python
print("Hello, World!")
```

**Output**

```
Hello, World!
```

### Running Python Code

```bash
python script.py     # run a file
python               # open the interactive shell (REPL)
```

> [!NOTE]
> On some systems the command is `python3` instead of `python`.

---

## 2. Syntax

Syntax is the **set of rules** that defines how a Python program must be written.

### Indentation

Python uses **indentation** (spaces at the start of a line) to define blocks of code. Other languages use curly braces `{}`. The standard is **4 spaces**.

```python
if 5 > 2:
    print("Five is greater than two")   # indented block
```

> [!WARNING]
> Wrong or inconsistent indentation raises an `IndentationError`.

### Comments

Comments are ignored by Python and are used to explain code.

```python
# This is a single-line comment

"""
This is a multi-line string,
often used as a docstring or block comment.
"""
```

### Case Sensitivity

`name`, `Name` and `NAME` are **three different** identifiers.
Identifiers are the names given to programming elements such as variables, functions, classes, objects, etc.

### Statements and Line Continuation

Each line is normally one statement. To split a long statement over several lines, wrap it in parentheses or use a backslash `\`.

```python
total = (1 + 2 + 3 +
         4 + 5)

total = 1 + 2 + 3 + \
        4 + 5
```

> [!TIP]
> Prefer parentheses over backslashes. They are cleaner and less error-prone.

---

## 3. Variables

A variable is a **name that refers to a value stored in memory**. In Python, a variable is created the moment you assign a value to it.

```python
name = "Alice"
age = 25
height = 5.7
```

### Dynamic Typing

A variable can be reassigned to a value of a different type.

```python
x = 10        # int
x = "ten"     # now a str
```

### Multiple Assignment

```python
a, b, c = 1, 2, 3        # different values
x = y = z = 0            # same value for all
```

### Swapping Values

```python
a, b = 10, 20
a, b = b, a
print(a, b)   # 20 10
```

### Naming Rules

| Rule | Valid | Invalid |
|------|-------|---------|
| Start with a letter or underscore | `user`, `_count` | `2nd_place` |
| Only letters, digits, underscores | `user_name1` | `my-var`, `my var` |
| Cannot be a keyword | `class_name` | `class`, `for` |
| Case-sensitive | `Age` ≠ `age` | |

> [!TIP]
> **Convention:** use `snake_case` for variable names, such as `first_name` or `total_price`.

---

## 4. Data Types

Every value in Python has a **type**. Use `type()` to check it.

| Category | Type | Example | Mutable? |
|----------|------|---------|:--------:|
| Numeric | `int` | `10`, `-3` | No |
| Numeric | `float` | `3.14`, `-0.5` | No |
| Numeric | `complex` | `2 + 3j` | No |
| Text | `str` | `"hello"`, `'hi'` | No |
| Boolean | `bool` | `True`, `False` | No |
| Sequence | `list` | `[1, 2, 3]` | Yes |
| Sequence | `tuple` | `(1, 2, 3)` | No |
| Sequence | `range` | `range(5)` | No |
| Set | `set` | `{1, 2, 3}` | Yes |
| Mapping | `dict` | `{"name": "Alice"}` | Yes |
| None | `NoneType` | `None` | No |

```python
print(type(10))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type("hi"))        # <class 'str'>
print(type([1, 2]))      # <class 'list'>
print(type(None))        # <class 'NoneType'>
```

### Mutable vs Immutable

- **Immutable**: cannot be changed after creation (`int`, `float`, `str`, `bool`, `tuple`)
- **Mutable**: can be changed in place (`list`, `set`, `dict`)

```python
nums = [1, 2, 3]
nums[0] = 99          # works, lists are mutable

word = "hello"
word[0] = "H"         # TypeError, strings are immutable
```

> [!IMPORTANT]
> Remember `{}` creates an empty **dictionary**, not a set. Use `set()` for an empty set.

---

## 5. Type Conversion

Type conversion means changing a value from one data type to another.

### Implicit Conversion

Python automatically converts a smaller type to a larger one to avoid data loss.

```python
result = 5 + 2.5
print(result)         # 7.5
print(type(result))   # <class 'float'>
```

### Explicit Conversion (Type Casting)

You convert the value yourself using built-in functions.

| Function | Purpose | Example | Result |
|----------|---------|---------|--------|
| `int()` | To integer | `int("42")` | `42` |
| `float()` | To float | `float("2.5")` | `2.5` |
| `str()` | To string | `str(100)` | `"100"` |
| `bool()` | To boolean | `bool(0)` | `False` |
| `list()` | To list | `list("abc")` | `['a', 'b', 'c']` |

```python
int(3.9)         # 3  (decimal part is cut off, not rounded)
int("hello")     # ValueError
```

### Truthy and Falsy Values

These values are **falsy**: `0`, `0.0`, `""`, `[]`, `{}`, `()`, `set()`, `None`, `False`. Everything else is **truthy**.

```python
bool("")         # False
bool([])         # False
bool("False")    # True  (any non-empty string is True)
```

---

## 6. Input and Output

### Output with `print()`

```python
print("Hello")
print("A", "B", "C")                 # A B C
print("A", "B", "C", sep="-")        # A-B-C
print("Loading", end="...")          # no newline at the end
```

### Formatted Output (f-strings)

```python
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")
print(f"Pi is approximately {3.14159:.2f}")   # Pi is approximately 3.14
```

### Input with `input()`

`input()` reads a line from the user and **always returns a string**.

```python
name = input("Enter your name: ")
print("Hello,", name)
```

To work with numbers, convert the input:

```python
age = int(input("Enter your age: "))
print("Next year you will be", age + 1)
```

> [!WARNING]
> Forgetting to convert `input()` is a very common bug. `"5" + "5"` gives `"55"`, not `10`.

---

## 7. Operators

Operators perform operations on values (called **operands**).

### Arithmetic Operators

| Operator | Meaning | Example | Result |
|:--------:|---------|---------|:------:|
| `+` | Addition | `7 + 3` | `10` |
| `-` | Subtraction | `7 - 3` | `4` |
| `*` | Multiplication | `7 * 3` | `21` |
| `/` | Division (always float) | `7 / 2` | `3.5` |
| `//` | Floor division | `7 // 2` | `3` |
| `%` | Modulus (remainder) | `7 % 2` | `1` |
| `**` | Exponent | `2 ** 3` | `8` |

### Comparison Operators

Return `True` or `False`.

| Operator | Meaning |
|:--------:|---------|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

### Assignment Operators

| Operator | Example | Same as |
|:--------:|---------|---------|
| `=` | `x = 5` | |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 3` | `x = x * 3` |
| `/=` | `x /= 3` | `x = x / 3` |

### Logical Operators

| Operator | Meaning |
|:--------:|---------|
| `and` | True if both conditions are true |
| `or` | True if at least one condition is true |
| `not` | Reverses the result |

```python
age = 20
print(age > 18 and age < 30)   # True
print(not (age > 18))          # False
```

### Identity Operators

Check whether two names refer to the **same object** in memory.

```python
a = [1, 2]
b = [1, 2]
c = a

print(a == b)       # True  (same value)
print(a is b)       # False (different objects)
print(a is c)       # True  (same object)
```

> [!IMPORTANT]
> Use `==` to compare **values**. Use `is` to compare **identity**, mainly for `None` (`x is None`).

### Membership Operators

```python
print("a" in "apple")        # True
print(5 not in [1, 2, 3])    # True
```

### Bitwise Operators

Work on the binary form of integers.

| Operator | Meaning | Example |
|:--------:|---------|---------|
| `&` | AND | `5 & 3` → `1` |
| `\|` | OR | `5 \| 3` → `7` |
| `^` | XOR | `5 ^ 3` → `6` |
| `~` | NOT | `~5` → `-6` |
| `<<` | Left shift | `5 << 1` → `10` |
| `>>` | Right shift | `5 >> 1` → `2` |

### Operator Precedence (High to Low)

| Order | Operators |
|:-----:|-----------|
| 1 | `()` |
| 2 | `**` |
| 3 | `*`, `/`, `//`, `%` |
| 4 | `+`, `-` |
| 5 | Comparison operators |
| 6 | `not` |
| 7 | `and` |
| 8 | `or` |

> [!TIP]
> When in doubt, use parentheses to make the order obvious.

---

## 8. Keywords and Identifiers

### Keywords

Keywords are **reserved words** with a special meaning in Python. They cannot be used as variable, function or class names.

```python
import keyword
print(keyword.kwlist)
```

| | | | | |
|---|---|---|---|---|
| `False` | `None` | `True` | `and` | `as` |
| `assert` | `async` | `await` | `break` | `class` |
| `continue` | `def` | `del` | `elif` | `else` |
| `except` | `finally` | `for` | `from` | `global` |
| `if` | `import` | `in` | `is` | `lambda` |
| `nonlocal` | `not` | `or` | `pass` | `raise` |
| `return` | `try` | `while` | `with` | `yield` |

> [!NOTE]
> The exact list can vary slightly between Python versions. Always check `keyword.kwlist` for your version.

### Identifiers

An identifier is the **name** given to a variable, function, class, module or any other object.

**Rules**

- Can contain letters, digits and underscores
- Cannot start with a digit
- Cannot contain spaces or special characters (`@`, `$`, `%`, `-`)
- Cannot be a keyword
- Are case-sensitive

### Naming Conventions (PEP 8)

| Item | Style | Example |
|------|-------|---------|
| Variables, functions | `snake_case` | `total_price`, `get_name()` |
| Classes | `PascalCase` | `StudentRecord` |
| Constants | `UPPER_CASE` | `MAX_SIZE` |
| Private (by convention) | leading underscore | `_internal` |

```python
student_name = "Riya"     # good
class = "A"               # SyntaxError: 'class' is a keyword
```

---

## 9. Quick Revision

| Topic | One-line summary |
|-------|------------------|
| Introduction | Python is a high-level, interpreted, dynamically typed language |
| Syntax | Indentation defines blocks, `#` starts a comment, code is case-sensitive |
| Variables | Names that refer to values, created on assignment |
| Data Types | `int`, `float`, `str`, `bool`, `list`, `tuple`, `set`, `dict`, `None` |
| Type Conversion | Use `int()`, `float()`, `str()`, `bool()` to convert explicitly |
| Input and Output | `print()` displays output, `input()` returns a string |
| Operators | Arithmetic, comparison, logical, identity, membership, bitwise |
| Keywords and Identifiers | Keywords are reserved, identifiers are names you choose |

---

**Next:** [02. Control Flow](./02-control-flow.md)
