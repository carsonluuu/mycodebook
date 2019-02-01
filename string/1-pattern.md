# [One Edit Distance](https://leetcode.com/problems/one-edit-distance/description/)

Given two strings**s** and**t**, determine if they are both one edit distance apart.

**Note:**

There are 3 possiblities to satisfy one edit distance apart:

1. Insert a character into _**s**_ to get _**t**_
2. Delete a character from _**s **_to get _**t**_
3. Replace a character of _**s**_ to get _**t**_

### Example

**Example 1:**

```
Input:
s = "ab", 
t = "acb"

Output: true

Explanation:
 We can insert 'c' into s
 to get t.
```

**Example 2:**

```
Input:
s = "cab", 
t = "ad"

Output:
 false

Explanation:
 We cannot get t from s by only one step.
```

**Example 3:**

```
Input:
s = "1203", 
t = "1213"

Output:
 true

Explanation:
 We can replace '0' with '1' to get t.
```

### Note

当当前位置不一样的时候，根据三种情况分别比较substring

edge case "" and "1"，最后判断一下

```
Math.abs(s.length() - t.length()) == 1;
```

### Code 

```java
public boolean isOneEditDistance(String s, String t) {
    for (int i = 0; i < Math.min(s.length(), t.length()); i++) {
        if (s.charAt(i) != t.charAt(i)) {
            if (s.length() == t.length()) {
                return s.substring(i + 1).equals(t.substring(i + 1));    
            } else if (s.length() > t.length()) {
                return s.substring(i + 1).equals(t.substring(i));
            } else {
                return s.substring(i).equals(t.substring(i + 1));
            }
        }
    }
    return Math.abs(s.length() - t.length()) == 1;
}
```



