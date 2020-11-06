98. Validate Binary Search Tree

### 题目地址
- [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

### 1,初步思路

```
/***** Recursive *****/
public boolean isValidBST(TreeNode root) {
    if (root == null) {
        return true;
    }
    if (root.left == null) {
        return true;
    }
    // 此处,存在问题. [1, 1]
    if (root.right == null) {
        return true;
    }

    // 此处,存在问题. 需要root.left, root.right 不能为null的前提, 才能进行比较
    if (root.left.val >= root.val || root.right.val <= root.val) {
        return false;
    }

    boolean left = isValidBST(root.left);
    boolean right = isValidBST(root.right);

    return left && right;
}
```

### 2,正确解法

```
/***** Recursive *****/
public boolean isValidBST(TreeNode root) {
    return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

private boolean isValidBST(TreeNode root, long minVal, long maxVal) {
    if (root == null) {
        return true;
    }
    // 注意: 等号
    if (maxVal <= root.val || root.val <= minVal) {
        return false;
    }
    return isValidBST(root.left, minVal, root.val) && isValidBST(root.right, root.val, maxVal);
}


/***** Inorder Traversal *****/

```

**参考资料**
- [My simple Java solution](https://leetcode.com/problems/validate-binary-search-tree/discuss/32109/My-simple-Java-solution-in-3-lines)