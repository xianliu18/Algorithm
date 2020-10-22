145.Binary Tree Posrorder Traversal

### 题目地址
- [Binary Tree Posrorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```

// 解法一: Iterative Postorder with two stack

public List<Integer> postOrderTraversal(TreeNode root) {
    List<Integer> res = new LinkedList<>();

    // 判空
    if (root == null) {
        return res;
    }

    Stack<TreeNode> s1 = new Stack<>();
    Stack<TreeNode> s2 = new Stack<>();
    s1.push(root);
    while (!s2.isEmpty()) {
        root = s1.pop();
        s2.push(root);
        if (root.left != null) {
            s1.push(root.left);
        }
        if (root.right != null) {
            s1.push(root.right);
        }
    }

    while (!s2.isEmpty()) {
        root = s2.pop();
        res.add(root.val);
    }
}

// 解法二: Iterative Postorder with One stack
public List<Integer> postOrderTraversal2(TreeNode root) {
    List<Integer> res = new LinkedList<>();
    
    TreeNode curr = root;
    Stack<TreeNode> stack = new Stack();

    while (curr != null || !stack.isEmpty()) {
        if (curr != null) {
            stack.push(curr);
            curr = curr.left;
        } else {
            TreeNode temp = stack.peek().right;
            if (temp == null) {
                temp = stack.pop();
                res.add(temp.val);

                while (!stack.isEmpty() && (temp == stack.peek().right)) {
                    temp = stack.pop();
                    res.add(temp.val);
                }
            } else {
                curr = temp;
            }
        }
    }
}

```

**参考资料**
- [Iterative Postorder Traversal of Binary Tree](https://www.youtube.com/watch?v=qT65HltK2uE&list=PLrmLmBdmIlpv_jNDXtJGYTPNQ2L1gdHxu&index=10)
- [Iterative Postorder using one stack](https://www.youtube.com/watch?v=xLQKdq0Ffjg&list=PLrmLmBdmIlpv_jNDXtJGYTPNQ2L1gdHxu&index=18)