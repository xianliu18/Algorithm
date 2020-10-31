116.Populating Next Right Pointers in Each Node

### 题目地址
- [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

### 1,初步思路

```

```

### 2,正确解法

```
public class TreeLinkNode {
    public int val;
    public TreeLinkNode left;
    public TreeLinkNode right;
    public TreeLinkNode next;

    public TreeLinkNode() {}

    public TreeLinkNode(int _val) {
        this.val = _val;
    }

    public TreeLinkNode(int _val, TreeLinkNode _left, TreeLinkNode _right, TreeLinkNode _next) {
        this.val = _val;
        this.left = _left;
        this.right = _right;
        this.next = _next;
    }
}

/***** Iterative: O(1) space, O(n) Time *****/
public TreeLinkNode connect(TreeLinkNode root) {
    if (root == null) {
        return null;
    }

    TreeLinkNode levelStart = root;
    while (levelStart != null) {
        TreeLinkNode curr = levelStart;
        while (curr != null) {
            if (curr.left != null) {
                curr.left.next = curr.right;
            }
            if (curr.right != null && curr.next != null) {
                curr.right.next = curr.next.left;
            }
            curr = curr.next;
        }
        levelStart = levelStart.left;
    }
    return root;
}


/***** Recursive: O(1) Space and O(n) Time *****/
public TreeLinkNode connect2(TreeLinkNode root) {

    if (root == null) {
        return null;
    }

    if (root.left != null) {
        root.left.next = root.right;
    }
    if (root.right != null && root.next != null) {
        root.right.next = root.next.left;
    }
    connect2(root.left);
    connect2(root.right);
    return root;
}


/***** Level Traversal use Dequeue: O(n) Space and O(n) Time *****/
public TreeLinkNode connect3(TreeLinkNode root) {

    if (root == null) {
        return null;
    }

    Queue<TreeLinkNode> queue = new LinkedList<>();
    queue.offer(root);
    queue.offer(null);
    while (!queue.isEmpty()) {
        TreeLinkNode curr = queue.poll();

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

```

**参考资料**
- [Java solution with O(1) memory, O(n) time](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/discuss/37461/Java-solution-with-O(1)-memory%2B-O(n)-time)