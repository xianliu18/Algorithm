### 1. AVL Trees
- Self-balancing Binary Search Tree(平衡二叉搜索树)
- AVL 树得名于它的发明者G. M. Adelson-Velsky和E. M. Landis

```
// Insertion
//      left    left:  need one right rotation
//      left    right: need one left and one right rotation
//      right   right: need one left rotation
//      right   left:  need one right and one left rotation

public class AVLTree {

    private TreeNode leftRotate(TreeNode root) {
        TreeNode newRoot = root.right;
        root.right = root.right.left;
        newRoot.left = root;
        root.height = setHeight(root);
        root.size = setSize(root);
        newRoot.height = setHeight(newRoot);
        newRoot.size = setSize(newRoot);
        return newRoot;
    }

    private TreeNode rightRotate(TreeNode root) {
        TreeNode newRoot = root.left;
        root.left = root.left.right;
        newRoot.right = root;
        root.height = setHeight(root);
        root.size = setSize(root);
        newRoot.height = setHeight(newRoot);
        newRoot.size = setSize(newRoot);
        return newRoot;
    }

    private int setHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + Math.max((root.left != null ? root.left.height : 0), (root.right != null ? root.right.height : 0));
    }

    private int height(TreeNode root) {
        if (root == null) {
            return 0;
        } else {
            return root.height;
        }
    }

    private int setSize(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + Math.max((root.left != null ? root.left.size : 0), (root.right != null ? root.right.size : 0));
    }

    private int balance(TreeNode rootleft, TreeNode rootRight) {
        return height(rootLeft) - height(rootRight);
    }

    public TreeNode insert(TreeNode root, int val) {
        if (root == null) {
            return TreeNode.newNode(val);
        }

        /***** 1, Perform standard BST insert *****/
        if (root.val <= val) {
            root.right = insert(root.right, val);
        } else {
            root.left = insert(root.left, val);
        }

        /***** 2, Starting from w, travel up and find the first unbalanced node. *****/
        int balance = balance(root.left, root.right);

        /***** 3, Re-balance the tree by performing appropriage rotations on the subtree rooted with z. *****/
        if (balance > 1) {
            // 不平衡点发生在左侧
            if (height(root.left.left) >= height(root.left.right)) {
                root = rightRotate(root);
            } else {
                root.left = leftRotate(root.left);
                root = rightRotate(root);
            }
        } else if (balance < -1) {
            // 不平衡点发生在右侧
            if (height(root.right.right) >= height(root.right.left)) {
                root = leftRotate(root);
            } else {
                root.right = rightRotate(root.right);
                root = leftRotate(root);
            }
        } else {
            root.height = setHeight(root);
            root.size = setSize(root);
        }
        return root;
    }
}
```

**参考资料:**
- [Wikipedia](https://en.wikipedia.org/wiki/AVL_tree)
- [GeeksforGeeks](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)