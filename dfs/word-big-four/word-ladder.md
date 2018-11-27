# [Word Ladder](https://leetcode.com/problems/word-ladder/description/)

Given two words \(_beginWord \_and \_endWord_\), and a dictionary's word list, find the length of shortest transformation sequence from _beginWord \_to \_endWord_, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that \_beginWord \_is \_not \_a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume \_beginWord \_and \_endWord \_are non-empty and are not the same.

### Example

**Example 1:**

```
Input:

beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```
Input:

beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]


Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

### Note

这题其实是BFS + Graph，但也不容易了。本质是使用BFS找抽象/隐式图的最短路径

把各个图节点想象成每个单词，相邻节点的edit distance都是1，把起点和终点也加进去

BFS遍历搜索字典，由于需要返回层数，需要分层，三层循环，最内层遍历的是one edit distance的包含在字典的所有单词

搜索字典的时候需要对每个单词的字母通过26个字母变换，否则如果字典单词很多会超时

> I think, that time complexity is O\(N\*L^2\), where N is size of the dictionary and M is length of the word
>
> * To generate neighbors - O\(26 \* L\)
> * To check if the word exists in dict - O\(L\). This is a reason why it is better to put all words to the`Set`. Note, that the original version of this problem uses`List <String> wordList`. It is a bit confusing since author changed the signature to`Set<String> dict`.
> * To generate a tree and traverse the tree via BFS - O\(N\)
>
> So, the result is O\(26 \* L \* L \* N\) -&gt; O\(L^2 \* N\)

ps: hash\_map的时间是O\(key.size\(\)\) 因为key变成hash code即为index

优化可以用**双向BFS**，起点终点相遇

### Code

```java
public class Solution {
    /*
     * @param start: a string
     * @param end: a string
     * @param dict: a set of string
     * @return: An integer
     */
    public int ladderLength(String start, String end, Set<String> dict) {
        // write your code here
        if (dict.size() == 0) {
            return 0;
        }

        if (start.equals(end)) {
            return 1;
        }

        dict.add(start);
        dict.add(end);

        int res = 1;
        Queue<String> q = new LinkedList<>();
        Set<String> s = new HashSet<>();
        q.offer(start);
        s.add(start);
        while (!q.isEmpty()) {
            res++;
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String curr = q.poll();
                for (String next : getNextWords(curr, dict)) {
                    if (s.contains(next)) {
                        continue;
                    }
                    if (next.equals(end)) {
                        return res;    
                    }
                    q.offer(next);
                    s.add(next);
                }
            }
        }
        return 0;
    }

    // get connections with given word.
    // for example, given word = 'hot', dict = {'hot', 'hit', 'hog'}
    // it will return ['hit', 'hog']
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
}
```



