328.Odd Even Linked List

### 题目地址
- [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)

### 1,初步思路

```
/**
 * 1,全部遍历:
 * 2,两个链表:
 *      - 奇数链表
 *      - 偶数链表
 * 3,最终组装在一起
 */
 public ListNode oddEvenList(ListNode head) {
     if (head == null) {
         return head;
     }
     ListNode oddNode = new ListNode(-1);
     ListNode evenNode = new ListNode(0);
     ListNode evenHead = null;
     ListNode curr = head;
     int i = 1;
     while (curr != null) {
         if (i % 2 == 1) {
             // 奇数位
             oddNode.next = curr;
             oddNode = oddNode.next;
         } else {
             // 偶数位
             if (i == 2) {
                 evenHead = curr;
             }
             evenNode.next = curr;
             evenNode = evenNode.next;
         }
         curr = curr.next;
         i++;
     }
     oddNode.next = evenHead;
     return head;
 }
```

### 2,正确解法

```
// 解法一:
public ListNode oddEvenList(ListNode head) {
    if (head != null) {
        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;

        while (even != null && even.next != null) {
            odd.next = odd.next.next;
            even.next = even.next.next;
            odd = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
    }
    return head;
}
```

**参考资料**
- [Simple O(N) time, O(1), space Java solution.](https://leetcode.com/problems/odd-even-linked-list/discuss/78079/Simple-O(N)-time-O(1)-space-Java-solution.)