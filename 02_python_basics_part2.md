# Python Basics Part 2: Control Flow and Data Structures

## Table of Contents
1. [Making Decisions (if statements)](#making-decisions-if-statements)
2. [Loops (Repeating Actions)](#loops-repeating-actions)
3. [Lists (Storing Multiple Items)](#lists-storing-multiple-items)
4. [Dictionaries (Key-Value Pairs)](#dictionaries-key-value-pairs)
5. [Tuples (Unchangeable Lists)](#tuples-unchangeable-lists)
6. [Sets (Unique Items)](#sets-unique-items)

## Making Decisions (if statements)

Programs need to make decisions based on different conditions. This is where `if` statements come in.

### Basic if Statement
```python
age = 18

if age >= 18:
    print("You are an adult")
    print("You can vote")

print("This line always runs")
```

### if-else Statement
```python
age = 16

if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")

# Example with user input
temperature = int(input("What's the temperature? "))

if temperature > 30:
    print("It's hot outside!")
else:
    print("It's not too hot")
```

### if-elif-else Statement
```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"Your grade is: {grade}")
```

### Multiple Conditions
```python
age = 25
has_license = True
has_car = False

# Using 'and' - both conditions must be True
if age >= 18 and has_license:
    print("You can drive!")

# Using 'or' - at least one condition must be True
if has_license or has_car:
    print("You have some form of transportation")

# Using 'not' - reverses the condition
if not has_car:
    print("You don't have a car")

# Complex conditions
if age >= 18 and (has_license or has_car):
    print("You have transportation options")
```

### Nested if Statements
```python
weather = "sunny"
temperature = 25

if weather == "sunny":
    if temperature > 20:
        print("Perfect day for a picnic!")
    else:
        print("Sunny but a bit cold")
else:
    if temperature > 20:
        print("Warm but not sunny")
    else:
        print("Not a great day for outdoor activities")
```

### Practical Examples

#### Example 1: Login System
```python
correct_username = "admin"
correct_password = "password123"

username = input("Enter username: ")
password = input("Enter password: ")

if username == correct_username and password == correct_password:
    print("Login successful!")
    print("Welcome to the system")
else:
    print("Invalid username or password")
```

#### Example 2: Grade Calculator
```python
math_score = float(input("Enter math score: "))
science_score = float(input("Enter science score: "))
english_score = float(input("Enter english score: "))

average = (math_score + science_score + english_score) / 3

print(f"Your average is: {average:.2f}")

if average >= 90:
    print("Excellent work!")
    letter_grade = "A"
elif average >= 80:
    print("Good job!")
    letter_grade = "B"
elif average >= 70:
    print("You're doing okay")
    letter_grade = "C"
elif average >= 60:
    print("You need to study more")
    letter_grade = "D"
else:
    print("You're failing")
    letter_grade = "F"

print(f"Letter grade: {letter_grade}")
```

#### Example 3: Simple Calculator
```python
num1 = float(input("Enter first number: "))
operation = input("Enter operation (+, -, *, /): ")
num2 = float(input("Enter second number: "))

if operation == "+":
    result = num1 + num2
    print(f"{num1} + {num2} = {result}")
elif operation == "-":
    result = num1 - num2
    print(f"{num1} - {num2} = {result}")
elif operation == "*":
    result = num1 * num2
    print(f"{num1} * {num2} = {result}")
elif operation == "/":
    if num2 != 0:
        result = num1 / num2
        print(f"{num1} / {num2} = {result}")
    else:
        print("Error: Cannot divide by zero!")
else:
    print("Invalid operation!")
```

## Loops (Repeating Actions)

Loops let you repeat code multiple times without writing it over and over.

### for Loop - When You Know How Many Times

#### Basic for Loop with range()
```python
# Print numbers 0 to 4
for i in range(5):
    print(i)

# Print numbers 1 to 5
for i in range(1, 6):
    print(i)

# Count by 2s from 0 to 10
for i in range(0, 11, 2):
    print(i)  # 0, 2, 4, 6, 8, 10

# Count backwards
for i in range(10, 0, -1):
    print(i)  # 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

#### Looping Through Strings
```python
name = "Python"

for letter in name:
    print(letter)
# P
# y
# t
# h
# o
# n

# Count vowels in a word
word = "programming"
vowels = "aeiou"
vowel_count = 0

for letter in word:
    if letter.lower() in vowels:
        vowel_count += 1

print(f"The word '{word}' has {vowel_count} vowels")
```

### while Loop - When You Don't Know How Many Times

#### Basic while Loop
```python
# Count from 1 to 5
count = 1
while count <= 5:
    print(count)
    count += 1  # Very important! Increment the counter

print("Done!")
```

#### User Input with while Loop
```python
# Keep asking until user enters 'quit'
while True:
    user_input = input("Enter something ('quit' to exit): ")
    if user_input.lower() == 'quit':
        break
    print(f"You entered: {user_input}")

print("Goodbye!")
```

#### Password Attempts
```python
correct_password = "secret123"
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    password = input("Enter password: ")
    if password == correct_password:
        print("Access granted!")
        break
    else:
        attempts += 1
        remaining = max_attempts - attempts
        if remaining > 0:
            print(f"Wrong password. {remaining} attempts remaining.")
        else:
            print("Access denied. Too many failed attempts.")
```

### Loop Control: break and continue

#### break - Exit the Loop
```python
# Find first even number
for i in range(1, 10):
    if i % 2 == 0:
        print(f"First even number: {i}")
        break
```

#### continue - Skip to Next Iteration
```python
# Print odd numbers only
for i in range(1, 10):
    if i % 2 == 0:
        continue  # Skip even numbers
    print(i)  # Only prints 1, 3, 5, 7, 9
```

### Practical Loop Examples

#### Example 1: Multiplication Table
```python
number = int(input("Enter a number: "))

print(f"Multiplication table for {number}:")
for i in range(1, 11):
    result = number * i
    print(f"{number} x {i} = {result}")
```

#### Example 2: Number Guessing Game
```python
import random

# Computer picks a random number
secret_number = random.randint(1, 100)
attempts = 0

print("I'm thinking of a number between 1 and 100!")

while True:
    guess = int(input("Enter your guess: "))
    attempts += 1
    
    if guess == secret_number:
        print(f"Congratulations! You guessed it in {attempts} attempts!")
        break
    elif guess < secret_number:
        print("Too low! Try again.")
    else:
        print("Too high! Try again.")
```

#### Example 3: Sum of Numbers
```python
# Sum all numbers from 1 to n
n = int(input("Enter a positive number: "))
total = 0

for i in range(1, n + 1):
    total += i

print(f"The sum of numbers from 1 to {n} is: {total}")

# Alternative method
total = sum(range(1, n + 1))
print(f"Using sum(): {total}")
```

## Lists (Storing Multiple Items)

Lists are like containers that can hold multiple items in order.

### Creating Lists
```python
# Empty list
empty_list = []

# List with numbers
numbers = [1, 2, 3, 4, 5]

# List with strings
fruits = ["apple", "banana", "cherry"]

# Mixed list (different types)
mixed = [1, "hello", 3.14, True]

# List with variables
name = "Alice"
age = 25
person = [name, age, "student"]
```

### Accessing List Items
```python
fruits = ["apple", "banana", "cherry", "date"]

# Access by index (starts at 0)
print(fruits[0])   # apple (first item)
print(fruits[1])   # banana (second item)
print(fruits[-1])  # date (last item)
print(fruits[-2])  # cherry (second to last)

# Slicing (getting multiple items)
print(fruits[1:3])   # ['banana', 'cherry']
print(fruits[:2])    # ['apple', 'banana'] (first 2 items)
print(fruits[2:])    # ['cherry', 'date'] (from index 2 to end)
print(fruits[::-1])  # ['date', 'cherry', 'banana', 'apple'] (reversed)
```

### Modifying Lists
```python
numbers = [1, 2, 3, 4, 5]

# Change an item
numbers[0] = 10
print(numbers)  # [10, 2, 3, 4, 5]

# Add items
numbers.append(6)        # Add to end
print(numbers)           # [10, 2, 3, 4, 5, 6]

numbers.insert(1, 15)    # Insert at index 1
print(numbers)           # [10, 15, 2, 3, 4, 5, 6]

# Remove items
numbers.remove(15)       # Remove first occurrence of 15
print(numbers)           # [10, 2, 3, 4, 5, 6]

last_item = numbers.pop()  # Remove and return last item
print(f"Removed: {last_item}")  # Removed: 6
print(numbers)           # [10, 2, 3, 4, 5]

del numbers[0]           # Delete item at index 0
print(numbers)           # [2, 3, 4, 5]
```

### List Methods
```python
fruits = ["apple", "banana", "cherry", "apple"]

# Information about list
print(len(fruits))           # 4 (length)
print(fruits.count("apple")) # 2 (how many times "apple" appears)
print(fruits.index("cherry")) # 2 (index of first "cherry")

# Sorting
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
numbers.sort()               # Sort in place
print(numbers)               # [1, 1, 2, 3, 4, 5, 6, 9]

fruits.sort()                # Sort alphabetically
print(fruits)                # ['apple', 'apple', 'banana', 'cherry']

# Reverse
numbers.reverse()
print(numbers)               # [9, 6, 5, 4, 3, 2, 1, 1]

# Clear all items
fruits.clear()
print(fruits)                # []
```

### Looping Through Lists
```python
fruits = ["apple", "banana", "cherry"]

# Method 1: Direct iteration
for fruit in fruits:
    print(fruit)

# Method 2: Using index
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# Method 3: Using enumerate (gets both index and value)
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# Method 4: With starting number
for i, fruit in enumerate(fruits, 1):
    print(f"{i}: {fruit}")  # Starts counting from 1
```

### List Comprehensions (Elegant Way to Create Lists)
```python
# Traditional way
squares = []
for i in range(10):
    squares.append(i * i)
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# List comprehension way
squares = [i * i for i in range(10)]
print(squares)  # Same result, more concise

# More examples
even_numbers = [i for i in range(20) if i % 2 == 0]
print(even_numbers)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

words = ["hello", "world", "python"]
uppercase_words = [word.upper() for word in words]
print(uppercase_words)  # ['HELLO', 'WORLD', 'PYTHON']
```

### Practical List Examples

#### Example 1: Shopping List
```python
shopping_list = []

while True:
    print("\n--- Shopping List ---")
    print("1. Add item")
    print("2. Remove item")
    print("3. View list")
    print("4. Clear list")
    print("5. Exit")
    
    choice = input("Choose an option: ")
    
    if choice == "1":
        item = input("Enter item to add: ")
        shopping_list.append(item)
        print(f"Added '{item}' to the list")
    
    elif choice == "2":
        if shopping_list:
            item = input("Enter item to remove: ")
            if item in shopping_list:
                shopping_list.remove(item)
                print(f"Removed '{item}' from the list")
            else:
                print("Item not found in the list")
        else:
            print("List is empty")
    
    elif choice == "3":
        if shopping_list:
            print("Your shopping list:")
            for i, item in enumerate(shopping_list, 1):
                print(f"{i}. {item}")
        else:
            print("Your list is empty")
    
    elif choice == "4":
        shopping_list.clear()
        print("List cleared")
    
    elif choice == "5":
        print("Goodbye!")
        break
    
    else:
        print("Invalid choice")
```

#### Example 2: Grade Book
```python
# Store student grades
grades = []

# Add some grades
print("Enter student grades (enter -1 to stop):")
while True:
    grade = float(input("Enter grade: "))
    if grade == -1:
        break
    if 0 <= grade <= 100:
        grades.append(grade)
    else:
        print("Grade must be between 0 and 100")

if grades:
    # Calculate statistics
    average = sum(grades) / len(grades)
    highest = max(grades)
    lowest = min(grades)
    
    print(f"\n--- Grade Statistics ---")
    print(f"Number of grades: {len(grades)}")
    print(f"Average grade: {average:.2f}")
    print(f"Highest grade: {highest}")
    print(f"Lowest grade: {lowest}")
    
    # Count letter grades
    a_count = len([g for g in grades if g >= 90])
    b_count = len([g for g in grades if 80 <= g < 90])
    c_count = len([g for g in grades if 70 <= g < 80])
    d_count = len([g for g in grades if 60 <= g < 70])
    f_count = len([g for g in grades if g < 60])
    
    print(f"\nGrade Distribution:")
    print(f"A's: {a_count}")
    print(f"B's: {b_count}")
    print(f"C's: {c_count}")
    print(f"D's: {d_count}")
    print(f"F's: {f_count}")
```

## Dictionaries (Key-Value Pairs)

Dictionaries store data in key-value pairs, like a real dictionary where you look up a word (key) to find its meaning (value).

### Creating Dictionaries
```python
# Empty dictionary
empty_dict = {}

# Dictionary with data
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A",
    "subjects": ["Math", "Science", "English"]
}

# Another way to create
person = dict(name="Bob", age=25, city="New York")
```

### Accessing Dictionary Values
```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

# Access values by key
print(student["name"])    # Alice
print(student["age"])     # 20

# Safe access with get() - won't cause error if key doesn't exist
print(student.get("name"))     # Alice
print(student.get("height"))   # None
print(student.get("height", 0))  # 0 (default value)
```

### Modifying Dictionaries
```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

# Add or update values
student["height"] = 165       # Add new key-value pair
student["age"] = 21          # Update existing value
student["subjects"] = ["Math", "Science"]  # Add list as value

print(student)
# {'name': 'Alice', 'age': 21, 'grade': 'A', 'height': 165, 'subjects': ['Math', 'Science']}

# Remove items
del student["height"]         # Remove key-value pair
removed_grade = student.pop("grade")  # Remove and return value
print(f"Removed grade: {removed_grade}")

# Update multiple values at once
student.update({"city": "Boston", "major": "Computer Science"})
print(student)
```

### Dictionary Methods
```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A",
    "subjects": ["Math", "Science"]
}

# Get all keys, values, or items
keys = student.keys()          # dict_keys(['name', 'age', 'grade', 'subjects'])
values = student.values()      # dict_values(['Alice', 20, 'A', ['Math', 'Science']])
items = student.items()        # dict_items([('name', 'Alice'), ('age', 20), ...])

# Convert to lists if needed
key_list = list(student.keys())
value_list = list(student.values())

# Check if key exists
if "name" in student:
    print("Name is in the dictionary")

if "height" not in student:
    print("Height is not in the dictionary")

# Get number of items
print(len(student))  # 4
```

### Looping Through Dictionaries
```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A"
}

# Loop through keys
for key in student:
    print(key)  # name, age, grade

# Loop through values
for value in student.values():
    print(value)  # Alice, 20, A

# Loop through key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")
# name: Alice
# age: 20
# grade: A
```

### Nested Dictionaries
```python
# Dictionary containing other dictionaries
students = {
    "student1": {
        "name": "Alice",
        "age": 20,
        "grades": [85, 92, 78]
    },
    "student2": {
        "name": "Bob",
        "age": 21,
        "grades": [90, 87, 93]
    }
}

# Access nested data
print(students["student1"]["name"])  # Alice
print(students["student2"]["grades"][0])  # 90

# Add to nested dictionary
students["student1"]["email"] = "alice@email.com"
```

### Practical Dictionary Examples

#### Example 1: Contact Book
```python
contacts = {}

while True:
    print("\n--- Contact Book ---")
    print("1. Add contact")
    print("2. Search contact")
    print("3. Update contact")
    print("4. Delete contact")
    print("5. List all contacts")
    print("6. Exit")
    
    choice = input("Choose an option: ")
    
    if choice == "1":
        name = input("Enter name: ")
        phone = input("Enter phone number: ")
        email = input("Enter email: ")
        
        contacts[name] = {
            "phone": phone,
            "email": email
        }
        print(f"Added {name} to contacts")
    
    elif choice == "2":
        name = input("Enter name to search: ")
        if name in contacts:
            print(f"Name: {name}")
            print(f"Phone: {contacts[name]['phone']}")
            print(f"Email: {contacts[name]['email']}")
        else:
            print("Contact not found")
    
    elif choice == "3":
        name = input("Enter name to update: ")
        if name in contacts:
            phone = input("Enter new phone (press enter to skip): ")
            email = input("Enter new email (press enter to skip): ")
            
            if phone:
                contacts[name]["phone"] = phone
            if email:
                contacts[name]["email"] = email
            print(f"Updated {name}")
        else:
            print("Contact not found")
    
    elif choice == "4":
        name = input("Enter name to delete: ")
        if name in contacts:
            del contacts[name]
            print(f"Deleted {name}")
        else:
            print("Contact not found")
    
    elif choice == "5":
        if contacts:
            for name, info in contacts.items():
                print(f"{name}: {info['phone']}, {info['email']}")
        else:
            print("No contacts found")
    
    elif choice == "6":
        print("Goodbye!")
        break
    
    else:
        print("Invalid choice")
```

#### Example 2: Word Counter
```python
text = input("Enter some text: ").lower()

# Remove punctuation and split into words
import string
for punct in string.punctuation:
    text = text.replace(punct, "")

words = text.split()

# Count words using dictionary
word_count = {}
for word in words:
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1

# Alternative method using get()
word_count = {}
for word in words:
    word_count[word] = word_count.get(word, 0) + 1

# Display results
print("\nWord frequencies:")
for word, count in word_count.items():
    print(f"{word}: {count}")

# Most common word
most_common = max(word_count, key=word_count.get)
print(f"\nMost common word: '{most_common}' ({word_count[most_common]} times)")
```

## Tuples (Unchangeable Lists)

Tuples are like lists, but you cannot change them after creation. They're perfect for data that shouldn't change.

### Creating Tuples
```python
# Empty tuple
empty_tuple = ()

# Tuple with items
coordinates = (10, 20)
rgb_color = (255, 0, 128)
person = ("Alice", 25, "Engineer")

# Single item tuple (note the comma!)
single_item = (42,)  # Without comma, it's just parentheses

# Tuple without parentheses (still a tuple)
point = 3, 4
print(type(point))  # <class 'tuple'>
```

### Accessing Tuple Items
```python
person = ("Alice", 25, "Engineer", "Boston")

# Access by index (same as lists)
print(person[0])    # Alice
print(person[-1])   # Boston

# Slicing
print(person[1:3])  # (25, 'Engineer')

# Unpacking (assign tuple items to variables)
name, age, job, city = person
print(f"{name} is {age} years old")

# Partial unpacking
name, age, *rest = person
print(f"Name: {name}, Age: {age}, Rest: {rest}")
```

### Tuple Methods
```python
numbers = (1, 2, 3, 2, 4, 2, 5)

# Count occurrences
print(numbers.count(2))  # 3

# Find index of first occurrence
print(numbers.index(3))  # 2

# Length
print(len(numbers))      # 7

# Check if item exists
print(2 in numbers)      # True
```

### Why Use Tuples?
```python
# 1. For coordinates or fixed data
point = (10, 20)
rgb_color = (255, 0, 0)  # Red

# 2. Return multiple values from function
def get_name_age():
    return "Alice", 25

name, age = get_name_age()

# 3. Dictionary keys (tuples can be keys, lists cannot)
locations = {
    (0, 0): "Origin",
    (1, 1): "Northeast", 
    (-1, -1): "Southwest"
}

# 4. Swapping variables
a = 10
b = 20
a, b = b, a  # Now a=20, b=10
```

### Practical Tuple Examples

#### Example 1: Student Records
```python
# Store student information as tuples
students = [
    ("Alice", 20, "Computer Science", 3.8),
    ("Bob", 21, "Mathematics", 3.6),
    ("Charlie", 19, "Physics", 3.9),
    ("Diana", 22, "Chemistry", 3.7)
]

# Find student with highest GPA
best_student = max(students, key=lambda student: student[3])
print(f"Best student: {best_student[0]} with GPA {best_student[3]}")

# List all computer science students
cs_students = [student for student in students if student[2] == "Computer Science"]
for student in cs_students:
    name, age, major, gpa = student
    print(f"{name}: {major}, GPA: {gpa}")
```

#### Example 2: Menu System
```python
# Menu items as tuples (name, price)
menu = [
    ("Burger", 8.99),
    ("Pizza", 12.50),
    ("Salad", 6.75),
    ("Pasta", 9.25),
    ("Sandwich", 7.50)
]

print("--- Restaurant Menu ---")
for i, (item, price) in enumerate(menu, 1):
    print(f"{i}. {item}: ${price:.2f}")

# Calculate total bill
order = []
while True:
    choice = input("\nEnter item number (or 'done' to finish): ")
    if choice.lower() == 'done':
        break
    
    try:
        index = int(choice) - 1
        if 0 <= index < len(menu):
            order.append(menu[index])
            item_name, price = menu[index]
            print(f"Added {item_name} (${price:.2f}) to order")
        else:
            print("Invalid item number")
    except ValueError:
        print("Please enter a valid number")

if order:
    print("\n--- Your Order ---")
    total = 0
    for item, price in order:
        print(f"{item}: ${price:.2f}")
        total += price
    print(f"Total: ${total:.2f}")
```

## Sets (Unique Items)

Sets are collections that automatically remove duplicates and are great for finding unique items.

### Creating Sets
```python
# Empty set (note: {} creates empty dict, not set)
empty_set = set()

# Set with items
numbers = {1, 2, 3, 4, 5}
colors = {"red", "green", "blue"}

# Create set from list (removes duplicates)
numbers_list = [1, 2, 2, 3, 3, 3, 4, 5]
unique_numbers = set(numbers_list)
print(unique_numbers)  # {1, 2, 3, 4, 5}

# Create set from string
letters = set("hello")
print(letters)  # {'h', 'e', 'l', 'o'} - duplicates removed
```

### Set Operations
```python
fruits = {"apple", "banana", "cherry"}

# Add items
fruits.add("orange")
print(fruits)  # {'apple', 'banana', 'cherry', 'orange'}

# Add multiple items
fruits.update(["grape", "mango"])
print(fruits)

# Remove items
fruits.remove("banana")      # Raises error if item doesn't exist
fruits.discard("kiwi")       # Doesn't raise error if item doesn't exist

# Pop random item
random_fruit = fruits.pop()
print(f"Removed: {random_fruit}")

# Clear all items
# fruits.clear()
```

### Set Mathematics
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# Union (items in either set)
union = set1 | set2  # or set1.union(set2)
print(union)  # {1, 2, 3, 4, 5, 6, 7, 8}

# Intersection (items in both sets)
intersection = set1 & set2  # or set1.intersection(set2)
print(intersection)  # {4, 5}

# Difference (items in first set but not second)
difference = set1 - set2  # or set1.difference(set2)
print(difference)  # {1, 2, 3}

# Symmetric difference (items in either set, but not both)
sym_diff = set1 ^ set2  # or set1.symmetric_difference(set2)
print(sym_diff)  # {1, 2, 3, 6, 7, 8}
```

### Practical Set Examples

#### Example 1: Find Common Interests
```python
alice_hobbies = {"reading", "swimming", "cooking", "photography"}
bob_hobbies = {"swimming", "gaming", "cooking", "music"}
charlie_hobbies = {"reading", "gaming", "travel", "photography"}

# Find common hobbies between Alice and Bob
common_alice_bob = alice_hobbies & bob_hobbies
print(f"Alice and Bob both like: {common_alice_bob}")

# Find hobbies that all three share
common_all = alice_hobbies & bob_hobbies & charlie_hobbies
print(f"All three like: {common_all}")

# Find unique hobbies for each person
alice_unique = alice_hobbies - bob_hobbies - charlie_hobbies
bob_unique = bob_hobbies - alice_hobbies - charlie_hobbies
charlie_unique = charlie_hobbies - alice_hobbies - bob_hobbies

print(f"Only Alice likes: {alice_unique}")
print(f"Only Bob likes: {bob_unique}")
print(f"Only Charlie likes: {charlie_unique}")

# All hobbies combined
all_hobbies = alice_hobbies | bob_hobbies | charlie_hobbies
print(f"All hobbies: {all_hobbies}")
```

#### Example 2: Remove Duplicates from User Input
```python
print("Enter words separated by spaces:")
user_input = input().lower()
words = user_input.split()

# Remove duplicates using set
unique_words = set(words)

print(f"Original words: {words}")
print(f"Unique words: {list(unique_words)}")
print(f"Number of duplicates removed: {len(words) - len(unique_words)}")

# Find duplicates
word_counts = {}
for word in words:
    word_counts[word] = word_counts.get(word, 0) + 1

duplicates = {word for word, count in word_counts.items() if count > 1}
if duplicates:
    print(f"Duplicate words: {duplicates}")
else:
    print("No duplicates found")
```

## Summary

In Part 2, you learned:

**Decision Making:**
- `if`, `elif`, `else` statements
- Logical operators (`and`, `or`, `not`)
- Nested conditions and complex logic

**Loops:**
- `for` loops for known repetitions
- `while` loops for unknown repetitions
- `break` and `continue` for loop control
- Looping through different data types

**Data Structures:**
- **Lists**: Ordered, changeable collections `[1, 2, 3]`
- **Dictionaries**: Key-value pairs `{"name": "Alice", "age": 25}`
- **Tuples**: Ordered, unchangeable collections `(1, 2, 3)`
- **Sets**: Unordered collections of unique items `{1, 2, 3}`

**Key Concepts:**
- When to use each data structure
- How to loop through collections
- Methods for modifying and accessing data
- Practical applications and examples

**Next**: In Part 3, we'll learn about functions (including recursive functions that call themselves), file handling, and error handling.