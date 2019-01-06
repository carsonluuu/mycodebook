# [Minimum Window Substring](https://www.lintcode.com/problem/minimum-window-substring/description)

Given a string source and a string target, find the minimum window in source which will contain all the characters in target.

### Example

For source =`"ADOBECODEBANC"`, target =`"ABC"`, the minimum window is`"BANC"`

### Note

稍微复杂一点的滑动窗口，需要返回窗口的开始和结束的位置

需要包括所有的给定字符，所以得先加入set，需要维护一个`match`变量，不管是否match了就把对应的减1，因为在左边走的时候要加回来，这里是因为给定的target也会有重复的，要set值是0了才能说都包括了

取最值的时候要判断一下条件，因为我们需要两个指针的值对应的子串

```java
if (set[source.charAt(i)] >= 0) {
    matched--;
}
```

这这个判断说明这个还是有match的，我们要把match的值减回去，因为现在在移动左边界了

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



