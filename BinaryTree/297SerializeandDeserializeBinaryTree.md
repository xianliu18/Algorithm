297. Serialize and Deserialize Binary Tree

### 题目地址
- [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** PreOrder Traversal *****/
private static final String spliter = ",";
private static final String NN = "#";

public String serialize(TreeNode root) {
    StringBuilder sb = new StringBuilder();
    buildString(root, sb);
    return sb.toString();
}

private void buildString(TreeNode node, StringBuilder sb) {
    if (node == null) {
        sb.append(NN).append(spliter);
    } else {
        sb.append(node.val).append(spliter);
        buildString(node.left, sb);
        buildString(node.right, sb);
    }
}

// Decodes your encoded data to tree.
public TreeNode deserialize(String data) {
    Deque<String> nodes = new LinkedList<>();
    nodes.addAll(Arrays.asList(data.split(spliter)));
    return buildTree(nodes);
}

private TreeNode buildTree(Deque<String> nodes) {
    String val = nodes.remove();
    if (val.equals(NN)) {
        return null;
    } else {
        TreeNode node = new TreeNode(Integer.valueOf(val));
        node.left = buildTree(nodes);
        node.right = buildTree(nodes);
        return node;
    }
}


/***** Level Order *****/
public String serialize(TreeNode root) {
    if (root == null) {
        return "";
    }

    Queue<TreeNode> queue = new LinkedList<>();
    StringBuilder res = new StringBuilder();
    queue.offer(root);
    while (!queue.isEmpty()) {
        TreeNode curr = queue.poll();
        if (curr == null) {
            res.append("#,");
            continue;
        }
        res.append(curr.val + ",");
        queue.add(curr.left);
        queue.add(curr.right);
    }
    return res.toString();
}

public TreeNode deserialize(String data) {
    if (data == "") {
        return null;
    }
    Queue<TreeNode> queue = new LinkedList<>();
    String[] values = data.split(",");
    TreeNode root = new TreeNode(Integer.parseInt(values[0]));
    queue.add(root);
    for (int i = 1; i < values.length; i++) {
        TreeNode parent = queue.poll();
        if (!values[i].equals("#")) {
            TreeNode left = new TreeNode(Integer.parseInt(values[i]));
            parent.left = left;
            queue.add(left);
        }
        if (!values[++i].equals("#")) {
            TreeNode right = new TreeNode(Integer.parseInt(values[i]));
            parent.right = right;
            queue.add(right);
        }
    }
    return root;
}
```

**参考资料**
- [Easy to understand Java Solution](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/discuss/74253/Easy-to-understand-Java-Solution)
- [Short and straight forward BFS Java code with a queue](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/discuss/74264/Short-and-straight-forward-BFS-Java-code-with-a-queue)