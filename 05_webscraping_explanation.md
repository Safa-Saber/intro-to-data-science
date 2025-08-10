# Complete Web Scraping Tutorial: Wikipedia Data Extraction

## Overview
This tutorial demonstrates how to scrape data from a Wikipedia page about marriage ages by country, organize it by continent, clean the data, and save it to CSV files.

## Part 1: Setting Up and Basic Web Scraping

### Importing the Tools
```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
import re
```

Think of these as getting your toolbox ready:
- **requests**: This is like a messenger that goes to websites and asks for their content
- **BeautifulSoup**: This is like a translator that converts messy webpage code into something we can easily read and search through
- **pandas**: A tool for organizing data (like Excel for Python)
- **re**: A tool for finding specific text patterns (used later for cleaning data)

### The Main Function - getParsedWebpage()

#### The Function Definition
```python
def getParsedWebpage(url):
```
This creates a reusable "recipe" that takes a website address (URL) as input and gives back the webpage content.

#### The Headers - Pretending to be a Browser
```python
headers = {
    "User-Agent": "Mozilla/5.0...",
    # ... more headers
}
```
**Why do we need this?** Some websites don't like robots visiting them, so they block automated requests. These headers make our code pretend to be a real person using Firefox browser. It's like wearing a disguise to get into a club!

#### Making the Request
```python
response = requests.get(url, headers=headers)
```
This line sends our "messenger" (requests) to the website with our disguise (headers) and asks for the webpage content.

#### Checking if it Worked
```python
if response.status_code != 200:
    # Something went wrong
else:
    # Success! Process the content
```
**Status codes are like response messages:**
- 200 = "Success! Here's your content"
- 404 = "Page not found"
- 403 = "Access denied"

#### Parsing the Content
```python
return BeautifulSoup(response.content, 'html.parser')
```
If everything worked, BeautifulSoup takes the raw HTML code (which looks messy) and organizes it into something we can easily search through and extract information from.

#### Error Handling
```python
except requests.exceptions.RequestException as e:
    print(f"An error occurred: {e}")
    return 'error'
```
This is like having a backup plan. If anything goes wrong (internet problems, website down, etc.), instead of crashing, the code politely says "error" and continues.

## Part 2: Getting and Analyzing the Webpage

### Using the Function
```python
url = 'https://en.wikipedia.org/wiki/List_of_countries_by_age_at_first_marriage'
soup = getParsedWebpage(url)
```
Here we:
1. Specify which Wikipedia page we want to visit
2. Call our function to get the content
3. Store the organized webpage content in a variable called `soup`

### Finding Page Structure
```python
continents = ['Africa', 'Asia', 'Europe', 'Americas', 'Oceania']
continent_headings = soup.find_all('h2')
filtered_continent_headings = [heading for heading in continent_headings 
                              if any(continent in heading.get_text() for continent in continents)]
tables = soup.find_all('table', {'class': 'wikitable'})

# Print the number of continents found and their names
print(f"Number of Continents Found: {len(filtered_continent_headings)}")
for heading in filtered_continent_headings:
    print(heading.get_text().strip())

print()  # Add a blank line for spacing
print(f"Number of Tables Found: {len(tables)}")
```

**What's happening here:**
- We define a list of continent names we're looking for
- We find all heading tags (`<h2>`) on the page
- We filter these headings to only keep ones that mention our continents
- We find all Wikipedia-style tables (they have class='wikitable')
- We print out what we found to verify our page analysis worked

**Think of it like:** Going through a textbook and marking all the chapter headings that mention continents, then finding all the data tables and counting them.

## Part 3: Basic Page Analysis

### Understanding What We Found
After successfully fetching the webpage, we can analyze its structure to understand what data is available. The code shows us how many continent sections and data tables exist on the page, which helps us verify that our scraping approach is working correctly.

## Part 4: Data Processing

### Basic Data Display
```python
print(f"Number of Tables Found: {len(tables)}")
```

This simply shows us how many data tables were found on the webpage, helping us verify that our scraping worked correctly.

## Simple Analogy for the Whole Process
Think of this like organizing information from a library book:

1. **Part 1**: Get permission to enter the library (headers) and find the right book (web request)
2. **Part 2**: Look through the book and identify which sections are about different continents, and count how many data tables there are
3. **Part 3**: Copy the important information from tables into organized notes
4. **Part 4**: Count and verify what we found

The end result: Instead of manually reading through a complex webpage, you now have the webpage content organized and ready for further analysis!

---

## Where Do These Headers Come From?

The headers in our code are HTTP headers that browsers automatically send when they visit websites. Here's what each one means and how to find them:

### What Each Header Does (And Why They're Important):

