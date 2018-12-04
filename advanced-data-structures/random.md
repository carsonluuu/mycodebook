# Random

包括一些和随机有关的问题

### Reservoir Sampling

很重要的随机理论

### Generate n different random numbers in Java

java8

```java
final int[] ints = new Random().ints(1, 50).distinct().limit(6).toArray();
```

java7

```java
public static void main(final String[] args) throws Exception {
    final Random random = new Random();
    final Set<Integer> intSet = new HashSet<>();
    while (intSet.size() < 6) {
        intSet.add(random.nextInt(49) + 1);
    }
    final int[] ints = new int[intSet.size()];
    final Iterator<Integer> iter = intSet.iterator();
    for (int i = 0; iter.hasNext(); ++i) {
        ints[i] = iter.next();
    }
    System.out.println(Arrays.toString(ints));
}
```



