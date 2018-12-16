# Semaphore

A semaphore controls access to a shared resource through the use of a counter. If the counter is greater than zero, then access is allowed. If it is zero, then access is denied. What the counter is counting are permits that allow access to the shared resource. Thus, to access the resource, a thread must be granted a permit from the semaphore.

In general, to use a semaphore, the thread that wants access to the shared resource tries to acquire a permit.

* If the semaphore’s count is greater than zero, then the thread acquires a permit, which causes the semaphore’s count to be decremented.
* Otherwise, the thread will be blocked until a permit can be acquired.
* When the thread no longer needs an access to the shared resource, it releases the permit, which causes the semaphore’s count to be incremented.
* If there is another thread waiting for a permit, then that thread will acquire a permit at that time.

Java provide **Semaphore **class in_java.util.concurrent_package that implements this mechanism, so you don’t have to implement your own semaphores.

**Using Semaphores as Locks\(**[**preventing race condition**](https://practice.geeksforgeeks.org/problems/what-is-race-condition)**\)**

A **race condition** is an undesirable situation that occurs when a device or system attempts to perform two or more operations at the same time, but because of the nature of the device or system, the operations must be done in the proper sequence to be done correctly.

We can use a semaphore to lock access to a resource, each thread that wants to use that resource must first call _acquire\( \)_

before accessing the resource to acquire the lock. When the thread is done with the resource, it must call _release\( \) _to release lock. Here is an example that demonstrate this

https://www.geeksforgeeks.org/semaphore-in-java/

