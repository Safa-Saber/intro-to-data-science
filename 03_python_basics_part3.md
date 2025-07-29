# Python Basics Part 3: Functions and File Handling

## Table of Contents
1. [Functions (Organizing Your Code)](#functions-organizing-your-code)
2. [Function Parameters and Arguments](#function-parameters-and-arguments)
3. [Scope and Variables](#scope-and-variables)
4. [Recursive Functions](#recursive-functions)
5. [File Handling](#file-handling)
6. [Error Handling](#error-handling)
7. [Modules and Libraries](#modules-and-libraries)

## Functions (Organizing Your Code)

Functions are like mini-programs that perform specific tasks. They help you organize code, avoid repetition, and make programs easier to understand.

### Why Use Functions?
```python
# Without functions - repetitive code
print("Welcome to our store!")
print("Thank you for shopping with us!")
print("Have a great day!")

print("Welcome to our store!")
print("Thank you for shopping with us!")
print("Have a great day!")

# With functions - cleaner and reusable
def greet_customer():
    print("Welcome to our store!")
    print("Thank you for shopping with us!")
    print("Have a great day!")

greet_customer()  # Call the function
greet_customer()  # Use it again
```

### Creating Basic Functions
```python
# Function with no parameters
def say_hello():
    print("Hello, World!")

# Call the function
say_hello()

# Function that returns a value
def get_greeting():
    return "Hello, World!"

message = get_greeting()
print(message)

# Function with multiple statements
def introduce_yourself():
    name = "Python"
    print(f"Hi, I'm {name}")
    print("I'm a programming language")
    print("Nice to meet you!")

introduce_yourself()
```

### Functions with Return Values
```python
# Simple calculation function
def add_numbers(a, b):
    result = a + b
    return result

# Use the function
sum_result = add_numbers(5, 3)
print(sum_result)  # 8

# Function can return different types
def get_user_info():
    return "Alice", 25, "Engineer"  # Returns a tuple

name, age, job = get_user_info()

# Function with conditional returns
def check_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

grade = check_grade(85)
print(f"Your grade is: {grade}")

# Function that returns early
def find_first_even(numbers):
    for num in numbers:
        if num % 2 == 0:
            return num  # Exit function immediately
    return None  # If no even number found

numbers = [1, 3, 7, 8, 9]
first_even = find_first_even(numbers)
print(first_even)  # 8
```

## Function Parameters and Arguments

### Basic Parameters
```python
# Function with one parameter
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Alice is the argument

# Function with multiple parameters
def introduce(name, age, city):
    print(f"Hi, I'm {name}")
    print(f"I'm {age} years old")
    print(f"I live in {city}")

introduce("Bob", 25, "New York")
```

### Default Parameters
```python
# Function with default values
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")              # Hello, Alice!
greet("Bob", "Hi")         # Hi, Bob!
greet("Charlie", "Hey")    # Hey, Charlie!

# More complex default parameters
def create_profile(name, age=18, city="Unknown", job="Student"):
    profile = {
        "name": name,
        "age": age,
        "city": city,
        "job": job
    }
    return profile

# Different ways to call
profile1 = create_profile("Alice")
profile2 = create_profile("Bob", 25)
profile3 = create_profile("Charlie", 30, "Boston")
profile4 = create_profile("Diana", 28, "Seattle", "Engineer")

print(profile1)  # {'name': 'Alice', 'age': 18, 'city': 'Unknown', 'job': 'Student'}
```

### Keyword Arguments
```python
def book_flight(passenger, destination, departure_date, seat_class="Economy"):
    print(f"Booking flight for {passenger}")
    print(f"Destination: {destination}")
    print(f"Date: {departure_date}")
    print(f"Class: {seat_class}")

# Positional arguments
book_flight("Alice", "Paris", "2024-06-15")

# Keyword arguments (can be in any order)
book_flight(destination="Tokyo", passenger="Bob", departure_date="2024-07-20", seat_class="Business")

# Mix of positional and keyword
book_flight("Charlie", destination="London", departure_date="2024-08-10")
```

### Variable-Length Arguments

#### *args (Variable Positional Arguments)
```python
def sum_all(*numbers):
    """Sum any number of arguments"""
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))           # 6
print(sum_all(1, 2, 3, 4, 5))     # 15
print(sum_all(10))                # 10

def print_items(*items):
    print("Items received:")
    for i, item in enumerate(items, 1):
        print(f"{i}. {item}")

print_items("apple", "banana", "cherry")
print_items("red", "green", "blue", "yellow")
```

#### **kwargs (Variable Keyword Arguments)
```python
def create_user(**user_info):
    """Create user with any number of attributes"""
    print("Creating user with the following information:")
    for key, value in user_info.items():
        print(f"{key}: {value}")

create_user(name="Alice", age=25, city="Boston", job="Engineer")
create_user(name="Bob", email="bob@email.com", phone="123-456-7890")

def process_order(order_id, *items, **details):
    """Function with all types of parameters"""
    print(f"Processing order {order_id}")
    print("Items:")
    for item in items:
        print(f"  - {item}")
    print("Details:")
    for key, value in details.items():
        print(f"  {key}: {value}")

process_order("ORD001", "laptop", "mouse", "keyboard", 
              customer="Alice", priority="high", shipping="express")
```

### Practical Function Examples

#### Example 1: Calculator Functions
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):
    if b == 0:
        return "Error: Cannot divide by zero"
    return a / b

def calculator():
    """Simple calculator program"""
    while True:
        print("\n--- Calculator ---")
        print("1. Add")
        print("2. Subtract")
        print("3. Multiply")
        print("4. Divide")
        print("5. Exit")
        
        choice = input("Choose operation: ")
        
        if choice == "5":
            print("Goodbye!")
            break
        
        if choice in ["1", "2", "3", "4"]:
            try:
                num1 = float(input("Enter first number: "))
                num2 = float(input("Enter second number: "))
                
                if choice == "1":
                    result = add(num1, num2)
                elif choice == "2":
                    result = subtract(num1, num2)
                elif choice == "3":
                    result = multiply(num1, num2)
                elif choice == "4":
                    result = divide(num1, num2)
                
                print(f"Result: {result}")
            except ValueError:
                print("Please enter valid numbers")
        else:
            print("Invalid choice")

# Run the calculator
# calculator()
```

#### Example 2: Password Validator
```python
def check_password_strength(password):
    """Check if password meets security requirements"""
    issues = []
    
    if len(password) < 8:
        issues.append("Password must be at least 8 characters long")
    
    if not any(c.isupper() for c in password):
        issues.append("Password must contain at least one uppercase letter")
    
    if not any(c.islower() for c in password):
        issues.append("Password must contain at least one lowercase letter")
    
    if not any(c.isdigit() for c in password):
        issues.append("Password must contain at least one number")
    
    special_chars = "!@#$%^&*()_+-=[]{}|;:,.<>?"
    if not any(c in special_chars for c in password):
        issues.append("Password must contain at least one special character")
    
    return issues

def generate_password_report(password):
    """Generate a detailed password strength report"""
    issues = check_password_strength(password)
    
    if not issues:
        return "Strong password! ✓"
    else:
        report = "Password issues found:\n"
        for issue in issues:
            report += f"• {issue}\n"
        return report

# Test the password validator
test_passwords = ["weak", "StrongPassword123!", "NoNumbers!", "no-uppercase123!"]

for pwd in test_passwords:
    print(f"Password: '{pwd}'")
    print(generate_password_report(pwd))
    print("-" * 40)
```

## Scope and Variables

### Local vs Global Scope
```python
# Global variable
global_var = "I'm global"

def test_scope():
    # Local variable
    local_var = "I'm local"
    print(global_var)  # Can access global
    print(local_var)   # Can access local

test_scope()
# print(local_var)  # Error! local_var doesn't exist outside function

# Modifying global variables
counter = 0

def increment():
    global counter  # Tell Python we want to modify the global variable
    counter += 1

def get_counter():
    return counter  # Can read global without 'global' keyword

print(counter)  # 0
increment()
print(get_counter())  # 1
increment()
print(get_counter())  # 2
```

### Function vs Global Scope Example
```python
name = "Global Alice"

def outer_function():
    name = "Outer Bob"
    
    def inner_function():
        name = "Inner Charlie"
        print(f"Inner: {name}")
    
    inner_function()
    print(f"Outer: {name}")

outer_function()
print(f"Global: {name}")

# Output:
# Inner: Charlie
# Outer: Bob
# Global: Global Alice
```

## Recursive Functions

Recursive functions are functions that call themselves. They're useful for solving problems that can be broken down into smaller, similar problems.

### Understanding Recursion
```python
# Simple example: Countdown
def countdown(n):
    if n <= 0:  # Base case - stop condition
        print("Blast off!")
    else:
        print(n)
        countdown(n - 1)  # Recursive call

countdown(5)
# Output: 5, 4, 3, 2, 1, Blast off!
```

### Classic Recursive Examples

#### Example 1: Factorial
```python
def factorial(n):
    """Calculate factorial of n (n!)"""
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    else:
        return n * factorial(n - 1)

print(factorial(5))  # 120 (5 * 4 * 3 * 2 * 1)
print(factorial(0))  # 1

# How it works:
# factorial(5) = 5 * factorial(4)
# factorial(4) = 4 * factorial(3) 
# factorial(3) = 3 * factorial(2)
# factorial(2) = 2 * factorial(1)
# factorial(1) = 1  (base case)
# Working backwards: 2*1=2, 3*2=6, 4*6=24, 5*24=120
```

#### Example 2: Fibonacci Sequence
```python
def fibonacci(n):
    """Calculate the nth Fibonacci number"""
    # Base cases
    if n <= 1:
        return n
    # Recursive case
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

# Print first 10 Fibonacci numbers
for i in range(10):
    print(f"F({i}) = {fibonacci(i)}")

# Output: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
```

#### Example 3: Sum of List
```python
def sum_list(numbers):
    """Sum all numbers in a list using recursion"""
    # Base case: empty list
    if not numbers:
        return 0
    # Recursive case: first number + sum of rest
    else:
        return numbers[0] + sum_list(numbers[1:])

numbers = [1, 2, 3, 4, 5]
print(sum_list(numbers))  # 15

# How it works:
# sum_list([1,2,3,4,5]) = 1 + sum_list([2,3,4,5])
# sum_list([2,3,4,5]) = 2 + sum_list([3,4,5])
# sum_list([3,4,5]) = 3 + sum_list([4,5])
# sum_list([4,5]) = 4 + sum_list([5])
# sum_list([5]) = 5 + sum_list([])
# sum_list([]) = 0  (base case)
```

#### Example 4: Directory Tree Walker
```python
import os

def list_files(directory, indent=0):
    """Recursively list all files and folders"""
    try:
        items = os.listdir(directory)
        for item in items:
            print("  " * indent + item)
            item_path = os.path.join(directory, item)
            if os.path.isdir(item_path):
                list_files(item_path, indent + 1)  # Recursive call for subdirectories
    except PermissionError:
        print("  " * indent + "[Permission Denied]")

# Example usage (be careful with large directories!)
# list_files(".")  # List current directory
```

### Recursion vs Iteration
```python
# Factorial using recursion
def factorial_recursive(n):
    if n <= 1:
        return 1
    return n * factorial_recursive(n - 1)

# Factorial using iteration (loop)
def factorial_iterative(n