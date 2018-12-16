# Single Number

Given a **non-empty** array of integers, every element appears_twice_except for one. Find that single one.

### Example

**Example 1:**

```
Input:
 [2,2,1]

Output:
 1
```

**Example 2:**

```
Input:
 [4,1,2,1,2]

Output:
 4
```

### Note

使用异或

### Code

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for(int i = 0; i < nums.length; i++)
            res ^= nums[i];
        return res;
    }
}
```



