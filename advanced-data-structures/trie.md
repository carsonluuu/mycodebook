# Trie

A Trie is a special data structure used to store strings that can be visualized like a tree. It consists of nodes and edges. Each node consists of at max 26 children and edges connect each parent node to its children. These 26 pointers are nothing but pointers for each of the 26 letters of the English alphabet A separate edge is maintained for every edge.

Strings are stored in a top to bottom manner on the basis of their prefix in a trie. All prefixes of length 1 are stored at until level 1, all prefixes of length 2 are sorted at until level 2 and so on.

A Trie data structure is very commonly used for representing the words stored in a dictionary. Each level represents one character of the word being formed. A word available in the dictionary can be read off from the Trie by starting from the root and going till the leaf.

There are several other data structures, like balanced trees and hash tables, which give us the possibility to search for a word in a dataset of strings. Then why do we need trie? Although hash table has O\(1\) time complexity for looking for a key, it is not efficient in the following operations:

* Finding all keys with a common prefix.
* Enumerating a dataset of strings in lexicographical order.

Another reason why trie outperforms hash table, is that as hash table increases in size, there are lots of hash collisions and the search time complexity could deteriorate to O\(n\), where n is the number of keys inserted. Trie could use less space compared to Hash Table when storing many keys with the same prefix. In this case using trie has only O\(m\) time complexity, where m is the key length. Searching for a key in a balanced tree costs O\(mlogn\) time complexity.

### Trie node structure

Trie is a rooted tree. Its nodes have the following fields:

* Maximum of R links to its children, where each link corresponds to one of R character values from dataset alphabet. In this article we assume that R is 26, the number of lowercase latin letters.
* Boolean field which specifies whether the node corresponds to the end of the key, or is just a key prefix.

![](https://leetcode.com/media/original_images/208_Node.png "Representation of a key in trie")

### Insertion of a key to a trie

We insert a key by searching into the trie. We start from the root and search a link, which corresponds to the first key character. There are two cases :

* A link exists. Then we move down the tree following the link to the next child level. The algorithm continues with searching for the next key character.
* A link does not exist. Then we create a new node and link it with the parent's link matching the current key character. We repeat this step until we encounter the last character of the key, then we mark the current node as an end node and the algorithm finishes.

###### ![](https://leetcode.com/media/original_images/208_TrieInsert.png "Insertion of keys into a trie")**Complexity Analysis**

* Time complexity: O\(m\), where m is the key length.

In each iteration of the algorithm, we either examine or create a node in the trie till we reach the end of the key. This takes only m operations.

* Space complexity: O\(m\)

In the worst case newly inserted key doesn't share a prefix with the the keys already inserted in the trie. We have to add m new nodes, which takes us O\(m\) space.

### Search for a key in a trie

Each key is represented in the trie as a path from the root to the internal node or leaf. We start from the root with the first key character. We examine the current node for a link corresponding to the key character. There are two cases :

* A link exist. We move to the next node in the path following this link, and proceed searching for the next key character.
* A link does not exist. If there are no available key characters and current node is marked as`isEnd`we return true. Otherwise there are possible two cases in each of them we return false :

  * There are key characters left, but it is impossible to follow the key path in the trie, and the key is missing.
  * No key characters left, but current node is not marked as `isEnd`. Therefore the search key is only a prefix of another key in the trie.

![](https://leetcode.com/media/original_images/208_TrieSearchKey.png "Search of a key in a trie")

###### **Complexity Analysis**

* Time complexity: O\(m\) In each step of the algorithm we search for the next key character. In the worst case the algorithm performs m operations.

* Space complexity: O\(1\)

### Search for a key prefix in a trie

The approach is very similar to the one we used for searching a key in a trie. We traverse the trie from the root, till there are no characters left in key prefix or it is impossible to continue the path in the trie with the current key character. The only difference with the mentioned above`search for a key`algorithm is that when we come to an end of the key prefix, we always return true. We don't need to consider the `isEnd`mark of the current trie node, because we are searching for a prefix of a key, not for a whole key.

###### ![](https://leetcode.com/media/original_images/208_TrieSearchPrefix.png "Search of a key prefix in a trie") **Complexity Analysis**

* Time complexity: O\(m\)

* Space complexity: O\(1\)

###  Hash

Hash vs Trie

互相可替代

Trie 耗费更少的空间，单次查询 Trie 耗费更多的时间（复杂度相同，Trie 系数大一些）



