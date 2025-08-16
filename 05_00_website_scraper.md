# Super Simple Web Scraper

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
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
        "Accept-Encoding": "gzip, deflate",
        "Accept-Language": "en-GB,en-US;q=0.9,en;q=0.8",
        "Cache-Control": "max-age=0",
        "Upgrade-Insecure-Requests": "1",
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36",
        "Referer": "http://quotes.toscrape.com/"
    }
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'

# Scrape quotes
url = 'http://quotes.toscrape.com/'
soup = getParsedWebpage(url)

if soup != 'error':
    quotes = soup.find_all('div', class_='quote')
    
    for i, quote in enumerate(quotes[:5], 1):
        text = quote.find('span', class_='text').text
        author = quote.find('small', class_='author').text
        print(f"{i}. {text} - {author}")
else:
    print("Failed to scrape website")
```

## Explanation of Each Line

**Line-by-line breakdown:**

```python
import requests
from bs4 import BeautifulSoup
```
- **Line 1**: Import the `requests` library to download web pages
- **Line 2**: Import `BeautifulSoup` to parse and extract data from HTML

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
        "Referer": "http://quotes.toscrape.com/"
    }
```
- **Lines 4-11**: Create headers dictionary to make our request look like a real browser
  - `Accept`: Tell server what file types we can handle
  - `Accept-Encoding`: Compression methods we support
  - `Accept-Language`: Preferred languages (English GB, US)
  - `Cache-Control`: Don't use cached version, get fresh data
  - `Upgrade-Insecure-Requests`: Prefer secure HTTPS connections
  - `User-Agent`: Pretend to be Chrome browser on Mac
  - `Referer`: Tell server we came from the quotes website

```python
    response = requests.get(url, headers=headers)
```
- **Line 12**: Send GET request to the website with our fake browser headers

```python
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'
```
- **Line 13**: Check if request was successful (status code 200 = OK)
- **Line 14**: If successful, parse the HTML content and return it
- **Line 15**: If failed, return 'error' string

```python
url = 'http://quotes.toscrape.com/'
soup = getParsedWebpage(url)
```
- **Line 16**: Set the website URL we want to scrape
- **Line 17**: Call our function to download and parse the website

```python
if soup != 'error':
```
- **Line 18**: Check if the website was successfully downloaded

```python
    quotes = soup.find_all('div', class_='quote')
```
- **Line 19**: Find all HTML `<div>` elements with class="quote" on the page

```python
    for i, quote in enumerate(quotes[:5], 1):
```
- **Line 20**: Loop through first 5 quotes, with numbering starting at 1

```python
        text = quote.find('span', class_='text').text
        author = quote.find('small', class_='author').text
```
- **Line 21**: Find the quote text inside `<span class="text">` and extract text
- **Line 22**: Find the author name inside `<small class="author">` and extract text

```python
        print(f"{i}. {text} - {author}")
```
- **Line 23**: Print the numbered quote with author

```python
else:
    print("Failed to scrape website")
```
- **Line 24-25**: If website download failed, show error message

**What happens when you run it:**
1. Downloads the quotes website
2. Parses the HTML to find quote elements
3. Extracts text and author from each quote
4. Prints 5 formatted quotes with numbers
