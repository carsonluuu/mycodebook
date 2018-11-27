# Search in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

### Example

For`[4, 5, 1, 2, 3]`and`target=1`, return`2`.

For`[4, 5, 1, 2, 3]`and`target=0`, return`-1`.

### Note1

![](/assets/rotatedSorted.png)

M1可能落在左半边, 也可能落在右半边. M1 &gt;= S1, 左; M1 &lt; S1, 右

即把数组分为了两部分,粉色部分\[S,M\]和橙色部分\[M\]

我们想去掉一半, 让它仍保持RSA\(rotated sorted array\)

如果M落在左, 切掉\[S,M\]; 如果M落在右, 切掉\[M,E\]

分类讨论，这里选择比较和mid和start位置数的大小来决定抛弃哪一半：

nums\[mid\] == target --&gt; return mid

nums\[start\] &lt; nums\[mid\]: 在左边

* nums\[start\] &lt;= target &lt;= nums\[mid\] --&gt; 在左边：end = mid
* else --&gt; 在右边: start = mid

start &gt;= mid: 在右边

* nums\[mid\] &lt;= target &lt;= nums\[end\] --&gt; 在右边：start = mid
* else --&gt; 在左边: end = mid

### Code1

```
public class Solution {
    /**
     * @param A: an integer rotated sorted array
     * @param target: an integer to be searched
     * @return: an integer
     */
    public int search(int[] A, int target) {
        // write your code here
        if (A == null || A.length == 0) {
            return -1;
        }
        int start = 0, end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] == target) {
                return mid;
            }
            if (A[start] < A[mid]) {
                if (A[start] <= target && target <= A[mid]) {
                    end = mid;
                } else {
                    start = mid;
                }
            } else {
                if (A[mid] <= target && target <= A[end]) {
                    start = mid;
                } else {
                    end = mid;
                }
            }
        }
        if (A[start] == target) {
            return start;
        }
        if (A[end] == target) {
            return end;
        }
        return -1;
    }
}
```

### Note2

如果我们这里允许重复， 这里考虑最坏情况:

```
这个问题在面试中不会让实现完整程序
只需要举出能够最坏情况的数据是 [1,1,1,1... 1] 里有一个0即可。
在这种情况下是无法使用二分法的，复杂度是O(n)
因此写个for循环最坏也是O(n)，那就写个for循环就好了
如果你觉得，不是每个情况都是最坏情况，你想用二分法解决不是最坏情况的情况，那你就写一个二分吧。
反正面试考的不是你在这个题上会不会用二分法。这个题的考点是你想不想得到最坏情况。
```

二分法，增加一个分支，最坏情况会一直增加，这样就是O（n）：

```
else if (nums[start] == nums[mid]) {
    start++;
}
```

### Code2

```java
public class Solution {
    /**
     * @param A: an integer ratated sorted array and duplicates are allowed
     * @param target: An integer
     * @return: a boolean 
     */
    public boolean search(int[] nums, int target) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return false;
        }

        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[start] < nums[mid]) {
                if (nums[start] <= target && target <= nums[mid]) {
                    end = mid;
                } else {
                    start = mid;
                }
            } else if (nums[start] > nums[mid]) {
                if (nums[mid] <= target && target <= nums[end]) {
                    start = mid;
                } else {
                    end = mid;
                }
            } else if (nums[start] == nums[mid]) {
                start++;
            }
        }

        if (nums[start] == target || nums[end] == target) {
            return true;
        }
        return false;
    }
}
```



