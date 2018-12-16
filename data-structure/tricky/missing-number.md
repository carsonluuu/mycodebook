# Missing Number

Given an array containingndistinct numbers taken from`0, 1, 2, ..., n`, find the one that is missing from the array.

### Example

**Example 1:**

```
Input:
 [3,0,1]

Output:
 2
```

**Example 2:**

```
Input:
 [9,6,4,2,3,5,7,0,1]

Output:
 8
```

### Note

找0到N-1可以使用求和法

### Code

```java
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int sum = (n+1)*n/2;
        for (int num : nums) {
            sum -= num;
        }
        return sum;
    }
}
```



