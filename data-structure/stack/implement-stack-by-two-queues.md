# Implement Stack by Two Queues

Implement a stack by two queues. The queue is first in first out \(FIFO\). That means you can not directly pop the last element in a queue.

### Example

```
push(1)
pop()
push(2)
isEmpty() // return false
top() // return 2
pop()
isEmpty() // return true
```

### Note

### Code

```java
public class Stack {
    /*
     * @param x: An integer
     * @return: nothing
     */
    Queue<Integer> q;
    public Stack() {
        q = new LinkedList<>();
    }
    
    public void push(int x) {
        // write your code here
        q.offer(x);
        for (int i = 0; i < q.size() - 1; i++) {
            q.offer(q.poll());    
        }
    }

    /*
     * @return: nothing
     */
    public void pop() {
        // write your code here
        q.poll();
    }

    /*
     * @return: An integer
     */
    public int top() {
        // write your code here
        return q.peek();
    }

    /*
     * @return: True if the stack is empty
     */
    public boolean isEmpty() {
        // write your code here
        return q.isEmpty();
    }
}
```



