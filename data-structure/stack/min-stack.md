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

优化版 - 存差值，只用一个栈，缺点是需要数字类型转换，最大值减最小值会越界

```java
public class MinStack {
    long min;
    Stack<Long> stack;

    public MinStack(){
        stack=new Stack<>();
    }
    
    public void push(int x) {
        if (stack.isEmpty()){
            stack.push(0L);
            min=x;
        }else{
            stack.push(x-min);//Could be negative if min value needs to change
            if (x<min) min=x;
        }
    }

    public void pop() {
        if (stack.isEmpty()) return;
        
        long pop=stack.pop();
        
        if (pop<0)  min=min-pop;//If negative, increase the min value
        
    }

    public int top() {
        long top=stack.peek();
        if (top>0){
            return (int)(top+min);
        }else{
           return (int)(min);
        }
    }

    public int getMin() {
        return (int)min;
    }
}
```



