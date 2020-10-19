206.Reverse Linked List

### 题目地址
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

### 1,初步思路

```
// 错误解法
public ListNode reverseList(ListNode head) {
    ListNode itera = head;
    ListNode result = head;
    while (itera != null && itera.next != null) {
        // 生成顶点
        ListNode temp = result;
        result = itera.next;
        result.next = temp;
        // 将遍历节点向后移动一位
        itera.next = itera.next.next;
        itera = itera.next;
    }
    return result;
}
```

### 2,正确解法

```
/* Iteration solution */
public ListNode reverseList(ListNode head) {
    ListNode newHead = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = newHead;
        newHead = head;
        head = next;
    }
    return newHead;
}

/* recursion solution */
public ListNode reverseList01(ListNode head) {
    return reverseListInt(head, null);
}

private ListNode reverseListInt(ListNode head, ListNode newHead) {
    if (head == null) {
        return newHead;
    }
    ListNode next = head.next;
    head.next = newHead;
    return reverseListInt(next, head);
}
```

**参考资料**
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/discuss/58125/In-place-iterative-and-recursive-Java-solution)
- [How can I reverse a linked list](https://stackoverflow.com/questions/9076923/how-can-i-reverse-a-linked-list)