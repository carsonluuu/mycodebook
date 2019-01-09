# [Word Break II](https://leetcode.com/problems/word-break-ii/description/)

Given a **non-empty **string\_s\_and a dictionary\_wordDict\_containing a list of **non-empty **words, add spaces in\_s\_to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

### Example

**Example 1:**

```
Input: 

s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]

Output:
[
  "cats and dog",
  "cat sand dog"
]
```

**Example 2:**

```
Input:

s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]

Output:

[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]

Explanation:
 Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]

Output:
[]
```

### Note

与之前Word Break I不同的是，这里要求打印出所有组合，所以memo变成这个substring对应其可以被拆出来的list of String，dfs的返回值也是list of String。所以还是遍历所有分割点，分割点之前prefix需要在字典里，分割点之后的suffix送入递归，把其返回结果依次加入

Time worst：O\(2^n\) -&gt; O\(n^2\)

Space: O\(2^n\)

 解释：

```
dict = ["a", "aa", "aaa", "aaaa" ...]
string = "aaaaaaaaaa ...."
```

这种例子中，意味着 string 中`任意分割`方案，都是合法的分割方案，也就是说，“aaaaaa..” 存在多少中分割方法，就是多少个答案。那么有多少个分割方法呢？`2^(n-1)`。因为任何两个a之间的间隙都可以选择割开或者不割开。那么n-1个间隙，就有 2^\(n-1\) 个分割方案。

### Code

```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> res = new ArrayList<>();
        if (s == null || s.length() == 0) {
            return res;
        }

        Set<String> dict = new HashSet<>();
        for (String str : wordDict) {
            dict.add(str);
        }

        Map<String, List<String>> memo = new HashMap<>();

        return helper(s, dict, memo);
    }

    private List<String> helper(String s, 
                                Set<String> dict,
                                Map<String, List<String>> memo) {
        if (memo.containsKey(s)) {
            return memo.get(s);
        }

        List<String> res = new ArrayList<>();
        if (dict.contains(s)) {
            res.add(s);
        }

        for (int len = 1; len < s.length(); len++) {
            String word = s.substring(0, len);
            if (!dict.contains(word)) {
                continue;
            }
            String suffix = s.substring(len);
            List<String> seg = helper(suffix, dict, memo);
            for (String ss : seg) {
                res.add(word + " " + ss);
            }
        }

        memo.put(s, res);
        return res; 
    }
}
```



