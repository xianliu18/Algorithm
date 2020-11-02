700. Search in a Binary Search Tree

### 题目地址
- [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)

### 1,初步思路

```
/***** Iterative *****/
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null) {
        return null;
    }
    TreeNode curr = root;
    while (curr != null) {
        if (curr.val > val) {
            curr = curr.left;
        } else if (curr.val < val) {
            curr = curr.right;
        } else {
            break;
        }
    }
    return curr;
}


/***** Recursive *****/
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) {

        // 此处多余: return root == null ? null : root;
        
        return root;
    }
    TreeNode result = null;
    if (root.val > val) {
        result = searchBST(root.left, val);
    } else if (root.val < val) {
        result = searchBST(root.right, val);
    }
    return result;
}
```

### 2,正确解法

```

```

**参考资料**
- []()