430.Flattern a Multilevel Doubly Linked List

### 题目地址
- [Flattern a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)

### 1,初步思路

```
// 没有思路
```

### 2,正确解法

```
// 解法一:
/**
 * 1, Start from the head, move one step each time to the next node.
 * 2, When meet with a node with child, say node p, follow its child chain to the end and connect the 
 * tail node with p.next, by doing this we merged the child chain back to the main thread.
 * 3, Return to p and proceed until find next node with child.
 * 4, Repeat until reach null.
 */
 public Node flattern(Node head) {
     if (head == null) {
         return head;
     }
     Node p = head;
     while (p != null) {
         // CASE1: if no child, proceed
         if (p.child == null) {
             p = p.next;
             continue;
         }
         // CASE2: got child, find the tail of the child and link it to p.next
         Node temp = p.child;
         while (temp.next != null) {
             temp = temp.next;
         }
         // Connect tail with p.next, if it is not null
         temp.next = p.next;
         if (p.next != null) {
             p.next.prev = temp;
         }
         // Connect p with p.child, and remove p.child
         p.next = p.child;
         p.child.prev = p;
         p.child = null;
     }
     return head;
 }
```

**参考资料**
- [Easy Understanding Java beat 95.7% with Explanation](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/discuss/150321/Easy-Understanding-Java-beat-95.7-with-Explanation)