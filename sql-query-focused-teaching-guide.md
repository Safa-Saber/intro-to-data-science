# SQL Query Mastery: Learn by Doing

## Introduction
This guide focuses on learning SQL queries through practice. We'll create simple tables with basic constraints, load them with data, and then practice hundreds of queries from simple to complex.

---

## Part 1: Create Simple Tables

```sql
-- 1. Students table (basic info)
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT CHECK (age >= 5 AND age <= 25),
    gender VARCHAR(10),
    city VARCHAR(50),
    grade INT CHECK (grade >= 1 AND grade <= 12),
    gpa DECIMAL(3,2) CHECK (gpa >= 0 AND gpa <= 4),
    enrollment_date DATE
);

-- 2. Teachers table
CREATE TABLE teachers (
    teacher_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    subject VARCHAR(50),
    salary DECIMAL(10,2),
    hire_date DATE,
    department VARCHAR(50)
);

-- 3. Courses table
CREATE TABLE courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100) NOT NULL,
    teacher_id INT,
    credits INT,
    department VARCHAR(50),
    room_number VARCHAR(10)
);

-- 4. Enrollments table (which student takes which course)
CREATE TABLE enrollments (
    enrollment_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    midterm_score DECIMAL(5,2),
    final_score DECIMAL(5,2),
    grade VARCHAR(2)
);

-- 5. Clubs table
CREATE TABLE clubs (
    club_id INT PRIMARY KEY AUTO_INCREMENT,
    club_name VARCHAR(100) NOT NULL,
    advisor_teacher_id INT,
    meeting_day VARCHAR(20),
    room VARCHAR(10),
    budget DECIMAL(10,2)
);

-- 6. Club_members table
CREATE TABLE club_members (
    membership_id INT PRIMARY KEY AUTO_INCREMENT,
    club_id INT,
    student_id INT,
    join_date DATE,
    role VARCHAR(50)
);
```

---

## Part 2: Insert Sample Data

