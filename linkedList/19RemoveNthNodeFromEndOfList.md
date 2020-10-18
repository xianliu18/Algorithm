19.Remove Nth Node From End of List

### 题目地址
- [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### 1,初步思路

```
/**
 * 如何定位?
 */
```

### 2,正确解法

```
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode start = new ListNode(0);
    start.next = head;
    ListNode slow = start;
    ListNode fast = start;

    // Move fast in front so that the gap between slow and fast becomes n
    for (int i = 1; i <= n+1; i++) {
        fast = fast.next;
    }

    // Move fast to the end, maintaining the gap
    while (fast != null) {
        slow = slow.next;
        fast = fast.next;
    }

    // skip the desired one
    slow.next = slow.next.next;
    return start.next;
}
```

**参考资料**
- [Simple Java Solution in one pass](https://leetcode.com/problems/remove-nth-node-from-end-of-list/discuss/8804/Simple-Java-solution-in-one-pass)