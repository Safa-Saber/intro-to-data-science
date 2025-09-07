# Student Exam Data Analysis Assignment

## Objective
Learn data cleaning, statistical analysis, and visualization using pandas, matplotlib, and seaborn with student exam score data.

## Required Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## Dataset
Use the following student exam data organized by school:

```python
school_data = {
    'Lincoln High': [
        {'Student': 'Alice', 'Math': '85', 'Science': '78', 'English': '92', 'Average': '85.0', 'Grade': 'B'},
        {'Student': 'Bob', 'Math': '72', 'Science': '89', 'English': '76', 'Average': '79.0', 'Grade': 'C'},
        {'Student': 'Charlie', 'Math': '95', 'Science': '91', 'English': '88', 'Average': '91.3', 'Grade': 'A'},
        {'Student': 'Diana', 'Math': '68', 'Science': '74', 'English': '82', 'Average': '74.7', 'Grade': 'C'},
        {'Student': 'Eva', 'Math': '88', 'Science': '85', 'English': '90', 'Average': '87.7', 'Grade': 'B'},
    ],
    'Roosevelt Academy': [
        {'Student': 'Frank', 'Math': '79', 'Science': '83', 'English': '75', 'Average': '79.0', 'Grade': 'C'},
        {'Student': 'Grace', 'Math': '93', 'Science': '96', 'English': '89', 'Average': '92.7', 'Grade': 'A'},
        {'Student': 'Henry', 'Math': '81', 'Science': '77', 'English': '84', 'Average': '80.7', 'Grade': 'B'},
        {'Student': 'Iris', 'Math': '65', 'Science': '71', 'English': '69', 'Average': '68.3', 'Grade': 'D'},
        {'Student': 'Jack', 'Math': '87', 'Science': '82', 'English': '91', 'Average': '86.7', 'Grade': 'B'},
    ],
    'Washington Prep': [
        {'Student': 'Kate', 'Math': '90', 'Science': '88', 'English': '93', 'Average': '90.3', 'Grade': 'A'},
        {'Student': 'Leo', 'Math': '76', 'Science': '79', 'English': '73', 'Average': '76.0', 'Grade': 'C'},
        {'Student': 'Mia', 'Math': '82', 'Science': '86', 'English': '80', 'Average': '82.7', 'Grade': 'B'},
        {'Student': 'Noah', 'Math': '94', 'Science': '92', 'English': '96', 'Average': '94.0', 'Grade': 'A'},
        {'Student': 'Olivia', 'Math': '70', 'Science': '75', 'English': '78', 'Average': '74.3', 'Grade': 'C'},
    ]
}
```

## Tasks

### Task 1: Data Cleaning and Preparation
1. Remove any empty school data (if exists)
2. Convert the data to pandas DataFrames for each school
3. Clean the numeric columns ('Math', 'Science', 'English', 'Average') by:
   - Converting them to numeric data types
   - Handling any invalid entries
4. Drop rows with missing data in key subject columns
5. Save each school's cleaned data as a CSV file

### Task 2: Focus Analysis on One School
1. Extract data for 'Lincoln High' school only
2. Count the total number of students
3. Convert subject scores to numeric types
4. Calculate and display the mean scores for Math, Science, and English

### Task 3: Statistical Analysis
For Lincoln High students, calculate and display:
- **Mode** (most frequent score) for Math and Science
- **Median** scores for Math and Science  
- **Standard Deviation** for Math and Science scores
- **Variance** for Math and Science scores

### Task 4: Data Visualization
Create two visualizations for Lincoln High:

1. **Bar Plot**: Show average scores by student (sorted from highest to lowest)
   - Use seaborn barplot
   - Rotate x-axis labels for readability
   - Add appropriate title and labels

2. **Violin Plot**: Show the distribution of Math scores by student
   - Use seaborn violinplot
   - Sort students by their Math scores
   - Add appropriate title and labels

## Challenge Task 🚀

**Multi-School Comparison Analysis**

1. Combine all school data into a single DataFrame with a 'School' column
2. Calculate the average Math score for each school
3. Create a comparison visualization showing:
   - A grouped bar chart comparing Math, Science, and English averages across all three schools
   - Use different colors for each subject
   - Add a legend and proper labels
4. Identify which school has:
   - The highest overall average score
   - The most consistent scores (lowest standard deviation)
   - The best Math performance

**Bonus**: Create a heatmap showing the correlation between Math, Science, and English scores across all schools.

## Submission Requirements
- Submit your Python script (.py file)
- Include all generated CSV files
- Add comments explaining each step
- Include screenshots of your visualizations
- Write a brief summary (2-3 sentences) of your findings from the challenge task

## Grading Criteria
- **Data Cleaning (25%)**: Proper handling of data types and missing values
- **Statistical Analysis (25%)**: Correct calculation of statistical measures
- **Visualizations (25%)**: Clear, well-labeled charts
- **Challenge Task (25%)**: Creative analysis and insights

## Tips
- Always check your data types after conversion
- Use `.head()` to preview your DataFrames
- Add titles and labels to make your plots professional
- Round numerical results to 2 decimal places for clarity

**Due Date**: [Insert your due date here]