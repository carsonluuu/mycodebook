# [Generalized Abbreviation](https://leetcode.com/problems/generalized-abbreviation/)

Write a function to generate the generalized abbreviations of a word.

**Note: **The order of the output does not matter.

### **Example**

```
Input: "word"
Output: ["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```

### Note

这里考虑一下缩写还是不缩写，开始传入一个空字符串，退出条件是position index（一直累加）达到字符串的长度

* 缩写：记录count加1
* 不缩写：当前字符串加上当前count数再加上当前字符，然后清空count

### Code

```java
class Solution {
    public List<String> generateAbbreviations(String word) {
        List<String> res = new ArrayList<>();

        helper(word, res, "", 0, 0);

        return res;
    }

    private void helper(String word, List<String> res, String curr,
                        int pos, int count) {
        if (pos == word.length()) {
            res.add(count > 0 ? curr + count : curr);
            return;
        }

        helper(word, res, curr, pos + 1, count + 1);
        helper(word, res, curr + (count > 0 ? count : "") + word.charAt(pos), pos + 1, 0);
    }
}
```



