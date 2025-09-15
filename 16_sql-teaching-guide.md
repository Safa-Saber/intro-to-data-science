# SQL Teaching Guide: Creating Tables and Queries

## Part 1: Single Table Example

### Step 1: Create a Simple Table
```sql
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT,
    Grade VARCHAR(10)
);
```

**Explanation:**
- `StudentID` → Unique number for each student (increases automatically)
- `FirstName` and `LastName` → Student names
- `Age` → Their age
- `Grade` → Their class/level (e.g., "A", "B", "C")

### Step 2: Insert Data into the Table
```sql
INSERT INTO Students (FirstName, LastName, Age, Grade)
VALUES 
('Ali', 'Rahimi', 15, 'A'),
('Sara', 'Hosseini', 16, 'B'),
('Omar', 'Karimi', 14, 'A'),
('Layla', 'Ahmadi', 15, 'C'),
('John', 'Smith', 17, 'B');
```

### Step 3: View the Data
```sql
SELECT * FROM Students;
```

**Result:**
| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| 1 | Ali | Rahimi | 15 | A |
| 2 | Sara | Hosseini | 16 | B |
| 3 | Omar | Karimi | 14 | A |
| 4 | Layla | Ahmadi | 15 | C |
| 5 | John | Smith | 17 | B |

---

## Part 2: Multiple Tables with Relationships

### Step 1: Create Tables
```sql
-- Students table
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT
);

-- Courses table
CREATE TABLE Courses (
    CourseID INT AUTO_INCREMENT PRIMARY KEY,
    CourseName VARCHAR(100),
    TeacherName VARCHAR(50)
);

-- Enrollments table (connects Students and Courses)
CREATE TABLE Enrollments (
    EnrollmentID INT AUTO_INCREMENT PRIMARY KEY,
    StudentID INT,
    CourseID INT,
    Grade VARCHAR(5),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```

### Step 2: Insert Data

#### Add Students
```sql
INSERT INTO Students (FirstName, LastName, Age) VALUES
('Ali', 'Rahimi', 15),
('Sara', 'Hosseini', 16),
('Omar', 'Karimi', 14),
('Layla', 'Ahmadi', 15);
```

#### Add Courses
```sql
INSERT INTO Courses (CourseName, TeacherName) VALUES
('Mathematics', 'Mr. Khan'),
('English', 'Ms. Fatima'),
('Science', 'Dr. Ali');
```

#### Add Enrollments (which student takes which course + grade)
```sql
INSERT INTO Enrollments (StudentID, CourseID, Grade) VALUES
(1, 1, 'A'),   -- Ali takes Mathematics
(1, 2, 'B'),   -- Ali takes English
(2, 1, 'A'),   -- Sara takes Mathematics
(2, 3, 'A'),   -- Sara takes Science
(3, 2, 'C'),   -- Omar takes English
(4, 3, 'B');   -- Layla takes Science
```

---

## Part 3: Simple SELECT Queries (Start Here!)

### Basic Queries - One Table at a Time

#### 1. Show all students
```sql
SELECT * FROM Students;
```
This shows everything in the Students table.

#### 2. Show all courses
```sql
SELECT * FROM Courses;
```
This shows everything in the Courses table.

#### 3. Show only student names (not everything)
```sql
SELECT FirstName, LastName FROM Students;
```
Sometimes we don't need all columns, just specific ones!

#### 4. Find students who are 15 years old
```sql
SELECT * FROM Students 
WHERE Age = 15;
```
**Result:** Shows Ali and Layla (both age 15)

#### 5. Find students older than 14
```sql
SELECT * FROM Students 
WHERE Age > 14;
```
**Result:** Shows Ali, Sara, and Layla

#### 6. Find students with Grade 'A'
```sql
SELECT FirstName, LastName, Grade 
FROM Students 
WHERE Grade = 'A';
```
(Note: This only works with our first single table example)

#### 7. Find courses taught by teachers whose name starts with 'Mr'
```sql
SELECT * FROM Courses 
WHERE TeacherName LIKE 'Mr%';
```
**Result:** Shows Mathematics (taught by Mr. Khan)

#### 8. Order students by age (youngest first)
```sql
SELECT * FROM Students 
ORDER BY Age;
```
Shows students from youngest to oldest.

#### 9. Order students by age (oldest first)
```sql
SELECT * FROM Students 
ORDER BY Age DESC;
```
DESC means "descending" - from highest to lowest.

#### 10. Find students whose name contains 'a'
```sql
SELECT * FROM Students 
WHERE FirstName LIKE '%a%';
```
The % symbol means "anything can be here"

