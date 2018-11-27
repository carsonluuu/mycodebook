# Implement Trie \(Prefix Tree\)

Implement a trie with insert, search, and startsWith methods.

### Example

```
insert("lintcode")
search("code")
>>> false
startsWith("lint")
>>> true
startsWith("linterror")
>>> false
insert("linterror")
search("lintcode)
>>> true
startsWith("linterror")
>>> true
```

### Code

```java
public class Trie {
    class TrieNode {
        public boolean isWord;
        public TrieNode[] children;
        public TrieNode() {
            children = new TrieNode[26];
            isWord = false;
        }
    }

    private TrieNode root;

    public Trie() {
        // do intialization if necessary
        root = new TrieNode();
    }

    /*
     * @param word: a word
     * @return: nothing
     */
    public void insert(String word) {
        // write your code here
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            int index = (int)(word.charAt(i) - 'a');
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            } 
            node = node.children[index];
        }
        node.isWord = true;
    }

    /*
     * @param word: a word
     * @return: the TrieNode after the prefix
     */
    public TrieNode find(String prefix) {
        // write your code here
        TrieNode node = root;
        for (int i = 0; i < prefix.length(); i++) {
            int index = (int)(prefix.charAt(i) - 'a');
            if (node.children[index] == null) {
                return null;
            } 
            node = node.children[index];
        }
        return node;
    }

    /*
     * @param word: A string
     * @return: if the word is in the trie.
     */
    public boolean search(String word) {
        // write your code here
        TrieNode node = find(word);
        return node != null && node.isWord;
    }

    /*
     * @param prefix: A string
     * @return: if there is any word in the trie that starts with the given prefix.
     */
    public boolean startsWith(String prefix) {
        // write your code here
        TrieNode node = find(prefix);
        return node != null;
    }

    /*
    * @param prefix: A string
    * @return: all the prefix strings.
    */
    public List<String> findWords(String prefix) {
            List<String> res = new ArrayList<>();
            TrieNode node = find(prefix);
            findWordsHelper(res, prefix, node);

            return res;
        }

    private void findWordsHelper(List<String> res, String s, TrieNode node) {
        if (node.isWord) {
            res.add(s);
        }

        for (int i = 0; i < 26; i++) {
            if (node.children[i] != null) {
                char c = (char)(i + 'a');
                findWordsHelper(res, s + c, node.children[i]);
            }
        }
    }
}
```

给一个HashMap版本的

```java
class Trie {

    private class TrieNode {
        private HashMap<Character, TrieNode> children;
        private boolean hasWord;
        public TrieNode() {
            this.children = new HashMap<>();
            this.hasWord = false;
        }
    }

    private TrieNode root;

    /** Initialize your data structure here. */
    public Trie() {
        this.root = new TrieNode();
    }

    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode curr = this.root;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if (!curr.children.containsKey(c)) {
                curr.children.put(c, new TrieNode());
            }
            curr = curr.children.get(c);
        }
        curr.hasWord = true;
    }

    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode curr = this.root;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if (!curr.children.containsKey(c)) {
                return false;
            }
            curr = curr.children.get(c);
        }
        return curr.hasWord;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode curr = this.root;
        for (int i = 0; i < prefix.length(); i++) {
            char c = prefix.charAt(i);
            if (!curr.children.containsKey(c)) {
                return false;
            }
            curr = curr.children.get(c);
        }
        return true;
    }
}
```



