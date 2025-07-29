# Python Data Tables and Charts

## Table of Contents
1. [Working with Tables (Pandas)](#working-with-tables-pandas)
2. [Reading CSV Files](#reading-csv-files)
3. [Table Operations](#table-operations)
4. [Creating Charts](#creating-charts)
5. [Bar Charts Examples](#bar-charts-examples)
6. [Required Libraries](#required-libraries)

## Required Libraries

First, install the necessary libraries:

```bash
pip install pandas matplotlib
```

Then import them in your Python code:

```python
import pandas as pd
import matplotlib.pyplot as plt
```

## Working with Tables (Pandas)

### What is a Table (DataFrame)?

A table in pandas is called a **DataFrame**. Think of it like an Excel spreadsheet with:
- **Rows**: Each row represents one record (like a person, product, etc.)
- **Columns**: Each column represents one attribute (like name, age, price, etc.)
- **Index**: Row numbers (0, 1, 2, 3...) that help identify each row

### Why Use Tables?
- Store and organize large amounts of data
- Easily filter, sort, and analyze data
- Read data from files (CSV, Excel, etc.)
- Create charts and visualizations
- Perform calculations across rows and columns

### Creating Tables

#### Method 1: From a Dictionary
```python
import pandas as pd

# Create a table from a dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 22],
    'City': ['New York', 'London', 'Paris', 'Tokyo', 'Sydney'],
    'Salary': [50000, 60000, 70000, 55000, 45000]
}

df = pd.DataFrame(data)
print(df)
```

Output:
```
      Name  Age      City  Salary
0    Alice   25  New York   50000
1      Bob   30    London   60000
2  Charlie   35     Paris   70000
3    Diana   28     Tokyo   55000
4      Eve   22    Sydney   45000
```

#### Method 2: From Lists
```python
# Create table from lists
names = ['John', 'Jane', 'Mike']
ages = [28, 32, 25]
cities = ['Boston', 'Chicago', 'Miami']

df = pd.DataFrame({
    'Name': names,
    'Age': ages,
    'City': cities
})
print(df)
```

#### Method 3: Empty Table (Add Data Later)
```python
# Create empty table with column names
df = pd.DataFrame(columns=['Name', 'Age', 'Score'])
print(df)  # Empty table

# Add rows later
df.loc[0] = ['Alice', 25, 95]
df.loc[1] = ['Bob', 30, 87]
print(df)
```

### Table Information
```python
# Basic information about the table
print("Table shape (rows, columns):", df.shape)  # (5, 4)
print("Number of rows:", len(df))                # 5
print("Column names:", list(df.columns))         # ['Name', 'Age', 'City', 'Salary']
print("Data types:", df.dtypes)                  # Shows data type of each column
print("Table info:")
print(df.info())                                 # Detailed information
```

### Retrieving Rows from Tables

#### Get First/Last Rows
```python
# Show first few rows (default 5)
print("First 5 rows:")
print(df.head())

# Show first 3 rows
print("First 3 rows:")
print(df.head(3))

# Show first 1 row
print("First row:")
print(df.head(1))

# Show last few rows (default 5)
print("Last 5 rows:")
print(df.tail())

# Show last 2 rows
print("Last 2 rows:")
print(df.tail(2))
```

#### Get Specific Rows by Position
```python
# Get one row by index number
print("Row 0 (first row):")
print(df.iloc[0])

print("Row 2 (third row):")
print(df.iloc[2])

print("Last row:")
print(df.iloc[-1])

# Get multiple rows by position
print("Rows 0, 1, 2:")
print(df.iloc[0:3])  # First 3 rows

print("Rows 1 and 3:")
print(df.iloc[[1, 3]])  # Specific rows

print("Rows 2 to 4:")
print(df.iloc[2:5])  # Rows 2, 3, 4
```

#### Get Rows by Range
```python
# Different ways to get multiple rows
print("First 3 rows (method 1):")
print(df[0:3])

print("Rows 1 to 3:")
print(df[1:4])

print("Every other row:")
print(df[::2])  # Rows 0, 2, 4...

print("Rows in reverse order:")
print(df[::-1])
```

#### Get Rows by Condition
```python
# Filter rows based on conditions
print("People older than 27:")
young_people = df[df['Age'] > 27]
print(young_people)

print("People from specific cities:")
us_people = df[df['City'].isin(['New York', 'Boston'])]
print(us_people)

print("People with salary above 55000:")
high_earners = df[df['Salary'] > 55000]
print(high_earners)

print("People aged between 25 and 32:")
age_range = df[(df['Age'] >= 25) & (df['Age'] <= 32)]
print(age_range)
```

### Retrieving Columns
```python
# Get one column
print("Names only:")
print(df['Name'])

# Get multiple columns
print("Name and Age:")
print(df[['Name', 'Age']])

print("All except Salary:")
print(df[['Name', 'Age', 'City']])
```

### Understanding .loc vs .iloc

**Important**: There are two main ways to access data in pandas:
- **`.iloc`** = **i**nteger **loc**ation (uses numbers: 0, 1, 2, 3...)
- **`.loc`** = **loc**ation (uses labels: column names, index names)

#### .iloc - Access by Position (Numbers)
```python
# .iloc uses row numbers and column numbers
# Format: df.iloc[row_number, column_number]

# Get specific cells using position numbers
print("Alice's age:", df.iloc[0, 1])      # Row 0, Column 1
print("Charlie's city:", df.iloc[2, 2])   # Row 2, Column 2
print("Diana's salary:", df.iloc[3, 3])   # Row 3, Column 3

# Get entire row by position
print("First person (row 0):")
print(df.iloc[0])

print("Third person (row 2):")
print(df.iloc[2])

# Get multiple rows by position
print("First 3 people:")
print(df.iloc[0:3])  # Rows 0, 1, 2

print("Rows 1 and 3:")
print(df.iloc[[1, 3]])  # Specific rows

# Get specific columns by position
print("First column (names):")
print(df.iloc[:, 0])  # All rows, column 0

print("First 2 columns:")
print(df.iloc[:, 0:2])  # All rows, columns 0 and 1
```

#### .loc - Access by Label (Names)
```python
# .loc uses column names and index labels
# Format: df.loc[row_label, column_name]

# Get specific cells using labels
print("Bob's age:", df.loc[1, 'Age'])          # Row 1, Age column
print("Eve's city:", df.loc[4, 'City'])        # Row 4, City column
print("Diana's salary:", df.loc[3, 'Salary'])  # Row 3, Salary column

# Get entire row by label
print("First person:")
print(df.loc[0])  # Same as iloc[0] when using default index

# Get multiple columns for one row
print("Alice's name and age:")
print(df.loc[0, ['Name', 'Age']])

# Get multiple rows and columns
print("First 3 people's names and ages:")
print(df.loc[0:2, ['Name', 'Age']])  # Rows 0-2, Name and Age columns

# Get all rows for specific columns
print("All names:")
print(df.loc[:, 'Name'])  # All rows, Name column

print("Names and salaries:")
print(df.loc[:, ['Name', 'Salary']])  # All rows, Name and Salary columns
```

#### When to Use .loc vs .iloc

**Use .iloc when:**
- You know the exact position (row 0, column 1)
- You want the first 5 rows, last 3 rows, etc.
- Working with position-based slicing

**Use .loc when:**
- You know the column names ('Name', 'Age', etc.)
- You want to be more readable and clear
- Working with labeled data

#### More Examples: .loc vs .iloc
```python
# Both do the same thing, but differently:

# Get Alice's age (first row, second column)
age_iloc = df.iloc[0, 1]        # Using position numbers
age_loc = df.loc[0, 'Age']      # Using labels
print(f"Alice's age: {age_iloc} = {age_loc}")

# Get first 3 people's names
names_iloc = df.iloc[0:3, 0]           # Rows 0-2, column 0
names_loc = df.loc[0:2, 'Name']        # Rows 0-2, Name column
print("Names (iloc):", names_iloc.tolist())
print("Names (loc):", names_loc.tolist())

# Get multiple columns
info_iloc = df.iloc[:, [0, 1]]         # All rows, columns 0 and 1
info_loc = df.loc[:, ['Name', 'Age']]  # All rows, Name and Age
print("Info using iloc:")
print(info_iloc.head(2))
print("Info using loc:")
print(info_loc.head(2))
```

### Retrieving Specific Cells - Complete Guide

#### Method 1: Using .iloc (Position-Based)
```python
# Single cell by position
print("Cell at row 0, column 1:", df.iloc[0, 1])
print("Cell at row 2, column 3:", df.iloc[2, 3])

# Multiple cells
print("Cells from row 0-1, column 1-2:")
print(df.iloc[0:2, 1:3])
```

#### Method 2: Using .loc (Label-Based)
```python
# Single cell by label
print("Alice's age:", df.loc[0, 'Age'])
print("Charlie's city:", df.loc[2, 'City'])

# Multiple cells
print("Names and ages for first 3 people:")
print(df.loc[0:2, ['Name', 'Age']])
```

#### Method 3: Using Column + Row Selection
```python
# Get column first, then row
print("Alice's salary:", df['Salary'][0])
print("Bob's city:", df['City'][1])

# This is the same as:
print("Alice's salary:", df['Salary'].iloc[0])
print("Bob's city:", df['City'].iloc[1])
```

#### Method 4: Using Conditions
```python
# Get value by condition
alice_salary = df[df['Name'] == 'Alice']['Salary'].iloc[0]
print("Alice's salary:", alice_salary)

# Alternative way
alice_row = df[df['Name'] == 'Alice']
alice_salary = alice_row['Salary'].iloc[0]
print("Alice's salary:", alice_salary)

# Get multiple values by condition
young_people_names = df[df['Age'] < 30]['Name']
print("Young people:", young_people_names.tolist())
```

### Understanding Basic Pandas Concepts

#### What is an Index?
The **index** is like row numbers for your table. By default, pandas creates numbers 0, 1, 2, 3... for each row.

```python
# Check the index
print("Index:", df.index)  # RangeIndex(start=0, stop=5, step=1)

# You can also set custom index
df_custom = df.set_index('Name')  # Use Name column as index
print(df_custom)
# Now 'Name' becomes the row labels instead of 0, 1, 2, 3...
```

#### What are Column Names?
**Columns** are the headers of your table (like 'Name', 'Age', 'City', 'Salary').

```python
# Get column names
print("Columns:", df.columns.tolist())  # ['Name', 'Age', 'City', 'Salary']

# Rename columns
df_renamed = df.rename(columns={'Name': 'Full_Name', 'Age': 'Years'})
print(df_renamed.columns.tolist())  # ['Full_Name', 'Years', 'City', 'Salary']
```

#### What does .iloc[] mean?
- **i** = integer
- **loc** = location
- It finds data using **position numbers** (0, 1, 2, 3...)

```python
# Think of iloc like this:
#       Column 0   Column 1   Column 2    Column 3
# Row 0   Alice       25      New York     50000
# Row 1   Bob         30      London       60000
# Row 2   Charlie     35      Paris        70000

# df.iloc[1, 2] means: Row 1, Column 2 = "London"
```

#### What does .loc[] mean?
- **loc** = location
- It finds data using **labels/names** ('Name', 'Age', etc.)

```python
# Think of loc like this:
#         Name       Age      City       Salary
# 0       Alice      25       New York   50000
# 1       Bob        30       London     60000
# 2       Charlie    35       Paris      70000

# df.loc[1, 'City'] means: Row 1, City column = "London"
```

#### Understanding Slicing [start:end]
In Python, slicing means getting a range of items.

```python
# For lists and strings:
my_list = [0, 1, 2, 3, 4]
print(my_list[1:4])  # [1, 2, 3] - starts at 1, stops BEFORE 4

# For pandas:
print(df.iloc[1:4])  # Rows 1, 2, 3 (stops BEFORE row 4)
print(df.iloc[0:3])  # Rows 0, 1, 2 (first 3 rows)

# Special slicing:
print(df.iloc[:3])   # First 3 rows (same as [0:3])
print(df.iloc[2:])   # From row 2 to the end
print(df.iloc[:])    # All rows
print(df.iloc[::2])  # Every 2nd row (0, 2, 4...)
```

#### Understanding Conditions and Filtering
When you write `df['Age'] > 30`, you get True/False for each row:

```python
# This creates a boolean mask (True/False for each row)
age_condition = df['Age'] > 30
print("Age > 30:")
print(age_condition)
# 0    False  (Alice is 25)
# 1    False  (Bob is 30) 
# 2    True   (Charlie is 35)
# 3    False  (Diana is 28)
# 4    False  (Eve is 22)

# Then df[condition] keeps only True rows
older_people = df[age_condition]
print("People older than 30:")
print(older_people)  # Only Charlie's row
```

#### Understanding Method Chaining
You can combine multiple operations:

```python
# Step by step:
step1 = df['Age'] > 25          # Get condition
step2 = df[step1]               # Filter rows
step3 = step2['Name']           # Get Name column
result = step3.tolist()         # Convert to list

# All in one line (method chaining):
result = df[df['Age'] > 25]['Name'].tolist()
print("Names of people older than 25:", result)
```

#### Common Pandas Methods Explained

**`.tolist()`** - Convert pandas Series to Python list
```python
names_series = df['Name']       # This is a pandas Series
names_list = df['Name'].tolist()  # This is a Python list
print(type(names_series))       # <class 'pandas.core.series.Series'>
print(type(names_list))         # <class 'list'>
```

**`.value_counts()`** - Count how many times each value appears
```python
# Count how many people from each city
city_counts = df['City'].value_counts()
print(city_counts)
# Each city: 1 (since all cities are different)
```

**`.unique()`** - Get unique values (no duplicates)
```python
unique_cities = df['City'].unique()
print("Unique cities:", unique_cities)
```

**`.nunique()`** - Count number of unique values
```python
num_cities = df['City'].nunique()
print("Number of different cities:", num_cities)  # 5
```

**`.isnull()`** - Check for missing values
```python
# Check if any values are missing (NaN/None)
missing_values = df.isnull()
print("Missing values:")
print(missing_values)  # All False if no missing data
```
```python
# Example 1: Get top 3 highest earners
top_earners = df.nlargest(3, 'Salary')
print("Top 3 earners:")
print(top_earners)

# Example 2: Get bottom 2 youngest people
youngest = df.nsmallest(2, 'Age')
print("2 youngest people:")
print(youngest)

# Example 3: Get random sample of rows
sample_rows = df.sample(n=2)  # Get 2 random rows
print("Random sample:")
print(sample_rows)

# Example 4: Get rows where name starts with specific letter
a_names = df[df['Name'].str.startswith('A')]
print("Names starting with 'A':")
print(a_names)
```

## Reading CSV Files

### Basic CSV Reading
```python
# Read CSV file
df = pd.read_csv('data.csv')
print(df.head())

# Read CSV with custom separator
df = pd.read_csv('data.txt', sep='\t')  # Tab-separated

# Read CSV and set index column
df = pd.read_csv('data.csv', index_col=0)
```

### Creating Sample CSV File
```python
# Create a sample CSV file first
import pandas as pd

data = {
    'Product': ['Apples', 'Bananas', 'Oranges', 'Grapes', 'Strawberries'],
    'Sales': [150, 200, 120, 180, 90],
    'Price': [2.50, 1.20, 3.00, 4.50, 5.00],
    'Category': ['Fruit', 'Fruit', 'Fruit', 'Fruit', 'Berry']
}

df = pd.DataFrame(data)
df.to_csv('sales_data.csv', index=False)
print("CSV file created!")
```

### Reading and Exploring CSV
```python
# Read the CSV file
df = pd.read_csv('sales_data.csv')

# Basic information
print("First 3 rows:")
print(df.head(3))

print("\nTable shape:", df.shape)
print("\nColumn names:", list(df.columns))
print("\nData types:")
print(df.dtypes)

# Summary statistics
print("\nSummary statistics:")
print(df.describe())
```

## Table Operations

### Basic Operations
```python
# Sort by column
df_sorted = df.sort_values('Sales', ascending=False)
print(df_sorted)

# Filter data
high_sales = df[df['Sales'] > 150]
print(high_sales)

# Add new column
df['Total_Value'] = df['Sales'] * df['Price']
print(df)

# Group by category
grouped = df.groupby('Category')['Sales'].sum()
print(grouped)
```

### Summary Operations
```python
# Basic statistics
print("Average sales:", df['Sales'].mean())
print("Total sales:", df['Sales'].sum())
print("Maximum price:", df['Price'].max())
print("Minimum price:", df['Price'].min())

# Count values
print("\nProduct count by category:")
print(df['Category'].value_counts())
```

### Understanding Chart Components

Before creating charts, let's understand the basic parts:

#### Chart Anatomy
```python
# Every chart has these basic parts:
# - Title: Main heading of the chart
# - X-axis: Horizontal line (bottom)
# - Y-axis: Vertical line (left side)
# - X-label: Description of what X-axis shows
# - Y-label: Description of what Y-axis shows
# - Legend: Explains colors/symbols (when multiple data series)
# - Grid: Light lines to help read values
```

#### matplotlib.pyplot Explained
```python
import matplotlib.pyplot as plt

# matplotlib = The main plotting library
# pyplot = Part of matplotlib that makes MATLAB-style plots
# plt = Short name we give to pyplot (just like pd for pandas)

# Think of plt as your drawing tool:
plt.figure()    # Create a new blank canvas
plt.bar()       # Draw bars
plt.plot()      # Draw lines
plt.scatter()   # Draw dots
plt.title()     # Add title
plt.show()      # Display the finished drawing
```

#### Understanding Figure and Figsize
```python
# figsize=(width, height) in inches
plt.figure(figsize=(10, 6))  # 10 inches wide, 6 inches tall
plt.figure(figsize=(8, 8))   # Square chart (good for pie charts)
plt.figure(figsize=(12, 4))  # Wide chart (good for many categories)

# If you don't specify figsize, you get default size
plt.figure()  # Uses default size
```

#### Understanding Common Parameters

**`rotation=45`** - Rotate text labels
```python
plt.xticks(rotation=45)    # Rotate x-axis labels 45 degrees
plt.xticks(rotation=90)    # Rotate x-axis labels 90 degrees (vertical)
plt.yticks(rotation=0)     # Keep y-axis labels horizontal (default)
```

**`alpha=0.7`** - Transparency (0=invisible, 1=solid)
```python
plt.bar(x, y, alpha=0.7)   # Slightly transparent bars
plt.bar(x, y, alpha=0.3)   # Very transparent bars
plt.bar(x, y, alpha=1.0)   # Solid bars (default)
```

**`color` vs `colors`**
```python
# color: One color for all elements
plt.bar(x, y, color='blue')        # All bars blue
plt.bar(x, y, color='#FF5733')     # All bars custom color

# colors: Different color for each element
colors_list = ['red', 'blue', 'green', 'yellow']
plt.bar(x, y, color=colors_list)   # Each bar different color
```

**`marker='o'`** - Symbols for line/scatter plots
```python
plt.plot(x, y, marker='o')    # Circles
plt.plot(x, y, marker='s')    # Squares  
plt.plot(x, y, marker='^')    # Triangles
plt.plot(x, y, marker='*')    # Stars
```

**`grid=True`** - Add grid lines
```python
plt.grid(True)              # Add grid lines
plt.grid(True, alpha=0.3)   # Add faint grid lines
plt.grid(False)             # No grid lines (default)
```

**`tight_layout()`** - Automatic spacing
```python
# Without tight_layout: labels might get cut off
plt.title('My Chart')
plt.xlabel('Long X-axis Label')
plt.show()

# With tight_layout: automatically adjusts spacing
plt.title('My Chart')
plt.xlabel('Long X-axis Label')
plt.tight_layout()  # Prevents labels from being cut off
plt.show()
```

#### Understanding Different Chart Types - When to Use

**Bar Charts** - Compare categories
```python
# Use when: Comparing different groups
# Example: Sales by product, population by city
# X-axis: Categories (products, cities)
# Y-axis: Numbers (sales, population)
```

**Line Charts** - Show trends over time
```python
# Use when: Data changes over time
# Example: Temperature over months, stock prices over days
# X-axis: Time (months, days, years)
# Y-axis: Values that change (temperature, price)
```

**Pie Charts** - Show parts of a whole
```python
# Use when: Showing percentages or proportions
# Example: Market share, budget breakdown
# Must add up to 100%
```

**Scatter Plots** - Show relationships
```python
# Use when: Looking for correlation between two variables
# Example: Height vs weight, study time vs grades
# X-axis: One variable
# Y-axis: Another variable
```

**Histograms** - Show distribution
```python
# Use when: Showing how data is spread out
# Example: Test scores, ages, heights in a group
# X-axis: Value ranges (score ranges)
# Y-axis: Count of items in each range
```

### Setting Up Matplotlib
```python
import matplotlib.pyplot as plt

# Basic chart setup
plt.figure(figsize=(10, 6))  # Set size (width, height)
plt.title('My Chart Title')
plt.xlabel('X-axis Label')
plt.ylabel('Y-axis Label')
plt.show()
```

### Chart Types Overview

Python matplotlib can create many types of charts:
- **Bar Charts**: Compare categories (sales by product)
- **Line Charts**: Show trends over time (temperature over months)
- **Pie Charts**: Show parts of a whole (market share)
- **Scatter Plots**: Show relationships between two variables
- **Histograms**: Show distribution of data
- **Box Plots**: Show data spread and outliers

## Bar Charts Examples

### Example 1: Basic Bar Chart from DataFrame
```python
import pandas as pd
import matplotlib.pyplot as plt

# Create sample data
data = {
    'City': ['New York', 'London', 'Paris', 'Tokyo', 'Sydney'],
    'Population': [8.4, 9.0, 2.2, 13.9, 5.3]
}

df = pd.DataFrame(data)

# Create bar chart
plt.figure(figsize=(10, 6))
plt.bar(df['City'], df['Population'])
plt.title('City Population (Millions)')
plt.xlabel('Cities')
plt.ylabel('Population (Millions)')
plt.xticks(rotation=45)  # Rotate x-axis labels
plt.tight_layout()  # Adjust layout
plt.show()
```

### Example 2: Horizontal Bar Chart
```python
# Same data as above
plt.figure(figsize=(10, 6))
plt.barh(df['City'], df['Population'])  # barh for horizontal
plt.title('City Population (Millions)')
plt.xlabel('Population (Millions)')
plt.ylabel('Cities')
plt.tight_layout()
plt.show()
```

### Example 3: Colored Bar Chart
```python
# Colors for each bar
colors = ['red', 'blue', 'green', 'orange', 'purple']

plt.figure(figsize)(10, 6))
plt.bar(df['City'], df['Population'], color=colors)
plt.title('City Population (Millions)')
plt.xlabel('Cities')
plt.ylabel('Population (Millions)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

## Line Charts

### Example 1: Basic Line Chart
```python
# Sample data: temperature over months
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
temperature = [30, 35, 45, 55, 65, 75]

plt.figure(figsize=(10, 6))
plt.plot(months, temperature, marker='o')  # marker='o' adds dots
plt.title('Temperature Over Months')
plt.xlabel('Months')
plt.ylabel('Temperature (°F)')
plt.grid(True)  # Add grid lines
plt.show()
```

### Example 2: Multiple Line Chart
```python
# Compare two years
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
temp_2023 = [30, 35, 45, 55, 65, 75]
temp_2024 = [28, 38, 48, 58, 68, 78]

plt.figure(figsize=(10, 6))
plt.plot(months, temp_2023, marker='o', label='2023')
plt.plot(months, temp_2024, marker='s', label='2024')
plt.title('Temperature Comparison')
plt.xlabel('Months')
plt.ylabel('Temperature (°F)')
plt.legend()  # Show legend
plt.grid(True)
plt.show()
```

## Pie Charts

### Example 1: Basic Pie Chart
```python
# Market share data
companies = ['Apple', 'Samsung', 'Google', 'Others']
market_share = [35, 25, 15, 25]

plt.figure(figsize=(8, 8))
plt.pie(market_share, labels=companies, autopct='%1.1f%%')
plt.title('Smartphone Market Share')
plt.show()
```

### Example 2: Exploded Pie Chart
```python
# Explode one slice to highlight it
explode = (0.1, 0, 0, 0)  # Explode first slice

plt.figure(figsize=(8, 8))
plt.pie(market_share, labels=companies, autopct='%1.1f%%', 
        explode=explode, colors=['lightblue', 'lightgreen', 'lightyellow', 'lightcoral'])
plt.title('Smartphone Market Share')
plt.show()
```

## Scatter Plots

### Example 1: Basic Scatter Plot
```python
# Sample data: height vs weight
height = [160, 165, 170, 175, 180, 185, 190]
weight = [55, 60, 65, 70, 75, 80, 85]

plt.figure(figsize=(8, 6))
plt.scatter(height, weight)
plt.title('Height vs Weight')
plt.xlabel('Height (cm)')
plt.ylabel('Weight (kg)')
plt.grid(True)
plt.show()
```

### Example 2: Colored Scatter Plot
```python
# Add colors based on gender
height = [160, 165, 170, 175, 180, 185, 190]
weight = [55, 60, 65, 70, 75, 80, 85]
gender = ['F', 'F', 'M', 'M', 'M', 'M', 'M']

# Create colors list
colors = ['red' if g == 'F' else 'blue' for g in gender]

plt.figure(figsize=(8, 6))
plt.scatter(height, weight, c=colors, alpha=0.7)
plt.title('Height vs Weight by Gender')
plt.xlabel('Height (cm)')
plt.ylabel('Weight (kg)')
plt.grid(True)
plt.show()
```

## Histograms

### Example 1: Basic Histogram
```python
import numpy as np

# Generate random test scores
np.random.seed(42)  # For reproducible results
scores = np.random.normal(75, 15, 100)  # Mean=75, std=15, 100 students

plt.figure(figsize=(8, 6))
plt.hist(scores, bins=10, color='skyblue', edgecolor='black')
plt.title('Distribution of Test Scores')
plt.xlabel('Scores')
plt.ylabel('Number of Students')
plt.grid(True, alpha=0.3)
plt.show()
```

### Example 2: Multiple Histograms
```python
# Compare two classes
class_a = np.random.normal(80, 10, 50)
class_b = np.random.normal(75, 12, 50)

plt.figure(figsize=(10, 6))
plt.hist(class_a, bins=15, alpha=0.7, label='Class A', color='blue')
plt.hist(class_b, bins=15, alpha=0.7, label='Class B', color='red')
plt.title('Score Distribution Comparison')
plt.xlabel('Scores')
plt.ylabel('Frequency')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

## Box Plots

### Example 1: Basic Box Plot
```python
# Sample data: test scores for different subjects
math_scores = [78, 85, 92, 88, 76, 95, 89, 82, 90, 87]
science_scores = [82, 79, 88, 91, 85, 77, 93, 86, 89, 84]
english_scores = [85, 88, 79, 92, 87, 83, 90, 86, 88, 91]

data = [math_scores, science_scores, english_scores]
labels = ['Math', 'Science', 'English']

plt.figure(figsize=(8, 6))
plt.boxplot(data, labels=labels)
plt.title('Score Distribution by Subject')
plt.ylabel('Scores')
plt.grid(True, alpha=0.3)
plt.show()
```

## Subplots (Multiple Charts)

### Example: Dashboard with Multiple Charts
```python
# Create sample data
df = pd.read_csv('sales_data.csv')

# Create 2x2 subplot grid
fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# Chart 1: Bar chart
axes[0, 0].bar(df['Product'], df['Sales'])
axes[0, 0].set_title('Sales by Product')
axes[0, 0].tick_params(axis='x', rotation=45)

# Chart 2: Line chart
axes[0, 1].plot(df['Product'], df['Price'], marker='o')
axes[0, 1].set_title('Price by Product')
axes[0, 1].tick_params(axis='x', rotation=45)

# Chart 3: Pie chart
axes[1, 0].pie(df['Sales'], labels=df['Product'], autopct='%1.1f%%')
axes[1, 0].set_title('Sales Distribution')

# Chart 4: Scatter plot
axes[1, 1].scatter(df['Price'], df['Sales'])
axes[1, 1].set_title('Price vs Sales')
axes[1, 1].set_xlabel('Price')
axes[1, 1].set_ylabel('Sales')

plt.tight_layout()
plt.show()
```

### Example 4: Chart from CSV Data
```python
# Read CSV and create chart
df = pd.read_csv('sales_data.csv')

plt.figure(figsize=(12, 6))
plt.bar(df['Product'], df['Sales'])
plt.title('Product Sales')
plt.xlabel('Products')
plt.ylabel('Sales (units)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Example 5: Multiple Bar Charts (Grouped)
```python
# Sample data with multiple categories
data = {
    'Month': ['Jan', 'Feb', 'Mar', 'Apr'],
    'Sales_2023': [100, 120, 140, 110],
    'Sales_2024': [110, 130, 160, 120]
}

df = pd.DataFrame(data)

# Create grouped bar chart
x = range(len(df['Month']))
width = 0.35

plt.figure(figsize=(10, 6))
plt.bar([i - width/2 for i in x], df['Sales_2023'], width, label='2023')
plt.bar([i + width/2 for i in x], df['Sales_2024'], width, label='2024')

plt.title('Monthly Sales Comparison')
plt.xlabel('Months')
plt.ylabel('Sales')
plt.xticks(x, df['Month'])
plt.legend()
plt.tight_layout()
plt.show()
```

### Example 6: Chart with Data Labels
```python
# Add values on top of bars
plt.figure(figsize=(10, 6))
bars = plt.bar(df['Product'], df['Sales'])

# Add data labels on bars
for bar in bars:
    height = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2., height,
             f'{height}', ha='center', va='bottom')

plt.title('Product Sales with Labels')
plt.xlabel('Products')
plt.ylabel('Sales (units)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

## Complete Example: CSV to Chart

### Step-by-Step Example
```python
import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Create sample CSV data
student_data = {
    'Student': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Math': [85, 92, 78, 96, 88],
    'Science': [90, 85, 92, 89, 94],
    'English': [88, 79, 85, 92, 87]
}

df = pd.DataFrame(student_data)
df.to_csv('student_grades.csv', index=False)
print("CSV file created!")

# Step 2: Read CSV file
df = pd.read_csv('student_grades.csv')
print("\nFirst 3 rows:")
print(df.head(3))

# Step 3: Basic table operations
print(f"\nTable shape: {df.shape}")
print(f"Average Math score: {df['Math'].mean():.1f}")
print(f"Highest Science score: {df['Science'].max()}")

# Step 4: Create bar chart for Math scores
plt.figure(figsize=(10, 6))
plt.bar(df['Student'], df['Math'])
plt.title('Student Math Scores')
plt.xlabel('Students')
plt.ylabel('Math Scores')
plt.ylim(0, 100)  # Set y-axis range
plt.tight_layout()
plt.show()

# Step 5: Create chart for all subjects
subjects = ['Math', 'Science', 'English']
x = range(len(df['Student']))
width = 0.25

plt.figure(figsize=(12, 6))
for i, subject in enumerate(subjects):
    plt.bar([j + i * width for j in x], df[subject], 
            width, label=subject)

plt.title('Student Scores by Subject')
plt.xlabel('Students')
plt.ylabel('Scores')
plt.xticks([i + width for i in x], df['Student'])
plt.legend()
plt.ylim(0, 100)
plt.tight_layout()
plt.show()
```

## Simple Data Analysis Example

```python
# Read sales data
df = pd.read_csv('sales_data.csv')

# Basic analysis
print("=== SALES ANALYSIS ===")
print(f"Total products: {len(df)}")
print(f"Total sales: {df['Sales'].sum()} units")
print(f"Average sales: {df['Sales'].mean():.1f} units")
print(f"Best selling product: {df.loc[df['Sales'].idxmax(), 'Product']}")

# Create summary chart
plt.figure(figsize=(12, 8))

# Subplot 1: Sales by product
plt.subplot(2, 2, 1)
plt.bar(df['Product'], df['Sales'], color='skyblue')
plt.title('Sales by Product')
plt.xticks(rotation=45)

# Subplot 2: Price by product
plt.subplot(2, 2, 2)
plt.bar(df['Product'], df['Price'], color='lightcoral')
plt.title('Price by Product')
plt.xticks(rotation=45)

# Subplot 3: Total value
plt.subplot(2, 2, 3)
total_value = df['Sales'] * df['Price']
plt.bar(df['Product'], total_value, color='lightgreen')
plt.title('Total Revenue by Product')
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

## Summary

**Tables with Pandas:**
- Create tables with `pd.DataFrame()`
- View data with `.head()`, `.tail()`, `.info()`
- Access columns with `df['column_name']`
- Filter with conditions like `df[df['column'] > value]`

**CSV Files:**
- Read with `pd.read_csv('filename.csv')`
- Save with `df.to_csv('filename.csv')`
- Always check data with `.head()` after reading

**Bar Charts:**
- Use `plt.bar()` for vertical bars
- Use `plt.barh()` for horizontal bars
- Add titles with `plt.title()`
- Add labels with `plt.xlabel()` and `plt.ylabel()`
- Show chart with `plt.show()`

**Required Libraries:**
- `pandas` for tables and CSV files
- `matplotlib.pyplot` for charts
- Install with `pip install pandas matplotlib`

**Best Practices:**
- Always use `plt.figure(figsize=(width, height))` to set chart size
- Use `plt.tight_layout()` to prevent overlapping
- Use `plt.xticks(rotation=45)` for long labels
- Add colors and labels to make charts more readable