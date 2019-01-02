# [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)

Given a string containing just the characters`'('`,`')'`,`'{'`,`'}'`,`'['`and`']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

### **Example**

**Example 1:**

```
Input:
 "()"

Output:
 true
```

**Example 2:**

```
Input:
 "()[]{}"

Output:
 true
```

**Example 3:**

```
Input:
 "(]"

Output:
 false
```

**Example 4:**

```
Input:
 "([)]"

Output:
 false
```

**Example 5:**

```
Input:
 "{[]}"

Output:
 true
```

### Note

匹配对应的

### Code

```java
class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<Character, Character>();
        map.put('(', ')');
        map.put('[', ']');
        map.put('{', '}');
        
        Stack<Character> stk = new Stack<Character> ();
        
        for(int i = 0; i < s.length(); i++){
            Character c = s.charAt(i);
            switch(c){
                case '(':
                case '[':
                case '{':
                    stk.push(c);break;
                case ')':
                case ']':
                case '}':
                    if( stk.isEmpty() || c != map.get(stk.pop()) ){
                        return false;
                    }
            }
        }
        return stk.isEmpty();
    }
}
```



