# [N-Queens](https://www.lintcode.com/problem/n-queens/description?_from=ladder&&fromId=1)

The n-queens puzzle is the problem of placing n queens on an`n×n`chessboard such that no two queens attack each other.

Given an integer`n`, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where`'Q'`and`'.'`both indicate a queen and an empty space respectively.

```
Example
```

There exist two distinct solutions to the 4-queens puzzle:

```
[
  // Solution 1
  [".Q..",
   "...Q",
   "Q...",
   "..Q."
  ],
  // Solution 2
  ["..Q.",
   "Q...",
   "...Q",
   ".Q.."
  ]
]
```

### Note

大体思路就是对每一行，按每一列挨个去试，试到了就保存结果没试到就回溯。难点大概就是用1个一维数组存皇后所在的坐标值。对于一个棋盘来说，每个点都有横纵坐标，用横纵坐标可以表示一个点。而这道题巧就巧在，每一行只能有一个皇后，也就是说，对于一行只能有一个纵坐标值，所以用1维数组能提前帮助解决皇后不能在同一行的问题。

那么用一维数组表示的话，方法是：一维数组的下标表示横坐标（哪一行），而数组的值表示纵坐标（哪一列）。

使用3个帮助函数来进行模块化编程

`List<Integer> list` 来表示每一行的Q的位置

`List<List<String>> res` 是棋盘，通过`draw`函数来进行绘制

`boolean isValid(int col, List<Integer> list)` 函数判断新加入的col是不是和之前list里面元素满足

```java
if (colIndex == col) {
    return false;
}
if (colIndex + rowIndex == col + row) {
    return false;
}
if (colIndex - rowIndex == col - row) {
    return false;
}
```

Time: O\(n!\)

Space:O\(n^2\)

### Code

```java
public class Solution {
    /*
     * @param n: The number of queens
     * @return: All distinct solutions
     */
    public List<List<String>> solveNQueens(int n) {
        // write your code here
        List<List<String>> res = new ArrayList<>();
        if (n <= 0) {
            return res;
        }

        search(res, new ArrayList<Integer>(), n);

        return res;
    }

    private void search(List<List<String>> res, List<Integer> list, int n) {
        if (list.size() == n) {
            res.add(draw(list));
            return;
        }

        for (int i = 0; i < n; i++) {
            if (!isValid(i, list)) {
                continue;
            }

            list.add(i);
            search(res, list, n);
            list.remove(list.size() - 1);
        }
    }

    private List<String> draw(List<Integer> list) {
        List<String> ans = new ArrayList<>();
        for (int i = 0; i < list.size(); i++) {
            StringBuilder sb = new StringBuilder();
            for (int j = 0; j < list.size(); j++) {
                if (j == list.get(i)) {
                    sb.append("Q");
                } else {
                    sb.append(".");
                }
            }
            ans.add(sb.toString());
        }
        return ans;
    }

    private boolean isValid(int col, List<Integer> list) {
        int row = list.size();
        for (int rowIndex = 0; rowIndex < list.size(); rowIndex++) {
            int colIndex = list.get(rowIndex); // Q's col
            if (colIndex == col) {
                return false;
            }
            if (colIndex + rowIndex == col + row) {
                return false;
            }
            if (colIndex - rowIndex == col - row) {
                return false;
            }            
        }

        return true;
    }
}
```



