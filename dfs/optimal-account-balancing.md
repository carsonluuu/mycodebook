# Optimal Account Balancing

A group of friends went on holiday and sometimes lent each other money. For example, Alice paid for Bill's lunch for $10. Then later Chris gave Alice $5 for a taxi ride. We can model each transaction as a tuple \(x, y, z\) which means person x gave person y $z. Assuming Alice, Bill, and Chris are person 0, 1, and 2 respectively \(0, 1, 2 are the person's ID\), the transactions can be represented as`[[0, 1, 10], [2, 0, 5]]`.

Given a list of transactions between a group of people, return the minimum number of transactions required to settle the debt.

**Note:**

1. A transaction will be given as a tuple \(x, y, z\). Note that `x ≠ y`and`z > 0`.
2. Person's IDs may not be linear, e.g. we could have the persons 0, 1, 2 or we could also have the persons 0, 2, 6.

**Example 1:**

```
Input:[[0,1,10], [2,0,5]]

Output:2

Explanation:
Person #0 gave person #1 $10.
Person #2 gave person #0 $5.

Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
```

**Example 2:**

```
Input:[[0,1,10], [1,0,1], [1,2,5], [2,0,5]]

Output: 1

Explanation:
Person #0 gave person #1 $10.
Person #1 gave person #0 $1.
Person #1 gave person #2 $5.
Person #2 gave person #0 $5.

Therefore, person #1 only need to give person #0 $4, and all debt is settled.
```

### Note

利用linkedlist来记录交易之后的数值，排序，从负数到正数

不停的修改list，利用hashCode来做memo的key

拿出队首，遍历剩下的所有元素，如果同号就剪枝叶，记录更小的操作数目

* 如果加起来是0就删掉，然后backtracking，restore
* 否则就把这个元素改写为加起来和值，然后backtracking，restore

放回队首元素，并更新memo

### Code

```java
class Solution {
    public int minTransfers(int[][] transactions) {
        Map<Integer, Long> map = new HashMap<>();
        for (int[] t : transactions) {
            long val1 = map.getOrDefault(t[0], 0l) - t[2];
            long val2 = map.getOrDefault(t[1], 0l) + t[2];
            map.put(t[0], val1);
            map.put(t[1], val2);
        }

        LinkedList<Long> list = new LinkedList<>();
        for (Long val : map.values()) {
            if (val != 0) {
                list.add(val);
            }
        }

        Collections.sort(list);

        return dfs(list, new HashMap<>());
    }

    private int dfs(LinkedList<Long> list, Map<Integer, Integer> memo) {
        if (list.isEmpty()) {
            return 0;
        }

        int hash = list.hashCode();
        if (memo.containsKey(hash)) {
            return memo.get(hash);
        }

        long first = list.removeFirst();
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < list.size(); i++) {
            long other = list.get(i);
            if (first * other > 0) {
                continue;
            }

            long newVal = first + other;
            if (newVal == 0) {
                list.remove(i);
                min = Math.min(min, dfs(list, memo) + 1);
                list.add(i, other);
            } else {
                list.set(i, newVal);
                min = Math.min(min, dfs(list, memo) + 1);
                list.set(i, other);
            }
        }

        list.addFirst(first);

    memo.put(hash, min);
    return min;
    }
}
```



