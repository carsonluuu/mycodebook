# Pair Iterator

```java
class Pair {
    String word;
    int count;
    public Pair(String word, int count) {
        this.word = word;
        this.count = count;
    }
    @Override
    public String toString() {
        return "[" + word + ": " + count + "]";
    }
}
```

### Example

```
["foo", "foo", "bar", "foo"] => [foo:2, bar:1]
```

### Code

```java
public class PairIterator implements Iterator<Pair> {
    private Iterator<String> it;
    private String next = null;
    int cnt;
    public PairIterator(List<String> input) {
        it = input.iterator();
        cnt = 0;
        if (it.hasNext()) {
            next = it.next();
        }
    }

    @Override
    public boolean hasNext() {
        return next != null;
    }

    @Override
    public Pair next() {
        String anchor = next;
        while (next.equals(anchor)) {
            cnt++;
            if (it.hasNext()) {
                next = it.next();
            } else {
                next = null;
                return new Pair(anchor, cnt);
            }
        }

        Pair res = new Pair(anchor, cnt);
        cnt = 0;

        return res;
    }
}
```



