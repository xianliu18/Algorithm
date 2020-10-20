234.Palindrome Linked List

### 题目地址
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```
// 解法一
// This can be solved by reversiing the 2nd half and compare the two halves.
/**
 * Move
 * Reverse
 * Compare
 */

 public boolean isPalindrome(ListNode head) {
     ListNode fast = head;
     ListNode slow = head;
     while (fast != null && fast.next != null) {
         fast = fast.next.next;
         slow = slow.next;
     }
     if (fast != null) {
         slow = slow.next;
     }
     slow = reverse(slow);
     fast = head;

     while (slow != null) {
         if (fast.val != slow.val) {
             return false;
         }
         fast = fast.next;
         slow = slow.next;
     }
     return true;
 }

 private ListNode reverse(ListNode head) {
     ListNode prev = null;
     while (head != null) {
         ListNode next = head.next;
         head.next = prev;
         prev = head;
         head = next;
     }
     return prev;
 }

```

**参考资料**
- [Java, easy to understand](https://leetcode.com/problems/palindrome-linked-list/discuss/64501/Java-easy-to-understand)