#### 11. Count how many students we have
```sql
SELECT COUNT(*) AS TotalStudents 
FROM Students;
```
**Result:** Shows 4

#### 12. Find the youngest age in our class
```sql
SELECT MIN(Age) AS YoungestAge 
FROM Students;
```
**Result:** Shows 14

#### 13. Find the oldest age in our class
```sql
SELECT MAX(Age) AS OldestAge 
FROM Students;
```
**Result:** Shows 16

---

## Part 4: Understanding JOINs

### What is a JOIN?

Imagine you have:
- 📚 **One notebook** with student names and their ages
- 📖 **Another notebook** with course names and teachers
- 📝 **A third notebook** that says which student is in which course

A **JOIN** is like opening all three notebooks at once and creating one big list that shows everything together!

### Why do we need JOINs?

Without JOIN, you'd have to:
1. Look at the Enrollments table (see StudentID = 1, CourseID = 1)
2. Go to Students table to find out StudentID 1 is "Ali"
3. Go to Courses table to find out CourseID 1 is "Mathematics"

With JOIN, the computer does all this matching for you instantly!

### Your First JOIN Query

#### Show student names with their courses
```sql
SELECT 
    Students.FirstName, 
    Students.LastName, 
    Courses.CourseName, 
    Enrollments.Grade
FROM Enrollments
JOIN Students ON Enrollments.StudentID = Students.StudentID
JOIN Courses ON Enrollments.CourseID = Courses.CourseID;
```

**Let's break this down:**
- `FROM Enrollments` - Start with the enrollments notebook
- `JOIN Students ON...` - Connect it with the Students notebook using StudentID as the "glue"
- `JOIN Courses ON...` - Also connect it with the Courses notebook using CourseID as the "glue"
- Now we can see student names AND course names together!

**Result:**
| FirstName | LastName | CourseName | Grade |
|-----------|----------|------------|-------|
| Ali | Rahimi | Mathematics | A |
| Ali | Rahimi | English | B |
| Sara | Hosseini | Mathematics | A |
| Sara | Hosseini | Science | A |
| Omar | Karimi | English | C |
| Layla | Ahmadi | Science | B |

### More JOIN Examples

#### Find all students taking Mathematics
```sql
SELECT 
    Students.FirstName, 
    Students.LastName
FROM Enrollments
JOIN Students ON Enrollments.StudentID = Students.StudentID
JOIN Courses ON Enrollments.CourseID = Courses.CourseID
WHERE Courses.CourseName = 'Mathematics';
```
**Result:** Shows Ali and Sara

#### Find what courses Ali is taking
```sql
SELECT 
    Students.FirstName,
    Courses.CourseName,
    Enrollments.Grade
FROM Enrollments
JOIN Students ON Enrollments.StudentID = Students.StudentID
JOIN Courses ON Enrollments.CourseID = Courses.CourseID
WHERE Students.FirstName = 'Ali';
```
**Result:** Shows Mathematics (A) and English (B)

---

## Part 5: Counting and Grouping

### Count how many students are in each course
```sql
SELECT 
    Courses.CourseName,
    COUNT(Enrollments.StudentID) AS StudentCount
FROM Courses
LEFT JOIN Enrollments ON Courses.CourseID = Enrollments.CourseID
GROUP BY Courses.CourseName;
```

**What's happening here?**
- We're counting students
- We're grouping them by course
- It's like asking: "How many kids are in Math class? How many in English?"

**Result:**
| CourseName | StudentCount |
|------------|--------------|
| Mathematics | 2 |
| English | 2 |
| Science | 2 |

### Show each student's course count
```sql
SELECT 
    Students.FirstName,
    Students.LastName,
    COUNT(Enrollments.CourseID) AS NumberOfCourses
FROM Students
LEFT JOIN Enrollments ON Students.StudentID = Enrollments.StudentID
GROUP BY Students.StudentID;
```

**Result:**
| FirstName | LastName | NumberOfCourses |
|-----------|----------|-----------------|
| Ali | Rahimi | 2 |
| Sara | Hosseini | 2 |
| Omar | Karimi | 1 |
| Layla | Ahmadi | 1 |

---

## Part 6: Updating Data

### Update a student's grade
```sql
UPDATE Enrollments 
SET Grade = 'B' 
WHERE StudentID = 3 AND CourseID = 2;
```
This changes Omar's English grade from C to B

### Add a new student
```sql
INSERT INTO Students (FirstName, LastName, Age) 
VALUES ('Maya', 'Zaidi', 16);
```

### Delete a student (be careful!)
```sql
DELETE FROM Students 
WHERE StudentID = 5;
```
This removes the student completely

