# [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/description/)

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits 
   `1-9`
   without repetition.
2. Each column must contain the digits 
   `1-9`
    without repetition.
3. Each of the 9
   `3x3`
   sub-boxes of the grid must contain the digits 
   `1-9`
    without repetition.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

The Sudoku board could be partially filled, where empty cells are filled with the character`'.'`.

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

### Note

row/col/cell都要满足，利用set进行验重

board\[3\*\(i/3\) + j/3\]\[3\*\(i%3\) + j%3 for cell

### Code

```
class Solution {
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


}
```



