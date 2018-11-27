# Max Stack

Design a max stack that supports push, pop, top, peekMax and popMax.

1. push\(x\) -- Push element x onto stack.
2. pop\(\) -- Remove the element on top of the stack and return it.
3. top\(\) -- Get the element on the top.
4. peekMax\(\) -- Retrieve the maximum element in the stack.
5. popMax\(\) -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

### Example

```
MaxStack stack = new MaxStack();
stack.push(5); 
stack.push(1);
stack.push(5);
stack.top(); -> 5
stack.popMax(); -> 5
stack.top(); -> 1
stack.peekMax(); -> 5
stack.pop(); -> 1
stack.top(); -> 5
```

### Note

不是最优解，和之前的不同点在于Remove Max，需要链表结构来支持lgN的popMax\(\).

 这里使用了deque的API来去除最后出现的target，优先队列用于找最大值

### Code

```java
class MaxStack {
    
    Deque<Integer> dqStack;
    PriorityQueue<Integer> pqMax;

    /** initialize your data structure here. */
    public MaxStack() {
        dqStack = new ArrayDeque<>();
        pqMax = new PriorityQueue<>( (a,b) ->(b - a) );
    }
    
    public void push(int x) {
        dqStack.addLast(x);
        pqMax.offer(x);
    }
    
    public int pop() {
        int deleteE = dqStack.removeLast();
        pqMax.remove(deleteE);
        return deleteE;
    }
    
    public int top() {
        return dqStack.getLast();
    }
    
    public int peekMax() {
        return pqMax.peek();
    }
    
    public int popMax() {
        int deleteE = pqMax.poll();
        dqStack.removeLastOccurrence(deleteE);
        return deleteE;
    }
}
```



