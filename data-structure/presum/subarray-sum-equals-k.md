# Subarray Sum Equals K

Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k.**

### **Example**

```
Input: nums = [1,1,1], k = 2
Output: 2
```

```
Input: nums = [1,2,-1,-1,2], k = 2
Output: 4
```

1. The length of the array is in range \[1, 20,000\].
2. The range of numbers in the array is \[-1000, 1000\] and the range of the integer **k **is \[-1e7, 1e7\].

### Note

Using HashMap to store \( key : the **PrefixSum**, value : how many ways get to this prefix sum\).

* Check if **PrefixSum** **-** **target** exists in hashmap or not, if it does, we added up the ways of this key
* For instance : in one path we have 1,2,-1,-1,2, then the prefix sum will be: 0, 1, 3, 2, 1, 3, let's say we want to find target sum is 2, then we will have{2}, {1,2,-1}, {2,-1,-1,2} and {2}ways.
* Meaning: `PrefixSum2 - PrefixSum1 = Target`

注意One Pass写法时候，其实没有把起始0加入循环，需要手动设置成map.put\(0,1\). PreSum数组则不用，因为它从index 0遍历到index len + 1。

### Code

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int len = nums.length;
        int[] presum = new int[len + 1];
        for (int i = 0; i < len; i++) {
            presum[i + 1] = presum[i] + nums[i];
        }

        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i <= len; i++) {
            int key = presum[i] - k;
            if (map.containsKey(key)) {
                res += map.get(key);
            }
            map.put(presum[i], map.getOrDefault(presum[i], 0) + 1);
        }

        return res;
    }
}
```

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        int res = 0, sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            
            if (map.containsKey(sum - k)) {
                res += map.get(sum - k);
            }
            
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        
        return res;
    }
}
```