```sql
-- Insert Students (30 students)
INSERT INTO students (first_name, last_name, age, gender, city, grade, gpa, enrollment_date) VALUES
('Ali', 'Ahmed', 16, 'Male', 'Cairo', 11, 3.75, '2022-09-01'),
('Sara', 'Hassan', 15, 'Female', 'Cairo', 10, 3.92, '2022-09-01'),
('Omar', 'Khalil', 17, 'Male', 'Alexandria', 12, 3.45, '2021-09-01'),
('Fatima', 'Noor', 14, 'Female', 'Giza', 9, 3.88, '2023-09-01'),
('Hassan', 'Saeed', 16, 'Male', 'Cairo', 11, 3.22, '2022-09-01'),
('Layla', 'Rashid', 15, 'Female', 'Alexandria', 10, 3.95, '2022-09-01'),
('Ahmed', 'Farouk', 17, 'Male', 'Luxor', 12, 3.67, '2021-09-01'),
('Zahra', 'Amin', 14, 'Female', 'Cairo', 9, 3.55, '2023-09-01'),
('Youssef', 'Hamza', 16, 'Male', 'Aswan', 11, 3.78, '2022-09-01'),
('Maryam', 'Salem', 15, 'Female', 'Cairo', 10, 3.91, '2022-09-01'),
('Khalid', 'Omar', 18, 'Male', 'Giza', 12, 3.15, '2021-09-01'),
('Aisha', 'Ibrahim', 14, 'Female', 'Cairo', 9, 3.83, '2023-09-01'),
('Mahmoud', 'Ali', 16, 'Male', 'Alexandria', 11, 3.41, '2022-09-01'),
('Nadia', 'Younis', 15, 'Female', 'Cairo', 10, 3.72, '2022-09-01'),
('Tariq', 'Mansour', 17, 'Male', 'Giza', 12, 3.58, '2021-09-01'),
('Hana', 'Karim', 14, 'Female', 'Luxor', 9, 3.96, '2023-09-01'),
('Bilal', 'Zayed', 16, 'Male', 'Cairo', 11, 3.29, '2022-09-01'),
('Salma', 'Adel', 15, 'Female', 'Alexandria', 10, 3.87, '2022-09-01'),
('Karim', 'Fawzy', 17, 'Male', 'Cairo', 12, 3.64, '2021-09-01'),
('Dina', 'Hossam', 14, 'Female', 'Aswan', 9, 3.81, '2023-09-01'),
('Rami', 'Sherif', 16, 'Male', 'Cairo', 11, 3.52, '2022-09-01'),
('Yasmin', 'Gamal', 15, 'Female', 'Giza', 10, 3.69, '2022-09-01'),
('Faris', 'Nabil', 18, 'Male', 'Cairo', 12, 3.33, '2021-09-01'),
('Lina', 'Mostafa', 14, 'Female', 'Alexandria', 9, 3.90, '2023-09-01'),
('Samir', 'Fouad', 16, 'Male', 'Cairo', 11, 3.48, '2022-09-01'),
('Rana', 'Tamer', 15, 'Female', 'Luxor', 10, 3.76, '2022-09-01'),
('Waleed', 'Anwar', 17, 'Male', 'Cairo', 12, 3.61, '2021-09-01'),
('Noura', 'Khaled', 14, 'Female', 'Giza', 9, 3.85, '2023-09-01'),
('Mazen', 'Hisham', 16, 'Male', 'Alexandria', 11, 3.44, '2022-09-01'),
('Jana', 'Wael', 15, 'Female', 'Cairo', 10, 3.79, '2022-09-01');

-- Insert Teachers (12 teachers)
INSERT INTO teachers (first_name, last_name, subject, salary, hire_date, department) VALUES
('Mohammad', 'Aziz', 'Mathematics', 55000, '2015-08-15', 'Mathematics'),
('Amira', 'Fahmy', 'English', 48000, '2018-09-01', 'English'),
('Khaled', 'Sharif', 'Physics', 62000, '2012-01-10', 'Science'),
('Leila', 'Habib', 'Chemistry', 58000, '2016-03-20', 'Science'),
('Tarek', 'Zaki', 'History', 52000, '2019-07-01', 'Social Studies'),
('Huda', 'Nasr', 'Biology', 54000, '2017-11-05', 'Science'),
('Saeed', 'Rashed', 'Arabic', 45000, '2020-02-15', 'Languages'),
('Mona', 'Sami', 'Geography', 50000, '2014-09-10', 'Social Studies'),
('Ibrahim', 'Khoury', 'Computer Science', 60000, '2013-06-01', 'Technology'),
('Dalia', 'Abbas', 'Art', 42000, '2021-01-20', 'Arts'),
('Wassim', 'Hamdi', 'Mathematics', 57000, '2011-08-01', 'Mathematics'),
('Rania', 'Morsi', 'English', 49000, '2019-09-15', 'English');

-- Insert Courses (20 courses)
INSERT INTO courses (course_name, teacher_id, credits, department, room_number) VALUES
('Algebra II', 1, 3, 'Mathematics', 'A101'),
('English Literature', 2, 3, 'English', 'B201'),
('Physics I', 3, 4, 'Science', 'LAB1'),
('Chemistry Basics', 4, 4, 'Science', 'LAB2'),
('World History', 5, 3, 'Social Studies', 'C301'),
('Biology', 6, 4, 'Science', 'LAB3'),
('Arabic Language', 7, 3, 'Languages', 'D101'),
('Geography', 8, 2, 'Social Studies', 'C302'),
('Programming Basics', 9, 3, 'Technology', 'COMP1'),
('Art Fundamentals', 10, 2, 'Arts', 'ART1'),
('Calculus I', 11, 4, 'Mathematics', 'A102'),
('Creative Writing', 12, 2, 'English', 'B202'),
('Physics II', 3, 4, 'Science', 'LAB1'),
('Organic Chemistry', 4, 4, 'Science', 'LAB2'),
('Ancient History', 5, 3, 'Social Studies', 'C303'),
('Geometry', 1, 3, 'Mathematics', 'A103'),
('Web Development', 9, 3, 'Technology', 'COMP2'),
('English Grammar', 2, 2, 'English', 'B203'),
('Environmental Science', 6, 3, 'Science', 'LAB4'),
('Statistics', 11, 3, 'Mathematics', 'A104');

-- Insert Enrollments (100 enrollments - students taking various courses)
INSERT INTO enrollments (student_id, course_id, enrollment_date, midterm_score, final_score, grade) VALUES
(1, 1, '2024-09-01', 85.5, 88.0, 'B+'),
(1, 2, '2024-09-01', 92.0, 89.5, 'A-'),
(1, 3, '2024-09-01', 78.0, 82.0, 'B-'),
(2, 1, '2024-09-01', 95.0, 98.0, 'A+'),
(2, 4, '2024-09-01', 88.5, 91.0, 'A-'),
(2, 5, '2024-09-01', 93.0, 95.5, 'A'),
(3, 11, '2024-09-01', 72.0, 75.5, 'C'),
(3, 13, '2024-09-01', 80.0, 85.0, 'B'),
(4, 6, '2024-09-01', 87.0, 90.0, 'A-'),
(4, 10, '2024-09-01', 91.0, 93.0, 'A'),
(5, 1, '2024-09-01', 68.0, 72.0, 'C-'),
(5, 2, '2024-09-01', 75.0, 78.0, 'C+'),
(6, 16, '2024-09-01', 94.0, 96.0, 'A'),
(6, 3, '2024-09-01', 92.5, 95.5, 'A'),
(7, 11, '2024-09-01', 82.0, 86.0, 'B'),
(7, 15, '2024-09-01', 88.0, 85.5, 'B+'),
(8, 7, '2024-09-01', 79.0, 81.0, 'B-'),
(8, 10, '2024-09-01', 83.0, 85.0, 'B'),
(9, 1, '2024-09-01', 86.5, 88.5, 'B+'),
(9, 4, '2024-09-01', 89.0, 91.0, 'A-'),
(10, 2, '2024-09-01', 92.0, 94.0, 'A'),
(10, 18, '2024-09-01', 90.5, 92.5, 'A-'),
(11, 11, '2024-09-01', 65.0, 68.0, 'D+'),
(11, 14, '2024-09-01', 70.0, 72.0, 'C-'),
(12, 6, '2024-09-01', 90.0, 88.0, 'B+'),
(12, 8, '2024-09-01', 85.0, 87.5, 'B+'),
(13, 16, '2024-09-01', 75.0, 77.0, 'C+'),
(13, 5, '2024-09-01', 78.0, 80.0, 'B-'),
(14, 1, '2024-09-01', 86.0, 88.0, 'B+'),
(14, 12, '2024-09-01', 84.5, 82.0, 'B'),
(15, 13, '2024-09-01', 78.5, 80.0, 'B-'),
(15, 3, '2024-09-01', 81.0, 83.5, 'B'),
(16, 7, '2024-09-01', 96.0, 98.5, 'A+'),
(16, 6, '2024-09-01', 94.0, 96.0, 'A'),
(17, 1, '2024-09-01', 70.0, 73.0, 'C'),
(17, 12, '2024-09-01', 72.0, 74.5, 'C'),
(18, 2, '2024-09-01', 91.0, 89.0, 'A-'),
(18, 19, '2024-09-01', 88.5, 90.5, 'A-'),
(19, 11, '2024-09-01', 85.0, 83.0, 'B'),
(19, 15, '2024-09-01', 82.0, 86.0, 'B'),
(20, 8, '2024-09-01', 87.0, 85.0, 'B+'),
(20, 9, '2024-09-01', 84.0, 86.0, 'B'),
(21, 1, '2024-09-01', 77.0, 79.0, 'C+'),
(21, 4, '2024-09-01', 80.0, 82.0, 'B-'),
(22, 2, '2024-09-01', 83.0, 85.0, 'B'),
(22, 18, '2024-09-01', 81.0, 83.0, 'B'),
(23, 11, '2024-09-01', 71.0, 69.0, 'D+'),
(23, 13, '2024-09-01', 73.0, 75.0, 'C'),
(24, 6, '2024-09-01', 93.0, 91.0, 'A-'),
(24, 19, '2024-09-01', 90.0, 92.0, 'A-'),
(25, 16, '2024-09-01', 76.0, 78.0, 'C+'),
(25, 5, '2024-09-01', 79.0, 81.0, 'B-'),
(26, 1, '2024-09-01', 88.0, 86.0, 'B+'),
(26, 12, '2024-09-01', 85.0, 87.0, 'B+'),
(27, 11, '2024-09-01', 81.0, 84.0, 'B'),
(27, 14, '2024-09-01', 83.0, 85.0, 'B'),
(28, 7, '2024-09-01', 91.0, 89.0, 'A-'),
(28, 8, '2024-09-01', 88.0, 90.0, 'A-'),
(29, 16, '2024-09-01', 74.0, 76.0, 'C+'),
(29, 9, '2024-09-01', 77.0, 79.0, 'C+'),
(30, 2, '2024-09-01', 89.0, 91.0, 'A-'),
(30, 18, '2024-09-01', 87.0, 89.0, 'B+'),
(1, 5, '2024-09-01', 83.0, 85.0, 'B'),
(2, 8, '2024-09-01', 91.0, 93.0, 'A'),
(3, 9, '2024-09-01', 77.0, 79.0, 'C+'),
(4, 7, '2024-09-01', 89.0, 91.0, 'A-'),
(5, 10, '2024-09-01', 71.0, 73.0, 'C'),
(6, 11, '2024-09-01', 95.0, 97.0, 'A+'),
(7, 4, '2024-09-01', 84.0, 86.0, 'B'),
(8, 12, '2024-09-01', 82.0, 84.0, 'B'),
(9, 6, '2024-09-01', 88.0, 90.0, 'A-'),
(10, 3, '2024-09-01', 93.0, 95.0, 'A');

-- Insert Clubs
INSERT INTO clubs (club_name, advisor_teacher_id, meeting_day, room, budget) VALUES
('Math Club', 1, 'Monday', 'A201', 5000),
('Science Club', 3, 'Tuesday', 'LAB5', 8000),
('Drama Club', 10, 'Wednesday', 'AUD1', 10000),
('Debate Club', 2, 'Thursday', 'B301', 3000),
('Chess Club', 11, 'Friday', 'C201', 2000),
('Photography Club', 10, 'Monday', 'ART2', 6000),
('Robotics Club', 9, 'Tuesday', 'COMP3', 15000),
('Music Club', 10, 'Wednesday', 'MUS1', 7000);

-- Insert Club Members
INSERT INTO club_members (club_id, student_id, join_date, role) VALUES
(1, 1, '2024-09-15', 'President'),
(1, 2, '2024-09-15', 'Vice President'),
(1, 5, '2024-09-16', 'Member'),
(1, 9, '2024-09-16', 'Treasurer'),
(2, 3, '2024-09-15', 'President'),
(2, 4, '2024-09-15', 'Secretary'),
(2, 6, '2024-09-16', 'Member'),
(2, 15, '2024-09-17', 'Member'),
(3, 10, '2024-09-15', 'President'),
(3, 14, '2024-09-16', 'Member'),
(3, 18, '2024-09-16', 'Member'),
(4, 2, '2024-09-15', 'Captain'),
(4, 7, '2024-09-16', 'Member'),
(4, 19, '2024-09-17', 'Member'),
(5, 11, '2024-09-15', 'President'),
(5, 13, '2024-09-16', 'Member'),
(5, 17, '2024-09-17', 'Member'),
(6, 8, '2024-09-15', 'President'),
(6, 16, '2024-09-16', 'Member'),
(7, 9, '2024-09-15', 'Team Lead'),
(7, 20, '2024-09-16', 'Member'),
(7, 25, '2024-09-17', 'Member'),
(8, 12, '2024-09-15', 'President'),
(8, 22, '2024-09-16', 'Member');
```

