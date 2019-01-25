# [Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/)

Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

### Example

**Example 1:**

```
Input: "bcabc"
Output: "abc"
```

**Example 2:**

```
Input: "cbacdcbc"
Output: "acdb"
```

### Note

维护一个单调递增的栈，栈内元素唯一。同时维护一个counting map

遍历元素，对于栈：

* 遇到栈内出现的元素，跳过
* 遇到栈顶元素比当前元素大的，根据counting map的情况进行pop（贪心法则：不是唯一的，那么我们到后面再去加它）

遍历元素，对于counting map：

* 更新其出现的counting

### Code

```java
class Solution {
    public String removeDuplicateLetters(String S) {
        Stack<Character> s = new Stack<>();
        Set<Character> visited = new HashSet<>();
        int[] set = new int[26];
        for (char c : S.toCharArray()) {
            set[c - 'a']++;    
        }

        for (char c : S.toCharArray()) {
            set[c - 'a']--;
            if (visited.contains(c)) { continue; }
            while (!s.isEmpty() && c < s.peek() && set[s.peek() - 'a'] != 0) {
                visited.remove(s.pop());
            }
            s.push(c);
            visited.add(c);
        }

        StringBuilder sb = new StringBuilder();
        while (!s.isEmpty()) {
            sb.append(s.pop());
        }

        return sb.reverse().toString();
    }
}
```



