# Python Basics Part 1: Getting Started and Basic Concepts

## Table of Contents
1. [What is Python?](#what-is-python)
2. [Installing Python](#installing-python)
3. [Running Python](#running-python)
4. [Python Syntax Basics](#python-syntax-basics)
5. [Variables](#variables)
6. [Data Types](#data-types)
7. [Basic Operators](#basic-operators)
8. [Input and Output](#input-and-output)

## What is Python?

Python is a programming language that lets you write instructions for computers to follow. It was created by Guido van Rossum in 1991 and is known for being easy to read and write.

### Why Learn Python?
- **Easy to understand**: Python looks similar to English
- **Popular**: Used by Google, Netflix, Instagram, and many others
- **Versatile**: Can build websites, analyze data, create games, and more
- **Great for beginners**: Simple syntax and helpful error messages

### What Can You Build with Python?
- Websites and web applications
- Games
- Data analysis and charts
- Automation scripts
- Mobile apps
- Artificial intelligence programs

## Installing Python

### Step 1: Download Python
1. Go to **python.org**
2. Click "Download Python" (get the latest version)
3. Run the installer

### Step 2: Installation Tips
- **Windows**: Check "Add Python to PATH" during installation
- **Mac**: Python might already be installed, but download the latest version
- **Linux**: Usually pre-installed, but you can update it

### Step 3: Check Installation
Open your command prompt or terminal and type:
```bash
python --version
```
You should see something like: `Python 3.11.0`

## Running Python

### Method 1: Interactive Mode (Python Shell)
Type `python` in your terminal:
```python
>>> print("Hello, World!")
Hello, World!
>>> 2 + 3
5
>>> exit()
```

### Method 2: Writing Python Files
1. Create a file called `my_program.py`
2. Write your code in the file
3. Run it: `python my_program.py`

### Method 3: Using IDLE
- IDLE comes with Python installation
- Good for beginners
- Has syntax highlighting and error checking

## Python Syntax Basics

### Indentation is Important!
Python uses spaces (indentation) to group code together:

```python
# Correct
if 5 > 3:
    print("Five is greater than three")
    print("This is also part of the if statement")
print("This is outside the if statement")

# Wrong - will cause an error
if 5 > 3:
print("This will cause an IndentationError")
```

**Rule**: Use 4 spaces for each level of indentation.

### Comments
Comments are notes in your code that Python ignores:

```python
# This is a comment
print("Hello")  # This is also a comment

# Comments help explain what your code does
# Use them to make your code easier to understand
```

### Case Sensitivity
Python cares about uppercase and lowercase letters:

```python
name = "Alice"
Name = "Bob"
NAME = "Charlie"

print(name)  # Alice
print(Name)  # Bob  
print(NAME)  # Charlie
```

These are three different variables!

## Variables

Variables are like containers that store data. Think of them as labeled boxes.

### Creating Variables
```python
# Storing text
name = "Alice"
city = "New York"

# Storing numbers
age = 25
price = 19.99

# Storing True/False values
is_student = True
has_car = False

# Using variables
print(name)  # Alice
print(age)   # 25
```

### Variable Naming Rules
```python
# Good variable names
first_name = "John"
age = 30
user_count = 100

# Bad variable names (will cause errors)
# 2name = "John"      # Can't start with number
# first-name = "John" # Can't use hyphens
# class = "Math"      # Can't use Python keywords
```

**Rules for naming variables**:
- Must start with a letter or underscore
- Can contain letters, numbers, and underscores
- Cannot use spaces or special characters
- Cannot use Python keywords (like `if`, `for`, `while`)

### Multiple Assignment
```python
# Assign multiple variables at once
x, y, z = 1, 2, 3
print(x)  # 1
print(y)  # 2
print(z)  # 3

# Assign same value to multiple variables
a = b = c = 10
print(a)  # 10
print(b)  # 10
print(c)  # 10
```

## Data Types

Python has several types of data. Here are the main ones:

### 1. Strings (Text)
```python
# Creating strings
name = "Alice"
message = 'Hello, World!'
long_text = """This is a 
multi-line string"""

# Combining strings
first_name = "John"
last_name = "Doe"
full_name = first_name + " " + last_name
print(full_name)  # John Doe

# String length
text = "Python"
print(len(text))  # 6

# Accessing characters
print(text[0])   # P (first character)
print(text[-1])  # n (last character)
```

### 2. Integers (Whole Numbers)
```python
# Positive and negative integers
age = 25
temperature = -5
zero = 0

# Math with integers
a = 10
b = 3
print(a + b)  # 13 (addition)
print(a - b)  # 7  (subtraction)  
print(a * b)  # 30 (multiplication)
print(a / b)  # 3.333... (division)
```

### 3. Floats (Decimal Numbers)
```python
# Numbers with decimal points
price = 19.99
temperature = 98.6
pi = 3.14159

# Math with floats
height = 5.8
weight = 150.5
average = (height + weight) / 2
print(average)  # 78.15
```

### 4. Booleans (True/False)
```python
# Boolean values
is_sunny = True
is_raining = False

# Comparisons create booleans
age = 20
is_adult = age >= 18
print(is_adult)  # True

is_teenager = age < 20
print(is_teenager)  # False
```

### Checking Data Types
```python
name = "Alice"
age = 25
height = 5.8
is_student = True

print(type(name))      # <class 'str'>
print(type(age))       # <class 'int'>
print(type(height))    # <class 'float'>
print(type(is_student)) # <class 'bool'>
```

### Converting Between Types
```python
# Convert string to integer
age_text = "25"
age_number = int(age_text)
print(age_number + 5)  # 30

# Convert integer to string
score = 95
score_text = str(score)
message = "Your score is " + score_text
print(message)  # Your score is 95

# Convert string to float
price_text = "19.99"
price_number = float(price_text)
print(price_number * 2)  # 39.98
```

## Basic Operators

### Arithmetic Operators
```python
a = 10
b = 3

print(a + b)   # 13 (addition)
print(a - b)   # 7  (subtraction)
print(a * b)   # 30 (multiplication)
print(a / b)   # 3.333... (division)
print(a // b)  # 3 (floor division - no decimals)
print(a % b)   # 1 (remainder/modulo)
print(a ** b)  # 1000 (exponentiation - a to the power of b)
```

### Comparison Operators
```python
x = 5
y = 3

print(x == y)  # False (equal to)
print(x != y)  # True  (not equal to)
print(x > y)   # True  (greater than)
print(x < y)   # False (less than)
print(x >= y)  # True  (greater than or equal to)
print(x <= y)  # False (less than or equal to)
```

### Assignment Operators
```python
number = 10

number += 5   # Same as: number = number + 5
print(number) # 15

number -= 3   # Same as: number = number - 3
print(number) # 12

number *= 2   # Same as: number = number * 2
print(number) # 24

number /= 4   # Same as: number = number / 4
print(number) # 6.0
```

### Logical Operators
```python
age = 25
has_license = True

# and - both conditions must be True
can_drive = age >= 18 and has_license
print(can_drive)  # True

# or - at least one condition must be True
is_eligible = age >= 65 or age <= 16
print(is_eligible)  # False

# not - reverses the boolean value
is_not_adult = not (age >= 18)
print(is_not_adult)  # False
```

## Input and Output

### Getting Input from Users
```python
# Ask user for input
name = input("What is your name? ")
print("Hello, " + name + "!")

# Input is always text, convert if needed
age_text = input("How old are you? ")
age = int(age_text)
print("Next year you will be", age + 1)

# Getting different types of input
price = float(input("Enter a price: "))
is_member = input("Are you a member? (yes/no): ") == "yes"
```

### Displaying Output
```python
# Basic printing
print("Hello, World!")
print(42)
print(3.14)

# Printing multiple things
name = "Alice"
age = 25
print("Name:", name, "Age:", age)

# Printing with separators
print("A", "B", "C", sep="-")  # A-B-C
print("A", "B", "C", sep="")   # ABC

# Printing without new line
print("Hello", end=" ")
print("World")  # Hello World (on same line)
```

### String Formatting (Simple Way)
```python
name = "Bob"
age = 30
score = 95.5

# Using + to combine
message = "Hello " + name + ", you are " + str(age) + " years old"
print(message)

# Using format()
message = "Hello {}, you are {} years old".format(name, age)
print(message)

# Using f-strings (Python 3.6+)
message = f"Hello {name}, you scored {score}%"
print(message)
```

## Practice Examples

### Example 1: Simple Calculator
```python
# Get two numbers from user
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

# Perform calculations
addition = num1 + num2
subtraction = num1 - num2
multiplication = num1 * num2
division = num1 / num2

# Display results
print(f"{num1} + {num2} = {addition}")
print(f"{num1} - {num2} = {subtraction}")
print(f"{num1} * {num2} = {multiplication}")
print(f"{num1} / {num2} = {division}")
```

### Example 2: Personal Information
```python
# Collect user information
first_name = input("Enter your first name: ")
last_name = input("Enter your last name: ")
age = int(input("Enter your age: "))
height = float(input("Enter your height in feet: "))

# Calculate birth year (approximately)
current_year = 2024
birth_year = current_year - age

# Display information
print("\n--- Your Information ---")
print(f"Full Name: {first_name} {last_name}")
print(f"Age: {age} years old")
print(f"Height: {height} feet")
print(f"Born around: {birth_year}")
```

### Example 3: Temperature Converter
```python
# Convert Celsius to Fahrenheit
celsius = float(input("Enter temperature in Celsius: "))
fahrenheit = (celsius * 9/5) + 32

print(f"{celsius}°C is equal to {fahrenheit}°F")

# Convert Fahrenheit to Celsius
fahrenheit = float(input("Enter temperature in Fahrenheit: "))
celsius = (fahrenheit - 32) * 5/9

print(f"{fahrenheit}°F is equal to {celsius:.2f}°C")
```

## Summary

In this part, you learned:
- How to install and run Python
- Python syntax basics (indentation, comments)
- How to create and use variables
- The main data types (strings, integers, floats, booleans)
- Basic operators for math and comparisons
- How to get input from users and display output
- Simple string formatting

**Next**: In Part 2, we'll learn about making decisions with if statements, repeating actions with loops, and organizing data with lists and dictionaries.