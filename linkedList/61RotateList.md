61.Rotate List

### 题目地址
- [Rotate List](https://leetcode.com/problems/rotate-list/)

### 1,初步思路

```
/**
 * 1, 获取LinkdeList的长度 size
 * 2, 需要转换的index = size - k % size
 *         - 特殊case:[1],  k = 0 或 1
 */
public ListNode rotateRight(ListNode head, int k) {
    if (head == null || k < 0) {
        return null;
    }
    // 获取list的长度
    int i = 0;
    ListNode iter = head;
    ListNode last = head;
    while (iter != null) {
        last = iter;
        iter = iter.next;
        i++;
    }
    int index = i - k % i;
    // 此处需要注意,k ==0 或 index == i的情况
    if (index == 0 || k == 0 || index == i) {
        return head;
    }
    ListNode prev = head;
    ListNode temp = head;
    for (int m = 1; m <= index; m++) {
        prev = temp;
        temp = temp.next;
    }
    prev.next = null;
    last.next = head;
    return temp;
}
```

### 2,正确解法

```
// 知道索引位置,索引递减遍历
public ListNode rotateRight(ListNode head, int k) {
    if (head == null) {
        return null;
    }
    // 获取链表长度
    ListNode iter = head;
    len++;
    while (iter.next != null) { // 此处,判断iter.next, 这样可以保留iter为最后一个值
        iter = iter.next;
        len++;
    }
    // 此时,iter处于链表结尾
    iter.next = head;

    // 重新遍历链表,为转换做准备
    ListNode newLast = head;
    for (int i = len - k % len; i > 1; i--) {
        newLast = newLast.next;
    }
    ListNode newHead = newLast.next;
    newLast.next = null;
    return newHead;
}

```

**参考资料**
- [Clean Java Solution with Brief Explanation](https://leetcode.com/problems/rotate-list/discuss/22751/Clean-Java-Solution-with-Brief-Explanation)