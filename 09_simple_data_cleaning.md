# Simple Data Cleaning Example

## Installation
```bash
pip install requests beautifulsoup4
```

## Complete Code

```python
import requests
from bs4 import BeautifulSoup
import re

def getParsedWebpage(url):
    headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'

# Scrape quotes (they need cleaning!)
url = 'http://quotes.toscrape.com/'
soup = getParsedWebpage(url)

if soup != 'error':
    quotes = soup.find_all('div', class_='quote')
    
    print("BEFORE CLEANING:")
    print("-" * 40)
    
    for i, quote in enumerate(quotes[:3], 1):
        raw_text = quote.find('span', class_='text').text
        raw_author = quote.find('small', class_='author').text
        print(f"{i}. {raw_text} by {raw_author}")
    
    print("\nAFTER CLEANING:")
    print("-" * 40)
    
    # START DATA CLEANING HERE
    for i, quote in enumerate(quotes[:3], 1):
        # Clean the text - make it uppercase and add stars
        raw_text = quote.find('span', class_='text').text
        clean_text = raw_text.upper()  # Make text UPPERCASE
        clean_text = f"⭐ {clean_text} ⭐"  # Add stars around the quote
        
        # Clean the author - remove extra spaces and make lowercase
        raw_author = quote.find('small', class_='author').text
        clean_author = raw_author.strip().lower()  # Remove spaces and make lowercase
        
        print(f"{i}. {clean_text} - {clean_author}")
else:
    print("Failed to scrape website")
```

## Explanation of Data Cleaning

**What is Data Cleaning?**
- Removing unwanted characters like quotes `"` and `"`
- Removing extra spaces with `.strip()`
- Fixing capitalization with `.title()`
- Making data consistent and neat

**Line-by-line cleaning explanation:**

```python
raw_text = quote.find('span', class_='text').text
```
- **Line 1**: Get the original messy text from the website

```python
clean_text = raw_text.replace('"', '').replace('"', '')
```
- **Line 2**: Remove opening `"` and closing `"` quote marks

```python
clean_text = clean_text.strip()
```
- **Line 3**: Remove extra spaces at beginning and end

```python
raw_author = quote.find('small', class_='author').text
clean_author = raw_author.strip().title()
```
- **Line 4-5**: Clean author name - remove spaces and make proper capitalization

**Common Cleaning Methods:**
- `.strip()` - removes spaces
- `.replace('old', 'new')` - replaces unwanted text
- `.title()` - makes proper capitalization
- `.lower()` - makes everything lowercase
- `.upper()` - makes everything uppercase

**Expected Output:**
```
BEFORE CLEANING:
----------------------------------------
1. "The world as we have created it..." by albert einstein
2. "It is our choices, Harry..." by j.k. rowling  
3. "There are only two ways..." by albert einstein

AFTER CLEANING:
----------------------------------------
1. The world as we have created it... - Albert Einstein
2. It is our choices, Harry... - J.K. Rowling
3. There are only two ways... - Albert Einstein
```

