101.Symmetric Tree

### 题目地址
- [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursion *****/
public boolean isSymmetric(TreeNode root) {
    return root == null || isSymmetricHelp(root.left, root.right);
}

private booleanisSymmetricHelp(TreeNode left, TreeNode right) {
    if (left == null || right == null) {
        return left == right;
    }

    if (left.val != right.val) {
        return false;
    }

    return isSymmetricHelp(left.left, right.right) &&
        isSymmetricHelp(left.right, right.left);
}


/***** Iteration *****/
public boolean isSymmetric2(TreeNode root) {
    
    if (root == null) {
        return true;
    }

    Stack<TreeNode> s1 = new Stack<>();
    Stack<TreeNode> s2 = new Stack<>();
    s1.push(root.left);
    s2.push(root.right);
    while (!s1.isEmpty() && !s2.isEmpty()) {
        TreeNode n1 = s1.pop();
        TreeNode n2 = s2.pop();
        if (n1 == null && n2 == null) {
            continue;
        }

        if (n1 == null || n2 == null) {
            return false;
        }
        if (n1.val != n2.val) {
            return false;
        }
        s1.push(n1.left);
        s2.push(n2.right);
        s1.push(n1.right);
        s2.push(n2.left);
    }
    return true;
}
```

**参考资料**
- [Iterative Traversal](https://leetcode.com/problems/symmetric-tree/discuss/33374/Recusive-solution-for-symmetric-tree%3A-is-it-an-optimal-solution-to-use-inorderTraversal)
- [Recursive and non-recursive solutions in Java](https://leetcode.com/problems/symmetric-tree/discuss/33054/Recursive-and-non-recursive-solutions-in-Java)