# Flatten 2D Vector

Implement an iterator to flatten a 2d vector.

### Example

```
Input: 2d vector =
[
  [1,2],
  [3],
  [4,5,6]
]
Output: [1,2,3,4,5,6]
Explanation: By calling next repeatedly until hasNext returns false, 
             the order of elements returned by next should be: [1,2,3,4,5,6].
```

### Code

```java
public class Vector2D implements Iterator<Integer> {

    private Iterator<List<Integer>> rowIt;
    private Iterator<Integer> colIt;

    public Vector2D(List<List<Integer>> vec2d) {
        rowIt = vec2d.iterator();
    }

    @Override
    public Integer next() {
        if (!hasNext()) {
            return null;
            //throw new NoSuchElementException();
        }
        return colIt.next();
    }

    @Override
    public boolean hasNext() {
        while ((colIt == null || !colIt.hasNext()) && rowIt.hasNext()) {
            colIt = rowIt.next().iterator();
        }
        return colIt != null && colIt.hasNext();
    }

    @Override
    public void remove() {
        if (colIt == null) {
            return;
        }
        colIt.remove();
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
```



