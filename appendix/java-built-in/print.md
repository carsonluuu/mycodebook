```java
int[] array = list.stream().mapToInt(i->i).toArray();
```

```java
import java.util.Arrays;

public class PrintArray {

    public static void main(String[] args) {

        // array
        String[] arrayStr = new String[]{"Java", "Node", "Python", "Ruby"};
        Arrays.stream(arrayStr).forEach(System.out::println);

        int[] arrayInt = {1, 3, 5, 7, 9};
        Arrays.stream(arrayInt).forEach(System.out::println);

        //2d array
        String[][] deepArrayStr = new String[][]{{"mkyong1", "mkyong2"}, {"mkyong3", "mkyong4"}};
        Arrays.stream(deepArrayStr).flatMap(x -> Arrays.stream(x)).forEach(System.out::println);

        int[][] deepArrayInt = new int[][]{{1, 3, 5, 7, 9}, {2, 4, 6, 8, 10}};
        Arrays.stream(deepArrayInt).flatMapToInt(x -> Arrays.stream(x)).forEach(System.out::println);

    }

}
```

```java
int mat[][] =
{
    { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
    { 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
    { 1, 1, 1, 1, 1, 1, 0, 1, 0, 1 },
    { 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 },
    { 1, 1, 1, 0, 1, 1, 1, 0, 1, 0 },
    { 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 },
    { 1, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
    { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
    { 1, 1, 0, 0, 0, 0, 1, 0, 0, 1 }
};

List<List<Integer>> list = Arrays.stream(mat)
        .map(row -> IntStream.of(row).boxed().collect(Collectors.toList()))
        .collect(Collectors.toList());
```



