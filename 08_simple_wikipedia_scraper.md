# Simple Wikipedia Table Scraper

## Installation
```bash
pip install requests beautifulsoup4
```

## Complete Code

```python
import requests
from bs4 import BeautifulSoup

def getParsedWebpage(url):
    headers = {
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8",
        "Accept-Language": "en-GB,en-US;q=0.9,en;q=0.8",
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36",
        "Referer": "https://en.wikipedia.org/"
    }
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'

# Scrape largest countries table
url = 'https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_area'
soup = getParsedWebpage(url)

if soup != 'error':
    table = soup.find('table', class_='wikitable')
    
    if table:
        rows = table.find_all('tr')[1:6]  # Skip header, get 5 countries
        
        print("Top 5 Largest Countries by Area:")
        print("-" * 50)
        
        for i, row in enumerate(rows, 1):
            cells = row.find_all(['td', 'th'])
            if len(cells) >= 3:
                rank = cells[0].get_text().strip()
                country = cells[1].get_text().strip()
                area = cells[2].get_text().strip()
                
                # Simple cleaning
                country = country.split('[')[0]  # Remove citations
                area = area.split('[')[0]        # Remove citations
                
                print(f"{i}. {country}: {area}")
    else:
        print("Table not found")
else:
    print("Failed to scrape website")
```

## What This Code Does

**Website**: Wikipedia page about countries by area
**Data**: Gets the 5 largest countries and their sizes

**Expected Output:**
```
Top 5 Largest Countries by Area:
--------------------------------------------------
1. Russia: 17,098,242 km2
2. Canada: 9,984,670 km2
3. United States: 9,833,517 km2
4. China: 9,596,960 km2
5. Brazil: 8,514,877 km2
```

## Simple Explanation

1. **Get Wikipedia page** about country areas
2. **Find the table** with country data
3. **Get first 5 rows** (skip header)
4. **Extract 3 pieces** from each row:
   - Rank number
   - Country name  
   - Area size
5. **Clean the data** (remove citations like [1])
6. **Print nicely** with numbers

## Key Learning Points

- **Wikipedia tables** are great for beginners
- **Simple data extraction** (rank, name, area)
- **Basic cleaning** with `.split('[')[0]`
- **Clear, numbered output**
- **Easy to understand** data (countries and sizes)

Perfect for students to see how table scraping works with real, interesting data!