---

## Part 3: SQL Queries - From Basic to Advanced

### Level 1: Basic SELECT Queries

```sql
-- 1. Select all students
SELECT * FROM students;

-- 2. Select specific columns
SELECT first_name, last_name, gpa FROM students;

-- 3. Select with WHERE condition
SELECT first_name, last_name, gpa 
FROM students 
WHERE gpa > 3.5;

-- 4. Multiple conditions with AND
SELECT first_name, last_name, age, gpa 
FROM students 
WHERE age >= 15 AND gpa > 3.7;

-- 5. Using OR condition
SELECT first_name, last_name, city 
FROM students 
WHERE city = 'Cairo' OR city = 'Alexandria';

-- 6. Using IN operator
SELECT first_name, last_name, city 
FROM students 
WHERE city IN ('Cairo', 'Giza', 'Luxor');

-- 7. Using NOT IN
SELECT first_name, last_name, city 
FROM students 
WHERE city NOT IN ('Cairo', 'Alexandria');

-- 8. Using BETWEEN
SELECT first_name, last_name, age 
FROM students 
WHERE age BETWEEN 15 AND 17;

-- 9. Using LIKE for pattern matching
SELECT first_name, last_name 
FROM students 
WHERE first_name LIKE 'A%';  -- Names starting with A

-- 10. LIKE with different patterns
SELECT first_name, last_name 
FROM students 
WHERE last_name LIKE '%ed';  -- Names ending with 'ed'

-- 11. Find names containing 'am'
SELECT first_name, last_name 
FROM students 
WHERE first_name LIKE '%am%';

-- 12. Using IS NULL
SELECT * FROM enrollments 
WHERE grade IS NULL;

-- 13. Using IS NOT NULL
SELECT * FROM enrollments 
WHERE grade IS NOT NULL;

-- 14. Combining multiple conditions
SELECT first_name, last_name, age, gpa, city 
FROM students 
WHERE (city = 'Cairo' OR city = 'Giza') 
  AND gpa > 3.5 
  AND age < 17;
```

