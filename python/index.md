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

## Functions

Functions are reusable blocks of code that perform a specific task. They can take inputs (arguments) and return outputs (return values).

### Function Syntax

We can also distinguish between:

- custom functions: user-defined functions that perform specific tasks.
- built-in functions: `print()`, `len()`, `sum()`, etc. these are part of the Python standard library.
- object methods: functions that are associated with an object. For example, `list.append()` is a method of the list object.

### help function

The help() function in Python can be used to get information about both built-in functions and object methods.

The help function displays function header and info on arguments and return value.

It pulls docstring from custom functions

```python
# built-in functions
help(print)

# built-in methods (object methods)
help(list.append)

# custom function
help(fn)
```

### Defining functions

```python
def least_difference(a, b, c):
    diff1 = abs(a - b)
    diff2 = abs(b - c)
    diff3 = abs(a - c)
    return min(diff1, diff2, diff3)
```

### doctring

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

### Functions that don't return

Functions that don't return, return None

### Default arguments

```python
def greet(name, msg="Hello"):
    print(f"{msg}, {name}!")
```

### Higher order functions

- Takes one or more functions as arguments, or
- Returns a function as a result.

```python
def apply_function(func, value):
    return func(value)

def double(x):
    return x * 2

result = apply_function(double, 4)  # Result will be 8
```

## Booleans

- **`True`** and
- **`False`**

### Boolean Conversion

Python provides the `bool()` function to explicitly convert values of other types into Booleans.

### Truthy and Falsey Values

In Python, certain values are considered "truthy" (evaluating to `True`) or "falsey" (evaluating to `False`).

Check online resources for a complete list of truthy and falsey values.

- Most numbers are considered "truthy" and convert to `True`, except for `0`, which converts to `False`.
- Non-empty strings are convert to `True`, while the empty string `""` are `False`.
- Generally, empty sequences (like lists and tuples, which are mentioned as future topics) are `False`, and non-empty sequences are `True`.

## Comparison Operators

- `==` equal to
- `!=` not equal to
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to

## Logical operators

Boolean values can be combined using the logical operators **`and`**, **`or`**, and **`not`** [4].

- `and` returns `True` only if both operands are `True`.
- `or` returns `True` if at least one operand is `True`.
- `not` negates the Boolean value of its operand.

it is recommended to use **parentheses** to explicitly define the order of evaluation.

## Conditional Statements

`if`, `elif`, `else` statements.

example:

```python
def inspect(x):
    if x == 0:
        print(x, "is zero")
    elif x > 0:
        print(x, "is positive")
    elif x < 0:
        print(x, "is negative")
    else:
        print(x, "is unlike anything I've ever seen...")
```

## Lists

**Lists** are ordered, mutable sequences created using square brackets `[]`. They can contain different data types and even nested lists.

```python
primes = [2-5]
planets = ['Mercury', 'Venus', 'Earth']
mixed_list = [1, 'hello', True]
nested_list = [['a', 'b'], [1, 2]]
```

### Indexing

- **Indexing** allows access to individual elements using zero-based indexing.

Negative indices access elements from the end [-1 is the last element].

```python
primes = [2, 3, 5]
primes[0] # 2
primes[-1] # 5
```

### Slicing

**Slicing** extracts sub-sequences using the format `[start:end:step]`

- start is inclusive, defaults to 0
- end is exclusive, defaults to the list length
- step is optional, defaults to 1
- Negative indices allow access to elements from the end of the list.

```python
primes = [2, 3, 5, 7, 11, 13]
primes[0:2] # [2, 3]
primes[:3] # [2, 3, 5]
primes[2:] # [5, 7, 11, 13]
primes[1:-1] # [3, 5, 7, 11]
```

### Mutability

Lists can be modified in place by assigning new values to indices or slices [4, 7].

```python
# make an example
primes = [2, 3, 5]
primes[0] = 7 # primes = [7, 3, 5]
```

### Built-in List Functions

These functions are not methods of the list object, meaning they are called directly with the list as an argument instead of using dot notation.

