102.Binary Tree Level Order Traversal

### 题目地址
- [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```
public class Solution {

    /***** Queue *****/
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> result = new LinkedList<>();

        if (root == null) {
            return result;
        }

        queue.offer(root);
        while (!queue.isEmpty()) {
            int levelNum = queue.size();
            List<Integer> subList = new LinkedList<>();
            for (int i = 0; i < levelNum; i++) {
                if (queue.peek().left != null) {
                    queue.offer(queue.peek().left);
                }
                if (queue.peek().right != null) {
                    queue.offer(queue.peek().right);
                }
                subList.add(queue.poll().val);
            }
            result.add(subList); 
        }
        return result;
    }


    /***** Queue and Counter *****/
    public List<List<Integer>> levelOrder2(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> result = new LinkedList<>();

        if (root == null) {
            return result;
        }

        int levelNum = 1;
        int currentCount = 0;
        queue.offer(root);
        while (!queue.isEmpty()) {
            List<Integer> subList = new LinkedList<>();
            while (levelNum > 0) {
                root = queue.poll();
                subList.add(root.val);
                levelNum--;
                if (root.left != null) {
                    currentCount++;
                    queue.add(root.left);
                }
                if (root.right != null) {
                    currentCount++;
                    queue.add(root.right);
                }
            }
            result.add(subList);
            levelNum = currentCount;
            currentCount = 0;
        }
        return result;
    }


    /***** DFS *****/
    public List<List<Integer>> levelOrder3(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        levelHelper(res, root, 0);
        return res;
    }

    private void levelHelper(List<List<Integer>> res, TreeNode root, int height) {
        if (root == null) {
            return;
        }

        if (height >= res.size) {
            res.add(new LinkedList<Integer>());
        }
        res.get(height).add(root.val);
        levelHelper(res, root.left, height + 1);
        levelHelper(res, root.right, height + 1);
    }
}

public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode () {}
    TreeNode(int val) {
        this.val = val;
    }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

**参考资料**
- []()