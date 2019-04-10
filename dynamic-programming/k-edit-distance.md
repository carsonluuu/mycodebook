# [K Edit Distance](https://www.lintcode.com/problem/k-edit-distance/description?_from=ladder&&fromId=4)

Given a set of strings which just has lower case letters and a target string, output all the strings for each the edit distance with the target no greater than`k`.

You have the following 3 operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

### Example

Given words =`["abc", "abd", "abcd", "adc"]`and target =`"ac"`, k =`1`  
Return`["abc", "adc"]`

### Note

暴力做法就是target和words一个个进行比较

优化做法，我们使用Trie加DFS加DP

* Trie存所有词
* DFS遍历Trie树上的所有a-z的节点
* dp\[i\] 表示从Trie的root节点走到当前node节点，形成的Prefix和 target的前i个字符的最小编辑距离

 dp指的是上一次的情况。现在更新i，j这个格子，那么我要往左上方看\(i-1, j-1\)，要往上看\(i-1, j\)，这两种就是分别对应dp数组里的dp\[j-1\]和dp\[j\]。然后我还要往左边看i, j-1，此时行不变，相当于我看next数组里我左边那个刚刚更新过的值，所以是next\[j-1\]

### Code

```java
public class Solution {
    private class TrieNode{
        Map<Character,TrieNode> children;
        String word;
        boolean isWord;
        TrieNode(){
            children = new HashMap<>();
        }
    }
    
    private class Trie{
        TrieNode root;
        Trie(){
            root = new TrieNode();
        }
        
        public void insert(String word){
            TrieNode curt = root;
            for(int i = 0; i < word.length(); i++){
                char c = word.charAt(i);
                if(!curt.children.containsKey(c)){
                    curt.children.put(c,new TrieNode());
                }
                curt = curt.children.get(c);
            }
            curt.isWord = true;
            curt.word = word;
        }
        
    }
    
    /**
     * @param words: a set of stirngs
     * @param target: a target string
     * @param k: An integer
     * @return: output all the strings that meet the requirements
     */
    public List<String> kDistance(String[] words, String target, int k) {
        // write your code here
        List<String> ans = new ArrayList<>();
        if(words == null || words.length == 0){
            return ans;
        }
        Trie trie = new Trie();
        for(String word : words){
            trie.insert(word);
        }
        //代表把root节点开始变成target[i]的operation
        int[] dp = new int[target.length() + 1];
        for(int i = 0; i <= target.length(); i++){
            dp[i] = i;
        }
        dfs(trie.root,target,k,ans,dp);
        return ans;
    }
    
    private void dfs(TrieNode node,String target,int k, List<String> ans, int[] dp){
        if(node.isWord && dp[target.length()] <= k){
            ans.add(node.word);
        }
        //dp代表这一行  ====>  [i-1,j-1],[i -1,j]
        //next代表dp的下一行   [i,j-1],    [i,j]
        int[] next = new int[target.length() + 1];
        node.children.forEach((ch,v) ->{
            next[0] = dp[0] + 1;
            for(int i = 1; i <= target.length(); i++){
                if(target.charAt(i - 1) == ch){
                    next[i] = dp[i - 1];
                }else{
                    //需要比较[左上，左，上]三个位置的值
                    //分别对应[replace,delete,add]三个操作
                    next[i] = Math.min(Math.min(dp[i - 1],dp[i]),next[i - 1]) + 1;
                }
            }
            dfs(v,target,k,ans,next);
        });
        
    }
    
}
```



