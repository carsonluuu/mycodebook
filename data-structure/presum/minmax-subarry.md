# Min/Max Subarray

Given an integer array`nums`, find the contiguous subarray \(containing at least one number\) which has the smallest/largest sum and return its sum.

```java
class Solution {
    public int minSubArray(int[] nums) {
        int sum = nums[0];
        int res = nums[0];
        
        for(int i = 1; i < nums.length; i++){
            sum = nums[i] + (sum > 0 ? 0 : sum);
            res = Math.min(res, sum);
        }
        return res;
    }
}
```

```
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = nums[0];
        int res = nums[0];
        
        for(int i = 1; i < nums.length; i++){
            sum = nums[i] + (sum < 0 ? 0 : sum);
            res = Math.max(res, sum);
        }
        return res;
    }
}
```

### Follow-up

circular case

```
a1 a2 a3 a4 a5 a6
----        -----
      =====
       min
```

* totalSum - min =  max
* totalSum - max =  min



