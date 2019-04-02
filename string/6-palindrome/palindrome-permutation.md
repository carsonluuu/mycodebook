# [Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation/description/)

Given a string, determine if a permutation of the string could form a palindrome.

### Example

**Example 1:**

```
Input:
"code"
Output:
 false
```

**Example 2:**

```
Input:
"aab"
Output:
 true
```

**Example 3:**

```
Input:
"carerac"
Output:
 true
```

### Note

计数一下吧，count最后是0或者1。1对应一个单独在最中间，且长度会一定是奇数

### Code

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }
        int[] set = new int[256];
        int cnt = 0;
        for (int i = 0; i < s.length(); i++) {
            set[s.charAt(i)]++;
            if (set[s.charAt(i)] % 2 == 0) {
                cnt--;
            } else {
                cnt++;
            }
        }
        
        return cnt <= 1;
    }
}
```

打印所有的结果，需要用DFS了

一样判断，然后使用permutation去两边加reverse和不reverse的结果

```java
class Solution {
    public List<String> generatePalindromes(String s) {
        int odd = 0;
        String mid = "";
        List<String> res = new ArrayList<>();
        List<Character> list = new ArrayList<>();
        Map<Character, Integer> map = new HashMap<>();
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            map.put(c, map.getOrDefault(c, 0) + 1);
            odd += map.get(c) % 2 != 0 ? 1 : -1;
        }
        
        for (Map.Entry<Character, Integer> e : map.entrySet()) {
            char key = e.getKey();
            int value = e.getValue();
            
            if (value % 2 == 1) {
                mid += key;
            }
            for (int i = 0; i < value / 2; i++) {
                list.add(key);
            }
        }
        
        if (odd > 1) {
            return res;
        }
        
        permutation(list, new StringBuilder(), res, new boolean[list.size()], mid);
        
        return res;
        
    }
    
    private void permutation(List<Character> list, StringBuilder sb, 
                        List<String> res, boolean[] visited,
                        String mid) {
        if (sb.length() == list.size()) {
            res.add(sb.toString() + mid + sb.reverse().toString());
            sb.reverse();
            return;
        }
        
        for (int i = 0; i < list.size(); i++) {
            if (visited[i]) {
                continue;
            }
            if (i > 0 && list.get(i) == list.get(i - 1) && !visited[i - 1]) {
                continue;
            }

            sb.append(list.get(i));
            visited[i] = true;
            permutation(list, sb, res, visited, mid);
            visited[i] = false;
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```



