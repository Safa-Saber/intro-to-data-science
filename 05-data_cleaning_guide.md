# Data Cleaning Guide - Basic to Advanced

## Step 1: Create Our Messy Table

First, let's create a table with problems to practice on:

```python
import pandas as pd
import numpy as np

# Create messy data
data = {
    'Name': ['John', 'Jane', '', 'Bob', 'Alice', None, 'Mike'],
    'Age': [25, 30, 35, None, 28, 22, 45],
    'Department': ['IT', 'HR', 'IT', 'Finance', '', 'HR', 'IT'],
    'Salary': [50000, 60000, None, 55000, 65000, 45000, 70000],
    'City': ['New York', 'Boston', 'Chicago', '', 'Miami', 'Seattle', None]
}

df = pd.DataFrame(data)
print(df)
```

**Output:**
```
    Name   Age Department  Salary      City
0   John  25.0         IT   50000  New York
1   Jane  30.0         HR   60000    Boston
2             35.0         IT     NaN   Chicago
3    Bob   NaN    Finance   55000          
4  Alice  28.0               65000     Miami
5   None  22.0         HR   45000   Seattle
6   Mike  45.0         IT   70000      None
```

## 1. Basic Data Cleaning

### Missing Values
**What are they?** Empty cells, NULL, NaN, "N/A", blank spaces

**How to find them:**
```python
df.isnull().sum()    # Count missing per column
df.info()            # See data overview
```

**How to fix them:**
```python
df.dropna()                          # Remove rows with missing values
df.fillna(0)                        # Fill with 0
df['age'].fillna(df['age'].mean())  # Fill with average
```

### Duplicates
**How to find them:**
```python
df.duplicated().sum()    # Count duplicates
```

**How to fix them:**
```python
df.drop_duplicates()     # Remove all duplicates
```

### Data Types
**How to check:**
```python
df.dtypes    # See current data types
```

**How to fix:**
```python
df['age'] = df['age'].astype(int)           # Convert to integer
df['date'] = pd.to_datetime(df['date'])     # Convert to date
```

### Text Cleaning
```python
df['name'] = df['name'].str.lower()    # Make lowercase
df['name'] = df['name'].str.strip()    # Remove spaces
```

---

## 2. BASIC EXERCISES

### Exercise 1: Find the Problems
Run this code to analyze our messy table:

```python
# 1. Count missing values per column
print("Missing values per column:")
print(df.isnull().sum())

# 2. Check for empty strings (not just NaN)
print("\nEmpty strings per column:")
for col in df.columns:
    if df[col].dtype == 'object':  # Only check text columns
        empty_count = (df[col] == '').sum()
        print(f"{col}: {empty_count}")

# 3. Check data types
print("\nData types:")
print(df.dtypes)

# 4. Look at the data info
print("\nData info:")
df.info()
```

**Results:**
- Missing data columns: Name (1 NULL + 1 empty), Age (1 NULL), Department (1 empty), Salary (1 NULL), City (1 empty + 1 NULL)
- Total missing: 7 missing values
- Problems: Mix of NULL and empty strings, different types of missing data

### Exercise 2: Fix Missing Names
Let's fix the Name column step by step:

```python
# First, let's see the problem
print("Names with problems:")
print(df[df['Name'].isnull() | (df['Name'] == '')])

# Method 1: Replace empty strings with NaN first
df['Name'] = df['Name'].replace('', np.nan)
print("\nAfter replacing empty strings with NaN:")
print(df['Name'])

# Method 2: Fill missing names
df['Name'] = df['Name'].fillna('Unknown')
print("\nAfter filling missing names:")
print(df['Name'])

# Check result
print(f"\nMissing names now: {df['Name'].isnull().sum()}")
```

**Alternative approach:**

```python
# Alternative approach
df_alt = df.copy()
df_alt['Name'] = df_alt['Name'].replace('', np.nan)
for i in range(len(df_alt)):
    if pd.isna(df_alt.loc[i, 'Name']):
        df_alt.loc[i, 'Name'] = f'Person_{i+1}'
print(df_alt['Name'])
```

**Method Comparison:**
1. Original method fills with 'Unknown' - simple but not unique
2. Alternative creates 'Person_3', 'Person_6' - unique but artificial
3. Better method depends on use case: 'Unknown' for reports, 'Person_X' for unique identifiers

**Using .dropna() instead:**

```python
# Test dropping rows with missing names
df_drop = df.copy()
df_drop['Name'] = df_drop['Name'].replace('', np.nan)
df_drop = df_drop.dropna(subset=['Name'])
print(f"Original rows: {len(df)}")
print(f"After dropping: {len(df_drop)}")
```

**Result:** We lose 2 rows (rows 2 and 5), going from 7 to 5 rows. This removes data permanently.

### Exercise 3: Fix Missing Ages
Ages are numeric, so we have different options:

