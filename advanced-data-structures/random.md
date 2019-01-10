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

### Multiple Calls with Non-repeated results

```java
public class RandomGetAds {
    int len;
    final Random random = new Random();
    RandomGetAds(String[] ads) {
        this.len = ads.length;
    }

    // O(1)
    public void randomGetAds(String[] ads) {
        if (len == 0) {
            System.out.println("all ads have been output");
        }
        int index = random.nextInt(len);
        System.out.println(ads[index]);

        moveToTail(ads, index, len);
        len--;
    }

    private void moveToTail(String[] ads, int index, int len) {
        String temp = ads[index];
        ads[index] = ads[len - 1];
        ads[len - 1] = temp;
    }

    public static void main(String[] args) {
        String[] ads = {"a", "b", "c", "d", "e", "f"};
        RandomGetAds r = new RandomGetAds(ads);
        // should out distinct ones
        r.randomGetAds(ads);
        r.randomGetAds(ads);
        r.randomGetAds(ads);
        r.randomGetAds(ads);
        r.randomGetAds(ads);
        r.randomGetAds(ads);
    }
}

```



