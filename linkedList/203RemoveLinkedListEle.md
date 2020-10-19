203.Remvoe Linked List Elements

### 题目地址
- [Remvoe Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)

### 1,初步思路

```
/**
 * 遍历链表,将当前值与待删除值比较:
 *     1, 如何执行删除操作?
 *            需要记录前一个值,删除时,将前一个值的指针指向当前值的后一个值
 *     2, 如何返回head?
 */
 // 错误解法
 public ListNode removeEle(ListNode head, int val) {
     ListNode previous = new ListNode(0);
     previous.next = head;
     ListNode cur = head;

     while (cur != null) {
         ListNode next = cur.next;
         if (cur.val == val) {
             previous.next = cur.next;
             cur = cur.next;
             continue;
         }
         previous = cur;
         cur = next;
     }

     return head;
 }

```

### 2,正确解法

```

// 三个变量
public ListNode removeElements(ListNode head, int val) {
    ListNode fakeHead = new ListNode(-1);
    fakeHead.next = head;
    ListNode curr = head;
    ListNode prev = fakeHead;
    while (curr != null) {
        if (curr.val == val) {
            prev.next = curr.next;
        } else {
            prev = prev.next;
        }
        curr = curr.next;
    }
    return fakeHead.next;
}

// 两个变量
public ListNode removeElements01(ListNode head, int val) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode cur = dummy;
    while (cur.next != null) {
        if (cur.next.val == val) {
            cur.next = cur.next.next;
        } else {
            cur = cur.next;
        }
    }
    return dummy.next;
}

```

**参考资料**
-[AC Java Solution](https://leetcode.com/problems/remove-linked-list-elements/discuss/57324/AC-Java-solution)
