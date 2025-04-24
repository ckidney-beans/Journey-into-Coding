---
title: Python Built-in Functions
tags:
  - python
  - functions
  - cheatsheet
---

# Python Built-in Functions Reference

This reference covers all built-in functions available in Python 3.11 and earlier versions, organized by category with examples and notes on usage.

## Table of Contents
- [Type Conversion Functions](#type-conversion-functions)
- [Math and Number Functions](#math-and-number-functions)
- [Sequence and Collection Functions](#sequence-and-collection-functions)
- [String Processing Functions](#string-processing-functions)
- [Object and Class Functions](#object-and-class-functions)
- [Input/Output Functions](#inputoutput-functions)
- [Variable and Environment Functions](#variable-and-environment-functions)
- [Iteration and Generator Functions](#iteration-and-generator-functions)
- [Functional Programming Functions](#functional-programming-functions)
- [Memory and System Functions](#memory-and-system-functions)
- [Special Functions](#special-functions)

## Type Conversion Functions

### `int()`
Converts a value to an integer.

```python
# Basic usage
int("123")  # Returns 123
int(12.7)   # Returns 12 (truncates, doesn't round)
int("FF", 16)  # Returns 255 (hexadecimal conversion)
```

### `float()`
Converts a value to a floating-point number.

```python
float("123.45")  # Returns 123.45
float("1.23e2")  # Returns 123.0
```

### `str()`
Converts a value to a string.

```python
str(123)  # Returns "123"
str([1, 2, 3])  # Returns "[1, 2, 3]"
```

### `bool()`
Converts a value to a boolean (True or False).

```python
bool(1)  # Returns True
bool(0)  # Returns False
bool([])  # Returns False (empty sequences are False)
bool([1, 2])  # Returns True (non-empty sequences are True)
```

### `complex()`
Creates a complex number or converts to a complex number.

```python
complex(1, 2)  # Returns (1+2j)
complex("1+2j")  # Returns (1+2j)
```

### `bytes()`
Returns a bytes object (immutable sequence of integers in range 0-255).

```python
bytes([65, 66, 67])  # Returns b'ABC'
bytes("hello", "utf-8")  # Returns b'hello'
```

### `bytearray()`
Returns a bytearray object (mutable sequence of integers in range 0-255).

```python
bytearray([65, 66, 67])  # Returns bytearray(b'ABC')
x = bytearray(b'hello')
x[0] = 106  # Change 'h' to 'j'
# x is now bytearray(b'jello')
```

### `memoryview()`
Creates a memory view object from an object that supports the buffer protocol.
- **Usage**: Low-level C-style memory access, efficient slicing without copying
- **Consider**: Direct buffer manipulation in libraries like NumPy is often preferable

```python
data = bytearray(b'abcefg')
v = memoryview(data)
v[1:4] = b'123'  # Modifies original data without copying
# data is now bytearray(b'a123fg')
```

### `object()`
Returns a new featureless object.
- **Usage**: Base for custom classes
- **Consider**: Rarely needed directly in modern Python; using `class X: pass` is more common

```python
obj = object()  # Creates a blank object
```

## Math and Number Functions

### `abs()`
Returns the absolute value of a number.

```python
abs(-5)  # Returns 5
abs(3.14)  # Returns 3.14
abs(complex(3, 4))  # Returns 5.0 (magnitude of complex number)
```

### `round()`
Round a number to a specified precision.

```python
round(3.14159, 2)  # Returns 3.14
round(1.5)  # Returns 2
round(2.5)  # Returns 2 (rounds to even number with ties)
```

### `divmod()`
Returns quotient and remainder as a tuple when dividing two numbers.

```python
divmod(13, 5)  # Returns (2, 3)
```

### `pow()`
Returns x to the power of y, with optional modulus.

```python
pow(2, 3)  # Returns 8 (same as 2**3)
pow(2, 3, 5)  # Returns 3 (same as (2**3) % 5)
```

### `sum()`
Sums items of an iterable.

```python
sum([1, 2, 3, 4])  # Returns 10
sum([0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1])  # Returns 0.9999999999999999
# For decimal precision, consider decimal module
```

### `max()`
Returns the largest item in an iterable or the largest of multiple arguments.

```python
max(5, 10, 3)  # Returns 10
max([1, 5, 3, 9])  # Returns 9
max("apple", "banana", key=len)  # Returns "banana" (by length)
```

### `min()`
Returns the smallest item in an iterable or the smallest of multiple arguments.

```python
min(5, 10, 3)  # Returns 3
min([1, 5, 3, 9])  # Returns 1
min("apple", "banana", key=len)  # Returns "apple" (by length)
```

### `hex()`
Converts an integer to a hexadecimal string.

```python
hex(255)  # Returns "0xff"
hex(-42)  # Returns "-0x2a"
```

### `oct()`
Converts an integer to an octal string.

```python
oct(8)  # Returns "0o10"
oct(100)  # Returns "0o144"
```

### `bin()`
Converts an integer to a binary string.

```python
bin(3)  # Returns "0b11"
bin(10)  # Returns "0b1010"
```

### `ord()`
Returns the Unicode code point for a character.

```python
ord('A')  # Returns 65
ord('€')  # Returns 8364
```

### `chr()`
Returns the character for a Unicode code point.

```python
chr(65)  # Returns 'A'
chr(8364)  # Returns '€'
```

### `hash()`
Returns the hash value of an object (if it has one).
- **Usage**: Used by dictionaries and sets for lookups
- **Consider**: Not meant for cryptographic purposes; use `hashlib` for that

```python
hash("hello")  # Returns an integer hash value
hash((1, 2, 3))  # Tuples are hashable
# hash([1, 2, 3])  # Error: lists are not hashable
```

## Sequence and Collection Functions

### `len()`
Returns the number of items in an object.

```python
len("hello")  # Returns 5
len([1, 2, 3])  # Returns 3
len({"a": 1, "b": 2})  # Returns 2
```

### `range()`
Creates a sequence of numbers.

```python
list(range(5))  # Returns [0, 1, 2, 3, 4]
list(range(2, 8))  # Returns [2, 3, 4, 5, 6, 7]
list(range(1, 10, 2))  # Returns [1, 3, 5, 7, 9]
```

### `sorted()`
Returns a new sorted list from an iterable.

```python
sorted([3, 1, 4, 1, 5, 9])  # Returns [1, 1, 3, 4, 5, 9]
sorted("hello")  # Returns ['e', 'h', 'l', 'l', 'o']
sorted({"c": 3, "a": 1, "b": 2}.items())  # Returns [('a', 1), ('b', 2), ('c', 3)]
sorted([("a", 2), ("c", 1), ("b", 3)], key=lambda x: x[1])  # Sort by second item: [('c', 1), ('a', 2), ('b', 3)]
```

### `reversed()`
Returns a reverse iterator.

```python
list(reversed([1, 2, 3]))  # Returns [3, 2, 1]
"".join(reversed("hello"))  # Returns "olleh"
```

### `enumerate()`
Returns an iterator of tuples containing indices and values.

```python
list(enumerate(["a", "b", "c"]))  # Returns [(0, 'a'), (1, 'b'), (2, 'c')]
list(enumerate(["a", "b", "c"], start=1))  # Returns [(1, 'a'), (2, 'b'), (3, 'c')]
```

### `zip()`
Creates an iterator that aggregates elements from multiple iterables.

```python
list(zip([1, 2, 3], ["a", "b", "c"]))  # Returns [(1, 'a'), (2, 'b'), (3, 'c')]
list(zip([1, 2], ["a", "b", "c"]))  # Returns [(1, 'a'), (2, 'b')] (stops at shortest)
```

### `iter()`
Returns an iterator object.

```python
i = iter([1, 2, 3])
next(i)  # Returns 1
next(i)  # Returns 2

# Custom stop iteration
def get_number():
    return 42

iterator = iter(get_number, 42)  # Stops when function returns 42
```

### `next()`
Retrieves the next item from an iterator.

```python
i = iter([1, 2, 3])
next(i)  # Returns 1
next(i)  # Returns 2
next(i)  # Returns 3
next(i, "done")  # Returns "done" (default value when iteration is complete)
```

### `filter()`
Constructs an iterator from elements that satisfy a function.

```python
list(filter(lambda x: x > 5, [3, 4, 5, 6, 7]))  # Returns [6, 7]
list(filter(None, [0, False, None, 1, True]))  # Returns [1, True] (filters out falsy values)
```

### `map()`
Applies a function to every item of an iterable.

```python
list(map(lambda x: x*2, [1, 2, 3, 4]))  # Returns [2, 4, 6, 8]
list(map(lambda x, y: x+y, [1, 2, 3], [4, 5, 6]))  # Returns [5, 7, 9]
```

### `list()`
Creates a list from an iterable.

```python
list("hello")  # Returns ['h', 'e', 'l', 'l', 'o']
list(range(3))  # Returns [0, 1, 2]
```

### `tuple()`
Creates a tuple from an iterable.

```python
tuple([1, 2, 3])  # Returns (1, 2, 3)
tuple("abc")  # Returns ('a', 'b', 'c')
```

### `set()`
Creates a set from an iterable.

```python
set([1, 2, 2, 3, 3, 3])  # Returns {1, 2, 3}
set("hello")  # Returns {'h', 'e', 'l', 'o'}
```

### `frozenset()`
Creates an immutable set from an iterable.
- **Usage**: When you need a hashable set (to use as a dictionary key)

```python
frozenset([1, 2, 2, 3])  # Returns frozenset({1, 2, 3})
d = {frozenset([1, 2]): "hashable"}  # Can be used as a dictionary key
```

### `dict()`
Creates a dictionary from key-value pairs.

```python
dict(a=1, b=2)  # Returns {'a': 1, 'b': 2}
dict([('a', 1), ('b', 2)])  # Returns {'a': 1, 'b': 2}
dict(zip(['a', 'b'], [1, 2]))  # Returns {'a': 1, 'b': 2}
```

### `slice()`
Returns a slice object representing the set of indices.
- **Usage**: Creating reusable slice objects

```python
s = slice(1, 5, 2)
[1, 2, 3, 4, 5][s]  # Returns [2, 4]
```

## String Processing Functions

### `format()`
Formats a value according to a format specifier.

```python
format(42, "b")  # Returns "101010" (binary)
format(12.3456, ".2f")  # Returns "12.35" (2 decimal places)
format("center", ">10")  # Returns "    center" (right-aligned in 10 spaces)
```

### `ascii()`
Returns a string containing a printable representation of an object.
- **Usage**: Debugging or logging non-ASCII strings

```python
ascii("hello")  # Returns "'hello'"
ascii("héllo")  # Returns "'h\\xe9llo'" (escape sequences for non-ASCII)
```

### `repr()`
Returns a string containing a printable representation of an object.

```python
repr("hello")  # Returns "'hello'"
repr([1, 2, 3])  # Returns "[1, 2, 3]"
```

### `input()`
Reads a line from input and returns it as a string.

```python
name = input("Enter your name: ")  # Displays prompt and waits for input
```

### `print()`
Prints objects to the text stream file.

```python
print("Hello, world!")  # Basic usage
print("Hello", "world", sep=", ")  # Output: "Hello, world"
print("No newline", end=" ")  # Prevents newline at the end
```

## Object and Class Functions

### `type()`
Returns the type of an object or creates a new type.

```python
type(123)  # Returns <class 'int'>
type("hello")  # Returns <class 'str'>

# Creating a new type
MyClass = type('MyClass', (object,), {'x': 42})
m = MyClass()
m.x  # Returns 42
```

### `isinstance()`
Checks if an object is an instance of a class or subclass.

```python
isinstance(5, int)  # Returns True
isinstance("hello", (str, list))  # Returns True (is instance of any in tuple)
isinstance(5, float)  # Returns False
```

### `issubclass()`
Checks if a class is a subclass of another class.

```python
issubclass(bool, int)  # Returns True (bool is a subclass of int)
issubclass(float, int)  # Returns False
```

### `id()`
Returns the identity (memory address) of an object.
- **Usage**: Debugging object identity issues

```python
a = [1, 2, 3]
b = a
id(a) == id(b)  # Returns True (same object)
id(a) == id([1, 2, 3])  # Returns False (different objects)
```

### `callable()`
Checks if an object appears callable.

```python
callable(len)  # Returns True (function is callable)
callable("hello")  # Returns False (strings aren't callable)
callable(lambda x: x)  # Returns True

class Test:
    def __call__(self):
        pass

callable(Test())  # Returns True
```

### `getattr()`
Gets the value of a named attribute of an object.

```python
class Person:
    name = "John"

p = Person()
getattr(p, "name")  # Returns "John"
getattr(p, "age", 25)  # Returns 25 (default if not found)
```

### `hasattr()`
Checks if an object has a named attribute.

```python
hasattr(str, "upper")  # Returns True
hasattr([1, 2], "append")  # Returns True
hasattr([1, 2], "push")  # Returns False
```

### `setattr()`
Sets the value of a named attribute of an object.

```python
class Person:
    pass

p = Person()
setattr(p, "name", "John")
p.name  # Returns "John"
```

### `delattr()`
Deletes a named attribute from an object.

```python
class Person:
    name = "John"

p = Person()
delattr(p, "name")
# Now p.name would raise an AttributeError
```

### `dir()`
Returns list of names in current scope or attributes of an object.

```python
dir()  # Returns names in current scope
dir(str)  # Returns attributes of str class: ['__add__', '__class__', ...]
```

### `vars()`
Returns the `__dict__` attribute of an object.
- **Usage**: Inspecting object attributes

```python
class Person:
    def __init__(self):
        self.name = "John"
        self.age = 30

p = Person()
vars(p)  # Returns {'name': 'John', 'age': 30}
```

### `property()`
Returns a property attribute.

```python
class Person:
    def __init__(self):
        self._name = "John"
    
    def get_name(self):
        return self._name
    
    def set_name(self, value):
        self._name = value
    
    name = property(get_name, set_name)

p = Person()
p.name  # Returns "John"
p.name = "Jane"
p._name  # Returns "Jane"
```

### `staticmethod()`
Transforms a method into a static method.

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b

Math.add(1, 2)  # Returns 3 without instance
```

### `classmethod()`
Transforms a method into a class method.

```python
class Person:
    count = 0
    
    def __init__(self, name):
        self.name = name
        Person.count += 1
    
    @classmethod
    def get_count(cls):
        return cls.count

Person("John")
Person("Jane")
Person.get_count()  # Returns 2
```

### `super()`
Returns a proxy object that delegates method calls to a parent or sibling class.

```python
class Parent:
    def greet(self):
        return "Hello from Parent"

class Child(Parent):
    def greet(self):
        return super().greet() + " and Child"

Child().greet()  # Returns "Hello from Parent and Child"
```

## Input/Output Functions

### `open()`
Opens a file and returns a file object.

```python
# Basic reading
with open("file.txt", "r") as f:
    content = f.read()

# Writing
with open("output.txt", "w") as f:
    f.write("Hello, world!")
    
# Binary mode
with open("image.png", "rb") as f:
    binary_data = f.read()
```

### `__import__()`
Low-level import function.
- **Usage**: Dynamic importing 
- **Consider**: Use `importlib.import_module()` instead in most cases

```python
math = __import__("math")
math.sqrt(16)  # Returns 4.0
```

## Variable and Environment Functions

### `globals()`
Returns the dictionary of the current global symbol table.
- **Usage**: Introspection, metaprogramming

```python
x = 10
globals()["x"]  # Returns 10
globals()["new_var"] = 20  # Creates a new global variable
```

### `locals()`
Returns a dictionary of the current local symbol table.

```python
def func():
    x = 10
    print(locals())  # Prints {'x': 10}

func()
```

### `exec()`
Executes Python code dynamically.
- **Usage**: Dynamic code execution (use with caution)
- **Consider**: Security implications when using with user input

```python
exec("x = 10")
x  # Returns 10

prog = "for i in range(3): print(i)"
exec(prog)  # Prints 0, 1, 2
```

### `eval()`
Evaluates a Python expression and returns the result.
- **Usage**: Evaluating simple expressions
- **Consider**: Security implications when using with user input

```python
eval("2 + 2")  # Returns 4
eval("'hello' + ' world'")  # Returns "hello world"
```

### `compile()`
Compiles source into a code or AST object.
- **Usage**: Precompiling code for repeated execution

```python
code = compile("2 + 2", "<string>", "eval")
eval(code)  # Returns 4

prog = compile("for i in range(3): print(i)", "<string>", "exec")
exec(prog)  # Prints 0, 1, 2
```

## Iteration and Generator Functions

### `all()`
Returns True if all elements of the iterable are true.

```python
all([True, True, True])  # Returns True
all([True, False, True])  # Returns False
all([])  # Returns True (vacuously true)
all([i > 0 for i in [1, 2, 3]])  # Returns True
```

### `any()`
Returns True if any element of the iterable is true.

```python
any([False, False, True])  # Returns True
any([False, False, False])  # Returns False
any([])  # Returns False (vacuously false)
any([i > 5 for i in [1, 2, 3]])  # Returns False
```

## Functional Programming Functions

### `lambda`
Creates an anonymous function.

```python
square = lambda x: x**2
square(5)  # Returns 25

# With map
list(map(lambda x: x**2, [1, 2, 3]))  # Returns [1, 4, 9]
```

### `reduce()`
Not built-in anymore, but available in functools module.
- **Usage**: Apply function cumulatively to items of a sequence
- **Consider**: Use `functools.reduce()` instead

```python
from functools import reduce
reduce(lambda x, y: x+y, [1, 2, 3, 4])  # Returns 10 (1+2+3+4)
```

## Memory and System Functions

### `help()`
Invokes the built-in help system.

```python
help(str.upper)  # Shows help for string's upper method
help(list)  # Shows help for list data type
```

### `__doc__`
Accesses the docstring of an object.

```python
print(str.__doc__)  # Prints the docstring for the str class
```

## Special Functions

### `breakpoint()`
Enters the debugger at the call site (Python 3.7+).
- **Usage**: Debugging
- **Consider**: Can be configured with environment variables

```python
def calculate():
    x = 10
    breakpoint()  # Execution will pause here
    return x * 2
```

### `__debug__`
Constant; True if Python not started with -O option.
- **Usage**: Conditional debug code

```python
if __debug__:
    print("Debug mode is on")
```

### `NotImplemented`
Special value which should be returned by binary special methods.
- **Usage**: Used in classes to indicate an operation is not supported

```python
class MyClass:
    def __add__(self, other):
        if isinstance(other, MyClass):
            return self.value + other.value
        return NotImplemented  # Let Python try other methods
```

### `Ellipsis` or `...`
Special value used as a placeholder.
- **Usage**: Multidimensional slicing, function type hints

```python
# NumPy slicing
arr[..., 0]  # All elements of the last dimension

# Type hints (Python 3.5+)
def func(x: int = ...) -> None:
    pass
```

## Better Alternatives in Modules

Here are some built-in functions that often have better alternatives in modules:

### Built-in math operations
**Consider**: `math` module for more mathematical functions
```python
import math
math.sin(0.5)  # Trigonometric functions
math.sqrt(16)  # Square root (more precise than pow())
math.log(100, 10)  # Logarithm with base
```

### Numeric operations
**Consider**: `numpy` for numerical computing
```python
import numpy as np
np.array([1, 2, 3]) + np.array([4, 5, 6])  # Array operations
np.mean([1, 2, 3, 4])  # Statistical functions
```

### Random operations
**Consider**: `random` module for random number generation
```python
import random
random.randint(1, 6)  # Random integer
random.choice(['apple', 'banana', 'cherry'])  # Random selection
```

### Date and time operations
**Consider**: `datetime` module for date and time handling
```python
from datetime import datetime, timedelta
now = datetime.now()
future = now + timedelta(days=10)
```

### Regular expression operations
**Consider**: `re` module for text pattern matching
```python
import re
pattern = re.compile(r'\d+')
pattern.findall("There are 123 apples and 456 oranges")
```

### File and path operations
**Consider**: `os`, `pathlib` modules for file operations
```python
from pathlib import Path
p = Path('myfile.txt')
p.exists()  # Check if file exists
```

### JSON operations
**Consider**: `json` module for JSON handling
```python
import json
data = json.loads('{"name": "John", "age": 30}')
json_string = json.dumps(data, indent=2)
```

### Collections operations
**Consider**: `collections` module for specialized container datatypes
```python
from collections import Counter
Counter(['apple', 'banana', 'apple', 'cherry', 'apple'])
# Counter({'apple': 3, 'banana': 1, 'cherry': 1})
```

### Decimal operations
**Consider**: `decimal` module for precise decimal arithmetic
```python
from decimal import Decimal
Decimal('0.1') + Decimal('0.1') + Decimal('0.1')  # Exactly 0.3
```

### Sorting complex data
**Consider**: `operator` module functions like `itemgetter` and `attrgetter`
```python
from operator import itemgetter
sorted([{'name': 'John', 'age': 30}, {'name': 'Jane', 'age': 25}], key=itemgetter('age'))
```

## Python Version-Specific Functions

### `aiter()` and `anext()`
Asynchronous versions of `iter()` and `next()` (Python 3.10+).

### `breakpoint()`
Enters the debugger (Python 3.7+).

## Historical and Deprecated Functions

### `apply()`
Deprecated since Python 2.3, removed in Python 3.
- **Alternative**: Use function(*args, **kwargs)

### `coerce()`
Removed in Python 3.
- **Alternative**: Explicit type conversion

### `intern()`
Now in `sys.intern()`.

### `reload()`
Now in `importlib.reload()`.

### `execfile()`
Removed in Python 3.
- **Alternative**: Use `exec(open(filename).read())`

### `cmp()`
Removed in Python 3.
- **Alternative**: Use (a > b) - (a < b)

### `unichr()`
Removed in Python 3.
- **Alternative**: Use `chr()`

### `reduce()`
Moved to `functools.reduce()` in Python 3.

### `file()`
Removed in Python 3.
- **Alternative**: Use `open()`
