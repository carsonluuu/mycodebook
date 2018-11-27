# Cartesian Product

We use a two-dimensional array setList\[\]\[\] to represent a collection array, and each element in setList\[i\] is an integer and is not the same. Find the cartesian product of setList\[0\],setList\[1\],...,setList\[setList.length - 1\].

* `1 <= setList.length <= 5`
* `1 <= setList[i].length <= 5`

### Example

Given setList =`[[1,2,3],[4],[5,6]]`, return`[[1,4,5],[1,4,6],[2,4,5],[2,4,6],[3,4,5],[3,4,6]]`,

```
Explanation:
The cartesian product of [1,2,3], [4] and [5,6] is [[1,4,5],[1,4,6],[2,4,5],[2,4,6],[3,4,5],[3,4,6]].
```

Given setList =`[[1,2,3],[4]]`, return`[[1,4],[2,4],[3,4]]`。

```
Explanation:
The cartesian product of [1,2,3] and [4] is [[1,4],[2,4],[3,4]].
```

### Note

DFS求笛卡尔积

pos 控制第几个set，i 控制这个set的第几个元素

### Code

```java
public class Solution {
    /**
     * @param setList: The input set list
     * @return: the cartesian product of the set list
     */
    public List<List<Integer>> getSet(int[][] setList) {
        // Write your code here
        List<List<Integer>> res = new ArrayList<>();
        if (setList == null|| setList.length == 0) return res;
        dfs(res, new ArrayList<>(), setList, 0);
        return res;
    }

    private void dfs (List<List<Integer>> res, List<Integer> list, 
                      int[][] setList, int pos) {
        if (pos == setList.length) {
            res.add(new ArrayList<Integer>(list));
            return;
        }

        for (int i = 0; i < setList[pos].length; i++) {
            list.add(setList[pos][i]);
            dfs(res, list, setList, pos + 1);
            list.remove(list.size() - 1);
        }
    }
}
```