### Level 2: Sorting and Limiting Results

```sql
-- 15. ORDER BY ascending
SELECT first_name, last_name, gpa 
FROM students 
ORDER BY gpa;

-- 16. ORDER BY descending
SELECT first_name, last_name, gpa 
FROM students 
ORDER BY gpa DESC;

-- 17. ORDER BY multiple columns
SELECT first_name, last_name, grade, gpa 
FROM students 
ORDER BY grade, gpa DESC;

-- 18. Top 5 students by GPA
SELECT first_name, last_name, gpa 
FROM students 
ORDER BY gpa DESC 
LIMIT 5;

-- 19. Students ranked 6-10 by GPA
SELECT first_name, last_name, gpa 
FROM students 
ORDER BY gpa DESC 
LIMIT 5 OFFSET 5;

-- 20. Youngest students
SELECT first_name, last_name, age 
FROM students 
ORDER BY age 
LIMIT 3;

-- 21. Alphabetical order
SELECT first_name, last_name 
FROM students 
ORDER BY last_name, first_name;
```

### Level 3: Aggregate Functions

```sql
-- 22. COUNT all students
SELECT COUNT(*) as total_students 
FROM students;

-- 23. COUNT with condition
SELECT COUNT(*) as high_achievers 
FROM students 
WHERE gpa >= 3.8;

-- 24. Average GPA
SELECT AVG(gpa) as average_gpa 
FROM students;

-- 25. Maximum and Minimum GPA
SELECT MAX(gpa) as highest_gpa, 
       MIN(gpa) as lowest_gpa 
FROM students;

-- 26. SUM of all credits
SELECT SUM(credits) as total_credits 
FROM courses;

-- 27. Average age by gender
SELECT gender, AVG(age) as avg_age 
FROM students 
GROUP BY gender;

-- 28. Count students by city
SELECT city, COUNT(*) as student_count 
FROM students 
GROUP BY city;

-- 29. Average GPA by grade level
SELECT grade, 
       COUNT(*) as num_students, 
       AVG(gpa) as avg_gpa 
FROM students 
GROUP BY grade;

-- 30. Statistics per city
SELECT city,
       COUNT(*) as total_students,
       AVG(gpa) as avg_gpa,
       MAX(gpa) as max_gpa,
       MIN(gpa) as min_gpa
FROM students
GROUP BY city;
```