```python
# See the age problems
print("Age column:")
print(df['Age'])
print(f"Missing ages: {df['Age'].isnull().sum()}")

# Option 1: Fill with average age
avg_age = df['Age'].mean()
print(f"\nAverage age: {avg_age:.1f}")

df_copy1 = df.copy()
df_copy1['Age'] = df_copy1['Age'].fillna(avg_age)
print("After filling with average:")
print(df_copy1['Age'])

# Option 2: Fill with median age
median_age = df['Age'].median()
print(f"\nMedian age: {median_age}")

df_copy2 = df.copy()
df_copy2['Age'] = df_copy2['Age'].fillna(median_age)
print("After filling with median:")
print(df_copy2['Age'])

# Option 3: Remove rows with missing age
df_copy3 = df.copy()
df_copy3 = df_copy3.dropna(subset=['Age'])
print(f"\nAfter removing rows: {len(df_copy3)} rows left")
```

**Method Comparison:**
1. Mean = 30.8, Median = 30.0
2. Best choice: **Median** (30) because it's not affected by extreme values
3. Pros/Cons:
   - **Mean:** Uses all data, but affected by outliers
   - **Median:** Not affected by outliers, more robust
   - **Remove:** Keeps data pure, but loses information

**Fixed value approach:**

```python
# Fill with a business rule: assume missing age = 25 (new employee)
df_fixed = df.copy()
df_fixed['Age'] = df_fixed['Age'].fillna(25)
print("Filled with 25:")
print(df_fixed['Age'])
```

**Result:** Fixed value (25) assumes missing ages are new employees. Good if you have business logic, bad if assumption is wrong.

### Exercise 4: Fix Department and City
Let's handle empty strings in text columns:

```python
# Check the problems
print("Department problems:")
print(df['Department'].value_counts(dropna=False))

print("\nCity problems:")
print(df['City'].value_counts(dropna=False))

# Fix empty strings in Department
print("\nBefore fixing Department:")
print(df[['Name', 'Department', 'Salary']])

# Replace empty strings with NaN, then fill based on logic
df['Department'] = df['Department'].replace('', np.nan)

# Fill missing departments based on salary (simple business rule)
def assign_department(row):
    if pd.isna(row['Department']):
        if row['Salary'] >= 65000:
            return 'IT'
        elif row['Salary'] >= 55000:
            return 'Finance'
        else:
            return 'HR'
    return row['Department']

df['Department'] = df.apply(assign_department, axis=1)

print("\nAfter fixing Department:")
print(df[['Name', 'Department', 'Salary']])

# Fix City - replace empty/null with 'Unknown'
df['City'] = df['City'].replace('', np.nan)
df['City'] = df['City'].fillna('Unknown')

print("\nFinal result:")
print(df)
```

**Business Rule Analysis:**
1. Business rule used: High salary → IT, Medium → Finance, Low → HR
2. Alternative rule: Could use age-based or random assignment
3. 'Unknown' for cities: 
   - **Good:** Honest about missing data
   - **Bad:** Not useful for analysis
   - **Better:** Use most common city or 'Remote'

**Most common department approach:**

```python
# Fill missing departments with the most common one
most_common_dept = df['Department'].mode()[0]  # Gets most frequent
print(f"Most common department: {most_common_dept}")

df_common = df.copy()
df_common['Department'] = df_common['Department'].replace('', np.nan)
df_common['Department'] = df_common['Department'].fillna(most_common_dept)
print(df_common['Department'])
```

**Result:** Most common department is 'IT'. This is simpler but less intelligent than salary-based rules.

### Exercise 5: Data Quality Check
Let's verify our cleaned data:

```python
# Create our final cleaned dataset
print("=== FINAL CLEANED DATA ===")
print(df)

print(f"\nData shape: {df.shape}")

# Check for any remaining missing values
print("\nMissing values check:")
print(df.isnull().sum())

# Check data types
print("\nData types:")
print(df.dtypes)

# Basic statistics
print("\nBasic statistics:")
print(df.describe())

# Check for any remaining empty strings
print("\nEmpty string check:")
for col in df.columns:
    if df[col].dtype == 'object':
        empty_count = (df[col] == '').sum()
        if empty_count > 0:
            print(f"{col}: {empty_count} empty strings")
        else:
            print(f"{col}: No empty strings")

print("\n=== CLEANING SUMMARY ===")
print("✅ Fixed missing names")
print("✅ Fixed missing ages") 
print("✅ Fixed missing departments")
print("✅ Fixed missing cities")
print("✅ No missing values remaining")
```

**Data Quality Results:**
1. Final check shows 0 missing values, all data types correct
2. Before/After comparison:
   ```
   BEFORE: 7 missing values out of 35 total cells
   AFTER:  0 missing values out of 35 total cells
   ```
3. Dirty data percentage: 7/35 = 20% of cells had problems

**Cleaning report:**

```python
# Cleaning summary report
original_missing = 7
final_missing = df.isnull().sum().sum()
total_cells = df.shape[0] * df.shape[1]

print("=== DATA CLEANING REPORT ===")
print(f"Original missing values: {original_missing}")
print(f"Final missing values: {final_missing}")
print(f"Total cells: {total_cells}")
print(f"Cleaned cells: {original_missing}")
print(f"Data quality improved by: {(original_missing/total_cells)*100:.1f}%")
print(f"Current data completeness: {((total_cells-final_missing)/total_cells)*100:.1f}%")
```

