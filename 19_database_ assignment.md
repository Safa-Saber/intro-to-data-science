# Database & Python Homework Assignment

## Part 1: Create Your Database

Open TablePlus and run this SQL code to create a database with employee records:

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS company_data;
USE company_data;

-- Create employees table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100),
    department VARCHAR(50),
    age INT,
    years_experience INT,
    salary DECIMAL(10,2),
    performance_score INT,
    projects_completed INT
);

-- Insert 70 employee records
INSERT INTO employees (name, department, age, years_experience, salary, performance_score, projects_completed) VALUES
('Emma Wilson', 'Sales', 28, 3, 45000.00, 85, 12),
('James Brown', 'IT', 35, 10, 75000.00, 92, 28),
('Olivia Davis', 'Marketing', 26, 2, 42000.00, 78, 8),
('William Miller', 'Sales', 41, 15, 68000.00, 88, 35),
('Sophia Garcia', 'HR', 29, 4, 48000.00, 82, 15),
('Michael Rodriguez', 'IT', 33, 8, 70000.00, 95, 25),
('Isabella Martinez', 'Marketing', 27, 3, 44000.00, 80, 10),
('Alexander Lopez', 'Finance', 38, 12, 72000.00, 87, 30),
('Charlotte Gonzalez', 'Sales', 30, 5, 52000.00, 90, 18),
('Daniel Hernandez', 'IT', 36, 11, 78000.00, 93, 32),
('Amelia Smith', 'Marketing', 25, 1, 38000.00, 75, 5),
('Matthew Johnson', 'HR', 32, 7, 55000.00, 84, 20),
('Emily Anderson', 'Finance', 34, 9, 65000.00, 86, 22),
('David Taylor', 'Sales', 29, 4, 48000.00, 83, 14),
('Sofia Thomas', 'IT', 31, 6, 62000.00, 91, 21),
('Joseph Moore', 'Marketing', 28, 3, 43000.00, 77, 9),
('Mia Jackson', 'HR', 37, 11, 60000.00, 85, 26),
('Henry Martin', 'Finance', 40, 14, 74000.00, 89, 33),
('Ava Lee', 'Sales', 26, 2, 41000.00, 79, 7),
('Samuel White', 'IT', 34, 9, 72000.00, 94, 27),
('Harper Harris', 'Marketing', 29, 4, 46000.00, 81, 11),
('Benjamin Clark', 'HR', 35, 10, 58000.00, 83, 24),
('Evelyn Lewis', 'Finance', 31, 6, 56000.00, 85, 19),
('Lucas Walker', 'Sales', 27, 3, 44000.00, 82, 10),
('Abigail Hall', 'IT', 39, 13, 80000.00, 96, 38),
('Mason Allen', 'Marketing', 30, 5, 48000.00, 78, 13),
('Elizabeth Young', 'HR', 33, 8, 54000.00, 86, 21),
('Ethan King', 'Finance', 36, 11, 68000.00, 88, 28),
('Avery Wright', 'Sales', 25, 1, 38000.00, 76, 4),
('Jacob Scott', 'IT', 32, 7, 65000.00, 90, 23),
('Lily Green', 'Marketing', 28, 3, 42000.00, 79, 8),
('Michael Baker', 'HR', 38, 12, 62000.00, 87, 29),
('Ella Hill', 'Finance', 29, 4, 50000.00, 84, 16),
('William Adams', 'Sales', 31, 6, 53000.00, 85, 17),
('Grace Nelson', 'IT', 35, 10, 73000.00, 92, 30),
('James Carter', 'Marketing', 27, 2, 40000.00, 77, 6),
('Chloe Mitchell', 'HR', 30, 5, 51000.00, 83, 15),
('Logan Roberts', 'Finance', 37, 11, 69000.00, 87, 31),
('Aria Turner', 'Sales', 26, 2, 40000.00, 78, 6),
('Ryan Phillips', 'IT', 33, 8, 68000.00, 91, 26),
('Scarlett Campbell', 'Marketing', 29, 4, 45000.00, 80, 10),
('Noah Parker', 'HR', 34, 9, 57000.00, 85, 22),
('Victoria Evans', 'Finance', 32, 7, 59000.00, 86, 20),
('Dylan Edwards', 'Sales', 28, 3, 46000.00, 81, 11),
('Zoe Collins', 'IT', 36, 11, 76000.00, 93, 34),
('Nathan Stewart', 'Marketing', 31, 6, 49000.00, 82, 14),
('Layla Sanchez', 'HR', 27, 2, 42000.00, 79, 7),
('Hunter Morris', 'Finance', 39, 13, 71000.00, 88, 32),
('Hannah Reed', 'Sales', 30, 5, 50000.00, 84, 16),
('Christian Cook', 'IT', 34, 9, 70000.00, 90, 28),
('Nora Bailey', 'Marketing', 25, 1, 37000.00, 75, 3),
('Jordan Bell', 'HR', 35, 10, 59000.00, 86, 25),
('Luna Murphy', 'Finance', 33, 8, 62000.00, 85, 21),
('Isaiah Rivera', 'Sales', 29, 4, 47000.00, 82, 13),
('Madison Cooper', 'IT', 37, 12, 77000.00, 94, 36),
('Adrian Richardson', 'Marketing', 28, 3, 43000.00, 78, 9),
('Penelope Cox', 'HR', 31, 6, 53000.00, 84, 18),
('Julian Howard', 'Finance', 36, 11, 67000.00, 87, 29),
('Aubrey Ward', 'Sales', 27, 2, 42000.00, 80, 8),
('Wyatt Torres', 'IT', 32, 7, 66000.00, 89, 24),
('Addison Peterson', 'Marketing', 30, 5, 47000.00, 81, 12),
('Gabriel Gray', 'HR', 38, 12, 61000.00, 86, 27),
('Lucy Ramirez', 'Finance', 28, 3, 48000.00, 83, 11),
('Jaxon Watson', 'Sales', 34, 9, 58000.00, 87, 23),
('Eleanor Brooks', 'IT', 40, 14, 82000.00, 95, 40),
('Lincoln Kelly', 'Marketing', 26, 2, 41000.00, 76, 5),
('Lillian Sanders', 'HR', 32, 7, 54000.00, 85, 19),
('Hudson Price', 'Finance', 35, 10, 64000.00, 86, 26),
('Stella Bennett', 'Sales', 31, 6, 51000.00, 83, 15),
('Easton Wood', 'IT', 29, 4, 58000.00, 88, 17);
```

## Part 2: Python Analysis Tasks

Complete the following tasks in Spyder. Write your code in a single Python file called `homework_solution.py`.

### Task 1: Connect to Database
Connect to your database and load all employee data into a pandas DataFrame. Print the first 5 rows to verify connection.

### Task 2: Basic Calculations
Calculate and print the following:
- Average salary of all employees
- Maximum and minimum salary
- Average age by department
- Total number of employees in each department

### Task 3: Data Filtering
Find and print:
- All employees with salary > 60000
- Employees in IT department with performance score > 90
- Count how many employees have more than 5 years experience

### Task 4: Create Visualizations
Create the following graphs (use matplotlib):

#### Graph 1: Bar Chart
Create a bar chart showing average salary by department

#### Graph 2: Scatter Plot
Create a scatter plot showing relationship between years_experience (x-axis) and salary (y-axis)

#### Graph 3: Subplots
Create a figure with 2 subplots side by side:
- Left: Histogram of employee ages
- Right: Pie chart of employees per department

## Submission Requirements

Submit your `homework_solution.py` file containing all the code for Tasks 1-4. Make sure your code:
- Runs without errors
- Has comments explaining what each section does
- Prints clear output for each task
- Creates all required visualizations

## Grading Rubric

| Task | Points |
|------|--------|
| Task 1: Database Connection | 25 |
| Task 2: Basic Calculations | 25 |
| Task 3: Data Filtering | 25 |
| Task 4: Visualizations | 25 |
| **Total** | **100** |

## Tips
- Remember to replace `"your_password"` with your actual MySQL password
- Use `print()` statements to clearly separate each task's output
- Add titles to your graphs using `plt.title()`
- Don't forget to close your database connection when done
- Test your code section by section before running everything

Good luck!
