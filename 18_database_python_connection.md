# Connecting MySQL Database to Python for Data Analysis

## Why Connect Databases to Python?

When working with data, we often need to:
- **Analyze large datasets** that are stored in databases
- **Perform calculations** and statistics that go beyond SQL capabilities
- **Create visualizations** like charts and graphs
- **Build machine learning models** using real data
- **Automate reports** by combining database data with Python's analysis tools

Think of it this way: Your database (MySQL) is like a warehouse storing all your data, while Python is like a powerful calculator and visualization tool. Connecting them lets you use the best of both worlds!

## Step 1: Add Sample Data in TablePlus

First, let's create a simple database with some data. Open TablePlus and run this SQL:

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS school_data;
USE school_data;

-- Create a students table
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    grade DECIMAL(3,1),
    subject VARCHAR(50),
    attendance_percent INT
);

-- Insert sample data
INSERT INTO students (name, age, grade, subject, attendance_percent) VALUES
('Alice Johnson', 20, 85.5, 'Computer Science', 95),
('Bob Smith', 21, 78.0, 'Mathematics', 88),
('Carol White', 19, 92.3, 'Computer Science', 97),
('David Brown', 22, 88.7, 'Physics', 91),
('Emma Davis', 20, 95.0, 'Mathematics', 99),
('Frank Miller', 21, 72.5, 'Physics', 82),
('Grace Wilson', 19, 89.8, 'Computer Science', 94),
('Henry Taylor', 22, 76.4, 'Mathematics', 85),
('Iris Martinez', 20, 91.2, 'Physics', 96),
('Jack Anderson', 21, 83.6, 'Computer Science', 90);
```

## Step 2: Install MySQL Connector in Anaconda

Open Anaconda Prompt (Windows) or Terminal (Mac/Linux) and run:

```bash
conda install mysql-connector-python
```

Type 'y' when asked to proceed with installation.

## Step 3: Connect Database to Python

Open Spyder in Anaconda and create a new Python file. Here's the general connection format:

```python
import mysql.connector
import pandas as pd

# General connection format
conn = mysql.connector.connect(
    host="localhost",           # Database location (usually localhost)
    user="your_username",       # Your MySQL username
    password="your_password",   # Your MySQL password
    database="your_db_name"     # Name of your database
)

# Load data from database into pandas DataFrame
df = pd.read_sql("SELECT * FROM your_table", conn)

# Always close connection when done
conn.close()
```

**⚠️ You MUST replace these placeholders with your actual information:**
- `"your_username"` → Replace with `"root"` (or your MySQL username)
- `"your_password"` → Replace with the password you set for MySQL
- `"your_db_name"` → Replace with your database name (like `"school_data"`)
- `"your_table"` → Replace with your table name (like `"students"`)

### Example with our school database:

```python
import mysql.connector
import pandas as pd

# Actual connection with real values
conn = mysql.connector.connect(
    host="localhost",
    user="root",                 # Using root as username
    password="your_password",    # Put YOUR actual MySQL password here!
    database="school_data"       # The database we created in Step 1
)

# Load the students table
df = pd.read_sql("SELECT * FROM students", conn)
conn.close()

# Check if data loaded correctly
print("Data loaded successfully!")
print(df.head())
```

## Step 4: Simple Data Analysis Example

Now let's analyze our student data:

```python
import mysql.connector
import pandas as pd
import matplotlib.pyplot as plt

# Connect to database
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",  # Your MySQL password here
    database="school_data"
)

# Load data
df = pd.read_sql("SELECT * FROM students", conn)
conn.close()

# 1. Basic Statistics
print("=== BASIC STATISTICS ===")
print(f"Average Grade: {df['grade'].mean():.2f}")
print(f"Highest Grade: {df['grade'].max():.2f}")
print(f"Average Attendance: {df['attendance_percent'].mean():.1f}%")
print()

# 2. Group by Subject
print("=== AVERAGE GRADE BY SUBJECT ===")
subject_avg = df.groupby('subject')['grade'].mean()
print(subject_avg.round(2))
print()

# 3. Find Top Performers (grade > 90)
print("=== TOP PERFORMERS ===")
top_students = df[df['grade'] > 90]
print(top_students[['name', 'grade', 'subject']])
print()

# 4. Create a Simple Bar Chart
subject_counts = df['subject'].value_counts()
subject_counts.plot(kind='bar', title='Students per Subject')
plt.ylabel('Number of Students')
plt.xlabel('Subject')
plt.tight_layout()
plt.show()

# 5. Correlation Analysis
print("=== CORRELATION ===")
correlation = df['attendance_percent'].corr(df['grade'])
print(f"Correlation between Attendance and Grade: {correlation:.2f}")
if correlation > 0.5:
    print("Strong positive correlation - better attendance relates to better grades!")
