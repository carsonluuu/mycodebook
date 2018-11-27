# [Shuffle an Array](https://leetcode.com/problems/shuffle-an-array/description/)

Shuffle a set of numbers without duplicates.

**Example:**

```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

### Note

**Fisher-Yates Algorithm**

每个元素每次和后面的随机一个位置进行交换

On each iteration of the algorithm, we generate a random integer between the **current index** and the **last index** of the array

```
private int randRange(int min, int max) {
    return rand.nextInt(max - min) + min;
}
```

Then, we **swap** the elements at the current index and the chosen index - this simulates drawing \(and removing\) the element from the hat, as the next range from which we select a random index will not include the most recently processed one.

### Code

```java
class Solution {
    private int[] array;
    private int[] original;

    Random rand = new Random();

    private int randRange(int min, int max) {
        return rand.nextInt(max - min) + min;
    }

    private void swapAt(int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    public Solution(int[] nums) {
        array = nums;
        original = nums.clone();
    }

    public int[] reset() {
        array = original;
        original = original.clone();
        return original;
    }

    public int[] shuffle() {
        for (int i = 0; i < array.length; i++) {
            swapAt(i, randRange(i, array.length));
        }
        return array;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```



