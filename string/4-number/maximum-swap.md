# [Maximum Swap](https://leetcode.com/problems/maximum-swap/description/)

Given a non-negative integer, you could swap two digits **at most **once to get the maximum valued number. Return the maximum valued number you could get.

### Example

**Example 1:**

```
Input: 2736

Output: 7236

Explanation: Swap the number 2 and the number 7.
```

**Example 2:**

```
Input: 9973

Output: 9973

Explanation: No swap.
```

### Note

本质是寻找右边第一个最大的和左边第一个比它小的。需要满足左右的位置关系

从右往左遍历，记录最大的值和位置，需要continue

遇到比最大小的就记录，一直往左会找到最左边比最大值小的那个数字

如果一直右往左一直递增，是特殊情况，第二个if语句不会执行，left会一直是-1，直接返回

### Code

```java
class Solution {
    public int maximumSwap(int num) {
        String s = String.valueOf(num);
        char[] c = s.toCharArray();
        int len = c.length;

        int left = -1, right = -1;
        int max = -1, index = -1;
        for (int i = len - 1; i >= 0; i--) {
            if (c[i] > max) {
                index = i;
                max = c[i];
                continue;
            }
            
            if (c[i] < max) {
                left = i;
                right = index;
            }
        }
        
        System.out.println(right + " " + left);
        
        if (left == -1) {
            return num;
        }
        
        char temp = c[left];
        c[left] = c[right];
        c[right] = temp;
        
        return Integer.parseInt(String.valueOf(c));
    }
}
```