- **User-Agent**: Tells the website what browser and operating system you're using
  - *Why important*: This is the most crucial header! Websites use this to determine if you're a real browser or a bot

- **Upgrade-Insecure-Requests**: "1" tells the server you prefer HTTPS over HTTP
  - *Why important*: Real browsers always send this. Without it, your request looks suspicious and automated

- **Accept**: Lists what types of content your browser can handle
  - `text/html` = regular web pages
  - `application/xhtml+xml` = stricter HTML format
  - `application/xml` = XML data
  - `q=0.9` = quality values (preference ranking)
  - `*/*` = "I can accept anything else too"
  - *Why important*: Shows you're expecting normal web content, not just raw data like an API call

- **Accept-Encoding**: Tells the server what compression methods your browser supports
  - `gzip, deflate, br` = different compression algorithms
  - *Why important*: All modern browsers support compression. Without this, you look like an old/fake browser

- **Accept-Language**: Your preferred languages in order of preference
  - `en-GB,en-US;q=0.9,en;q=0.8` = British English first, then US English, then any English
  - *Why important*: Real users have language preferences. Bots often don't include this

- **DNT**: "Do Not Track" - asks websites not to track you (1 = enabled)
  - *Why important*: Many privacy-conscious users enable this, so including it makes you look more human

### Why These Specific Headers Matter for Web Scraping:

**The Detective Story Analogy:**
Think of a website as a security guard trying to figure out if you're a real visitor or a robot. Each missing header is like a clue that gives you away:

1. **Missing User-Agent**: "This person doesn't even know what browser they're using!"
2. **Missing Accept headers**: "They don't care what type of content they get back - that's weird!"
3. **Missing Accept-Language**: "They have no language preferences at all?"
4. **Missing Accept-Encoding**: "They don't want compressed files? Even old browsers support that!"

**Real browsers send ALL of these automatically**. When your Python script is missing any of them, it's like showing up to a costume party without a costume - you stand out immediately!

### Which Headers Are Most Critical?

**Essential (Website will likely block you without these):**
- `User-Agent` - This is #1 most important
- `Accept` - Shows you want normal web content

**Very Important (Many sites check these):**
- `Accept-Language` - Proves you're a real user with preferences
- `Accept-Encoding` - All modern browsers support compression

**Nice to Have (Adds to authenticity):**
- `Upgrade-Insecure-Requests` - Shows modern browser behavior
- `DNT` - Shows privacy awareness

### Testing Header Importance:

You can demonstrate this to students by trying requests with different header combinations:

```python
# This might get blocked:
minimal_headers = {"User-Agent": "Python"}

# This is better:
basic_headers = {"User-Agent": "Mozilla/5.0..."}

# This is most convincing:
complete_headers = {
    "User-Agent": "Mozilla/5.0...",
    "Accept": "text/html,application/xhtml+xml...",
    # ... all the others
}
```

### How to Find Real Browser Headers:

#### Method 1: Using Browser Developer Tools
1. Open any website in Chrome/Firefox
2. Press F12 to open Developer Tools
3. Go to the "Network" tab
4. Refresh the page (F5)
5. Click on the first request (usually the main webpage)
6. Look at the "Request Headers" section
7. Copy the headers you see there

#### Method 2: Using Online Tools
- Visit: https://httpbin.org/headers
- This website will show you exactly what headers your browser is sending

#### Method 3: Using Python to Check
```python
import requests

# Make a request to a site that shows your headers
response = requests.get('https://httpbin.org/headers')
print(response.json())
```

### Can We Use Simpler Headers?
Yes! For many websites, you only need the User-Agent:

```python
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}
```

---

## Complete Code

Here's the complete code that you can copy and paste to run the entire web scraping process:

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
import re

def getParsedWebpage(url):
    """
    Fetch and parse a webpage while handling access errors.

    Parameters:
        url (str): The URL of the webpage to fetch.

    Returns:
        BeautifulSoup object or str: Parsed webpage content or 'error' if the request fails.
    """
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:66.0) Gecko/20100101 Firefox/93.0",
        "Upgrade-Insecure-Requests": "1",
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
        "Accept-Encoding": "gzip, deflate, br",
        "Accept-Language": "en-GB,en-US;q=0.9,en;q=0.8",
        "DNT": "1"
    }

    try:
        response = requests.get(url, headers=headers)
        
        if response.status_code != 200:
            print(f"Failed to fetch the webpage. Status code: {response.status_code}")
            return 'error'
        else:
            print("Webpage fetched successfully!")
            return BeautifulSoup(response.content, 'html.parser')
    except requests.exceptions.RequestException as e:
        print(f"An error occurred: {e}")
        return 'error'

url = 'https://en.wikipedia.org/wiki/List_of_countries_by_age_at_first_marriage'
soup = getParsedWebpage(url)

