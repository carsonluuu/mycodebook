# [Stream of Characters](https://leetcode.com/problems/stream-of-characters/description/)

Implement the`StreamChecker`class as follows:

* `StreamChecker(words)`: Constructor, init the data structure with the given words.
* `query(letter)`: returns true if and only if for some`k >= 1`, the last`k`characters queried \(in order from oldest to newest, including this letter just queried\) spell one of the words in the given list.

### **Example**

```
StreamChecker streamChecker = new StreamChecker(["cd","f","kl"]); // init the dictionary.
streamChecker.query('a');          // return false
streamChecker.query('b');          // return false
streamChecker.query('c');          // return false
streamChecker.query('d');          // return true, because 'cd' is in the wordlist
streamChecker.query('e');          // return false
streamChecker.query('f');          // return true, because 'f' is in the wordlist
streamChecker.query('g');          // return false
streamChecker.query('h');          // return false
streamChecker.query('i');          // return false
streamChecker.query('j');          // return false
streamChecker.query('k');          // return false
streamChecker.query('l');          // return true, because 'kl' is in the wordlist
```

* `1 <= words.length <= 2000`
* `1 <= words[i].length <= 2000`
* Words will only consist of lowercase English letters.
* Queries will only consist of lowercase English letters.
* The number of queries is at most 40000.

### Note

Query指的是当收到一个letter的时候，查看最近收到的letter流的末尾是不是存在指定的单词，例如收到query\('a'\), query\('b'\), query\('c'\)之后，letter流就是"abc", 我们只需要检测\["c","bc","abc"\]中是否有指定单词。

插入时倒序插入，查询buf的单词是否存在于trie

### Code

```java
class StreamChecker {
    class TrieNode {
        boolean isWord = false;
        TrieNode[] children = new TrieNode[26];
    }
    
    TrieNode root =  new TrieNode();
    StringBuilder buf = new StringBuilder();
    
    void insert(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            int index = (int)(word.charAt(word.length() - 1 - i) - 'a');
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            } 
            node = node.children[index];
        }
        node.isWord = true;
    }
    
    public StreamChecker(String[] words) {
        for (String word: words){
            insert(word);
        }
    }
    
    public boolean query(char letter) {
        buf.insert(0, letter);
        if (buf.length() > 2000) { // Avoid TLE.
            buf.delete(2000, buf.length());
        }
        TrieNode node = root;
        for (char ch: buf.toString().toCharArray()){
            node = node.children[ch - 'a'];
            if (node == null){
                return false;
            }
            if (node.isWord == true){
                return true;
            }
        }
        return false;
    }
}

/**
 * Your StreamChecker object will be instantiated and called as such:
 * StreamChecker obj = new StreamChecker(words);
 * boolean param_1 = obj.query(letter);
 */
```



