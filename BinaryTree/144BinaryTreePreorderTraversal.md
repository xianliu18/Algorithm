144.Binary Tree Preorder Traversal

### 题目地址
- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```
// 解法一: recursive
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> pre = new LinkedList<Integer>();
    if (root == null) {
        return pre;
    }

    pre.add(root.val);
    pre.addAll(preorderTraversal(root.left));
    pre.addAll(preorderTraversal(root.right));
    return pre;
}

// 解法二: recursive
// recursive method with Helper method to have a LIST as parameter, so we can modify the parameter and
// don't have to instantiate a new List at each recursive call
public List<Integer> preorderTraversal2(TreeNode root) {
    List<Integer> pre = new LinkedList<>();
    preHelper(root, pre);
    return pre;
}
private void preHelper(TreeNode root, List<Integer> pre) {
    if (root == null) {
        return;
    }
    pre.add(root.val);
    preHelper(root.left, pre);
    preHelper(root.right, pre);
}

// 解法三:Iterative method with Stack
public List<Integer> preorderIter(TreeNode root) {
    List<Integer> pre = new LinkedList<Integer>();
    if (root == null) {
        return pre;
    }
    Stack<TreeNode> tovisit = new Stack<>();
    tovisit.push(root);
    while (!tovisit.empty()) {
        TreeNode visiting = tovisit.pop();
        pre.add(visiting.val);
        if (visiting.right != null) {
            tovisit.push(visiting.right);
        }
        if (visiting.left != null) {
            tovisit.push(visiting.left);
        }
    }
    return pre;
}

```

**参考资料**
- [3 Different Solutions](https://leetcode.com/problems/binary-tree-preorder-traversal/discuss/45468/3-Different-Solutions)
- [Iterative Preorder Traversal of Binary Tree](https://www.youtube.com/watch?v=elQcrJrfObg)