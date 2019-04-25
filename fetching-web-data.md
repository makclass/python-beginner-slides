# Fetching data with Python

CM540 Lecture 5

----

Workbook/Quiz Reminders:

- Workbook 1
- Workbook 2
- Quiz 1
- Quiz 2

----

In this lecture, we explore different ways to access network data.

----

1. Opening URL with Web Browser
2. Fetching data from XML source
2. Fetching from HTML source
3. Acting as a web browser to operate on web page

----

1. Opening URL with Web Browser via `webbrowser`.
2. Fetching data from XML source via `untangle`.
2. Fetching from HTML source via `beautifulsoup4`.
3. Pretending a web browser to operate on web page via `selenium`.

----

^ Sample of calling `web browsers

```python
import webbrowser

query = input("Please input search query to search Python doc. ")

url = "https://docs.python.org/3/search.html?q=" + query + "&check_keywords=yes&area=default"

webbrowser.open(url)
```

----

`webbrowser.open(url)` opens the URL in the default web browser.

----

^ Sample of google map search query near Macao.

```python
import webbrowser
import urllib.parse

query = input("Please input search query to search near-by Macao. ")

# A map search in Macao.
url = "https://www.google.com/maps/search/" + urllib.parse.quote(query) + "/@22.1612464,113.5303786,13z"

webbrowser.open(url)
```

----

`urllib.pares.quote(text)` encodes the string into URL friendly text.

----


What’s more than opening web browser?

----

Example: Things app x-callback-url

https://support.culturedcode.com/customer/en/portal/articles/2803573

----

^ An example of using `x-callback-url`

```python
import webbrowser

todos = []
while True:
    todo = input("Please enter a list of todo, or 'q' to quit: ")    
    if todo == "q":
        break
    todos.append(todo)    

url = "things:///add?titles={}".format("%0A".join(todos))

url = url.replace(" ","%20")

webbrowser.open(url)
```

----

- `%0A` is the new line in URL friendly representation.
- `%20` is spaces in URL friendly representation.


----

# Example of fetching JSON

----

^ Example of fetching JSON

```python
import urllib.request, json

url = "https://sample-json.netlify.com/macao-libraries.json"

with urllib.request.urlopen(url) as url:
    data = json.loads(url.read().decode())
    print(len(data))
```

----

# Example of fetching XML

----

`pip install untangle` to fetch XML.

----

^ Example of fetching XML

```python
import untangle
import datetime

def fetch():
    obj = untangle.parse('http://xml.smg.gov.mo/c_actual_brief.xml')

    temperature = obj.ActualWeatherBrief.Custom.Temperature.Value.cdata
    humidity = obj.ActualWeatherBrief.Custom.Humidity.Value.cdata

    print("現時澳門氣溫 " + temperature + " 度，濕度 " + humidity + "%。")

fetch()
```

----

現時澳門氣溫 28 度，濕度 80%

----

^ A better version 

```python
import untangle
import datetime

def fetch():
    obj = untangle.parse('http://xml.smg.gov.mo/c_actual_brief.xml')

    if type(obj.ActualWeatherBrief.Custom.Temperature) == type([]):
        temperature = obj.ActualWeatherBrief.Custom.Temperature[0].Value.cdata
    else:
        temperature = obj.ActualWeatherBrief.Custom.Temperature.Value.cdata

    humidity = obj.ActualWeatherBrief.Custom.Humidity.Value.cdata

```

----

- Temperature may be list or direct data.
- So we check if the Temperature is list or not.

----

# Fetching Web Data from HTML Source

----

Remember to `pip install beautifulsoup4`, `pip install lxml` and `pip install requests`.

----

Our target: news.gov.mo

----

```python
from bs4 import BeautifulSoup
import requests
 
res = requests.get("https://news.gov.mo/home/zh-hant")

soup = BeautifulSoup(res.text, "lxml")

print("\n".join( map(lambda x: x.getText().strip(), soup.select("h5"))) )
```

----

^ Better version with checking

```python
from bs4 import BeautifulSoup
import requests

try:
    res = requests.get("https://news.gov.mo/home/zh-hant")
except requests.exceptions.ConnectionError:
    print("Error: Invalid URL")
    exit()


soup = BeautifulSoup(res.text, "lxml")

