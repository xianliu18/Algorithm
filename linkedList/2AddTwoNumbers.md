2.Add Two Numbers

### 题目地址
- [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

### 1,初步思路

```
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
		/*
		 * 思路:
		 *    1, l1 和 l2 不为null
		 *    2, 如何处理l1 + l2 > 10的情况
		 *    3, 如何处理 l1 和 l2 两位数相加,得到三位数: 95 + 96
		 *    4, 存在问题: l1:[9, 9], l2:[9]
		 */
		// 判空
		if (l1 == null || l2 == null) {
            // l1:[9, 9], l2: [9]

			return l1 == null ? l2 : l1;
		}

		ListNode head = null;
		int resultVal = l1.val + l2.val;
        // 处理 l1 + l2 > 10 的情况
		if (resultVal > 9) {
			head = new ListNode(resultVal % 10);
            // 处理两数相加大于10
			l1.next = l1.next == null ? new ListNode(1) : new ListNode(l1.next.val + 1);
			head.next = addTwoNumbers(l1.next, l2.next);
		} else {
			head = new ListNode(resultVal);
			head.next = addTwoNumbers(l1.next, l2.next);
		}
		return head;
	}
```

### 2,正确解法

```
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode prev = new ListNode(0);
	ListNode head = prev;
	int carry = 0;
	while (l1 != null || l2 != null || carry != 0) {
		ListNode cur = new ListNode(0);
		int sum = ((l2 == null) ? 0 : l2.val) + ((l1 == null) ? 0 : l1.val) + carry;
		cur.val = sum % 10;
		carry = sum / 10;
		prev.next = cur;
		prev = cur;

		l1 = (l1 == null) ? l1 : l1.nexr;
		l2 = (l2 == null) ? l2 : l2.next;
	}
	return head.next;
}
```