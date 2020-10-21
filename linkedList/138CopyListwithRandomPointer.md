138.Copy List with Random Pointer

### 题目地址
- [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

### 1,初步思路

```
// 没有思路
```

### 2,正确解法

```
/**
 * 1, Iterate the original list and duplicate each node. The duplicate of each node follows its original immediately.
 * 2, Iterate the new list and assign the random pointer for each duplicated node.
 * 3, Restore the original list adn extract the duplicated nodes.
 */

 public RandomListNode copyRandomList(RandomListNode head) {
     RandomListNode iter = head;
     RandomListNode next;

     // First round: make copy of each node.
     // and link them together side-by-side in a single list.
     while (iter != null) {
         next = iter.next;

         RandomListNode newCopy = new RandomListNode(iter.val);
         newCopy.next = next;
         iter.next = newCopy;

         iter = next;
     }

     // Second round: assign random pointers for the copy nodes
     iter = head;
     while (iter != null) {
         if (iter.random != null) {
             iter.next.random = iter.random.next;
         }

         iter = iter.next.next;
     }

     // Third round: restore the original list, and extract the copy list.
     iter = head;
     RandomListNode pseudoHead = new RandomListNode(0);
     RandomListNode copy;
     RandomListNode copyIter = pseudoHead;
     while (iter != null) {
         next = iter.next.next;

         // extract the copy
         copy = iter.next;
         copyIter.next = copy;
         copyIter = copy;

         // restore the original list
         iter.next = next;
         iter = next;
     }

     return pseudoHead.next;
 }
```

**参考资料**
- [A solution with constant space complexity O(1) and linear time complexity O(N)](https://leetcode.com/problems/copy-list-with-random-pointer/discuss/43491/A-solution-with-constant-space-complexity-O(1)-and-linear-time-complexity-O(N))