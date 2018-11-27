# Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push\(x\) -- Push element x onto stack.
* pop\(\) -- Removes the element on top of the stack.
* top\(\) -- Get the top element.
* getMin\(\) -- Retrieve the minimum element in the stack.

### Example

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

### Note

使用两个栈，一个正常使用，一个用于记录最小值 所有操作是常数时间

push：对于正常栈，直接push。对于最小栈，如果其更小，压入，否则保持原样（是否做优化）

pop：优化的话，不是更小就不压入，所以要比较一下出栈的元素是不是和最小栈栈顶大小一样，一样也要出栈

### Code

```java
public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<Integer>();
        minStack = new Stack<Integer>();
    }

    public void push(int number) {
        stack.push(number);
        if (minStack.isEmpty()) {
            minStack.push(number);
        } else {
            minStack.push(Math.min(number, minStack.peek()));
        }
    }

    public int pop() {
        minStack.pop();
        return stack.pop();
    }

    public int min() {
        return minStack.peek();
    }
}
```

优化版

```java
class MinStack {

    private Stack<Integer> stack;
    private Stack<Integer> minstack;
    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
        minstack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        if (!minstack.isEmpty()) {
            int min = minstack.peek();
            if (x <= min)
                minstack.push(x);
        } else {
            minstack.push(x);
        }
    }

    public void pop() {
        int x = stack.pop();
        if (!minstack.isEmpty() && x == minstack.peek()) {
            minstack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minstack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```



