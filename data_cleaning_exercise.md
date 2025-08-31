# Data Cleaning Exercise - Life Expectancy Dataset

## Cleaning Tasks

### **Task 1: Load the Data**
* Put the table into a Pandas **DataFrame**.
* Print the raw data to see what we're working with.
* Check the shape and basic info about the dataset.

### **Task 2: Clean Country Names**
* Remove text inside `()` and `[]` from the **Country** column.
   * Example: `"Kenya (East Africa)" → "Kenya"`
   * Example: `"France [EU]" → "France"`
* Strip whitespace from start and end of country names.
* Convert country names to title case for consistency.

### **Task 3: Fix Numeric Columns**
* Columns `Men`, `Women`, `Average`, `Age_Gap`, `Age_Ratio`:
   * Replace commas `,` with dots `.` for decimal notation
   * Remove any non-numeric characters except dots
   * Convert to `float` using `pd.to_numeric(errors="coerce")`
   * Handle any remaining invalid values

### **Task 4: Clean Year Column**
* Remove text in `[]` and `()` from the `Year` column.
   * Example: `"2020 [a]" → "2020"`
   * Example: `"2019 (est)" → "2019"`
* Convert column to integer type.
* Check for any years that seem unrealistic (too old or future dates).

### **Task 5: Clean Population Column**
* Remove commas and convert to numeric format
* Handle values with 'M' (millions) and 'K' (thousands) suffixes
* Convert all population values to actual numbers

### **Task 6: Handle Missing Data**
* Identify missing values in each column
* Remove rows where **Country** is `"-"`, "N/A", or empty
* Remove rows where ALL numeric values are missing
* Decide how to handle rows with some missing numeric values

### **Task 7: Data Validation**
* Check for duplicate countries
* Verify that Age_Gap = Women - Men (approximately)
* Ensure all life expectancy values are reasonable (between 30-90 years)
* Check that years are within a reasonable range (1990-2024)

### **Task 8: Final Verification**
* Print the cleaned DataFrame
* Show summary statistics:
   * Mean life expectancy for Men, Women, and Average
   * Number of valid countries after cleaning
   * Data types of all columns
   * Number of missing values per column

---

## Sample Dataset

```python
import pandas as pd
import numpy as np

# Sample data with common data quality issues
data = {
    'Country': [
        'Japan (East Asia)',
        'Switzerland [EU]',
        'Singapore',
        'Australia (Oceania)',
        'Iceland [Nordic]',
        'Italy (Southern Europe)',
        'Spain [EU]',
        'South Korea',
        'France [Western EU]',
        'Canada (North America)',
        'Norway [Scandinavia]',
        'Luxembourg [EU]',
        'Sweden (Nordic)',
        '-',
        'New Zealand',
        'United Kingdom [EU]',
        'Germany [Central EU]',
        'Finland (Nordic)',
        'Austria [EU]',
        'Belgium [EU]',
        'Netherlands [Western EU]',
        'Ireland [EU]',
        'Denmark [Nordic]',
        'Portugal [EU]',
        'Slovenia [EU]'
    ],
    'Men': [
        '81,1', '81,6', '81.2', '80,5', '80.8', 
        '80,9', '80.1', '79.3', '79,4', '79.2',
        '80.1', '80,0', '80.4', '-', '80.0',
        '79.2', '78,5', '78.7', '78,9', '78.1',
        '79,2', '78.8', '78,1', '78.3', '78.2'
    ],
    'Women': [
        '87,1', '85,2', '85.5', '84,6', '83.8',
        '85,2', '85.8', '85.4', '85,3', '83.9',
        '83.9', '84,5', '84.1', '-', '83.5',
        '82.9', '83,2', '83.5', '83,4', '83.1',
        '82,8', '82.1', '82,2', '84.4', '83.9'
    ],
    'Average': [
        '84,2', '83,4', '83.4', '82,6', '82.3',
        '83,1', '83.0', '82.4', '82,4', '81.6',
        '82.0', '82,3', '82.3', '-', '81.8',
        '81.1', '80,9', '81.1', '81,2', '80.6',
        '81,0', '80.5', '80,2', '81.4', '81.1'
    ],
    'Age_Gap': [
        '6,0', '3,6', '4.3', '4,1', '3.0',
        '4,3', '5.7', '6.1', '5,9', '4.7',
        '3.8', '4,5', '3.7', '-', '3.5',
        '3.7', '4,7', '4.8', '4,5', '5.0',
        '3,6', '3.3', '4,1', '6.1', '5.7'
    ],
    'Age_Ratio': [
        '1,074', '1,044', '1.053', '1,051', '1.037',
        '1,053', '1.071', '1.077', '1,074', '1.059',
        '1.047', '1,056', '1.046', '-', '1.044',
        '1.047', '1,060', '1.061', '1,057', '1.064',
        '1,045', '1.042', '1,052', '1.078', '1.073'
    ],
    'Year': [
        '2022', '2022 [a]', '2022', '2021 [est]', '2022',
        '2022 [b]', '2022', '2022', '2021 [c]', '2022',
        '2022 [d]', '2022', '2022', '2022', '2021',
        '2021 [e]', '2022', '2022 [f]', '2022', '2022',
        '2022 [g]', '2022', '2022 [h]', '2022', '2022'
    ],
    'Population': [
        '125,416,877', '8,796,669', '5.454M', '25,788,215', '376K',
        '59,037,474', '47,558,630', '51.8M', '68,084,217', '38.2M',
        '5,425,270', '640K', '10,549,347', 'N/A', '5.2M',
        '67,508,936', '83,294,633', '5,540,745', '8,939,617', '11,590,266',
        '17,564,014', '5,033,164', '5,822,763', '10,467,366', '2,119,675'
    ]
}

# Create DataFrame
df = pd.DataFrame(data)
print("Raw Dataset:")
print(df)
```

---

## Expected Outcomes

After completing all tasks, your cleaned dataset should have:

1. **Clean country names** without parentheses or brackets
2. **Proper numeric data types** for all quantitative columns
3. **Integer years** without annotations
4. **Standardized population values** in actual numbers
5. **No empty or invalid rows**
6. **Consistent data formatting** throughout

## Bonus Tasks (Optional)

### **Task 9: Data Analysis**
* Find the top 5 countries with highest life expectancy
* Calculate correlation between men's and women's life expectancy
* Identify countries with the largest gender gap in life expectancy

### **Task 10: Data Visualization**
* Create a scatter plot of Men vs Women life expectancy
* Plot a histogram of the age gaps
* Create a bar chart of top 10 countries by average life expectancy

### **Task 11: Export Clean Data**
* Save the cleaned DataFrame to a CSV file
* Create a summary report of the cleaning process
* Document any assumptions made during cleaning

---

## Common Issues to Watch For

- Mixed decimal separators (commas vs dots)
- Text annotations in numeric fields
- Inconsistent country name formatting
- Missing value indicators ('-', 'N/A', empty strings)
- Population values with unit suffixes (M, K)
- Unrealistic or outlier values
- Duplicate entries

Remember to always inspect your data before and after each cleaning step!