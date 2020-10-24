## 二叉树学习

![二叉树数据](https://github.com/Noodlescn/Algorithm/blob/master/BinaryTree/Introduction/Example1.png)

**参考资料:**
- [Binary Tree](https://www.youtube.com/watch?v=ZM-sV9zQPEs&list=PLrmLmBdmIlpv_jNDXtJGYTPNQ2L1gdHxu&index=1&pbjreload=101)
- [Algorithms(4th Edition)](https://www.amazon.com/Algorithms-4th-Robert-Sedgewick/dp/032157351X/ref=sr_1_3?dchild=1&keywords=algorithm&qid=1603512435&sr=8-3)


### 0. TreeNode 代码定义

```
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode() {}
    TreeNode(int vval) {
        this.val = val;
    }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

### 1, Binary Tree Traversal
- PreOrder(前序遍历):`V - L - R`
  - 按照上图数据,输出结果:`10  15  3  5  6  30  2  9  8`
- InOrder(中序遍历): `L - V - R`
  - 按照上图数据,输出结果:`5  3  15  6  10  30  9  2  8`
- PostOrder(后序遍历):`L - R - V`
  - 按照上图数据,输出结果:`5  3  6  15  9  8  2  30  10`

其中:<br/>
V: 表示当前节点,visited <br/>
L: 当前节点的左节点,left <br/>
R: 当前节点的右节点,right <br/>

#### 1.1 PreOrder(前序遍历)

```
// 算法实现
/*********** Recursive ***********/

public void preOrder(TreeNode head) {
    if (head != null) {
        System.out.println(head.val);
        preOrder(head.left);
        preOrder(head.right);
    }
}


/*********** Iterative ***********/

public void iterPreOrder(TreeNode head) {
    if (head == null) {
        return;
    }
    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.add(head);
    while (!stack.isEmpty()) {
        head = stack.pop();
        System.out.println(head.val);
        if (head.right != null) {
            stack.push(head.right);
        }
        if (head.left != null) {
            stack.push(head.left);
        }
    }
}
```

#### 1.2 InOrder(中序遍历)

```
// 算法实现
/*********** Recursive ***********/

public void inOrder(TreeNode head) {
    if (head != null) {
        inOrder(head.left);
        System.out.println(head.val);
        inOrder(head.right);
    }
}


/*********** Iterative ***********/
public void iterInOrder(TreeNode head) {
    if (head == null) {
        return;
    }
    Stack<TreeNode> stack = new Stack<TreeNode>();
    while (true) {
        if (head != null) {
            stack.push(head);
            head = head.left;
        } else {
            if (s.isEmpty()) {
                break;
            }
            head = head.pop();
            System.out.println(head.val);
            head = head.right;
        }
    }
}


```

#### 1.3 PostOrder(后序遍历)

```
// Iterative with two Stack
public void iteratePostOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    Stack<TreeNode> s1 = new Stack<TreeNode>();
    Stack<TreeNode> s2 = new Stack<TreeNode>();
    s1.push(root);
    while (!s1.isEmpty()) {
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
        System.out.println(root.val);
    }
}
```

#### 1.4 Level Order Traversal

```
public void levelOrderTraversal(TreeNode root) {
    if (root == null) {
        return;
    }
    // 队列
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.add(root);
    while (!queue.isEmpty()) {
        root = queue.peek();
        Sysem.out.println(root.val);
        if (root.left != null) {
            queue.add(root.left);
        }
        if (root.right != null) {
            queue.add(root.right);
        }
    }
}

```

### 2. Binary Search Tree(BST, 二分查找树)
- 定义(摘自<算法(第四版)>):

```
一棵二叉查找树(BST)是一棵二叉树,其中每个结点都含有一个Comparable的键(以及相关联的值)且每个结点的键都大于
其左子树中任意结点的键而小于右子树的任意结点的键。
```

#### 2.1 查询时间复杂度
- Balanced BST: O(logN)
- BST: O(N)

#### 2.2 代码实现

```
// 查找 
// 1, Recursive 
public TreeNode binarySearch(TreeNode head, int key) {
    if (head == null) {
        return null;
    }
    if (head.val == key) {
        return head;
    }
    if (head.val > key) {
        binarySearch(head.left, key);
    } else {
        binarySearch(head.right, key);
    }
}


// Insertion
// Iterative
public TreeNode insert(TreeNode root, int data) {
    TreeNode newNode = new TreeNode(data);

    if (root == null) {
        return newNode;
    }

    TreeNode parent = null;
    TreeNode curr = root;
    while(current != null) {
        parent = current;
        if (current.val < val) {
            current = current.right;
        } else {
            current = current.left;
        }
    }
    if (parent.val < val) {
        parent.right = newNode;
    }  else {
        parent.left = newNode;
    }
    return root;
}
```

### 3. Question
#### 3.1 Same Tree

```
public boolean sameTree(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) {
        return true;
    }
    if (root1 == null || root2 == null) {
        return false;
    }
    
    return root1.data == root2.data
    && sameTree(root1.left, root2.left)
    && sameTree(root1.right, root2.right);
}
```

#### 3.2 Size Of Binary Tree

```
public int size(TreeNode root) {
    if (root == null) {
        return 0;
    }
    int leftSize = size(root.left);
    int rightSize = size(root.right);
    return leftSize + rightSize + 1;
}
```


#### 3.3 Height Of Binary Tree

```
public int height(TreeNode root) {
    if (root == null) {
        return 0;
    }
    int leftHeight = height(root.left);
    int rightHeight = height(root.right);
    return 1 + max(leftHeight, rightHeight);
}
```

#### 3.4 Root To Leaf Sum Binary Tree

```
public boolean rootToLeafSum(TreeNode root, int sum, List<Integer> result) {
    if (root == null) {
        return false;
    }
    // 判断该结点,是否为叶子结点
    if (root.left == null && root.right == null) {
        if (root.val == sum) {
            result.add(root.val);
            return true;
        } else {
            return false;
        }
    }
    if (rootToLeafSum(root.left, sum - root.val, result)) {
        result.add(root.val);
        return true;
    }
    if (rootToLeafSum(root.right, sum - root.val, result)) {
        result.add(root.val);
        return true;
    }
    return false;
}

```

#### 3.5 Is Binary Tree a Binary Search Tree

```
public boolean isBST(TreeNode root, int min, int max) {
    if (root == null) {
        return true;
    }
    if (root.val <= min || root.val > max) {
        return false;
    }
    return isBST(root.left, min, max) && isBST(root.right, min, max);
}
```
