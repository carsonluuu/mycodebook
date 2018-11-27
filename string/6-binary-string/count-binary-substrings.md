# [Count Binary Substrings](https://leetcode.com/problems/count-binary-substrings/description/)

Give a string`s`, count the number of non-empty \(contiguous\) substrings that have the same number of 0's and 1's, and all the 0's and all the 1's in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

**Example 1:**

```
Input: "00110011"
Output: 6
Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".

Notice that some of these substrings repeat and are counted the number of times they occur.

Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.
```

**Example 2:**

```
Input: "10101"
Output: 4
Explanation: There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.
```

### **Note**

大致就是算一下连续元素，并用pre来记录之前的结果，然后之前组和当前组取小的那个

First, I count the number of 1 or 0 grouped consecutively.  
For example "0110001111" will be`[1, 2, 3, 4]`.

Second, for any possible substrings with 1 and 0 grouped consecutively, the number of valid substring will be the minimum number of 0 and 1.  
For example "0001111", will be`min(3, 4) = 3`, \(`"01", "0011", "000111"`\)

记得加上最后的

### Code

```java
class Solution {
    public int countBinarySubstrings(String s) {
        int cur = 1, pre = 0, res = 0;
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) cur++;
            else {
                res += Math.min(cur, pre);
                pre = cur;
                cur = 1;
            }
        }
        return res + Math.min(cur, pre);
    }
}
```