### Level 4: GROUP BY with HAVING

```sql
-- 31. Cities with more than 5 students
SELECT city, COUNT(*) as student_count 
FROM students 
GROUP BY city 
HAVING COUNT(*) > 5;

-- 32. Grades with average GPA above 3.5
SELECT grade, AVG(gpa) as avg_gpa 
FROM students 
GROUP BY grade 
HAVING AVG(gpa) > 3.5;

-- 33. Departments with more than 3 courses
SELECT department, COUNT(*) as course_count 
FROM courses 
GROUP BY department 
HAVING COUNT(*) > 3;

-- 34. Teachers earning above average salary
SELECT first_name, last_name, salary
FROM teachers
WHERE salary > (SELECT AVG(salary) FROM teachers);

-- 35. Cities with high-performing students
SELECT city, 
       COUNT(*) as num_students,
       AVG(gpa) as avg_gpa
FROM students
GROUP BY city
HAVING AVG(gpa) > 3.6
ORDER BY avg_gpa DESC;
```

### Level 5: Basic JOINs

```sql
-- 36. Students and their courses (INNER JOIN)
SELECT s.first_name, s.last_name, c.course_name
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id;

-- 37. Courses and their teachers
SELECT c.course_name, t.first_name, t.last_name, c.room_number
FROM courses c
INNER JOIN teachers t ON c.teacher_id = t.teacher_id;

-- 38. Student enrollment details
SELECT s.first_name, s.last_name, c.course_name, e.midterm_score, e.final_score, e.grade
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id
WHERE s.student_id = 1;

-- 39. Teachers and their departments
SELECT DISTINCT t.first_name, t.last_name, t.department, t.salary
FROM teachers t
INNER JOIN courses c ON t.teacher_id = c.teacher_id
ORDER BY t.department, t.salary DESC;

-- 40. Club members and their clubs
SELECT s.first_name, s.last_name, cl.club_name, cm.role
FROM students s
INNER JOIN club_members cm ON s.student_id = cm.student_id
INNER JOIN clubs cl ON cm.club_id = cl.club_id
ORDER BY cl.club_name, cm.role;
```

### Level 6: Advanced JOINs

```sql
-- 41. LEFT JOIN - All students, even those not enrolled
SELECT s.first_name, s.last_name, COUNT(e.enrollment_id) as courses_taken
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.first_name, s.last_name;

-- 42. Students not enrolled in any course
SELECT s.first_name, s.last_name
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id
WHERE e.enrollment_id IS NULL;

-- 43. All teachers and their course count
SELECT t.first_name, t.last_name, COUNT(c.course_id) as num_courses
FROM teachers t
LEFT JOIN courses c ON t.teacher_id = c.teacher_id
GROUP BY t.teacher_id, t.first_name, t.last_name;

-- 44. Cross department teaching
SELECT t.first_name, t.last_name, t.department as teacher_dept, c.department as course_dept
FROM teachers t
INNER JOIN courses c ON t.teacher_id = c.teacher_id
WHERE t.department != c.department;

-- 45. Students in multiple clubs
SELECT s.first_name, s.last_name, COUNT(cm.club_id) as num_clubs
FROM students s
INNER JOIN club_members cm ON s.student_id = cm.student_id
GROUP BY s.student_id, s.first_name, s.last_name
HAVING COUNT(cm.club_id) > 1;
```

