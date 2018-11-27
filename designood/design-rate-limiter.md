# [Logger Rate Limiter](https://leetcode.com/problems/logger-rate-limiter/description/)

Design a logger system that receive stream of messages along with its timestamps, each message should be printed if and only if it is**not printed in the last 10 seconds**.

Given a message and a timestamp \(in seconds granularity\), return true if the message should be printed in the given timestamp, otherwise returns false.

It is possible that several messages arrive roughly at the same time.

### **Example**

```
Logger logger = new Logger();

// logging string "foo" at timestamp 1
logger.shouldPrintMessage(1, "foo"); returns true; 

// logging string "bar" at timestamp 2
logger.shouldPrintMessage(2,"bar"); returns true;

// logging string "foo" at timestamp 3
logger.shouldPrintMessage(3,"foo"); returns false;

// logging string "bar" at timestamp 8
logger.shouldPrintMessage(8,"bar"); returns false;

// logging string "foo" at timestamp 10
logger.shouldPrintMessage(10,"foo"); returns false;

// logging string "foo" at timestamp 11
logger.shouldPrintMessage(11,"foo"); returns true;
```

### Note

用一个 hashmap 做一个类似 inverted index 功能就可以了，需要注意的地方是如果这轮输出了 true，要同时更新 hashmap 里面的 timestamp，输出 false 的时候不更新，因为还没 print.

### Code

```java
class Logger {
    Map<String, Integer> map;
    /** Initialize your data structure here. */
    public Logger() {
        map = new HashMap<>();
    }
    
    /** Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity. */
    public boolean shouldPrintMessage(int timestamp, String message) {
        boolean flag = false;
        if (!map.containsKey(message) || timestamp - map.get(message) >= 10) {
            flag = true;
            map.put(message, timestamp);
        }
        
        return flag;
    }
}

/**
 * Your Logger object will be instantiated and called as such:
 * Logger obj = new Logger();
 * boolean param_1 = obj.shouldPrintMessage(timestamp,message);
 */
```



