# Find the Missing Number II

Giving a string with number from 1-`n`in random order, but miss`1`number.Find that number.

### Example

**Example1**

```
Input: n = 20 and str = 19201234567891011121314151618
Output: 17
Explanation:
19'20'1'2'3'4'5'6'7'8'9'10'11'12'13'14'15'16'18
```

**Example2**

```
Input: n = 6 and str = 56412
Output: 3
Explanation:
5'6'4'1'2
```

### Note

两种写法，传字符串还是传index，没次分两个位置，对数字的数组进行isFound的backtracking

### Code

```java
public class Solution {
    /**
     * @param n: An integer
     * @param str: a string with number from 1-n in random order and miss one number
     * @return: An integer
     */
    private int missing;
    
    public int findMissing2(int n, String str) {
        // write your code here
        // 19201234567891011121314151618
        missing = -1;
        
        //helper(n, str, 0, new boolean[n + 1]);
        dfs(n, str, new boolean[n + 1]);
        
        return missing;
    }
    
    private void dfs(int n, String s, boolean[] isFound) {
        if (missing != -1) {
            return;
        }
        
        if (s.equals("")) {
            for (int i = 1; i <= n; i++) {
                if (!isFound[i]) {
                    missing = i;
                    return;
                }
            }
            return;
        }
        
        if (s.charAt(0) == '0') {
            return;
        }
        
        for (int i = 1; i <= 2; i++) {
            if (i <= s.length()) {
                int num = Integer.parseInt(s.substring(0, i));
                if (0 < num && num <= n && !isFound[num]) {
                    isFound[num] = true;
                    dfs(n, s.substring(i), isFound);
                    isFound[num] = false;
                }
            }
        }
    }
    
    private void helper(int n, 
                        String str, 
                        int start,
                        boolean[] isFound) {
        if (missing != -1) {
            return;
        }
        
        if (start == str.length()) {
            for (int i = 1; i <= n; i++) {
                if (!isFound[i]) {
                    missing = i;
                    return;
                }
            }
            return;
        }
        
        if (str.charAt(start) == '0') {
            return;
        }
        
        for (int i = start; i <= start + 1 && i < str.length(); i++) {
            int num = Integer.parseInt(str.substring(start, i + 1));
            if (num > 0 && num <= n && !isFound[num]) {
                isFound[num] = true;
                helper(n, str, i + 1, isFound);
                isFound[num] = false;
            }
        }
    }
}
```



