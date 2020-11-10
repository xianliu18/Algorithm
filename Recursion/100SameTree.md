100. Same Tree

### 题目地址
- [Same Tree](https://leetcode.com/problems/same-tree/)

### 1,初步思路

```
/***** Iterative *****/
public boolean isSameTree(TreeNode p, TreeNode q) {
    
    Stack<TreeNode> left = new Stack<>();
    Stack<TreeNode> right = new Stack<>();
    left.add(p);
    right.add(q);
    while (!left.isEmpty()) {
        TreeNode leftNode = left.pop();
        TreeNode rightNode = right.pop();

        // 此处,不知道如何去add element

        if (leftNode == null && rightNode == null) {
            continue;
        }
        if (leftNode == null || rightNode == null) {
            return false;
        }
        if (leftNode.val != rightNode.val) {
            return false;
        }
    }

    return true;
}

```

### 2,正确解法

```
/***** Recursion *****/
public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) {
        return true;
    }
    if (p == null || q == null) {
        return false;
    }
    if (p.val != q.val) {
        return false;
    }

    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}


/***** Iterative *****/
public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) {
        return true;
    }

    if (p == null || q == null) {
        return false;
    }

    Stack<TreeNode> left = new Stack<>();
    Stack<TreeNode> right = new Stack<>();
    left.add(p);
    right.add(q);
    while (!left.isEmpty() && !right.isEmpty()) {
        TreeNode leftNode = left.pop();
        TreeNode rightNode = right.pop();

        if (leftNode.val != rightNode.val) {
            return false;
        }

        // compare their left child
        if (leftNode.left == null || rightNode.left == null) {
            if (leftNode.left != null || rightNode.left != null) {
                return false;
            }
        } else {
            left.add(leftNode.left);
            right.add(rightNode.left);
        }

        // compare their right child
        if (leftNode.right == null || rightNode.right == null) {
            if (leftNode.right != null || rightNode.right != null) {
                return false;
            }
        } else {
            left.add(leftNode.right);
            right.add(rightNode.right);
        }
    }
    
    return left.isEmpty() && right.isEmpty();
}


// Deque
public boolean isSameTree(TreeNode p, TreeNode q) {
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(p);
    queue.offer(q);
    while (!queue.isEmpty()) {
        TreeNode f = queue.poll();
        TreeNode s = queue.poll();
        if (f == null && s == null) {
            continue;
        } else if (f == null || s == null || f.val != s.val) {
            return false;
        }

        queue.add(f.left);
        queue.add(s.left);
        queue.add(f.right);
        queue.add(s.right);
    }

    return true;
}
```

**参考资料**
- [Non-recursive Method](https://leetcode.com/problems/same-tree/discuss/32684/My-non-recursive-method)