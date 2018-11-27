# [Longest Substring with At Most K Distinct Characters](https://www.lintcode.com/problem/longest-substring-with-at-most-k-distinct-characters/description)

Given a string_s_, find the length of the longest substring T that contains at most k distinct characters.

### Example

For example, Given s =`"eceba"`,`k = 3`,

T is`"eceb"`which its length is`4`.

### Code

```java
public class Solution {
    /**
     * @param s: A string
     * @param k: An integer
     * @return: An integer
     */
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        // write your code here
        int res = 0;
        if (s == null || s.length() == 0) {
            return res;
        }
        int len = s.length();
        int j = 0, count = 0;
        int[] set = new int[256];
        for (int i = 0; i < len; i++) {
            while (j < len && count <= k) {
                if (set[s.charAt(j)]++ == 0) {
                    if (count == k) {
                        set[s.charAt(j)]--; //otherwise j will process one more
                        break;
                    }
                    count++;
                }
                j++;
            }

            res = Math.max(res, j - i);

            if (set[s.charAt(i)] == 1) {
                count--;
            }
            set[s.charAt(i)]--;
        }

        return res;
    }
}
```



