# [Two Sum](https://leetcode.com/problems/two-sum/description/)

Given an array of integers, return **indices **of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly **one solution, and you may not use the same element twice.

### **Example**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Note

不用额外空间的话稍微麻烦一些，需要建一个类预处理存原来的index，还要这么搞一下。。

```
int t1 = number[L].index;
int t2 = number[R].index;
int[] result = {Math.min(t1,t2), Math.max(t1,t2)};
```

两个算法的对比

1. Hash方法使用一个Hashmap结构来记录对应的数字是否出现，以及其下标。时间复杂度为O\(n\)O\(n\)。空间上需要开辟Hashmap来存储, 空间复杂度是O\(n\)O\(n\)。

2. Two pointers方法，基于有序数组的特性，不断移动左右指针，减少不必要的遍历，时间复杂度为O\(nlogn\)O\(nlogn\)， 主要是排序的复杂度。但是在空间上，不需要额外空间，因此额外空间复杂度是O\(1\)O\(1\)

### Code

```java
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < numbers.length; i++) {
        if (map.containsKey(target - numbers[i])) {
            result[0] = map.get(target - numbers[i]);
            result[1] = i + 1;
            return result;
        }
        map.put(numbers[i], i + 1);
    }
    return result;
}
```

```java
public class Solution {
    /*
     * @param numbers: An array of Integer
     * @param target: target = numbers[index1] + numbers[index2]
     * @return: [index1 + 1, index2 + 1] (index1 < index2)
     */
     class Pair {
         Integer value;
         Integer index;

         Pair(Integer value, Integer index) {
            this.value = value;
            this.index = index;
         }
         Integer getValue() {
             return this.value;
         }
     }

    class ValueComparator implements Comparator<Pair> {    

        @Override    
        public int compare(Pair o1, Pair o2) {    
            return o1.getValue().compareTo(o2.getValue());      
        }
    }

    public int[] twoSum(int[] numbers, int target) {
        // write your code here

        Pair[] number = new Pair[numbers.length];
        for (int i = 0; i < numbers.length; i++) {
            number[i] = new Pair(numbers[i], i);
        }
        Arrays.sort(number, new ValueComparator());
        int L = 0 , R = numbers.length - 1;
        while (L<R) {
            if (number[L].getValue() + number[R].getValue() == target) {
                int t1 = number[L].index;
                int t2 = number[R].index;
                int[] result = {Math.min(t1,t2), Math.max(t1,t2)};
                return result;
            }
            if (number[L].getValue() + number[R].getValue() < target) {
                L++;
            } else {
                R--;
            }
        }
        int[] res = {};
        return res;
    }
}
```



