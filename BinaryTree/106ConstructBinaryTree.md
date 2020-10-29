106.Construct Binary Tree from Inorder and Postorder Traversal

### 题目地址
- [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Iterative Solution *****/
public TreeNode buildTree(int[] inorder, int[] postorder) {
    // boundary case
    if (inorder.length == 0) {
        return null;
    }

    Stack<TreeNode> stack = new Stack<>();
    TreeNode root = new TreeNode(postorder[postorder.length - 1]);
    stack.push(root);

    int i = postorder.length - 2;
    int j = inorder.length - 1;

    while (i >= 0) {
        TreeNode curr = stack.peek();
        if (curr.val != inorder[j]) {
            // as long as we have not reach the rightmost node we can safely follow path and attach right child
            TreeNode right = new TreeNode(postorder[i]);
            curr.right = right;
            i--;
        } else {
            // found the node from stack where we have not visited its left subtree
            while (!stack.isEmpty() && stack.peek().val == inorder[j]) {
                curr = stack.pop();
                j--;
            }

            TreeNode left = new TreeNode(postorder[i]);
            curr.left = left;
            stack.push(left);
            i--;
        }
    }
}
```

**参考资料**
- [Iterative solution](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/discuss/34807/Java-iterative-solution-with-explanation)