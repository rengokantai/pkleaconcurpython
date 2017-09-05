# pkleaconcurpython

## 3. Parallelize it
### Understanding concurrency

#### I/O bottlenecks
__If the rate at which data is requested is slower than the rate at which it is consumed, then you have an I/O bottleneck.__
```
import urllib.request
import time
t0 = time.time()
req = urllib.request.urlopen('http://www.example.com')
pageHtml = req.read()
t1 = time.time()
print("Total Time To Fetch Page: {} Seconds".format(t1-t0))
```

BeautifulSoup
```
import urllib.request
import time
from bs4 import BeautifulSoup

t0 = time.time()
req = urllib.request.urlopen('http://www.example.com')
t1 = time.time()
print("Total Time To Fetch Page: {} Seconds".format(t1-t0))
soup = BeautifulSoup(req.read(), "html.parser")

for link in soup.find_all('a'):
  print(link.get('href'))

t2 = time.time()
print("Total Execeution Time: {} Seconds".format)
```