### Level 7: Complex Queries with Multiple JOINs

```sql
-- 46. Complete student academic report
SELECT 
    s.first_name,
    s.last_name,
    s.gpa,
    c.course_name,
    t.first_name as teacher_first,
    t.last_name as teacher_last,
    e.midterm_score,
    e.final_score,
    e.grade
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id
INNER JOIN teachers t ON c.teacher_id = t.teacher_id
WHERE s.gpa > 3.5
ORDER BY s.last_name, c.course_name;

-- 47. Department performance analysis
SELECT 
    c.department,
    COUNT(DISTINCT e.student_id) as total_students,
    AVG(e.midterm_score) as avg_midterm,
    AVG(e.final_score) as avg_final,
    COUNT(DISTINCT c.teacher_id) as num_teachers
FROM courses c
INNER JOIN enrollments e ON c.course_id = e.course_id
GROUP BY c.department
ORDER BY avg_final DESC;

-- 48. Teacher workload analysis
SELECT 
    t.first_name,
    t.last_name,
    COUNT(DISTINCT c.course_id) as courses_taught,
    COUNT(DISTINCT e.student_id) as total_students,
    AVG(e.final_score) as avg_student_score
FROM teachers t
INNER JOIN courses c ON t.teacher_id = c.teacher_id
INNER JOIN enrollments e ON c.course_id = e.course_id
GROUP BY t.teacher_id, t.first_name, t.last_name
ORDER BY total_students DESC;

-- 49. City-wise academic performance
SELECT 
    s.city,
    COUNT(DISTINCT s.student_id) as num_students,
    AVG(s.gpa) as avg_gpa,
    COUNT(DISTINCT e.course_id) as total_courses_taken,
    AVG(e.final_score) as avg_final_score
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.city
HAVING num_students > 2
ORDER BY avg_gpa DESC;

-- 50. Club popularity by grade
SELECT 
    s.grade,
    cl.club_name,
    COUNT(cm.student_id) as member_count
FROM clubs cl
INNER JOIN club_members cm ON cl.club_id = cm.club_id
INNER JOIN students s ON cm.student_id = s.student_id
GROUP BY s.grade, cl.club_name
ORDER BY s.grade, member_count DESC;
```

### Level 8: Subqueries

```sql
-- 51. Students with above-average GPA
SELECT first_name, last_name, gpa
FROM students
WHERE gpa > (SELECT AVG(gpa) FROM students);

-- 52. Highest paid teacher in each department
SELECT first_name, last_name, department, salary
FROM teachers t1
WHERE salary = (
    SELECT MAX(salary) 
    FROM teachers t2 
    WHERE t2.department = t1.department
);

-- 53. Students performing above course average
SELECT 
    s.first_name,
    s.last_name,
    c.course_name,
    e.final_score
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id
WHERE e.final_score > (
    SELECT AVG(e2.final_score)
    FROM enrollments e2
    WHERE e2.course_id = e.course_id
);

-- 54. Courses with enrollment above average
SELECT 
    c.course_name,
    COUNT(e.student_id) as enrollment_count
FROM courses c
INNER JOIN enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name
HAVING COUNT(e.student_id) > (
    SELECT AVG(enrollment_count)
    FROM (
        SELECT COUNT(student_id) as enrollment_count
        FROM enrollments
        GROUP BY course_id
    ) as avg_table
);

-- 55. Students in the most popular club
SELECT s.first_name, s.last_name
FROM students s
INNER JOIN club_members cm ON s.student_id = cm.student_id
WHERE cm.club_id = (
    SELECT club_id
    FROM club_members
    GROUP BY club_id
    ORDER BY COUNT(*) DESC
    LIMIT 1
);
```

### Level 9: UNION, INTERSECT, and Set Operations

```sql
-- 56. All people in the school (students and teachers)
SELECT first_name, last_name, 'Student' as role
FROM students
UNION
SELECT first_name, last_name, 'Teacher' as role
FROM teachers
ORDER BY last_name, first_name;

-- 57. High achievers (GPA > 3.8 OR Final Score > 95 in any course)
SELECT DISTINCT s.first_name, s.last_name
FROM students s
WHERE s.gpa > 3.8
UNION
SELECT DISTINCT s.first_name, s.last_name
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
WHERE e.final_score > 95;

-- 58. Students in both Math Club and Science Club
SELECT s.first_name, s.last_name
FROM students s
INNER JOIN club_members cm ON s.student_id = cm.student_id
INNER JOIN clubs c ON cm.club_id = c.club_id
WHERE c.club_name = 'Math Club'
  AND s.student_id IN (
    SELECT s2.student_id
    FROM students s2
    INNER JOIN club_members cm2 ON s2.student_id = cm2.student_id
    INNER JOIN clubs c2 ON cm2.club_id = c2.club_id
    WHERE c2.club_name = 'Science Club'
);
```

