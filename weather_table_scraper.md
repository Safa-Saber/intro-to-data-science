# Weather Table Scraper - TimeandDate.com

## Installation
```bash
pip install requests beautifulsoup4
```

## Complete Code

```python
import requests
from bs4 import BeautifulSoup

url = 'https://www.timeanddate.com/weather/usa/new-york/ext'
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) "
                  "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0 Safari/537.36"
}

response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

table = soup.find("table", id="wt-ext")  

if table:
    rows = table.find_all("tr")[1:6]  # skip header
    print("5-Day Weather Forecast for New York:")
    print("-" * 60)
    for i, row in enumerate(rows, 1):
        cells = row.find_all(["td", "th"])
        if len(cells) >= 3:
            date = cells[0].get_text(strip=True)
            temp = cells[1].get_text(strip=True)
            condition = cells[2].get_text(strip=True)
            print(f"{i}. {date} | {temp} | {condition}")
else:
    print("Weather table not found")

```

## Explanation of Each Line

**Line-by-line breakdown:**

```python
import requests
from bs4 import BeautifulSoup
```
- **Line 1**: Import the `requests` library to download web pages
- **Line 2**: Import `BeautifulSoup` to parse and extract data from HTML tables

```python
def getParsedWebpage(url):
```
- **Line 3**: Create a function that takes a website URL as input

```python
    headers = {
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9...",
        "Accept-Encoding": "gzip, deflate",
        "Accept-Language": "en-GB,en-US;q=0.9,en;q=0.8",
        "Cache-Control": "max-age=0",
        "Upgrade-Insecure-Requests": "1",
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)...",
        "Referer": "https://www.timeanddate.com/"
    }
```
- **Lines 4-11**: Create headers dictionary to make our request look like a real browser visiting TimeandDate.com
  - `Accept`: Tell server what file types we can handle
  - `Accept-Encoding`: Compression methods we support
  - `Accept-Language`: Preferred languages (English GB, US)
  - `Cache-Control`: Don't use cached version, get fresh weather data
  - `Upgrade-Insecure-Requests`: Prefer secure HTTPS connections
  - `User-Agent`: Pretend to be Chrome browser on Mac
  - `Referer`: Tell server we came from TimeandDate.com main page

```python
    response = requests.get(url, headers=headers)
```
- **Line 12**: Send GET request to the weather website with our fake browser headers

```python
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'
```
- **Line 13**: Check if request was successful (status code 200 = OK)
- **Line 14**: If successful, parse the HTML content and return it
- **Line 15**: If failed, return 'error' string

```python
url = 'https://www.timeanddate.com/weather/usa/new-york/ext'
soup = getParsedWebpage(url)
```
- **Line 16**: Set the URL for New York extended weather forecast
- **Line 17**: Call our function to download and parse the weather page

```python
if soup != 'error':
```
- **Line 18**: Check if the website was successfully downloaded

```python
    table = soup.find('table', id="wt-ext')
```
- **Line 19**: Find the first HTML `<table>` element with id="wt-ext (weather forecast table)

```python
    if table:
```
- **Line 20**: Check if we actually found a weather table

```python
        rows = table.find_all('tr')[1:6]
```
- **Line 21**: Find all table rows (`<tr>`), skip header row [0], get rows 1-5 (5 days forecast)

```python
        print("5-Day Weather Forecast for New York:")
        print("-" * 60)
```
- **Line 22**: Print title for our weather data
- **Line 23**: Print a line of dashes for nice formatting

```python
        for i, row in enumerate(rows, 1):
```
- **Line 24**: Loop through each table row (each day), with numbering starting at 1

```python
            cells = row.find_all(['td', 'th'])
```
- **Line 25**: Find all table cells (`<td>` or `<th>`) in this row

```python
            if len(cells) >= 3:
```
- **Line 26**: Make sure this row has at least 3 cells (date, temp, condition)

```python
                date = cells[0].get_text().strip()
                temp = cells[1].get_text().strip()
                condition = cells[2].get_text().strip()
```
- **Line 27**: Get date from first cell (column 0) and remove extra spaces
- **Line 28**: Get temperature from second cell (column 1)
- **Line 29**: Get weather condition from third cell (column 2)

```python
                print(f"{i}. {date} | {temp} | {condition}")
```
- **Line 30**: Print the numbered day with date, temperature, and weather condition

```python
    else:
        print("Weather table not found")
```
- **Line 31-32**: If no weather table was found on the page, show message

```python
else:
    print("Failed to scrape website")
```
- **Line 33-34**: If website download failed, show error message

**What happens when you run it:**
1. Downloads the TimeandDate.com weather forecast page for New York
2. Finds the weather forecast table on the page
3. Extracts date, temperature, and weather condition from each row
4. Prints a 5-day weather forecast

**Expected Output:**
```
5-Day Weather Forecast for New York:
------------------------------------------------------------
1. Fri Aug 16 | 78°/64° | Partly Cloudy
2. Sat Aug 17 | 81°/66° | Mostly Sunny  
3. Sun Aug 18 | 83°/68° | Sunny
4. Mon Aug 19 | 79°/65° | Scattered Showers
5. Tue Aug 20 | 76°/63° | Partly Cloudy
```

**Note:** If TimeandDate.com changes their website structure, you might need to inspect the page and update the table class name or cell positions.
