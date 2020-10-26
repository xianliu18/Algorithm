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


/*********** Morris ***********/
public void morrisPreorder(TreeNode root) {
    TreeNode current = root;
    while (current != null) {
        if (current.left == null) {
            System.out.print(current.val + " ");
            current = current.right;
        } else {
            TreeNode predecessor = current.left;
            while (predecessor.right != current && predecessor.right != null) {
                predecessor = predecessor.right;
            }

            if (predecessor.right == null) {
                predecessor.right = current;
                System.out.println(current.val + " ");
                current = current.left;
            } else {
                predecessor.right = null;
                current = current.right;
            }
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


/*********** Morris ***********/
public void morrisInorder(TreeNode root) {
    TreeNode current = root;
    while (current != null) {
        // left is null then print the node and go to right
        if (current.left == null) {
            System.out.println(current.val + " ");
            current = current.right;
        } else {
            // find the predecessor.
            TreeNode predecessor = current.left;

            // To find predecessor keep going right till right node is not null or 
            // right node is not current.
            while (predecessor.right != current && predecessor.right != null) {
                predecessor = predecessor.right;
            }

            // if right node is null then go left after establishing link from predecessor to current
            if (predecessor.right == null) {
                predecessor.right = current;
                current = current.left;
            } else {// left is already visit. Go right after visiting current.
                predecessor.right = null;
                System.out.print(current.val + " ");
                current = current.right;
            }
        }
    }
}
```

#### 1.3 PostOrder(后序遍历)

```
/*********** Two Stacks ***********/
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


/*********** One Stack ***********/
public void postOrderIterOneStack(TreeNode root) {
    TreeNode current = root;
    Deque<TreeNode> stack = new LinkedList<>();
    while (current != null || !stack.isEmpty()) {
        if (current != null) {
            stack.addFirst(current);
            current = current.left;
        } else {
            TreeNode temp = stack.peek().right;
            if (temp == null) {
                temp = stack.poll();
                System.out.print(temp.val + " ");
                while (!stack.isEmpty() && temp == stack.peek().right) {
                    temp = stack.poll();
                    System.out.print(temp.val + " ");
                }
            } else {
                current = temp;
            }
        }
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

#### 1.4.1 Level Order Traversal Level By Level

```
/*********** Two Queues ***********/
public void levelByLevelTraversal(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<TreeNode> q1 = new LinkedList<>();
    Quue<TreeNode> q2 = new LinkedList<>();
    q1.add(root);
    while (!q1.isEmpty() || !q2.isEmpty()) {
        while (!q1.isEmpty()) {
            root = q1.pop();
            System.out.println(root.val + " ");
            if (root.left != null) {
                q2.add(root.left);
            }
            if (root.right != null) {
                q2.add(root.right);
            }
        }
        // 打印换行符
        System.out.println();
        while (!q2.isEmpty()) {
            root = q2.pop();
            System.out.println(root.val + " ");
            if (root.left != null) {
                q1.add(root.left);
            }
            if (root.right != null) {
                q1.add(root.right);
            }
        }
        System.out.println();
    }
}


/*********** One Queue & Delimiter ***********/
public void levelByLevelOneQueueUsingDelimiter(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<TreeNode> q = new LinkedList<>();
    q.add(root);
    q.add(null);
    while (!q.isEmpty()) {
        root = q.pop();
        if (root != null) {
            System.out.println(root.val + " ");
            if (root.left != null) {
                q.add(root.left);
            }
            if (root.right != null) {
                q.add(root.right);
            }
        } else {
            if (!q.isEmpty()) {
                Sytem.out.println();
                q.add(null);
            }
        }
    }
}

/*********** One Queue & Counter ***********/
public void levelByLevelOneQueueUsingCount(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<TreeNode> q = new LinkedList<>();
    int levelCount = 1;
    int currentCount = 0;
    q.add(root);
    while (!q.isEmpty()) {
        while (levelCount > 0) {
            root = q.pop();
            System.out.println(root.val + " ");
            if (root.left != null) {
                currentCount++;
                q.add(root.left);
            }
            if (root.right != null) {
                currentCount++;
                q.add(root.right);
            }
            levelCount--;
        }
        System.out.println();
        levelCount = currentCount;
        currentCount = 0;
    }
}
```

#### 1.4.2 Level Order Traversal In Reverse

```
/*********** One Queue & One Stack ***********/
public void levelOrderTraversalInReverse(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<TreeNode> q = new LinkedList<>();
    Stack<TreeNode> s = new Stack<>();
    q.add(root);
    while (!q.isEmpty()) {
        root = q.pop();
        if (root.right != null) {
            q.add(root.right);
        }
        if (root.left != null) {
            q.add(root.left);
        }
        s.push(root);
    }
    while (!s.isEmpty()) {
        System.out.println(s.pop().val);
    }
}
```

#### 1.4.2 Level Order Traversal In Spiral Order

```
/*********** Two Stacks ***********/
public void levelTraversalSpiralOrder(TreeNode root) {
    if (root == null) {
        return;
    }
    Stack<TreeNode> s1 = new Stack<>();
    Stack<TreeNode> s2 = new Stack<>();
    s1.push(root);
    while (!s1.isEmpty() || !s2.isEmpty()) {
        while (!s1.isEmpty()) {
            root = s1.pop();
            System.out.println(root.val + " ");
            if (root.left != null) {
                s2.push(root.left);
            }
            if (root.right != null) {
                s2.push(root.right);
            }
        }
        while (!s2.isEmpty()) {
            root = s2.pop();
            System.out.println(root.val + " ");
            if (root.right != null) {
                s1.push(root.right);
            }
            if (root.left != null) {
                s1.push(root.left);
            }
        }
    }
}


/*********** A Deque and Delimiter***********/
public void spiralWithDequeDelimiter(TreeNode root) {
    if (root == null) {
        return;
    }
    Deque<TreeNode> deque = new LinkedList<>();
    deque.offer(null);
    deque.offFirst(root);
    // if only delimiter(in this case null) is left in queue then break;
    while (q.size() > 1) {
        root = q.peekFirst();
        while (root != null) {
            root = q.pollFirst();
            System.out.print(root.val + " ");
            if (root.left != null) {
                q.offerLast(root.left);
            }
            if (root.right != null) {
                q.offerLast(root.right);
            }
            root = q.peekFirst();
        }
        root = q.peekLast();
        while (root != null) {
            System.out.print(root.val + " ");
            root = q.pollLast();
            if (root.right != null) {
                q.offerFirt(root.right);
            }
            if (root.left != null) {
                q.offerFirst(root.left);
            }
            root = q.peekLast();
        }
    }
}


/*********** One Queue and Counter ***********/
public void spiralWithOneDeque(TreeNode root) {
    if (root == null) {
        return;
    }
    Deque<TreeNode> deque = new LinkedList<>();
    deque.offerFirst(root);
    int count = 1;
    boolean flip = true;
    while (!deque.isEmpty()) {
        int currentCount = 0;
        while (count > 0) {
            if (flip) {
                root = deque.pollFirst();
                System.out.print(root.val + " ");
                if (root.left != null) {
                    deque.offerLast(root.left);
                    currentCount++;
                }
                if (root.right != null) {
                    deque.offerLast(root.right);
                    currentCount++;
                }
            } else {
                root = deque.pollLast();
                System.out.print(root.val + " ");
                if (root.right != null) {
                    deque.offerFirst(root.right);
                    currentCount++;
                }
                if (root.left != null) {
                    deque.offerFirst(root.left);
                    currentCount++;
                }
            }
            count--;
        }
        flip = !flip;
        count = currentCount;
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

#### 3.6 Lowest Common Ancestor in Binary Search Tree

```
public TreeNode lowestCommonAncestor(TreeNode root, int p, int q) {
    if (root.val > Math.max(p, q)) {
        lowestCommonAncestor(root.left, p, q);
    } else (root.val < Math.min(p, q)) {
        lowestCommonAncestor(root.right, p, q);
    } else {
        return root;
    }
}
```

#### 3.6.1 Lowest Common Ancestor in Binary Tree

```
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode t1, TreeNode t2) {
    if (root == null) {
        return null;
    }
    if (root == n1 || root == n2) {
        return root;
    }

    TreeNode left = lowestCommonAncestor(root.left, t1, t2);
    TreeNode right = lowestCommonAncestor(root.right, t1, t2);

    if (left != null && right != null) {
        return root;
    }
    return left != null ? left : right;
}
```

#### 3.7 Largest BST in Binary Tree

```
/**
 * Traverse tree in post order fashion. Left and right nodes return 4 piece of information
 * to root which isBST, size of max BST, min and max in those subtree.
 * If both left and right subtree are BST and this node data is greater than max of left and 
 * less than min of right then it returns to above level left size + right size + 1 and new
 * min will be min of left side and new max will be max of right side.
 * 
 * References:
 * http://www.geeksforgeeks.org/find-the-largest-subtree-in-a-tree-that-is-also-a-bst/
 * https://leetcode.com/problems/largest-bst-subtree/
 */
public class LargestBSTInBinaryTree {

    public int largestBST(TreeNode root) {
        MinMax m = largest(root);
        return m.size;
    }

    private MinMax largest(TreeNode root) {
        if (root == null) {
            return new MinMax();
        }

        // PostOrder traversal of tree. First visit left and right then
        // use information of left and right to calculate largest BST
        MinMax leftMinMax = largest(root.left);
        MinMax rightMinMax = largest(root.right);

        MinMax m = new MinMax();
        if (leftMinMax.isBST == false || rightMinMax.isBST == false ||
            (leftMinMax.max > root.val || rightMinMax.min <= root.val)) {
                m.isBST = false;
                m.size = Math.max(leftMinMax.size, rightMinMax.size);
                return m;
        }

        // If we reach this point means subtree with this node as root is BST.
        // Set isBST as true.
        // Then set size as size of left + size of right + 1.
        // Set min and max to be returned to parent.
        m.isBST = true;
        m.size = leftMinMax.size + rightMinMax.size + 1;
        m.min = root.left != null ? leftMinMax.min : root.val;
        m.max = root.right != null ? rightMinMax.max : root.val;

        return m;
    }

}

class MinMax {
    int min;
    int max;
    boolean isBST;
    int size;

    MinMax() {
        min = Integer.MAX_VALUE;
        max = Integer.MIN_VALUE;
        isBST = true;
        size = 0;
    }
}
```