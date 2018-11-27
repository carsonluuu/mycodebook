# [Word Pattern](https://leetcode.com/problems/word-pattern/description/)

Given a`pattern`and a string`str`, find if`str`follows the same pattern.

Here **follow **means a full match, such that there is a bijection between a letter in`pattern`and a **non-empty **word in`str`.

### Example

**Example 1:**

```
Input: pattern = "abba", str = "dog cat cat dog"
Output: true
```

**Example 2:**

```
Input:pattern = "abba", str = "dog cat cat fish"
Output: false
```

**Example 3:**

```
Input: pattern = "aaaa", str = "dog cat cat dog"
Output: false
```

**Example 4:**

```
Input: pattern = "abba", str = "dog dog dog dog"
Output: false
```

**Notes:**  
You may assume`pattern`contains only lowercase letters, and`str`contains lowercase letters separated by a single space.

### Note

建立mapping：key是character，value是word

set记录出现的word

必须是双向映射：

* 当key存在，mapping对应的单词不相同时，就false
* 当value存在，mapping对应的字符不存在，就false

Time：O\(n\) - pattern length

Space：O\(n\)

### Code

```java
public class Solution {
    /**
     * @param pattern: a string, denote pattern string
     * @param str: a string, denote matching string
     * @return: an boolean, denote whether the pattern string and the matching string match or not
     */
    public boolean wordPattern(String pattern, String str) {
        // write your code here
        char[] patterns = pattern.toCharArray();
        String[] words = str.split(" ");

        Map<Character, String> map = new HashMap<>();
        Set<String> set = new HashSet<>();

        for (int i = 0; i < patterns.length; i++) {
            if (map.containsKey(patterns[i])) {
                if (!map.get(patterns[i]).equals(words[i])) {
                    return false;
                }
                continue;
            }

            if (set.contains(words[i])) {
                return false;
            }

            map.put(patterns[i], words[i]);
            set.add(words[i]);
        }

        return true;
    }
}
```



