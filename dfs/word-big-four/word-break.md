# [Word Break](https://leetcode.com/problems/word-break/description/)

Given a **non-empty **string\_s \_and a dictionary \_wordDict \_containing a list of **non-empty **words, determine if\_s\_can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

### Example

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]

Output: true

Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple", "pen"]

Output: true

Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".

Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]

Output: false
```

### Note

其实不简单的，可以采用dp或者记忆化搜索两种方法，注意的一点是，这个是存在就行，一旦满足（True）就要立即返回true

Time：O\(n^2\)

Space：O\(n\)

###### DP

思路就是对于一个词可以有length + 1个分割点，使用DP数组来记录在i位置分割，i左边能不能行，dp\[s.length\(\)\]就是结果。我们两层loop遍历，i - j 表示从 i 点开始往前j个点的位置，看这个分割点之前的能不能在字典中，一旦能的话就OK这个分割点设为true，然后记得要break

```
for j < i: dp[i] = true whenever (dp[j] && wordDict.contains(s.substring(j, i))
```

###### Memo

这里用类似Word Break II的方法，本质还是和DP类似，Memo表的key的是substring，value是boolean

通过dfs不断自顶向下的递归，以i作为分割点，看分割点之前是否存在于字典，分割点之后送入dfs进行递归，如果是一旦TRUE就写入并返回

### Code

Version 1 - DP

```java
public boolean wordBreak(String s, List<String> wordDict) {
    boolean[] dp = new boolean[s.length() + 1];
    dp[0] = true;
    for (int i = 1; i <= s.length(); i++) {
        for (int j = 0; j < i; j++) {
            if (dp[j] && wordDict.contains(s.substring(j, i))) {
                dp[i] = true;
                break;
            }
        }
    }       
    return dp[s.length()];
}
```

Version 2 - Memo

```java
public boolean wordBreak2(String s, List<String> wordDict) {
        Map<String, Boolean> mem = new HashMap<String, Boolean>();
        return helper(mem, s, wordDict);
    }

private boolean helper(Map<String, Boolean> mem, 
                       String s, 
                       List<String> wordDict) {

    if (mem.containsKey(s)) { return mem.get(s); }
    if (wordDict.contains(s)) {
        mem.put(s, true); 
        return true;
    }
    for (int i = 1; i < s.length(); i++) {
        if (wordDict.contains(s.substring(0, i)) && helper(mem, s.substring(i), wordDict)) {
            mem.put(s, true); 
            return true;
        }
    }
    mem.put(s, false); 
    return false;
}
```



