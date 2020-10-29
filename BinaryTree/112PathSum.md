112.Path Sum

### 题目地址
- [Path Sum](https://leetcode.com/problems/path-sum/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursion *****/
public boolean hasPathSum(TreeNode root, int sum) {
    if (root == null) {
        return false;
    }

    if (root.left == null && root.right == null) {
        return sum == root.val;
    }

    return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
}


/***** Iteration *****/
public boolean hasPathSum(TreeNode root, int sum) {

    Stack<TreeNode> stack = new Stack<>();
    Stack<Integer> sums = new Stack<>();

    stack.push(root);
    sums.push(sum);
    while (!stack.isEmpty() && root != null) {
        int value = sums.pop();
        TreeNode top = stack.pop();

        if (top.left == null && top.right == null && top.val == value) {
            return true;
        }
        if (top.right != null) {
            stack.push(top.right);
            sums.push(value - top.val);
        }
        if (top.left != null) {
            stack.push(top.left);
            sums.push(value - top.val);
        }
    }
    return false;
}
```

**参考资料**
- [Recursion solution](https://leetcode.com/problems/path-sum/discuss/36378/AcceptedMy-recursive-solution-in-Java)