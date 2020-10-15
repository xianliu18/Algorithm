141. Linked List Cycle

### 题目地址
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

### 1,初步思路

```

```

### 2,正确解法

```
// 解法一: 改变了链表
public boolean hasCycle(ListNode head) {
    ListNode p = head;
    ListNode pre = head;
    while (p != null && p.next != null) {
        if (p.next == head) {
            return true;
        }
        p = p.next;
        pre.next = head;
        pre = p;
    }
    return false;
}

// 解法二: Two pointer
// Youtube: https://www.youtube.com/watch?v=zbozWoMgKW0
// a + 2b + c = 2(a + b)
// https://leetcode.com/problems/linked-list-cycle-ii/discuss/44774/Java-O(1)-space-solution-with-detailed-explanation.


public ListNode hasCycle2(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
        if (fast == slow) {
            ListNode slow2 = head;
            while (slow != slow2) {
                slow2 = slow2.next;
                slow = slow.next;
            }
            return slow;
        }
    }
    return null;
}
```