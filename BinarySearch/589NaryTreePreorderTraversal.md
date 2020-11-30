589. N-ary Tree Preorder Traversal

### 题目地址
- [N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal/)

### 1,初步思路

```

```

### 2,正确解法

```
public List<Integer> preorder(Node root) {
    List<Integer> result = new ArrayList<>();
    if (root == null){
        return result;
    }

    Stack<Node> stack = new Stack<>();
    stack.add(root);

    while (!stack.isEmpty()) {
        root = stack.pop();
        result.add(root.val);
        for (int i = root.children.size() - 1; i>= 0; i--) {
            stack.add(root.children.get(i));
        }
    }
    return result;
}
```

**参考资料**
- [Java Iterative and Recursive Solutions](https://leetcode.com/problems/n-ary-tree-preorder-traversal/discuss/147955/Java-Iterative-and-Recursive-Solutions)