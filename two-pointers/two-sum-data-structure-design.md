# Two Sum III - Data structure design

Design and implement a TwoSum class. It should support the following operations:`add`and`find`.

`add`- Add the number to an internal data structure.  
`find`- Find if there exists any pair of numbers which sum is equal to the value.

### Example

```
add(1); add(3); add(5);
find(4) // return true
find(7) // return false
```

### Note

HashMap

### Code

```java
public class TwoSum {
    /*
     * @param number: An integer
     * @return: nothing
     */
    private Map<Integer, Integer> map = new HashMap<>();
    public void add(int number) {
        // write your code here
        map.put(number, map.getOrDefault(number, 0) + 1);
    }

    /*
     * @param value: An integer
     * @return: Find if there exists any pair of numbers which sum is equal to the value.
     */
    public boolean find(int value) {
        // write your code here
        for (Map.Entry<Integer, Integer> e : map.entrySet()) {
            int i = e.getKey();
            int j = value - i;
            int count = e.getValue();
            if ((i == j && count > 1) || (i != j && map.containsKey(j)) ) {
                return true;
            }
        }
        return false;
    }
}
```



