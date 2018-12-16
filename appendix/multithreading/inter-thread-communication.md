# Inter-thread Communication

**What is Polling and what are problems with it?**  
The process of testing a condition repeatedly till it becomes true is known as polling.

Polling is usually implemented with the help of loops to check whether a particular condition is true or not. If it is true, certain action is taken. This waste many CPU cycles and makes the implementation inefficient.  
For example, in a classic queuing problem where one thread is producing data and other is consuming it.

**How Java multi threading tackles this problem?**  
To avoid polling, Java uses three methods, namely,**wait\(\), notify\(\) and notifyAll\(\).**  
All these methods belong to object class as final so that all classes have them. They must be used within a synchronized block only.

* **wait\(\) - **It tells the calling thread to give up the lock and go to sleep until some other thread enters the same monitor and calls notify\(\).
* **notify\(\) - **It wakes up one single thread that called wait\(\) on the same object. It should be noted that calling notify\(\) does not actually give up a lock on a resource.
* **notifyAll\(\) - **It wakes up all the threads that called wait\(\) on the same object.

  




