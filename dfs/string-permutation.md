# [String Permutation](https://www.lintcode.com/problem/string-permutation-ii/description)

Given a string, find all permutations of it without duplicates.

### Example

Given`"abb"`, return`["abb", "bab", "bba"]`.

Given`"aabb"`, return`["aabb", "abab", "baba", "bbaa", "abba", "baab"]`.

### Note

输入变成了char array，细节稍微有一点不一样

### Code

```java
public class Solution {
    /*
     * @param str: A string
     * @return: all permutations
     */
    public List<String> stringPermutation2(String str) {
        // write your code here
        List<String> result = new ArrayList<String>();
        if (str == null) {
            return result;
        }
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        int length = str.length();
        boolean[] visited = new boolean[length];
        String one = "";
        getList(chars, one, visited, result);
        return result;
    }

    public void getList(char[] chars, String one, boolean[] visited, List<String> result) {
        if (one.length() == chars.length) {
            result.add(one);
            return;
        }
        for (int i = 0; i < chars.length; i++) {
            if (visited[i] || 
               (i > 0 && chars[i] == chars[i-1] 
               && visited[i-1] == false)) {
                continue;
            }
            one += chars[i];
            visited[i] = true;
            getList(chars, one, visited, result);
            one = one.substring(0, one.length()-1);
            visited[i] = false;
        }
    }
}
```



