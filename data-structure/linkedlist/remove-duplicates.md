# [Remove Duplicates](https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/)

Write a removeDuplicates\(\) function which takes a list and deletes any duplicate nodes from the list. The list is not sorted.

### Example

if the linked list is 12-&gt;11-&gt;12-&gt;21-&gt;41-&gt;43-&gt;21 then removeDuplicates\(\) should convert the list to 12-&gt;11-&gt;21-&gt;41-&gt;43.

### Note

* 排序（merge sort）+双指针
* 哈希Set

### Code

```java
class LinkedList 
{ 
    Node head;  // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int data; 
        Node next; 
        Node(int d) {data = d; next = null; } 
    } 

    void removeDuplicates() { 
        /*Another reference to head*/
        Node current = head; 

        /* Pointer to store the next pointer of a node to be deleted*/
        Node next_next; 

        /* do nothing if the list is empty */
        if (head == null)     
            return; 

        /* Traverse list till the last node */
        while (current.next != null) { 

            /*Compare current node with the next node */
            if (current.data == current.next.data) { 
                next_next = current.next.next; 
                current.next = null; 
                current.next = next_next; 
            } 
            else // advance if no deletion 
               current = current.next; 
        } 
    } 
}
```

```java
import java.util.HashSet; 
  
public class removeDuplicates { 
    static class node { 
        int val; 
        node next; 
  
        public node(int val) { 
            this.val = val; 
        } 
    } 
      
    /* Function to remove duplicates from a 
       unsorted linked list */
    static void removeDuplicate(node head) { 
        // Hash to store seen values 
        HashSet<Integer> hs = new HashSet<>(); 
      
        /* Pick elements one by one */
        node current = head; 
        node prev = null; 
        while (current != null) { 
            int curval = current.val; 
              
             // If current value is seen before 
            if (hs.contains(curval)) { 
                prev.next = current.next; 
            } else { 
                hs.add(curval); 
                prev = current; 
            } 
            current = current.next; 
        }  
    } 
}
```



