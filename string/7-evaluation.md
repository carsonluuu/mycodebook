# [Simplify Path](https://leetcode.com/problems/simplify-path/description/)

Given an absolute path for a file \(Unix-style\), simplify it.

-

In a UNIX-style file system, a period \('.'\) refers to the current directory, so it can be ignored in a simplified path. Additionally, a double period \(".."\) moves up a directory, so it cancels out whatever the last directory was. For more information, look here: [https://en.wikipedia.org/wiki/Path\_\(computing\)\#Unix\_style](https://en.wikipedia.org/wiki/Path_%28computing%29#Unix_style)

**Corner Cases:**

* Did you consider the case where **path **= `"/../"`? In this case, you should return`"/"`.
* Another corner case is the path might contain multiple slashes`'/'`together, such as`"/home//foo/"`.
  In this case, you should ignore redundant slashes and return`"/home/foo"`.

### Example

**path**=`"/home/"`, =&gt;`"/home"`  
**path**=`"/a/./b/../../c/"`, =&gt;`"/c"`  
**path**=`"/a/../../b/../c//.//"`, =&gt;`"/c"`  
**path**=`"/a//b////c/d//././/.."`, =&gt;`"/a/b/c"`

### Note

String\[\] paths = path.split\("/+"\) -&gt; 分割

stack来处理情况：

* 是 ”..“ 需要pop
* 不是"." 也不是""，进栈

```
//注意这个case
if (res.length() == 0) {
    return "/";
}
```

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



