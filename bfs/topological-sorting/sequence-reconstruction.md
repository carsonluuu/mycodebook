# Sequence Reconstruction

Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 104. Reconstruction means building a shortest common supersequence of the sequences in seqs \(i.e., a shortest sequence so that all sequences in seqs are subsequences of it\). 

Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

### Example

**Example 1:**

```
Input: org: [1,2,3], seqs: [[1,2],[1,3]]
Output: false
Explanation: [1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
```

**Example 2:**

```
Input: org: [1,2,3], seqs: [[1,2]]
Output: false
Explanation: The reconstructed sequence can only be [1,2].
```

**Example 3:**

```
Input: org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]
Output: true
Explanation: The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
```

**Example 4:**

```
Input: org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]
Output: true
```

### Note

only one topological sorting exists..

Be aware of the edge cases and graph/indegree setting-up  

```java
class Solution {
    /*
    org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]
    org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]
    */
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        Map<Integer, Set<Integer>> aList = new HashMap<>();
        Map<Integer, Integer> indegree = new HashMap<>();
        
        for (List<Integer> seq : seqs) {
            for (int i = 0; i < seq.size(); i++) {
                aList.putIfAbsent(seq.get(i), new HashSet<>());
                indegree.putIfAbsent(seq.get(i), 0);
                if (i > 0 && !aList.get(seq.get(i - 1)).contains(seq.get(i))) {
                    aList.get(seq.get(i - 1)).add(seq.get(i));
                    indegree.put(seq.get(i), indegree.get(seq.get(i)) + 1);
                }
            }
        }
        
        if (org.length != indegree.size()) {
            return false;
        }
        
        Queue<Integer> q = new LinkedList<>();
        for (Integer key : indegree.keySet()) {
            if (indegree.get(key) == 0) {
                q.add(key);
            }
        }
        
        int index = 0;
        while (q.size() == 1) {
            int curr = q.poll();
            if (org[index++] != curr) {
                return false;
            }
            for (Integer neighbor : aList.get(curr)) {
                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    q.add(neighbor);
                }
            }
        }
        
        return index == org.length;
    }
}
```