### Level 10: Advanced Analytical Queries

```sql
-- 59. Ranking students by GPA
SELECT 
    first_name,
    last_name,
    gpa,
    RANK() OVER (ORDER BY gpa DESC) as gpa_rank
FROM students;

-- 60. Top 3 students per grade
SELECT * FROM (
    SELECT 
        first_name,
        last_name,
        grade,
        gpa,
        ROW_NUMBER() OVER (PARTITION BY grade ORDER BY gpa DESC) as rank_in_grade
    FROM students
) ranked
WHERE rank_in_grade <= 3;

-- 61. Running total of enrollments
SELECT 
    enrollment_date,
    COUNT(*) as daily_enrollments,
    SUM(COUNT(*)) OVER (ORDER BY enrollment_date) as cumulative_enrollments
FROM enrollments
GROUP BY enrollment_date;

-- 62. Performance trend analysis
SELECT 
    s.first_name,
    s.last_name,
    c.course_name,
    e.midterm_score,
    e.final_score,
    e.final_score - e.midterm_score as improvement,
    CASE 
        WHEN e.final_score - e.midterm_score > 5 THEN 'Improved'
        WHEN e.final_score - e.midterm_score < -5 THEN 'Declined'
        ELSE 'Stable'
    END as trend
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id
ORDER BY improvement DESC;

-- 63. Comprehensive student profile
WITH student_stats AS (
    SELECT 
        s.student_id,
        COUNT(e.course_id) as courses_taken,
        AVG(e.final_score) as avg_score,
        MAX(e.final_score) as best_score,
        MIN(e.final_score) as worst_score
    FROM students s
    LEFT JOIN enrollments e ON s.student_id = e.student_id
    GROUP BY s.student_id
),
club_participation AS (
    SELECT 
        student_id,
        COUNT(club_id) as clubs_joined,
        GROUP_CONCAT(role) as roles
    FROM club_members
    GROUP BY student_id
)
SELECT 
    s.first_name,
    s.last_name,
    s.gpa,
    s.city,
    COALESCE(ss.courses_taken, 0) as courses_taken,
    COALESCE(ss.avg_score, 0) as avg_score,
    COALESCE(cp.clubs_joined, 0) as clubs_joined,
    COALESCE(cp.roles, 'None') as club_roles
FROM students s
LEFT JOIN student_stats ss ON s.student_id = ss.student_id
LEFT JOIN club_participation cp ON s.student_id = cp.student_id
ORDER BY s.gpa DESC;
```

### Level 11: CASE Statements and Conditional Logic

```sql
-- 64. Grade classification
SELECT 
    first_name,
    last_name,
    gpa,
    CASE 
        WHEN gpa >= 3.9 THEN 'Excellent'
        WHEN gpa >= 3.7 THEN 'Very Good'
        WHEN gpa >= 3.5 THEN 'Good'
        WHEN gpa >= 3.0 THEN 'Satisfactory'
        ELSE 'Needs Improvement'
    END as performance_level
FROM students
ORDER BY gpa DESC;

-- 65. Course difficulty analysis
SELECT 
    c.course_name,
    AVG(e.final_score) as avg_score,
    COUNT(e.student_id) as total_students,
    CASE 
        WHEN AVG(e.final_score) < 70 THEN 'Very Difficult'
        WHEN AVG(e.final_score) < 80 THEN 'Challenging'
        WHEN AVG(e.final_score) < 90 THEN 'Moderate'
        ELSE 'Easy'
    END as difficulty_level
FROM courses c
INNER JOIN enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name;

-- 66. Salary brackets
SELECT 
    first_name,
    last_name,
    salary,
    CASE 
        WHEN salary >= 60000 THEN 'Senior Level'
        WHEN salary >= 50000 THEN 'Mid Level'
        WHEN salary >= 40000 THEN 'Junior Level'
        ELSE 'Entry Level'
    END as salary_bracket
FROM teachers
ORDER BY salary DESC;
```

### Level 12: String Functions and Data Manipulation

