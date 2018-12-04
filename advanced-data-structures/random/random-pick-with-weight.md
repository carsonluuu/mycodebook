# [Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/description/)

Given an array`w`of positive integers, where`w[i]`describes the weight of index`i`, write a function`pickIndex` which randomly picks an index in proportion to its weight.

Note:

1. `1 <= w.length <= 10000`
2. `1 <= w[i] <= 10^5`
3. `pickIndex` will be called at most`10000`times.

### Example

**Example 1:**

```
Input: 
["Solution","pickIndex"]
[[[1]],[]]
Output: 
[null,0]
```

**Example 2:**

```
Input: 
["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
Output: 
[null,0,1,1,1,0]
```

**Explanation of Input Syntax:**

The input is two lists: the subroutines called and their arguments. `Solution`'s constructor has one argument, the array`w`.`pickIndex`has no arguments. Arguments are always wrapped with a list, even if there aren't any.

### Note

Use accumulated freq array to get idx.  
w\[\] = {2,5,3,4} =&gt; wsum\[\] = {2,7,10,14}  
then get random val`random.nextInt(14)+1`, idx is in range`[1,14]`

```
idx in [1,2] return 0
idx in [3,7] return 1
idx in [8,10] return 2
idx in [11,14] return 3
```

then become LeetCode 35. Search Insert Position  
Time:`O(n)`to init,`O(logn)`for one pick  
Space:`O(n)`

### Code

```java
class Solution {
    Random random;
    int[] presum;
    int[] nums;
    public Solution(int[] w) {
        int len = w.length;
        nums = w;
        random = new Random();
        presum = new int[len + 1];
        for (int i = 0; i < len; i++) {
            presum[i + 1] = presum[i] + w[i];
        }
    }
    
    public int pickIndex() {
        int len = presum.length;
        int target = random.nextInt(presum[len - 1]) + 1; // closed range: [1, presum[len - 1]]
        int index = binarySearch(target);
        
        return index - 1;
    }
    
    private int binarySearch(int target) {
        int start = 0, end = presum.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (presum[mid] < target) {
                start = mid;
            } else if (presum[mid] > target) {
                end = mid;
            } else {
                return mid;
            }
        }
        
        if (presum[start] >= target) {
            return start;
        }
        if (presum[end] >= target) {
            return end;
        }
        
        return end + 1;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```



