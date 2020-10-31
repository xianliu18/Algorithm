19.Remove Nth Node From End of List

### 题目地址
- [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Iterative *****/
public TreeNode buildTree(int[] preorder, int[] inorder) {
    // boundary case
    if (preorder.length == 0) {
        return null;
    }

    Stack<TreeNode> stack = new Stack<>();
    TreeNode root = new TreeNode(preorder[0]);
    stack.push(root);

    int i = 1;
    int j = 0;

    while (i <= preorder.length - 1) {
        TreeNode curr = stack.peek();
        if (curr.val != inorder[j]) {
            TreeNode left = new TreeNode(preorder[i]);
            curr.left = left;
            stack.push(left);
            i++;
        } else {
            while (!stack.isEmpty() && stack.peek().val == inorder[j]) {
                curr = stack.pop();
                j++;
            }

            TreeNode right = new TreeNode(preorder[i]);
            curr.right = right;
            stack.push(right);
            i++;
        }
    }
    return root;
}


/***** Recursive *****/

public TreeNode buildTree(int[] preorder, int[] inorder) {
    return helper(0, 0, inorder.length - 1, preorder, inorder);
}

public TreeNode helper(int preStart, int inStart, int inEnd, int[] preorder, int[] inorder) {

    // 1, Base Case
    if (preStart > preorder.length || inStart > inEnd) {
        return null;
    }

    // 2, Build the current node.
    TreeNode curr = new TreeNode(preorder[preStart]);

    // 3, Find the pivot in the inorder.
    int inPivot = 0;
    for (int i = 0; i < inorder.length; i++) {
        if (inorder[i] == preorder[preStart]) {
            inPivot = i;
            break;
        }
    }

    // 4, return root
    cur.left = helper(preStart + 1, inStart, inPivot - 1, preorder, inorder);
    cur.right = helper(perStart + inPivot - inStart + 1, inPivot + 1, inEnd, preorder, inorder);
    return cur;
}
```

**参考资料**
- [Java with Picure](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/discuss/683377/Java-with-Picture)