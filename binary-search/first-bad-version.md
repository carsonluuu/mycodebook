# First Bad Version

The code base version is an integer start from 1 to n. One day, someone committed a bad version in the code case, so it caused this version and the following versions are all failed in the unit tests. Find the first bad version.

You can call`isBadVersion`to help you determine which version is the first bad one. The details interface can be found in the code's annotation part.

### Example

Given n =`5`:

```
isBadVersion(3) -> false
isBadVersion(5) -> true
isBadVersion(4) -> true
```

Here we are 100% sure that the 4th version is the first bad version.

### Note

只知道是不是bad version，是bad那么就抛弃右边，不是bad就抛弃左边

最后先后判断start和end即可

### Code

```java
/**
 * public class SVNRepo {
 *     public static boolean isBadVersion(int k);
 * }
 * you can use SVNRepo.isBadVersion(k) to judge whether 
 * the kth code version is bad or not.
*/

public class Solution {
    /*
     * @param n: An integer
     * @return: An integer which is the first bad version.
     */
    public int findFirstBadVersion(int n) {
        // write your code here
        int start = 1, end = n;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (SVNRepo.isBadVersion(mid)) {
                end = mid;
            } else {
                start = mid;
            }
        }
        
        if (SVNRepo.isBadVersion(start)) {
            return start;
        } else {
            return end;
        }
    }
}
```



