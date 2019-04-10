# [Scramble String](https://leetcode.com/problems/scramble-string/description/)

Given a string_s1_, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation of _s1_=`"great"`:

```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node`"gr"`and swap its two children, it produces a scrambled string`"rgeat"`.

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
```

We say that`"rgeat"`is a scrambled string of`"great"`.

Similarly, if we continue to swap the children of nodes`"eat"`and`"at"`, it produces a scrambled string`"rgtae"`.

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
```

We say that`"rgtae"`is a scrambled string of`"great"`.

Given two string _s1 _and _s2 _of the same length, determine if _s2 _is a scrambled string of _s1_.

### **Example**

**Example 1:**

```
Input:
 s1 = "great", s2 = "rgeat"

Output:
 true
```

**Example 2:**

```
Input:
 s1 = "abcde", s2 = "caebd"

Output:
 false
```

### Note

DP的方法难

暴力做+Memo优化

### Code

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1 == null || s2 == null) {
            return false;
        }
        
        if (s1.length() != s2.length()) {
            return false;
        }
        
        if (s1.equals(s2)) {
            return true;
        }
        
        int len = s1.length();
        int[] set = new int[26];
        for (int i = 0; i < len; i++) {
            set[s1.charAt(i) - 'a']++;
            set[s2.charAt(i) - 'a']--;
        }
        
        for (int i = 0; i < 26; i++) {
            if (set[i] != 0) {
                return false;
            }
        }
        
        for (int i = 1; i < len; i++) {
            if (isScramble(s1.substring(0, i), s2.substring(0, i)) &&
                isScramble(s1.substring(i), s2.substring(i))) {
                return true;
            }
            if (isScramble(s1.substring(0, i), s2.substring(len - i)) &&
                isScramble(s1.substring(i), s2.substring(0, len - i))) {
                return true;
            }
        }
        
        return false;
    }
}
```

```java
public class Solution {
    /**
     * @param s1 A string
     * @param s2 Another string
     * @return whether s2 is a scrambled string of s1
     */
    HashMap<String, Boolean> hash = new HashMap<String, Boolean>();

    public boolean isScramble(String s1, String s2) {
        // Write your code here
        if (s1.length() != s2.length())
            return false;

        if (hash.containsKey(s1 + "#" + s2))
            return hash.get(s1 + "#" + s2);

        int n = s1.length();
        if (n == 1) {
            return s1.charAt(0) == s2.charAt(0);
        }
        for (int k = 1; k < n; ++k) {
            if (isScramble(s1.substring(0, k), s2.substring(0, k)) && 
                isScramble(s1.substring(k, n), s2.substring(k, n))
                || isScramble(s1.substring(0, k), s2.substring(n - k, n)) &&
                   isScramble(s1.substring(k, n), s2.substring(0, n - k))) {
                hash.put(s1 + "#" + s2, true);
                return true;
            }
        }
        hash.put(s1 + "#" + s2, false);
        return false;
    }
}

```



