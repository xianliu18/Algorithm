117.Populating Next Right Pointers in Each Node II

### 题目地址
- [Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Level Traversal: O(n) Space, O(n) Time *****/
public TreeLinkNode connect(TreeLinkNode root) {

    if (root == null) {
        return null;
    }

    Queue<TreeLinkNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    while (!queue.isEmpty()) {
        Node curr = queue.poll();

        if (curr == null) {
            if (queue.size() > 0) {
                queue.offer(null);
            }
        } else {
            curr.next = queue.peek();
            if (curr.left != null) {
                queue.offer(curr.left);
            }
            if (curr.right != null) {
                queue.offer(curr.right);
            }
        }
    }
    return root;
}


/***** Iterative  *****/
public TreeLinkNode connect2(TreeLinkNode root) {

    if (root == null) {
        return null;
    }

    TreeLinkNode dummy = new TreeLinkNode(0);
    TreeLinkNode p = dummy;
    TreeLinkNode head = root;
    
    // if the head of the traverse layer is not null, then traverse that layer
    while (head != null) {
        TreeLinkNode curr = head;
        while (curr != null) {
            if (curr.left != null) {
                p.next = curr.left;
                p = p.next;
            }
            if (curr.right != null) {
                p.next = curr.right;
                p = p.next;
            }
            curr = curr.next;
        }

        // after traversed to the end of the current layer, move to the next layer
        head = dummy.next;
        dummy.next = null;
        p = dummy;
    }
    return root;
}
```

**参考资料**
- [O(1) Space O(n) complexity Iterative Solution](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/discuss/37828/O(1)-space-O(n)-complexity-Iterative-Solution)