# Set Mismatch

The set`S`originally contains numbers from 1 to`n`. But unfortunately, due to the data error, one of the numbers in the set got duplicated to **another **number in the set, which results in repetition of one number and loss of another number.

Given an array `nums` representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

### **Example**

```
Input:
 nums = [1,2,2,4]

Output:
 [2,3]
```

### Note

在1-N中找重复两次的数，直接在数组上进行state改变，让它变负数，再次遇到重复的数的话，其值就是负数了，直接找到

### Code

```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        int dup = -1, missing = 1;
        for (int n : nums) {
            if (nums[Math.abs(n) - 1] < 0) {
                dup = Math.abs(n);
            } else {
                nums[Math.abs(n) - 1] *= -1;
            }
        }
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > 0) {
                missing = i + 1;
            }
        }
        
        return new int[]{dup, missing};
    }
}
```



