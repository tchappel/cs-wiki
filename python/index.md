# Python Cheatsheet

## Variables Declaration/Instantiation

In Python, variables are created when you assign a value to them:

```python
x = 5
y = "Hello, World!"
z = 3.14
```

You don't need to declare the type of the variable, Python automatically infers the type based on the value assigned.

## Arithmetic Operations (PEMDAS)

Python follows the standard mathematical order of operations, which is Parentheses, Exponents, Multiplication and Division (from left to right), Addition and Subtraction (from left to right):

```python
result = (2 + 3) * 4  # Parentheses first
result = 2 ** 3       # Exponents
result = 10 / 2 * 3   # Multiplication and Division
result = 5 + 2 - 1    # Addition and Subtraction
```

You can use these operations to perform calculations in your Python code.

---

id: 2eedq2ekz36kpqzep23k6ks
title: Functions
desc: ''
updated: 1741900746149
created: 1741900108818

---

## help function

The help function displays function header and info on arguments and return value.

It pulls docstring from custom functions

```python
help(fn)
```

## Defining functions

```python
def least_difference(a, b, c):
    diff1 = abs(a - b)
    diff2 = abs(b - c)
    diff3 = abs(a - c)
    return min(diff1, diff2, diff3)
```

## doctring

A special kind of comment used to describe the purpose and usage of a function, method, class, or module in Python. They are enclosed in triple quotes and can be accessed using the **doc** attribute. Docstrings help in understanding the code better and are used by documentation generation tools to create reference manuals.

```python
def least_difference(a, b, c):
    """Return the smallest difference between any two numbers
    among a, b and c.

    >>> least_difference(1, 5, -5)
    4
    """
    diff1 = abs(a - b)
    diff2 = abs(b - c)
    diff3 = abs(a - c)
    return min(diff1, diff2, diff3)
```

## Functions that don't return

Functions that don't return, return None

## Default arguments

```python
def greet(name, msg="Hello"):
    print(f"{msg}, {name}!")
```

## Higher order functions

- Takes one or more functions as arguments, or
- Returns a function as a result.

```python
def apply_function(func, value):
    return func(value)

def double(x):
    return x * 2

result = apply_function(double, 4)  # Result will be 8
```
