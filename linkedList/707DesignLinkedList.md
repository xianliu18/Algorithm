707. Design Linked List

### 题目地址
- [Design Linked List](https://leetcode.com/problems/design-linked-list/)

### 1,初步思路

```
/**
 * 存在问题: 如何表述当前的head?
 */
 
public class MyLinkedList {
    int val;
    MyLinkedList next;

    public MyLinkedList(){
    }

    public int get(int index) {
        int i = 0;
        MyLinkedList cur = this;
        while (true) {
            if (i == index) {
                return cur.val;
            }
            i++;
            cur = this.next;
        }
    }

    public void addAtHead(int val) {
        MyLinkedList head = this;
        this.val = val;
        this.next = head;
    }

    public void addAtTail(int val) {
        MyLinkedList cur = new MyLinkedList();
        cur.val = val;
        cur.next = null;
        MyLinkedList temp = this;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = cur;
    }

    public void addAtIndex(int index, int val) {
        if (index == 0) {
            addAtHead(val);
        }
        int i = 0;
        MyLinkedList cur = this;
        MyLinkedList prev = null;
        while (true) {
            if (i == index - 1) {
                if (cur.next == null) {
                    addAtTail(val);
                } else {
                    MyLinkedList temp = new MyLinkedList();
                    temp.val = val;
                    temp.next = cur;
                    prev.next = temp;
                }
            }
            i++;
            prev = cur;
            cur = this.next;
        }
    }

    public void deleteAtIndex(int index) {
    }
}
```

### 2,正确解法

```
class MyLinkedList {

    class Node {
        int val;
        Node next;
        public Node(int val) {
            this.val = val;
        }
    }

    public MyLinkedList() {

    }

    public int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }
        Node current = head;
        for (int i = 0; i < index; i++) {
            current = current.next;
        }
        return current.val;
    }

    public void addAtHead(int val) {
        Node prev = head;
        head = new Node(val);
        head.next = prev;
        size++;
    }

    public void addAtTail(int val) {
        Node node = new Node(val);
        size++;
        if (head == null) {
            head = node;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = node;
        }
    }

    public void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }
        if (index == 0) {
            addAtHead(val);
        } else {
            size++;
            Node current = head;
            for (int i = 0; i < index - 1; i++) {
                current = current.next;
            }
            Node node = new Node(val);
            node.next = current.next;
            current.next = node;
        }
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        size--;
        if (index == 0) {
            head = head.next;
            return;
        }
        Node current = head;
        for (int i = 0; i < index - 1; i++) {
            current = current.next;
        }
        current.next = current.next.next;
    }
}
```