- `len(list)`: Returns the number of elements in the list.
- `sorted(list)`: Returns a new sorted list.
- `sum(list)`: Returns the sum of the elements.
- `min(list)`: Returns the minimum element.
- `max(list)`: Returns the maximum element.

### List Methods

Accessed using dot syntax (e.g., list.append(item), list.sort()).

- `append(item)`: Adds an `item` to the end of the list.

```python
planets.append('Pluto')
```

- `pop()`: Removes and returns the last element of the list.

```python
last_planet = planets.pop()
```

- `index(item)`: Returns the index of the first occurrence of `item`.
  - Raises a `ValueError` if the item is not found.
  - Use the `in` operator to check for existence.

```python
planets = ['Mercury', 'Venus', 'Earth']
is_pluto_in = 'Pluto' in planets
earth_index = planets.index('Earth')
```

## Tuples

**Tuples** are ordered, immutable sequences created using parentheses `()` or by separating values with commas.

```python
my_tuple = (1, 2, 3)
another_tuple = 4, 5, 6
```

### Tuple Use Cases

Often used for functions returning multiple values [6, 14] or for swapping variables concisely [14].

```python
numerator, denominator = (0.5).as_integer_ratio()
a = 1
b = 2
a, b = b, a # Swapping a and b
```

### Immutability

Tuples cannot be changed after creation.

Attempting to modify a tuple will result in a `TypeError`.

### Tuple Indexing

Tuples support indexing similar to lists.

### Tuple Slicing

Tuples are sliced exactly like lists but slicing returns a new tuple instead of a list!

### Tuples and built-in list functions

Most built-in functions that work on lists also work on tuples because they operate on iterable sequences in general.

```python
t = (3, 1, 4, 1, 5)
print(len(t))  # Output: 5
print(sum(t))  # Output: 14
print(min(t))  # Output: 1
print(max(t))  # Output: 5
print(sorted(t))  # Output: [1, 1, 3, 4, 5] (returns a new **list**, not a tuple)
```

### Tuples Methods

Since tuples are immutable, they have only two built-in methods:

- `count(value)` Returns the number of times value appears in the tuple.
- `index(value)` Returns the index of the first occurrence of value. Raises ValueError if not found.

Since tuples cannot be modified, the usual workaround is converting the tuple into a list, modifying it, and converting it back:

The `list()` built-in function in Python is used to create a new list from an iterable.

```python
t = (1, 2, 3)
temp_list = list(t)
temp_list.append(4)
t = tuple(temp_list)
print(t)  # Output: (1, 2, 3, 4)
```

## Loops

### For in Loop

The object to the right of the "in" can be any object that supports iteration.

```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
for planet in planets:
    print(planet, end=' ') # print all on same line
```

You can even loop through each character in a string:

```python
s = 'steganograpHy is the practicE of conceaLing a file, message, image, or video within another fiLe, message, image, Or video.'
msg = ''
# print all the uppercase letters in s, one at a time
for char in s:
    if char.isupper():
        print(char, end='')
```

use `range()` to loop to repeat n times

```python
for i in range(5):
    print("Doing important work. i =", i)
```

### While loop

The **while** loop continues executing as long as the condition is `True`.

```python
i = 0
while i < 10:
    print(i, end=' ')
    i += 1 # increase the value of i by 1
```

there is no do-while loop in Python.

### break and continue

**break** exits the loop entirely, while **continue** skips the current iteration and continues with the next one.

```python
for num in range(10):
    if num == 3:
        continue  # Skip number 3 and move to the next iteration
    
    if num == 7:
        print("Breaking at", num)
        break  # Stop the loop when num is 7
    
    print(num)
```

### List comprehensions

List comprehensions provide a concise way to create lists. They consist of brackets containing an expression followed by a `for` clause, and can include optional `if` clauses.

```python
[expression for item in iterable if condition]
```

- expression → The operation or transformation applied to each item.
- item → Each element in the iterable (e.g., list, range, string).
- iterable → The source of elements (e.g., list, tuple, range).
- if condition (optional) → Filters elements based on a condition.

example:

```python
numbers = [i**2 for i in range(5)]
print(numbers)  # O
```

Go see external resources for more complex cases and examples.