```sql
-- 67. Concatenate names
SELECT 
    CONCAT(first_name, ' ', last_name) as full_name,
    UPPER(city) as city_upper,
    LENGTH(first_name) as name_length
FROM students;

-- 68. Extract initials
SELECT 
    first_name,
    last_name,
    CONCAT(LEFT(first_name, 1), '.', LEFT(last_name, 1), '.') as initials
FROM students;

-- 69. Format course codes
SELECT 
    course_name,
    room_number,
    CONCAT(UPPER(LEFT(department, 3)), '-', course_id) as course_code
FROM courses;

-- 70. Search and replace
SELECT 
    first_name,
    REPLACE(city, 'Cairo', 'Capital City') as modified_city
FROM students
WHERE city = 'Cairo';
```

### Level 13: Date Functions

```sql
-- 71. Calculate teacher tenure
SELECT 
    first_name,
    last_name,
    hire_date,
    DATEDIFF(CURDATE(), hire_date) as days_employed,
    FLOOR(DATEDIFF(CURDATE(), hire_date) / 365) as years_employed
FROM teachers;

-- 72. Enrollment timeline
SELECT 
    YEAR(enrollment_date) as year,
    MONTH(enrollment_date) as month,
    COUNT(*) as enrollments
FROM enrollments
GROUP BY YEAR(enrollment_date), MONTH(enrollment_date);

-- 73. Recent enrollments
SELECT 
    s.first_name,
    s.last_name,
    e.enrollment_date
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
WHERE e.enrollment_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
```

### Level 14: Complex Business Logic Queries

```sql
-- 74. Honor roll calculation
SELECT 
    s.first_name,
    s.last_name,
    s.gpa,
    COUNT(e.course_id) as courses,
    AVG(e.final_score) as avg_score,
    CASE 
        WHEN s.gpa >= 3.8 AND AVG(e.final_score) >= 90 THEN 'High Honors'
        WHEN s.gpa >= 3.5 AND AVG(e.final_score) >= 85 THEN 'Honors'
        ELSE 'Regular'
    END as honor_status
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.first_name, s.last_name, s.gpa
HAVING COUNT(e.course_id) >= 3;

-- 75. Department budget analysis
SELECT 
    c.department,
    COUNT(DISTINCT c.course_id) as num_courses,
    COUNT(DISTINCT c.teacher_id) as num_teachers,
    SUM(t.salary) as total_salaries,
    AVG(t.salary) as avg_salary
FROM courses c
INNER JOIN teachers t ON c.teacher_id = t.teacher_id
GROUP BY c.department
ORDER BY total_salaries DESC;

-- 76. Student risk assessment
SELECT 
    s.first_name,
    s.last_name,
    s.gpa,
    COUNT(CASE WHEN e.final_score < 70 THEN 1 END) as failing_courses,
    AVG(e.final_score) as avg_score,
    CASE 
        WHEN s.gpa < 2.5 OR COUNT(CASE WHEN e.final_score < 70 THEN 1 END) > 0 THEN 'At Risk'
        WHEN s.gpa < 3.0 THEN 'Monitor'
        ELSE 'Good Standing'
    END as status
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id
GROUP BY s.student_id, s.first_name, s.last_name, s.gpa;

-- 77. Optimal class size analysis
SELECT 
    c.course_name,
    c.credits,
    COUNT(e.student_id) as enrolled,
    AVG(e.final_score) as avg_performance,
    CASE 
        WHEN COUNT(e.student_id) <= 5 THEN 'Too Small'
        WHEN COUNT(e.student_id) BETWEEN 6 AND 15 THEN 'Optimal'
        WHEN COUNT(e.student_id) BETWEEN 16 AND 25 THEN 'Large'
        ELSE 'Overcrowded'
    END as class_size_status
FROM courses c
LEFT JOIN enrollments e ON c.course_id = e.course_id
GROUP BY c.course_id, c.course_name, c.credits;
```

### Level 15: Performance and Optimization Queries

```sql
-- 78. Find duplicate enrollments
SELECT 
    student_id,
    course_id,
    COUNT(*) as enrollment_count
FROM enrollments
GROUP BY student_id, course_id
HAVING COUNT(*) > 1;

-- 79. Identify inactive courses
SELECT 
    c.course_name,
    c.teacher_id,
    COALESCE(enrollment_count, 0) as students_enrolled
FROM courses c
LEFT JOIN (
    SELECT course_id, COUNT(*) as enrollment_count
    FROM enrollments
    GROUP BY course_id
) e ON c.course_id = e.course_id
WHERE enrollment_count IS NULL OR enrollment_count = 0;

-- 80. Data quality check
SELECT 
    'Students with missing data' as issue,
    COUNT(*) as count
FROM students
WHERE first_name IS NULL 
   OR last_name IS NULL 
   OR gpa IS NULL
UNION
SELECT 
    'Enrollments with missing scores' as issue,
    COUNT(*) as count
FROM enrollments
WHERE midterm_score IS NULL 
   OR final_score IS NULL;
```

