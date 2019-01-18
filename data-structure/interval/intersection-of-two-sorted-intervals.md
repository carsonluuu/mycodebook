```java
public static List<Interval> Intersactions(final List<Interval> intervalA, final List<Interval> intervalB) {
    int i = 0, j = 0;
    final List<Interval> intersaction = new ArrayList<>();
    while (i < intervalA.size() && j < intervalB.size()) {
      final int start = Math.max(intervalA.get(i).getStart(), intervalB.get(j).getStart());
      final int end = Math.min(intervalA.get(i).getEnd(), intervalB.get(j).getEnd());

      if (end > start) {
        intersaction.add(new Interval(start, end));
      }
      if (intervalA.get(i).getEnd() < intervalB.get(j).getEnd()) {
        i++;
      } else {
        j++;
      }
    }
    return intersaction;
  }
```



