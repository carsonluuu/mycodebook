# **Thread Pools**

Server Programs such as database and web servers repeatedly execute requests from multiple clients and these are oriented around processing a large number of short tasks. An approach for building a server application would be to create a new thread each time a request arrives and service this new request in the newly created thread. While this approach seems simple to implement, it has significant disadvantages. A server that creates a new thread for every request would spend more time and consume more system resources in creating and destroying threads than processing actual requests.

Since active threads consume system resources, a[JVM](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)creating too many threads at the same time can cause the system to run out of memory. This necessitates the need to limit the number of threads being created.

**What is ThreadPool in Java?**

**A thread pool reuses previously created threads to execute current tasks and offers a solution to the problem of thread cycle overhead and resource thrashing.**Since the thread is already existing when the request arrives, the delay introduced by thread creation is eliminated, making the application more responsive.

**Risks in using Thread Pools**

* * 1. [**Deadlock**](https://www.geeksforgeeks.org/deadlock-in-java-multithreading/)**:**
       While deadlock can occur in any multi-threaded program, thread pools introduce another case of deadlock, one in which all the executing threads are waiting for the results from the blocked threads waiting in the queue due to the unavailability of threads for execution.
    2. **Thread Leakage :**
       Thread Leakage occurs if a thread is removed from the pool to execute a task but not returned to it when the task completed. As an example, if the thread throws an exception and pool class does not catch this exception, then the thread will simply exit, reducing the size of the thread pool by one. If this repeats many times, then the pool would eventually become empty and no threads would be available to execute other requests.
    3. **Resource Thrashing :**
       If the thread pool size is very large then time is wasted in context switching between threads. Having more threads than the optimal number may cause starvation problem leading to resource thrashing as explained.



