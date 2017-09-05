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

## Life of a Thread
### Threads in Python
#### Thread State
Five states:
- New Thread: In the New Thread state, our thread hasn't started, and it hasn't been allocated resources. 

sample:
```
import threading
import time
# A very simple method for our thread to execute
def threadWorker():
  # it is only at the point where the thread starts executing
  # that it's state goes from 'Runnable' to a 'Running'
  # state
  print("My Thread has entered the 'Running' State")
  # If we call the time.sleep() method then our thread
  # goes into a not-runnable state. We can do no further work
  # on this particular thread
  time.sleep(10)
  # Thread then completes its tasks and terminates
  print("My Thread is terminating")

# At this point in time, the thread has no state
# it hasn't been allocated any system resources
myThread = threading.Thread(target=threadWorker)
# When we call myThread.start(), Python allocates the necessary system 
# resources in order for our thread to run and then calls the thread's
# run method. It goes from 'Starting' state to 'Runnable' but not running 
myThread.start()
# Here we join the thread and when this method is called
# our thread goes into a 'Dead' state. It has finished the
# job that it was intended to do.
myThread.join()
print("My Thead has entered a 'Dead' state")
```


output
```
My Thread has entered the 'Running' State
My Thread is terminating
My Thead has entered a 'Dead' state
```
#### Different types of threads

#### The ways to start a thread


### Starting loads of threads
#### Example
```
import threading
import time
import random

def executeThread(i):
  print("Thread {} started".format(i))
  sleepTime = random.randint(1,10)
  time.sleep(sleepTime)
  print("Thread {} finished executing".format(i))
for i in range(10):
  thread = threading.Thread(target=executeThread, args=(i,))
  thread.start()
  print("Active Threads:" , threading.enumerate())
```
