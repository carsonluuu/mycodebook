# [Minimum Window Substring](https://www.lintcode.com/problem/minimum-window-substring/description)

Given a string source and a string target, find the minimum window in source which will contain all the characters in target.

### Example

For source =`"ADOBECODEBANC"`, target =`"ABC"`, the minimum window is`"BANC"`

### Note

稍微复杂一点的滑动窗口

需要包括所有的给定字符，所以得先加入set

### Code

```java
public class Solution {
    /**
     * @param source : A string
     * @param target: A string
     * @return: A string denote the minimum window, return "" if there is no such a string
     */
    public String minWindow(String source , String target) {
        // write your code here
        String res = "";
        if (target == null || target.length() == 0) {
            return res;
        }
        
        int[] set = new int[256];
        for (char c : target.toCharArray()) {
            set[c]++;
        }
        
        int matched = 0, minLen = Integer.MAX_VALUE;
        int j = 0, len = target.length();
        for (int i = 0; i < source.length(); i++) {
            while (j < source.length() && matched < len) {
                if (set[source.charAt(j)] > 0) {
                    matched++;
                }
                
                set[source.charAt(j)]--;
                j++;
            }
            
            if (j - i < minLen && matched == len) {
                minLen = j - i;
                res = source.substring(i, j);
            }
            
            if (set[source.charAt(i)] >= 0) {
                matched--;
            }
            set[source.charAt(i)]++;
        }
        
        return res;
    }
}
```



