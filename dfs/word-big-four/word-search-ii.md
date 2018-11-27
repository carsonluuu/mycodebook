# [Word Search II](https://leetcode.com/problems/word-search-ii/description/)

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

### **Example**

```
Input: 
words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]

Output: ["eat","oath"]

You may assume that all inputs are consist of lowercase lettersa-z.
```

### Note

与前置题目不同的是，这里需要返回给定words集合的所有包含在2D board的单词

这里使用trie进行剪枝，`insert`方法把所有待查找的单词插入trie中，`search`方法判断是否在trie中，`startWith`方法判断是否为前缀

递归和前置题目类似，搜索2D board的所有元素，给出一个通俗版本，返回结果可以用set去重，问题不大，当然还可以极限提速度。。 见 [https://leetcode.com/problems/word-search-ii/discuss/59780/Java-15ms-Easiest-Solution-\(100.00\)](https://leetcode.com/problems/word-search-ii/discuss/59780/Java-15ms-Easiest-Solution-%28100.00%29)

Time: O\(m \* n \* wl \* 4^wl\) -&gt; O\(m \* n \* 4^wl\)  wl is the average length of words

Space: O\(cnt \* wl\) cnt is the number of words

### Code

```java
public class Solution {
    /**
     * @param board: A list of lists of character
     * @param words: A list of string
     * @return: A list of string
     */

    class Trie {
        class TrieNode {
            public boolean isWord;
            public TrieNode[] children;
            public TrieNode() {
                isWord = false;
                children = new TrieNode[26];
            }
        }

        public TrieNode root;

        public Trie() {
            root = new TrieNode();
        }

        public void insert(String s) {
            TrieNode p = root;
            for (int i = 0; i < s.length(); i++) {
                int index = (int)(s.charAt(i) - 'a');
                if (p.children[index] == null) {
                    p.children[index] = new TrieNode();
                }
                p = p.children[index];
            }
            p.isWord = true;
        }

        public TrieNode find(String s) {
            TrieNode p = root;
            for (int i = 0; i < s.length(); i++) {
                int index = (int)(s.charAt(i) - 'a');
                if (p.children[index] == null) {
                    return null;
                }
                p = p.children[index];
            }
            return p;
        } 

        public boolean search(String word) {
            TrieNode node = find(word);
            return node != null && node.isWord;
        }

        public boolean startsWith(String prefix) {
            TrieNode node = find(prefix);
            return node != null;
        }
    } 

    public int[] dx = {1, 0, -1, 0};
    public int[] dy = {0, 1, 0, -1};

    public List<String> wordSearchII(char[][] board, List<String> words) {
        // write your code here
        List<String> res = new ArrayList<>();

        Trie trie = new Trie();
        for (String word : words) {
            trie.insert(word);
        }

        int m = board.length;
        int n = board[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                search(board, "", i, j, trie, res);
            }
        }

        return res;
    }

    private void search(char[][] board, String str,
                        int x, int y, Trie trie,
                        List<String> res) {
        str += board[x][y];
        if (!trie.startsWith(str)) {
            return;
        }

        if (trie.search(str) && !res.contains(str)) {
            res.add(str);
        }

        char temp = board[x][y];
        board[x][y] = '#';
        for (int i = 0; i < 4; i++) {
            if (!isValid(board, x + dx[i], y + dy[i])) {
                continue;
            }
            search(board, str, x + dx[i], y + dy[i], trie, res);
        }
        board[x][y] = temp;

    }

    private boolean isValid(char[][] board, int x, int y) {
        if (x < 0 || x >= board.length ||
            y < 0 || y >= board[0].length) {
            return false;
        }

        return board[x][y] != '#';
    }
}
```



