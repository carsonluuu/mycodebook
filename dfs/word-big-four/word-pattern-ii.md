# Word Pattern II

Given a`pattern`and a string`str`, find if`str`follows the same pattern.

Here **follow **means a full match, such that there is a [bijection](https://baike.baidu.com/item/双射/942799?fr=aladdin) between a letter in`pattern`and a **non-empty **substring in`str`.\(i.e if`a`corresponds to`s`, then`b`cannot correspond to`s`. For example, given pattern =`"ab"`, str =`"ss"`, return`false`.\)

Notice：

You may assume both`pattern`and`str`contains only lowercase letters.

### Example

Given pattern =`"abab"`, str =`"redblueredblue"`, return`true`.  
Given pattern =`"aaaa"`, str =`"asdasdasdasd"`, return`true`.  
Given pattern =`"aabb"`, str =`"xyzabcxzyabc"`, return`false`.

### Note

类似Word Pattern，不过这里没有给你分词了，需要自己暴力去试，依旧需要双向mapping（Map + Set）

逻辑：

* 如果map包含字符，看看当前substring是不是以这个map的value开头，不是就false了，递归传递子串
  ```java
  p.substring(1), 
  s.substring(map.get(c).length())
  ```
* 如果map不包含字符，暴力一个个位置拆分去试，for循环，如果set里面有，则continue继续找（必须双向映射）

  ```java
  p.substring(1)
  s.substring(i + 1)
  ```

Time：O\(2^len\_str\) \(因为隐含条件是 len\_pattern &lt;= len\_str\)

Space： O\(2^len\_str \* wordLength\)

### Code

```java
public class Solution {
    /**
     * @param pattern: a string,denote pattern string
     * @param str: a string, denote matching string
     * @return: a boolean
     */
    public boolean wordPatternMatch(String p, String s) {
        // write your code here
        Map<Character, String> map = new HashMap<>();
        Set<String> set = new HashSet<>();

        return helper(p, s, map, set);
    }

    private boolean helper(String p, String s, 
                           Map<Character, String> map,
                           Set<String> set) {
        if (p.length() == 0) {
            return s.length() == 0;
        }                       

        char c = p.charAt(0);
        if (map.containsKey(c)) {
            if (!s.startsWith(map.get(c))) {
                return false;
            }

            return helper(p.substring(1), 
                          s.substring(map.get(c).length()),
                          map, set);
        } else {
            for (int i = 0; i < s.length(); i++) {
                String word = s.substring(0, i + 1);
                if (set.contains(word)) {
                    continue;
                }
                map.put(c, word);
                set.add(word);
                if (helper(p.substring(1), 
                           s.substring(i + 1), 
                           map, set)) {
                    return true;           
                }
                set.remove(word);
                map.remove(c);
            }
        }

        return false;
    }
}
```



