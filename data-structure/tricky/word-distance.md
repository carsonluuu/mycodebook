# [Word Distance](https://leetcode.com/problems/shortest-word-distance-ii/description/)

Design a class which receives a list of words in the constructor, and implements a method that takes two words _word1 _and _word2 _and return the shortest distance between these two words in the list. 

### **Example**

  
Assume that words =`["practice", "makes", "perfect", "coding", "makes"]`.

```
Input:
word1 = “coding”, 
word2 = “practice”
Output: 3
```

```
Input:
word1 = "makes", 
word2 = "coding"
Output: 1
```

###  Note 1

**只call一次的normal情况**

遍历一遍words list，找到word1就更新pointer1，找到word2就更新pointer2。  
每找到任何一个word，就计算出当前distance，跟min打擂台。

时间复杂度：O\(n\)  
空间复杂度：O\(1\)

### Code1

```java
public int shortestDistance1(String[] words, String word1, String word2) {
    int one = -1, two = -1;
    int res = Integer.MAX_VALUE;
    for (int i = 0; i < words.length; i++) {
        if (word1.equals(words[i])) {
            one = i;
        }
        if (word2.equals(words[i])) {
            two = i;
        }

        if (one != -1 && two != -1) {
            res = Math.min(res, Math.abs(one - two));
        }
    }

    return res;
}
```

### Note 2

**多次调用**

会调用shortest函数非常多次，所以使用HashMap来存储words，key为word，value为index组成的list。  
计算shortest word distance的时候，使用双指针遍历一遍即可。

时间复杂度  
存储：O\(N\)，查找：O\(m+n\)/O\(N\)

空间复杂度  
存储：O\(N\)，查找：O\(N\)

### Code 2

```java
HashMap<String, List<Integer>> map;

    public WordDistance(String[] words) {
        map = new HashMap();
        for (int i = 0; i < words.length; i++) {
            List<Integer> indexes = map.getOrDefault(words[i], new ArrayList());
            indexes.add(i);
            map.put(words[i], indexes);
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> p1 = map.get(word1);
        List<Integer> p2 = map.get(word2);
        int min = Integer.MAX_VALUE;
        int i = 0, j = 0;
        while (i < p1.size() && j < p2.size()) {
            int wp1 = p1.get(i);
            int wp2 = p2.get(j);
            if (wp1 < wp2) {
                min = Math.min(min, wp2 - wp1);
                i++;
            } else {
                min = Math.min(min, wp1 - wp2);
                j++;
            }
        }
        return min;
    }
```

### Note 3

**相同单词不同位置**

标示一下是否是相同的单词，不是相同的就正常处理，相同就单独处理一下

### Code 3

```java
public int shortestWordDistance(String[] words, String word1, String word2) {
    boolean same = word1.equals(word2);
    int one = -1, two = -1;
    int res = Integer.MAX_VALUE;
    for (int i = 0; i < words.length; i++) {
        if (words[i].equals(word1)) {
            if (same) {
                two = one; //former one
            }
            one = i;
        } else if (words[i].equals(word2)) {
            two = i;
        }
        if (one != -1 && two != -1) {
            res = Math.min(res, Math.abs(one - two));
        }
    }
    
    return res;
}
```