```

## What You Just Learned

✅ **Database Connection:** You connected MySQL to Python using `mysql.connector`  
✅ **Data Import:** You loaded database tables into pandas DataFrames  
✅ **Analysis:** You performed statistics, grouping, and filtering on real database data  
✅ **Visualization:** You created charts from database data  

## Common Issues & Solutions

| Problem | Solution |
|---------|----------|
| "Access denied for user" | Check your password is correct |
| "Unknown database" | Make sure you created the database in TablePlus |
| "Module not found" | Run the conda install command again |
| Connection timeout | Make sure MySQL is running in TablePlus |

## Next Steps

Now that you can connect your database to Python, you can:

**Query any data:** Pull any table or specific records from your database into Python.

**Advanced analysis:** Use NumPy, SciPy, and Scikit-learn for complex statistics and calculations.

**Create visualizations:** Make charts and graphs with Matplotlib or Seaborn.

**Build reports:** Generate automated reports combining database queries with Python analysis.

**Machine learning:** Train models to predict patterns using your database.

**Automation:** Schedule scripts to run automatically and update reports.

Remember: Database stores, Python analyzes! 🚀

## Next Steps - Code Examples

Here are simple examples showing what you can do by combining MySQL with Python:

### 1. Query Any Data
```python
import mysql.connector
import pandas as pd

conn = mysql.connector.connect(
    host="localhost", user="root", 
    password="your_password", database="school_data"
)

# Query specific students with conditions
high_performers = pd.read_sql("""
    SELECT name, grade, subject 
    FROM students 
    WHERE grade > 85 AND attendance_percent > 90
""", conn)

print("High Performers with Good Attendance:")
print(high_performers)
conn.close()
```

### 2. Advanced Analysis with NumPy & SciPy
```python
import numpy as np
from scipy import stats

# After loading your data...
conn = mysql.connector.connect(
    host="localhost", user="root",
    password="your_password", database="school_data"
)
df = pd.read_sql("SELECT * FROM students", conn)
conn.close()

# Statistical analysis
grades = df['grade'].values
attendance = df['attendance_percent'].values

# Calculate statistics that SQL can't do easily
std_deviation = np.std(grades)
percentile_75 = np.percentile(grades, 75)
correlation_test = stats.pearsonr(attendance, grades)

print(f"Grade Standard Deviation: {std_deviation:.2f}")
print(f"75th Percentile Grade: {percentile_75:.2f}")
print(f"Correlation Test p-value: {correlation_test[1]:.4f}")
```

### 3. Create Professional Visualizations
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
conn = mysql.connector.connect(
    host="localhost", user="root",
    password="your_password", database="school_data"
)
df = pd.read_sql("SELECT * FROM students", conn)
conn.close()

# Create a nice visualization
plt.figure(figsize=(10, 5))

# Subplot 1: Box plot by subject
plt.subplot(1, 2, 1)
df.boxplot(column='grade', by='subject')
plt.title('Grade Distribution by Subject')
plt.suptitle('')  # Remove default title

# Subplot 2: Scatter plot
plt.subplot(1, 2, 2)
plt.scatter(df['attendance_percent'], df['grade'], alpha=0.6)
plt.xlabel('Attendance %')
plt.ylabel('Grade')
plt.title('Attendance vs Grade')

plt.tight_layout()
plt.show()
```

### 4. Build Automated Reports
```python
from datetime import datetime

# Connect and analyze
conn = mysql.connector.connect(
    host="localhost", user="root",
    password="your_password", database="school_data"
)
df = pd.read_sql("SELECT * FROM students", conn)
conn.close()

# Generate report
report_date = datetime.now().strftime("%Y-%m-%d")
report = f"""
STUDENT PERFORMANCE REPORT - {report_date}
{'='*40}
Total Students: {len(df)}
Average Grade: {df['grade'].mean():.2f}
Average Attendance: {df['attendance_percent'].mean():.1f}%

TOP 3 STUDENTS:
{df.nlargest(3, 'grade')[['name', 'grade']].to_string(index=False)}

SUBJECTS SUMMARY:
{df.groupby('subject')['grade'].agg(['mean', 'min', 'max']).round(2).to_string()}
"""

# Save report to file
with open(f'report_{report_date}.txt', 'w') as f:
    f.write(report)
    
print("Report generated!")
print(report)
```


## Important Notes

- **Install required libraries**: Some examples need additional libraries. Install them with:
  ```bash
  conda install numpy scipy scikit-learn matplotlib seaborn
  pip install schedule --break-system-packages
  ```

- **Start simple**: Begin with examples 1-3, then try the advanced ones

- **Modify for your needs**: These are templates - change them to fit your specific data and requirements

- **Always close connections**: Notice how every example closes the database connection after use
