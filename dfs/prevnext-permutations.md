# Previous/Next Permutation

### Example

For`[1,3,2,3]`, the previous permutation is`[1,2,3,3]`

For`[1,2,3,4]`, the previous permutation is`[4,3,2,1]`

```
[1, 2, 2, 1, 1, 3, 3, 4, 5] prev [1, 2, 1, 5, 4, 3, 3, 2, 1]
```

For`[1,3,2,3]`, the next permutation is`[1,3,3,2]`

For`[4,3,2,1]`, the next permutation is`[1,2,3,4]`

```
[1, 2, 1, 5, 4, 3, 3, 2, 1] next [1, 2, 2, 1, 1, 3, 3, 4, 5]
```

### Note

迭代法求全排列的主要组成部分

previous:

* 1234之前是4321，所以保证之后部分递**减**，找到转折点index，转折数index - 1
* 找到转折点之后的最后一个比转折数**小**的数，交换它们
* 对index到最后递增的子数组进行反转

12**2**1**1**3345 --&gt; 12**1**1**2**3345 --&gt; 121**543321**

next:

* 4321之后是1234，所以保证之后部分递**增**，找到转折点index，转折数index - 1
* 找到转折点之后的最后一个比转折数**大**的数，交换它们
* 对index到最后递减的子数组进行反转

12**1**5433**2**1 --&gt; 12**2**5433**1**1 --&gt; 122**113345**

### Code

```java
public class Solution {
    /*
     * @param nums: A list of integers
     * @return: A list of integers that's previous permuation
     */
    public List<Integer> previousPermuation(List<Integer> nums) {
        // write your code here
        int len = nums.size();
        if (len < 2) {
            return nums;
        }

        int index = len - 1;
        while (index > 0) {
            if (nums.get(index - 1) > nums.get(index)) {
                break;
            }
            index--;
        }

        if (index == 0) {
            reverse(nums, 0, len - 1);
            return nums;
        }

        int val = nums.get(index - 1);
        int j = len - 1;
        while (index <= j) {
            if (nums.get(j) < val) {
                break;
            }
            j--;
        }

        swap(nums, j, index - 1);
        reverse(nums, index, len - 1);

        return nums;
    }

    public void swap(List<Integer> nums, int i, int j) {
        Integer tmp = nums.get(i);
        nums.set(i, nums.get(j));
        nums.set(j, tmp);
    }
    public void reverse(List<Integer> nums, int i, int j) {
        while (i < j) {
            swap(nums, i, j);
            i++; j--;
        }
    }
}
```

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers
     */
    public int[] nextPermutation(int[] nums) {
        // write your code here
        int len = nums.length;
        if (len < 2) {
            return nums;
        }

        int index = len - 1;
        while (index > 0) {
            if (nums[index - 1] < nums[index]) {
                break;
            }
            index--;
        }

        if (index == 0) {
            reverse(nums, 0, len - 1);
            return nums;
        }

        int val = nums[index - 1];
        int j = len - 1;
        while (index <= j) {
            if (nums[j] > val) {
                break;
            }
            j--;
        }

        swap(nums, j, index - 1);
        reverse(nums, index, len - 1);

        return nums;
    }

    public void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
    public void reverse(int[] nums, int i, int j) {
        while (i < j) {
            swap(nums, i, j);
            i++; j--;
        }
    }
}
```