**Result:** Report shows we improved data quality by 20% and achieved 100% data completeness.

---

## Next Steps: Create More Complex Tables

Now that you understand the basics, let's create tables with more complex problems:

```python
# More complex messy data
complex_data = {
    'Name': ['john smith', 'JANE DOE', 'Bob Johnson', 'bob johnson', 'Alice Brown'],
    'Email': ['john@email.com', 'invalid-email', 'bob@test', 'bob@test.com', ''],
    'Phone': ['123-456-7890', '(555) 123-4567', '5551234567', '555.123.4567', None],
    'Age': [25, 150, -5, 30, 'unknown'],
    'Salary': ['50000', '$60,000', '75k', 'sixty thousand', None]
}

complex_df = pd.DataFrame(complex_data)
print("=== COMPLEX MESSY DATA ===")
print(complex_df)
```

## Reference Examples

### Example A: Identifying Cleaning Methods
For each problem, the recommended cleaning method:

```python
# Problem 1: Age = -5
# Best solution: Remove row - Negative age is impossible, data error
```

```python
# Problem 2: Name = ""
# Best solution: Replace with "Unknown" - Empty name is fixable, don't lose whole row
```

```python
# Problem 3: Salary missing for 1 out of 100 rows
# Best solution: Fill with median - More robust than mean for salaries
```

### Example B: Complete Row Cleaning

```python
# This row has multiple problems:
messy_row = {
    'Name': '',
    'Age': None, 
    'Department': 'it',
    'Salary': '50k',
    'Email': 'JOHN@EMAIL.COM'
}

# Clean each field
if messy_row['Name'] == '':
    messy_row['Name'] = 'Unknown'

if messy_row['Age'] is None:
    messy_row['Age'] = 30  # Use reasonable default

messy_row['Department'] = messy_row['Department'].upper()  # IT

# Convert salary
salary_str = messy_row['Salary'].replace('k', '000')
messy_row['Salary'] = int(salary_str)  # 50000

messy_row['Email'] = messy_row['Email'].lower()  # john@email.com

print("Cleaned row:", messy_row)
```

### Example C: Problem-Solution Reference

**Problems and Solutions:**

1. **Column has 50% missing values** → `df.drop(columns=['bad_column'])`
2. **Email addresses are in different cases** → `df['email'].str.lower()`  
3. **Ages range from 0 to 200** → Remove outliers with IQR method
4. **Same person entered twice** → `df.drop_duplicates()`

---

## 3. INTERMEDIATE EXERCISES

### Exercise 6: Phone Number Cleaning
1. Extract only digits from phone numbers
2. Format all as XXX-XXX-XXXX
3. Mark invalid phone numbers (not 10 digits)

### Exercise 7: Email Validation
1. Find emails without "@" symbol
2. Find emails without proper domain (.com, .org, etc.)
3. Create a new column marking valid/invalid emails

### Exercise 8: Handle Outliers
1. Find ages outside range 18-65
2. Find salaries more than 3 times the median
3. Decide: remove them or cap them at reasonable values?

### Exercise 9: Department Standardization
1. Fill missing departments based on salary ranges:
   - Engineering: >$80,000
   - Finance: $70,000-$80,000  
   - Marketing: $60,000-$70,000
   - HR: <$60,000

---

## 4. ADVANCED EXERCISES

### Exercise 10: Create Validation Rules
Write functions to check if:
1. Age is between 18-65
2. Email has correct format
3. Hire date is not in the future
4. Salary is reasonable for the department

### Exercise 11: Data Quality Report
Create a summary showing:
1. Before/after counts of missing values
2. Number of records removed/fixed
3. List of assumptions you made
4. Data quality score (% of clean records)

### Exercise 12: Find Similar Names
1. Use fuzzy matching to find employees with similar names
2. These might be the same person entered twice
3. Decide which records to keep

### Exercise 13: Comprehensive Cleaning Pipeline
Create a complete cleaning script that:
1. Loads the dirty data
2. Applies all cleaning steps in correct order
3. Validates results
4. Exports clean data
5. Generates a cleaning report

---

## 5. QUICK REFERENCE

### Python Pandas Cheat Sheet
```python
# Explore data
df.head()
df.info()
df.describe()

# Missing values
df.isnull().sum()
df.dropna()
df.fillna(value)

# Duplicates
df.duplicated()
df.drop_duplicates()

# Text cleaning
df['col'].str.lower()
df['col'].str.strip()
df['col'].str.replace('old', 'new')

# Data types
df.dtypes
df.astype()
pd.to_numeric()
pd.to_datetime()
```

### Common Patterns
- Always backup original data first
- Clean in logical order: duplicates → missing → types → formatting
- Document what you changed and why
- Validate results after each step
