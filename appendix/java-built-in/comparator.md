# Comparator

Comparator is an interface, we can override the compare method to customize our sorting

对于数组、链表、堆等结构，标准库中排序方法，往往是对于基本类型的升序排序，有的时候，不一定能满足我们的要求。例如我们有一些特殊的顺序要求，或待排序的对象类型不是基本类型。此时，就需用到**自定义排序**。自定义排序可以用在很多地方，比如数组排序，堆的排序规则等。Java实现自定义排序，主要有两种方法：

### 1.实现Comparable接口：

以`Interval`区间为例，在定义该类时，让其实现Comparable，并重写其中的compareTo方法，使得Interval类可以进行大小比较，这样也可实现自定义的排序：

```
class Interval implements Comparable<Interval> {
    int left, right;
    Interval(int left, int right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int compareTo(Interval o) {
        return this.left - o.left;
    }
}
```

这样，在其他地方就可以直接对Interval对象的大小进行比较。完整的测试方法如下：

```
import java.util.ArrayList;
import java.util.List;
import static java.util.Collections.sort;

// Interval类如上

public class Main {
    public static void main(String[] args) {
        List<Interval> A = new ArrayList<>();
        A.add(new Interval(1, 7));
        A.add(new Interval(5, 6));
        A.add(new Interval(3, 4));
        System.out.println("Before sort:");
        for (Interval i : A)
            System.out.println("(" + i.left + ", " + i.right + ")");

        sort(A);
        System.out.println("After sort:");
        for (Interval i : A)
            System.out.println("(" + i.left + ", " + i.right + ")");
    }
}
```

输出可以自行观察，不再赘述。

### 2.定义比较类：

该方法定义一个新的比较类，使其继承自Comparator，并完善其中的compare\(\)方法。在调用时，使用该比较类进行比较。仍以`Interval`为例：

```
class Interval { // 注意，这里没有继承自Comparable
    int left, right;
    Interval(int left, int right) {
        this.left = left;
        this.right = right;
    }
}

class MyCmp implements Comparator<Interval> {
    @Override
    public int compare(Interval o1, Interval o2) {
        return o1.left - o2.left;
    }
}
```

要对`List<Interval> A`进行排序时，调用如下方法，填入一个比较类的对象即可：

```
A.sort(new MyCmp());
```

```java
/**
 * Definition for a Connection.
 * public class Connection {
 *   public String city1, city2;
 *   public int cost;
 *   public Connection(String city1, String city2, int cost) {
 *       this.city1 = city1;
 *       this.city2 = city2;
 *       this.cost = cost;
 *   }
 * }
 */

Collections.sort(connections, new Comparator<Connection>() {
    public int compare(Connection a, Connection b) {
        if (a.cost != b.cost) {
            return a.cost - b.cost;
        }
        if (!a.city1.equals(b.city1)) {
            return a.city1.compareTo(b.city1);
        }
        return a.city2.compareTo(b.city2);
    }
});
```

## Coding Problem

### Description

Give a new alphabet, such as {c,b,a,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z}. Sort the string array according to the new alphabet

### Example - [Verifying an Alien Dictionary](https://leetcode.com/problems/verifying-an-alien-dictionary/description/)

Given Alphabet =`{c,b,a,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z}`, String array =`{cab,cba,abc}`, return`{cba,cab,abc}`.

```
Explanation:
According to the new dictionary order, output the sorted result {cba, cab, abc}.
```

Given Alphabet =`{z,b,a,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,c}`, String array =`{bca,czb,za,zba,ade}`, return`{zba,za,bca,ade,czb}`.

```
Explanation:
According to the new dictionary order, output the sorted result {zba,za,bca,ade,czb}.
```

```java
public class Solution {
    /**
     * @param alphabet: the new alphabet
     * @param words: the original string array
     * @return: the string array after sorting
     */
    public String[] wordSort(char[] alphabet, String[] words) {
        // Write your code here
        Arrays.sort(words, new WordComparator(alphabet));

        return words;
    }

    class WordComparator implements Comparator<String> {
        Map<Character, Integer> map = new HashMap<>();
        public WordComparator(char[] alphabet) {
            for (int i = 0; i < alphabet.length; i++) {
                map.put(alphabet[i], i);
            }
        }

        public int compare(String a, String b) {
            int minLen = Math.min(a.length(), b.length());
            for (int i = 0; i < minLen; i++) {
                int aValue = map.get(a.charAt(i));
                int bValue = map.get(b.charAt(i));
                if (aValue == bValue) {
                    continue;
                } else {
                    return aValue - bValue;
                }
            }

            return a.length() - b.length();
        }
    }
}
```



