# Subarray

### Basics

`PrefixSum[i] = A[0] + A[1] + A[2] + ... + A[i - 1], PrefixSum[0] = 0, len(PrefixSum) = len(A) + 1`

`Sum(i~j) = PrefixSum[j + 1] - PrefixSum[i]`

### Subarray Equals to Target

* Using HashMap to store \( key : the **PrefixSum**, value : how many ways get to this prefix sum\). 
* Check if **PrefixSum** **-** **target** exists in hashmap or not, if it does, we added up the ways of this key
* For instance : in one path we have 1,2,-1,-1,2, then the prefix sum will be: 0, 1, 3, 2, 1, 3, let's say we want to find target sum is 2, then we will have{2}, {1,2,-1}, {2,-1,-1,2} and {2}ways.
* Meaning: `PrefixSum2 - PrefixSum1 = Target`



