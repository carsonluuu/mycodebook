# [Word Search](https://leetcode.com/problems/word-search/description/)

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

### **Example**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

### Note

属于DFS搜索路径是否存在。

按照给定的前缀暴力backtracking搜索四个方向，直到前缀包含这个待寻找的单词。

注意在同一层标记走过的路径，backtracking之后需要改动回来。

Time：O\(M\*N\)

Space：O\(1\) / O\(M + N\) stack space

### Code

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for (int i = 0; i < board.length; i++)
            for (int j = 0; j < board[0].length; j++){
                if (exist(board, i, j, word, 0))
                    return true;
            }
        return false;
    }

    private boolean exist(char[][] board, int i, int j, String word, int start){
        if (start >= word.length()) return true;
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) return false;
        if (board[i][j] == word.charAt(start++)) {
            char c = board[i][j];
            board[i][j] = '@';
            boolean res = exist(board, i + 1, j, word, start) || 
                          exist(board, i - 1, j, word, start) ||
                          exist(board, i, j + 1, word, start) ||
                          exist(board, i, j - 1, word, start);
            board[i][j] = c;
            return res;
        }
        return false;
    }

}
```



