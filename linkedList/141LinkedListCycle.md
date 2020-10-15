141. Linked List Cycle

### 题目地址
- [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

### 1,初步思路

```

```

### 2,正确解法

```
// 解法一:
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
public boolean hasCycle2(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    while (fast != null && fast.next != null) {
        if (fast.next == head) {
            return true;
        }
        fast = fast.next.next;
        slow = slow.next;
        if (fast == slow) {
            return true;
        }
    }
    return false;
}
```