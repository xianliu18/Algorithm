236. Lowest Common Ancestor of a Binary Tree

### 题目地址
- [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursive *****/
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    // base case
    if (root == null || root == p || root == q) {
        return root;
    }

    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);

    // result
    if (left == null) {
        return right;
    } else if (right == null) {
        return left;
    } else {
        // both left and right are not null, we found our result
        return root;
    }
}


/
```

**参考资料**
- [Java Solution](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/discuss/65225/4-lines-C%2B%2BJavaPythonRuby)