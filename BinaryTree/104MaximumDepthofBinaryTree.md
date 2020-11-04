104.Maximum Depth of Binary Tree

### 题目地址
- [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursion *****/
public int maxDepth(TreeNode root) {

    if (root == null) {
        return 0;
    }

    int leftMax = root.left == null ? 0 : maxDepth(root.left);
    int rightMax = root.right == null ? 0 : maxDepth(root.right);
    return 1 + Math.max(leftMax, rightMax);
}


/***** Iteration: Level traversal *****/
public int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    }

    int depth = 0;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        depth++;
        while (size > 0) {
            root = queue.poll();
            size--;
            if (root.left != null) {
                queue.offer(root.left);
            }
            if (root.right != null) {
                queue.offer(root.right);
            }
        }
    }
    return depth;
}

```

**参考资料**
- [Simple solution using Java](https://leetcode.com/problems/maximum-depth-of-binary-tree/discuss/34216/Simple-solution-using-Java)