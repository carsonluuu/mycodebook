# Deadlock in Java Multithreading

[**synchronized**](http://quiz.geeksforgeeks.org/synchronized-in-java/) keyword is used to make the class or method thread-safe which means only one thread can have lock of synchronized method and use it, other threads have to wait till the lock releases and anyone of them acquire that lock.  
It is important to use if our program is running in multi-threaded environment where two or more threads execute simultaneously. But sometimes it also causes a problem which is called [**Deadlock**](http://quiz.geeksforgeeks.org/operating-system-process-management-deadlock-introduction/). 

**Detect Dead Lock condition**

We can also detect deadlock by running this program on cmd. We have to collect Thread Dump. Command to collect depends on OS type. If we are using Windows and Java 8, command is jcmd $PID Thread.print  
We can get PID by running jps command.

**Avoid Dead Lock condition**

We can avoid dead lock condition by knowing its possibilities. It’s a very complex process and not easy to catch. But still if we try, we can avoid this. There are some methods by which we can avoid this condition. We can’t completely remove its possibility but we can reduce.

* **Avoid Nested Locks :**
  This is the main reason for dead lock. Dead Lock mainly happens when we give locks to multiple threads. Avoid giving lock to multiple threads if we already have given to one.
* **Avoid Unnecessary Locks :**
  We should have lock only those members which are required. Having lock on unnecessarily can lead to dead lock.
* **Using thread join :**
  Dead lock condition appears when one thread is waiting other to finish. If this condition occurs we can use Thread.join with maximum time you think the execution will take.

**Important Points :**

* If threads are waiting for each other to finish, then the condition is known as Deadlock.
* Deadlock condition is a complex condition which occurs only in case of multiple threads.
* Deadlock condition can break our code at run time and can destroy business logic.
* We should avoid this condition as much as we can.



