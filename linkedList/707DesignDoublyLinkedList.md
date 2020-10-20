707.Design Doubly Linked List

### 题目地址
- [Design Linked List](https://leetcode.com/problems/design-linked-list/)

### 1,初步思路

```

```

### 2,正确解法

```
class MyLinkedList {
    class ListNode {
        int val;
        ListNode prev, next;
        ListNode(int val) {
            this.val = val;
        }
    }

    ListNode head;
    ListNode tail;
    int size;

    public MyLinkedList() {
        head = new ListNode(0);
        tail = new ListNode(0);
        head.next = tail;
        tail.prev = head;
    }

    public int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }
        ListNode curr = head;
        for (int i = 0; i <= index; i++) {
            curr = curr.next;
        }
        return curr.val;
    }

    public void addAtHead(int val) {
        addAtIndex(0, val);
    }

    public void addAtTail(int val) {
        addAtIndex(size, val);
    }

    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) {
            return;
        }

        ListNode curr = head;
        for (int i = 0; i < index; i++) {
            curr = curr.next;
        }
        
        ListNode newNode = new ListNode(val);

        newNode.next = curr.next;
        newNode.prev = curr;
        curr.next.prev = newNode;
        curr.next = newNode;
        size++;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        ListNode curr = head;
        for (int i = 0; i <= index; i++) {
            curr = curr.next;
        }
        curr.next.prev = curr.prev;
        curr.prev.next = curr.next;
        size--;
    }
}
```

**参考资料**
- [Java Doubly Linked List Solution](https://leetcode.com/problems/design-linked-list/discuss/186459/Java-Doubly-Linked-List-solution-73ms)