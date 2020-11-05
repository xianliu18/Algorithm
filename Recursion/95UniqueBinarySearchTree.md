95. Unique Binary Search Trees II

### 题目地址
- [Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursive *****/
public List<TreeNode> generateTrees(int n) {
    if (n == 0) {
        return new ArrayList<TreeNode>();
    }
    return genTrees(1, n);
}

private List<TreeNode> genTrees(int start, int end) {
    List<TreeNode> list = new ArrayList<>();

    if (start > end) {
        list.add(null);
        return list;
    }

    if (start == end) {
        list.add(new TreeNode(start));
        return list;
    }

    List<TreeNode> leftList;
    List<TreeNode> rightList;
    for (int i = start; i<=end; i++) {
        leftList = genTrees(start, i - 1);
        rightList = genTrees(i+1, end);

        for (TreeNode lnode : leftList) {
            for (TreeNode rnode : rightList) {
                TreeNode root = new TreeNode(i);
                root.left = lnode;
                root.right = rnode;
                list.add(root);
            }
        }
    }
    return list;
}

```

**参考资料**
- [A Simple recursive solution](https://leetcode.com/problems/unique-binary-search-trees-ii/discuss/31494/A-simple-recursive-solution)