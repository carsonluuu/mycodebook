# [Simplify Path](https://leetcode.com/problems/simplify-path/description/)

Given an **absolute path **for a file \(Unix-style\), simplify it. Or in other words, convert it to the **canonical path**.

In a UNIX-style file system, a period`.` refers to the current directory. Furthermore, a double period`..` moves the directory up a level. For more information, see: [Absolute path vs relative path in Linux/Unix](https://www.linuxnix.com/abslute-path-vs-relative-path-in-linuxunix/)

Note that the returned canonical path must always begin with a slash`/`, and there must be only a single slash`/` between two directory names. The last directory name \(if it exists\)**must not** end with a trailing`/`. Also, the canonical path must be the **shortest **string representing the absolute path.

### Example

**Example 1:**

```
Input: "
/home/"
Output: "
/home"

Explanation:
 Note that there is no trailing slash after the last directory name.
```

**Example 2:**

```
Input: "
/../"
Output: "
/"
Explanation:
 Going one level up from the root directory is a no-op, as the root level is the highest level you can go.

```

**Example 3:**

```
Input: "
/home//foo/"
Output: "
/home/foo"
Explanation: 
In the canonical path, multiple consecutive slashes are replaced by a single one.

```

**Example 4:**

```
Input: "
/a/./b/../../c/"
Output: "
/c"
```

**Example 5:**

```
Input: "
/a/../../b/../c//.//"
Output: "
/c"
```

**Example 6:**

```
Input: "
/a//b////c/d//././/.."
Output: "
/a/b/c"

```

### Note

按 “/+” split，遇到“..”pop，遇到不是“.”或者“”就入栈

### Code

```java
class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        String[] paths = path.split("/+");
        for (String s : paths) {
            if (s.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();   
                }                
            } else if(!s.equals(".") && !s.equals(""))
                stack.push(s);
        }
        String res = "";
        while (!stack.isEmpty()) { 
            res = "/" + stack.pop() + res;
        }
        if (res.length() == 0) {
            return "/";
        }
        return res;
    }
}
```