if soup != 'error':
    print("Webpage content parsed successfully.")
else:
    print("Failed to parse the webpage.")

url = 'https://en.wikipedia.org/wiki/List_of_countries_by_age_at_first_marriage'
soup = getParsedWebpage(url)

if soup != 'error':
    continents = ['Africa', 'Asia', 'Europe', 'Americas', 'Oceania']
    continent_headings = soup.find_all('h2')
    filtered_continent_headings = [heading for heading in continent_headings if any(continent in heading.get_text() for continent in continents)]
    tables = soup.find_all('table', {'class': 'wikitable'})

    print(f"Number of Continents Found: {len(filtered_continent_headings)}")
    for heading in filtered_continent_headings:
        print(heading.get_text().strip())

    print()
    print(f"Number of Tables Found: {len(tables)}")
else:
    print("Failed to fetch the webpage.")
```



---

## Where Do These Headers Come From?

The headers in our code are HTTP headers that browsers automatically send when they visit websites. Here's what each one means and how to find them:

### What Each Header Does (And Why They're Important):

- **User-Agent**: Tells the website what browser and operating system you're using
  - *Why important*: This is the most crucial header! Websites use this to determine if you're a real browser or a bot

- **Upgrade-Insecure-Requests**: "1" tells the server you prefer HTTPS over HTTP
  - *Why important*: Real browsers always send this. Without it, your request looks suspicious and automated

- **Accept**: Lists what types of content your browser can handle
  - `text/html` = regular web pages
  - `application/xhtml+xml` = stricter HTML format
  - `application/xml` = XML data
  - `q=0.9` = quality values (preference ranking)
  - `*/*` = "I can accept anything else too"
  - *Why important*: Shows you're expecting normal web content, not just raw data like an API call

- **Accept-Encoding**: Tells the server what compression methods your browser supports
  - `gzip, deflate, br` = different compression algorithms
  - *Why important*: All modern browsers support compression. Without this, you look like an old/fake browser

- **Accept-Language**: Your preferred languages in order of preference
  - `en-GB,en-US;q=0.9,en;q=0.8` = British English first, then US English, then any English
  - *Why important*: Real users have language preferences. Bots often don't include this

- **DNT**: "Do Not Track" - asks websites not to track you (1 = enabled)
  - *Why important*: Many privacy-conscious users enable this, so including it makes you look more human

### How to Find Real Browser Headers:

#### Method 1: Using Browser Developer Tools
1. Open any website in Chrome/Firefox
2. Press F12 to open Developer Tools
3. Go to the "Network" tab
4. Refresh the page (F5)
5. Click on the first request (usually the main webpage)
6. Look at the "Request Headers" section
7. Copy the headers you see there

#### Method 2: Using Online Tools
- Visit: https://httpbin.org/headers
- This website will show you exactly what headers your browser is sending

#### Method 3: Using Python to Check
```python
import requests

# Make a request to a site that shows your headers
response = requests.get('https://httpbin.org/headers')
print(response.json())
```

### Why These Specific Headers Matter for Web Scraping:

**The Detective Story Analogy:**
Think of a website as a security guard trying to figure out if you're a real visitor or a robot. Each missing header is like a clue that gives you away:

1. **Missing User-Agent**: "This person doesn't even know what browser they're using!"
2. **Missing Accept headers**: "They don't care what type of content they get back - that's weird!"
3. **Missing Accept-Language**: "They have no language preferences at all?"
4. **Missing Accept-Encoding**: "They don't want compressed files? Even old browsers support that!"

**Real browsers send ALL of these automatically**. When your Python script is missing any of them, it's like showing up to a costume party without a costume - you stand out immediately!

### Which Headers Are Most Critical?

**Essential (Website will likely block you without these):**
- `User-Agent` - This is #1 most important
- `Accept` - Shows you want normal web content

**Very Important (Many sites check these):**
- `Accept-Language` - Proves you're a real user with preferences
- `Accept-Encoding` - All modern browsers support compression

**Nice to Have (Adds to authenticity):**
- `Upgrade-Insecure-Requests` - Shows modern browser behavior
- `DNT` - Shows privacy awareness

### Testing Header Importance:

You can demonstrate this to students by trying requests with different header combinations:

```python
# This might get blocked:
minimal_headers = {"User-Agent": "Python"}

# This is better:
basic_headers = {"User-Agent": "Mozilla/5.0..."}

# This is most convincing:
complete_headers = {
    "User-Agent": "Mozilla/5.0...",
    "Accept": "text/html,application/xhtml+xml...",
    # ... all the others
}
```

### Can We Use Simpler Headers?
Yes! For many websites, you only need the User-Agent:

```python
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
}
```

### Good Luck!!
