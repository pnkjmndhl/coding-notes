### getting the soup
```py
import requests
from bs4 import beautifulSoup

url = 'http://quotes.toscrape.com'
response = request.get(url)
soup = BeautifulSoup(response.text, 'lxml')
# the soup is ready
```

### isolating data
- `quotes = soup.find_all('<tag>', class_ = '<classname>')`
- if you have multiple tags inside a tag, grab that tag first and run `.find_all()` on that subset soup
- `quotes.text` to get the text from the tag

### data scraping on multiple pages
- practice scraping on `scrapingclub.com`
- grab the individual links
```py
pageNum = int(link.text) if link.text.isdigit() else None
if pageNum != None:
    x = link.get('href')
    urls.append(x)
# now loop throught this url
for i in urls:
    nreUrl = url + i
    response = requests.get(newUrl)
```



