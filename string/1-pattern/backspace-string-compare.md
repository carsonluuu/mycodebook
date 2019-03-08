# [Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/description/)

Given two strings `S` and`T`, return if they are equal when both are typed into empty text editors.`#`means a backspace character.

### **Example**

**Example 1:**

```
Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
```

**Example 2:**

```
Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
```

**Example 3:**

```
Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
```

**Example 4:**

```
Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
```

### Note

最优解就是

* 记录\#的数目，反向遍历。
* 当遇到\#大于0的时候就跳过下一个字符，并减少\#的count
* 如果遇到的是字符，且\#的count是0，就相互直接比较
* i或者j应该同时到起点

比较不太好写

### Code

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        if (S == null || T == null) {
            return true;
        }
        System.out.println(deal(S));
        System.out.println(deal(T));
        return deal(S).equals(deal(T));

    }

    private String deal(String S) {
        Stack<Character> stack = new Stack<>();
        //S = "a##c", T = "#a#c"
        for (char c : S.toCharArray()) {
            if (c == '#' && !stack.isEmpty()) {
                stack.pop();
            } else if (c != '#') {
                stack.push(c);
            }
        }
        return String.valueOf(stack);
    }
}
```

```java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        int i = S.length() - 1, j = T.length() - 1;
        int skipS = 0, skipT = 0;

        while (i >= 0 || j >= 0) { // While there may be chars in build(S) or build (T)
            while (i >= 0) { // Find position of next possible char in build(S)
                if (S.charAt(i) == '#') {skipS++; i--;}
                else if (skipS > 0) {skipS--; i--;}
                else break;
            }
            while (j >= 0) { // Find position of next possible char in build(T)
                if (T.charAt(j) == '#') {skipT++; j--;}
                else if (skipT > 0) {skipT--; j--;}
                else break;
            }
            // If two actual characters are different
            if (i >= 0 && j >= 0 && S.charAt(i) != T.charAt(j))
                return false;
            // If expecting to compare char vs nothing
            if ((i >= 0) != (j >= 0))
                return false;
            i--; j--;
        }
        return true;
    }
}
```