print("\n".join( map(lambda x: x.getText().strip(), soup.select("h5"))) )
```


----

^ Fetching news content

```python
from bs4 import BeautifulSoup
import requests

url_base = 'https://news.gov.mo/home/zh-hant/'

try:
    res = requests.get(url_base)
except requests.exceptions.ConnectionError:
    print("Error: Invalid URL")
    exit()


soup = BeautifulSoup(res.text, "lxml")

for news in soup.select("h5"):
    href = news.select('a')[0]['href']
    print(news.getText().strip() + '\n')
    # print(url_base + href)
    # fetch news content
    res = requests.get(url_base + href)
    s = BeautifulSoup(res.text, "lxml")
    content = s.select(".asideBody .langInfo p")
    print(content[2].getText() + '\n') # first 2 p are empty
    print('----\n')
```

----

# BeautifulSoup cheat sheet

https://gist.github.com/yoki/b7f2fcef64c893e307c4c59303ead19a

----

^ BeautifulSoup cheat sheet

```python
from bs4 import BeautifulSoup
import requests

url = "https://www.gov.uk/bank-holidays"

res = requests.get(url)

soup = BeautifulSoup(res.text, "lxml")

# tag: tag. e.g. h5, a
# class: .class
# id: #id

all_headings = soup.select("table:nth-of-type(1) .calendar-date")

# all_headings = soup.select(".calendar-title")

element_plain_text = lambda x: x.text

all_headings_text = list( map( element_plain_text, all_headings ))
#print(all_headings_text)

print( "\n".join(all_headings_text) )
```

----

# Selenium

----

# Selenium Pre-request

- Web browser, e.g. Firefox
- Web driver, e.g. GeckoDriver
- `pip install selenium` 

----

# Download Driver

https://github.com/mozilla/geckodriver/releases

----


## Selenium Cheat Sheets

- https://codoid.com/selenium-webdriver-python-cheat-sheet/
- http://allselenium.info/python-selenium-commands-cheat-sheet-frequently-used/
- http://akul.me/blog/2016/selenium-cheatsheet/
- https://gist.github.com/huangzhichong/3284966


----

^ Example of taking screenshot with Selenium

```python
'''Capture the screenshot of a website via Headless Firefox.'''

from selenium import webdriver
from selenium.webdriver.firefox.options import Options

options = Options()
options.add_argument('-headless')

browser = webdriver.Firefox(options=options)
browser.maximize_window()
browser.get('https://makclass.com/')
browser.save_screenshot('makclass.png')
browser.quit()
```

----

^ Example of auto login github and fetch all repositories

```python
'''Login Github via Selenium'''

from selenium import webdriver
from selenium.webdriver.firefox.options import Options
import time

options = Options()
options.add_argument('-headless')

browser = webdriver.Firefox(options=options)
browser.maximize_window()
browser.get('https://github.com/login')



form = browser.find_element_by_css_selector('form')

element = form.find_element_by_css_selector('#login_field')
element.send_keys('makzan-demo')

element = form.find_element_by_css_selector('#password')
element.send_keys('password')
form.submit()

time.sleep(3)

# After login, let's list our repostories:
browser.get('https://github.com/settings/repositories')
elements = browser.find_elements_by_css_selector('.listgroup-item > a')

print('\n\n'.join(map(lambda x: x.text, elements)))



# browser.quit()
```


----

^ Example of fetching stock price from AAStock

```lang-python
'''Fetch current stock from aastock.'''

from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException
from selenium.webdriver.firefox.options import Options
import time

stock_number = '0011'

options = Options()
options.add_argument('-headless')

browser = webdriver.Firefox(options=options)
browser.maximize_window()

browser.get('http://www.aastocks.com/tc/stocks/aboutus/companyinfo.aspx')
element = browser.find_element_by_css_selector('#txtHKQuote')
element.send_keys(stock_number)
browser.execute_script("shhkquote($('#txtHKQuote').val(), 'quote', mainPageMarket)")

trial_time = 0
while True:
    if trial_time > 5:
        break
    to_sleep = 0.1
    time.sleep(to_sleep)
    trial_time += to_sleep
    try:
        element = browser.find_element_by_css_selector('.font28')
        print(element.text)
        break
    except NoSuchElementException as e:
        pass



browser.quit()
```
