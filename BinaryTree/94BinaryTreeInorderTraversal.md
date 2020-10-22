94.Binary Tree Inorder Traversal

### 题目地址
- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```
// 解法一: recursive
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> res = new LinkedList<>();

    helper(root, res);

    return res;
}

private void helper(TreeNode root, List<Integer> res) {
    if (root != null) {
        if (root.left != null) {
            helper(root.left, res);
        }
        res.add(root.val);
        if (root.right != null) {
            helper(root.right, res);
        }
    }
}

// 解法二: iterative
public List<Integer> inorderTraversal2(TreeNode root) {
    List<Integer> res = new LinkedList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode cur = root;
    while (cur != null || !stack.isEmpty()) {
        while (cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        res.add(cur.val);
        cur = cur.right;
    }
    return res;
}


```

**参考资料**
- [Java solution, both recursion and iteration](https://leetcode.com/problems/binary-tree-inorder-traversal/discuss/31372/Java-solution-both-recursion-and-iteration)
- [Iterative Inorder Traversal of Binary Tree](https://www.youtube.com/watch?v=nzmtCFNae9k)