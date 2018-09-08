---
layout: post
title: Python Threading
date: 2018-01-27
---

## Multi-processing vs Threading

Threading 은 resource 공유
모든 Process 는 하나 이상의 thread를 가진다
하나의 Process 에 대해서 다수의 thread 존재 가능

```
# Ex (0)

from _thread import start_new_thread, allocate_lock
import time

# Problems may arise when threads share the same resource

number = 0

lock = allocate_lock()

def modifier(inp):
    global number
    number += 1
    time.sleep(1.0) # see how the result changes when you modify waiting time
    number = number * inp
    print(number)



thread1 = start_new_thread(modifier, (10,))
thread2 = start_new_thread(modifier, (10,))
thread3 = start_new_thread(modifier, (10,))
thread4 = start_new_thread(modifier, (10,))

while number < 10000:
    pass # this statement is used for all threads to end their job 
    	 # 									(instead of join())
```

## Threading in Python

파이썬은 기본적으로 single-thread이며, 파이썬 스크립트는 main thread에서 실행된다.

### Implementing Thread

파이썬에서 Thread를 만드는 방법은 크게 두 가지이다.

- 1. threading.Thread class 를 상속받은 뒤 run method 를 override 하는 방법(Recommended)
- 2. 실행 시키고자 하는 작업(= a callable object, for example a function)을 constructor(= \_\_init__) 에게 넘기는 방법

**1번으로 implement**

```
# Ex (1)

import threading

class MyClass(threading.Thread):
    def run(self):
        thread_name = self.getName()
        self.work()

    def work(self):
       t = threading.currentThread()
       str = input("type a sentence: ")
       print("in " + t.getName() + " print " + str)

def main():
    myclass = MyClass()
    myclass.start()

main()

```
**2번으로 implement8*

```
# Ex (2)

import threading


class MyClass():
	def __init__(self):
       self.thread1 = threading.Thread(name='thread1', target=self.work())
       self.thread1.start()

	def work(self):
       t = threading.currentThread()
       str = input("type a sentence: ")
       print("in " + t.getName() + " print " + str)


def main():
    myclass = MyClass()

main()

```

**2번의 simpler 버전**
<br>
참고 : threading 은 _thread를 기반으로 한 higher-level API module 이다. 예를 들면 자동으로 lock을 제공한다던가 하는, 사용자가 쓰기 쉬운 장점들이 있다.

```
# Ex (3)

from _thread import start_new_thread

class MyClass():
	def __init__(self):
		start_new_thread(function, argument)
	
		
```


### Thread Lock


-	같은 variable에 동시에 접근할 수 없도록 그리고 thread가 일을 완료하기 전까지 sleep하지 않도록 lock 을 걸어놓는 것



```
# Ex (4)
# Ex (0) 과 결과를 비교해 볼 것

from _thread import start_new_thread, allocate_lock
import time

# Problems may arise when threads share the same resource

number = 0

lock = allocate_lock()

def modifier(inp):
    global number
    lock.acquire() # start to lock
    number += 1
    time.sleep(1.0) 
    number = number * inp
    lock.release() # ends lock
    print(number)



thread1 = start_new_thread(modifier, (10,))
thread2 = start_new_thread(modifier, (10,))
thread3 = start_new_thread(modifier, (10,))
thread4 = start_new_thread(modifier, (10,))

while number < 10000:
    pass # this statement is used for all threads to end their job 
    	 # 									(instead of join())
```

### Daemon vs Non-Daemon thread

- Daemon thread 란 main program이 실행 중에 있을 때만 실행되는 thread 이다. 즉, main progrom이 exit하면 Daemon thread도 종료된다.


- Non-Daemon thread 가 default


### Join() 

- join 메쏘드를 call 한 thread가 일을 종료할 때까지 기다려준다

```
# Ex (5)

import threading

class MyClass(threading.Thread):
	def __init__(self):
		
	def run(self):
		thread_name = self.getName()
		str = printer()
		print("in " + thread_name + " print " + str)

def printer():
	input = input("type a sentence: ")
	return input
		
def main():
	myclass = MyClass()
	myclass.start()
	myclass.join() # myclass가 terminate 될 때까지 main thread가 기다려줌
	
```


### time Module

- time.sleep(second) : second 만큼 wait




### Queue

- 다수의 thread 가 하나의 resource를 쓰게 되면 골치 아파진다. Lock을 걸어야만 하는데, Lock을 걸지 않아도 Queue 를 사용해서 task를 각각의 thread에 나누면 된다.
- queue 에 [task1, task2, task3...] 이런 식으로 task 각각을 enqueue 한 뒤 각 thread가 순서대로(FIFO) task를 dequeue 해서 실행한다
- queue 가 empty 인 경우 block 된다 (= get()이 안된다는 뜻)
- 아래 예시는 5개의 웹페이지로부터 맨처음 1024바이트를 read해 오는 것이다
- 만약 5개의 웹페이지를 순차적으로 read 한다면 시간이 많이 걸리게 된다.
- 따라서 5개의 웹페이지를 동시에 read 하도록 multi threading 을 사용한다

- Queue 는 크게 세 가지 스텝으로 이루어진다 1) queue.Queue() 를 통해 queue 오브젝트 생성 2) queue.put() 을 통해 task 넣기 3) queue.get()을 통해 task 빼내기


```
Ex (6)

# ibm developer works의 예제 코드를 수정했음

import queue
import threading
from urllib import request
import time

hosts = ["http://yahoo.com", "http://google.com", "http://naver.com",
         "http://ibm.com", "http://apple.com"]
# "http://naver.com", "http://daum.net"

queue = queue.Queue()


class ThreadUrl(threading.Thread):
    """Threaded Url Grab"""
    def __init__(self, queue):
        threading.Thread.__init__(self)
        self.queue = queue



    def run(self):
            # grabs host from queue
        host = self.queue.get()
            # grabs urls of hosts and prints first 1024 bytes of page

        with request.urlopen(host) as f:
            print(f.read(1024))

        self.queue.task_done()



start = time.time()


def main():
    # spawn a pool of threads, and pass them queue instance
    for i in range(5):
        t = ThreadUrl(queue)
        t.setDaemon(True)
        t.start()

        # populate queue with data
    for host in hosts:
        queue.put(host)
    # wait on the queue until everything has been processed
    # (= get q.task_done() from all items in the queue)
    queue.join()


main()


print("Elapsed Time: %s" % (time.time() - start))

```
