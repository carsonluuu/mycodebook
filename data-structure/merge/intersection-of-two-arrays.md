# [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)

Given two arrays, write a function to compute their intersection.

### Example

**Example 1:**

```
Input: 
nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```
Input: 
nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

### Note

给一个二分的做法，查一查是不是在里面

或者用set

### Code

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums2); // binary search need sorted
        for(int num : nums1){
            if(binarySearch(nums2, num))//num1's elements are in num2
                set.add(num);//store elements in num1 will not repeat
        }
        int i = 0;
        int[] res = new int[set.size()];
        for(Integer num : set)
            res[i++] = num;
        
        return res;
        
        
    }
    public boolean binarySearch(int[] nums, int target){
        int lo = 0;
        int hi = nums.length - 1;
        while(lo <= hi){
            int mid = (hi - lo)/2 + lo;
            if(nums[mid] == target) return true;
            if(nums[mid] > target) hi = mid - 1;
            else                   lo = mid + 1;
        }
        return false;
    }
}
```



