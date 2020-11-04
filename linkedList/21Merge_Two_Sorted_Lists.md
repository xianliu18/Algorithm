### 题目地址
- https://leetcode.com/problems/merge-two-sorted-lists/

### 1, 初步思路

```
// 暂时没有思路,只是非常粗糙的想法
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    // 创建新的ListNode
    ListNode resultList = new ListNode();
    // 遍历ListNode l1, 以及ListNode l2
    for (int a = l1.val, b = l2.val; l1.next != null && l2.next != null; 
                a = l1.next.val, b = l2.next.val) {
        if (a < b) {
            resultList = new ListNode(a, new ListNode(b));
        } else {
            resultList = new ListNode(b, new ListNode(a));
        }
    }
    return resultList;
}
```

### 2. 别人的解法

```
// ListNode
public class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val }
    ListNode(int val, ListNode next) { this.val = val; this.next = next }
}


class Solution {

    // 解法一:正常遍历
    public ListNode mergeTwoLists01(ListNode l1, ListNode l2) {
        if (l1 == null || l2 == null) {
            return l1 == null ? l2 : l1;
        }
        ListNode head = null;
        ListNode node = null;
        if (l1.val < l2.val) {
            head = l1;
            l1 = l1.next;
        } else {
            head = l2;
            l2 = l2.next;
        }
        node = head;

        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                node.next = l1;
                l1 = l1.next;
            } else {
                node.next = l2;
                l2 = l2.next;
            }
            node = node.next
        }
        if (l1 == null) {
            node.next = l2;
        }
        if (l2 == null) {
            node.next = l1;
        }
        return head;
    }

    // 正常遍历:解法2
    public ListNode mergeTwoLists02(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        }

        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                curr.next = l1;
                l1 = l1.next;
            } else {
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        curr.next = l1 == null ? l2 : l1;
        return dummy.next;
    }

    // 解法二:递归
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null || l2 == null) {
            return l1 == null ? l2 : l1;
        }
        ListNode prev = new ListNode(0);
        ListNode head = prev;
        if (l1.val < l2.val) {
            prev.val = l1.val;
            prev.next = mergeTwoLists(l1.next, l2);
        } else {
            prev.val = l2.val;
            prev.next = mergeTwoLists(l1, l2.next);
        }
        return head;
    }
}
```

**参考资料:**
- [Java using recursion评论部分](https://leetcode.com/problems/merge-two-sorted-lists/discuss/9715/Java-1-ms-4-lines-codes-using-recursion)