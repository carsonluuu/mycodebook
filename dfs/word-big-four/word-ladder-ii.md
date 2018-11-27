# [Word Ladder II](https://leetcode.com/problems/word-ladder/description/)

Given two words \(_start\_and\_end_\), and a dictionary, find all shortest transformation sequence\(s\) from_start\_to\_end_, such that:

1. Only one letter can be changed at a time
2. Each intermediate word must exist in the dictionary

Notice

* All words have the same length.
* All words contain only lowercase alphabetic characters.

### Example

Given:  
start =`"hit"`  
end =`"cog"`  
dict =`["hot","dot","dog","lot","log"]`

Return

```
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
```

### Note

当要返回所有 path 的时候，细节处理就更多了。其实这题和 Longest Increasing Subsequence 的 follow-up ，返回所有 LIS 有相通的地方，都是维护一个 Directed Graph 关系并且从某一个终点进行 dfs 返回所有 valid path.

非常难了。有向图找最短距离用 BFS/有向图返回所有路径用 DFS 所以是DFS加上BFS

从起点到终点是BFS，终点到起点是DFS，需要记录：

```
Map<String, Integer> dist = new HashMap<>();  ---- 单词节点到起点的距离
```

```
Map<String, List<String>> map = new HashMap<>(); ---- graph的邻接表示
```

```
List<String> path = new ArrayList<>(); ---- 路径
```

不太清楚时间和空间复杂度

### Code

```java
public class Solution {
    /*
     * @param start: a string
     * @param end: a string
     * @param dict: a set of string
     * @return: a list of lists of string
     */
    public List<List<String>> findLadders(String start, String end, Set<String> dict) {
        // write your code here
        List<List<String>> res = new ArrayList<>();
        // if (!dict.contains(end)) {
        //     return res;    
        // }
        dict.add(start);
        dict.add(end);

        Map<String, Integer> dist = new HashMap<>();
        Map<String, List<String>> map = new HashMap<>();        
        List<String> path = new ArrayList<>();

        bfs(start, end, dict, dist, map);
        dfs(end, start, res, path, dist, map);

        return res;
    }

    private List<String> getNextWords(String word, Set<String> dict) {
        List<String> nextWords = new ArrayList<>();
        for (int i = 0; i < word.length(); i++) {
            for (char c = 'a'; c <= 'z'; c++) {
                if (c == word.charAt(i)) {
                    continue;
                }
                String newWord = replace(word, i, c);
                if (dict.contains(newWord)) {
                    nextWords.add(newWord);
                }
            }
        }

        return nextWords;
    }

    private String replace(String s, int index, char c) {
        char[] ch = s.toCharArray();
        ch[index] = c;
        return String.valueOf(ch);
    }

    private void bfs(String start, String end, 
                     Set<String> dict, 
                     Map<String, Integer> dist, 
                     Map<String, List<String>> map) {
        dist.put(start, 0);
        for (String ss : dict) {
            map.put(ss, new ArrayList<String>());
        }

        Queue<String> q = new LinkedList<>();
        q.offer(start);
        while (!q.isEmpty()) {
            String curr = q.poll();
            List<String> nextList = getNextWords(curr, dict);
            for (String next : nextList) {
                map.get(next).add(curr);
                if (!dist.containsKey(next)) {
                    dist.put(next, dist.get(curr) + 1);
                    q.offer(next);
                }
            }
        }                     
    }

    private void dfs(String curr, String start,
                     List<List<String>> res, 
                     List<String> path, 
                     Map<String, Integer> dist, 
                     Map<String, List<String>> map) {
        path.add(curr);
        if (curr.equals(start)) {
            Collections.reverse(path);
            res.add(new ArrayList<String>(path));
            Collections.reverse(path);
        } else {
            for (String next : map.get(curr)) {
                if (dist.containsKey(next) 
                    && dist.get(curr) == dist.get(next) + 1) {
                    dfs(next, start, res, path, dist, map);
                }
            }    
        }
        path.remove(path.size() - 1);                 
    }
}
```



