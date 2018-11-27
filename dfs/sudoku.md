### Sudoku

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy**all of the following rules**:

1. Each of the digits `1-9`must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the the digits `1-9`must occur exactly once in each of the 9`3x3`sub-boxes of the grid.

Empty cells are indicated by the character`'.'`.

### Example

**Example 1:**

```
Input:

[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]

Output:
 true
```

**Example 2:**

```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]

Output:
 false

Explanation:
Same as Example 1, except with the 5 in the top left corner being modified to 8.
Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)  
A sudoku puzzle...

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)  
...and its solution numbers marked in red.

**Note:**

* The given board contain only digits`1-9`and the character`'.'`.
* You may assume that the given Sudoku puzzle will have a single unique solution.
* The given board size is always`9x9`

### Note

Judge is Valid - set version: Time O\(9\*9\) space O\(3\*9\)

```
board[3*(i/3) + j/3][3*(i%3) + j%3]
i是0的时候，判断第一个九宫格，依次类推
```

```java
public boolean isValidSudoku(char[][] board) {
    for (int i = 0; i < 9; i++) {
        HashSet<Character> rows = new HashSet<>();
        HashSet<Character> cols = new HashSet<>();
        HashSet<Character> cell = new HashSet<>();
        for (int j = 0; j < 9; j++) {
            if (board[i][j] != '.' && !rows.add(board[i][j])) return false;
            if (board[j][i] != '.' && !cols.add(board[j][i])) return false;
            if (board[3*(i/3) + j/3][3*(i%3) + j%3] != '.' 
                && !cell.add(board[3*(i/3) + j/3][3*(i%3) + j%3])) 
                return false;                
        }
    }
    return true;
}
```

Judge is Valid - trick version 不推荐:

```java
public boolean isValidSudoku(char[][] board) {
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            if (board[i][j] == '.') continue;
            if (!isValid(board, i, j)) return false;
        }
    }
    return true;
}

private static boolean isValid(char[][] board, int i, int j) {
    for (int row = 0; row < 9; row++) {
        if (row == i) continue;
        if (board[row][j] == board[i][j]) return false;
    }
    for (int col = 0; col < 9; col++) {
        if (col == j) continue;
        if (board[i][col] == board[i][j]) return false;
    }
    for (int row = (i/3)*3; row < (i/3)*3 + 3; row++) {
        for (int col = (j/3)*3; col < (j/3)*3 + 3; col++) {
            if (row == i && col == j) continue;
            if (board[i][j] == board[row][col]) return false;
        }
    }
    return true;
}
```

Solver:

暴力去添加1到9，如果合适（valid）就继续dfs，search函数是boolean，不行就改回去，都不行这一层就是false

### Code

```java
class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length == 0) return;
        solve(board);
    }

    private static boolean solve(char[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == '.') {
                    for (char c = '1'; c <= '9'; c++) {
                        if (isValid(board, i, j, c)) {
                            board[i][j] = c;
                            if (solve(board)) return true;
                            else board[i][j] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }

    private static boolean isValid(char[][] board, int row, int col, char c) {
        for (int i = 0; i < board.length; i++) {
            if (board[i][col] != '.' && board[i][col] == c) return false;
            if (board[row][i] != '.' && board[row][i] == c) return false;
            if (board[3*(row/3) + i / 3][3*(col/3) + i % 3] != '.' 
                && board[3*(row/3) + i / 3][3*(col/3) + i % 3]== c) return false; 
        }
        return true;
    }
}
```



