# [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/description/)

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of **non-empty **words from the dictionary, where **words are sorted lexicographically by the rules of this new language**. Derive the order of letters in this language.

### Example

**Example 1:**

```
Input:

[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: 
"wertf"
```

**Example 2:**

```
Input:
[
  "z",
  "x"
]

Output: 
"zx"
```

**Example 3:**

```
Input:
[
  "z",
  "x",
  "z"
] 

Output: ""

Explanation:
 The order is invalid, so return "".
```

**Note:**

1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters, return any one of them is fine.

### Note

"wrt",

"wrf", t -&gt; f

"er", w -&gt; e

"ett", r -&gt; t

"rftt" e -&gt; r

建图：前一个字符串和后一个字符串比较不同的地方，之前的是key，所以之后的set是value（其degree加一）

对这个图进行topo排序

### Code

```java
public static String alienOrder(String[] words) {

    if (words == null || words.length == 0) return "";

    StringBuilder res = new StringBuilder();
    HashMap<Character, Set<Character>> map = new HashMap<>();
    int[] degree = new int[26];
    int count = 0;

    for (String word : words) {
        for (char c : word.toCharArray()) {
            if (degree[c - 'a'] == 0) {
                count++;
                degree[c - 'a'] = 1;
            }
        }
    }

    for (int i = 0; i < words.length - 1; i++) {
        char[] cur = words[i].toCharArray();
        char[] next = words[i + 1].toCharArray();
        int len = Math.min(cur.length, next.length);
        for (int j = 0; j < len; j++) {
            if (cur[j] != next[j]) {
                if (!map.containsKey(cur[j])) {
                    map.put(cur[j], new HashSet<>());
                }
                if (map.get(cur[j]).add(next[j])) {
                    degree[next[j] - 'a']++;
                }
                break;
            }
        }
    }

    Queue<Character> queue = new LinkedList<>();
    for (int i = 0; i < 26; i++) {
        if (degree[i] == 1) {
            queue.offer((char)('a' + i));
        }
    }

    while (!queue.isEmpty()) {
        char c = queue.poll();
        res.append(c);
        if (map.containsKey(c)) {
            for (char ch : map.get(c)) {
                if (--degree[ch - 'a'] == 1) {
                    queue.offer(ch);
                }
            }
        }
    }

    if (res.length() != count) return "";
    return res.toString();
}

```



