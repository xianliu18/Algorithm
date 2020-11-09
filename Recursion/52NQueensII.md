52. N-Queens II

### 题目地址
- [N-Queens II](https://leetcode.com/problems/n-queens-ii/)

### 1,初步思路

```

```

### 2,正确解法

```
// 第一种解法
int result = 0;

public int totalNQueens(int n) {
    boolean[] vertical = new boolean[n];
    boolean[] leftfall = new boolean[2 * n - 1];
    boolean[] rightfall = new boolean[2 * n - 1];

    helper(n, vertical, leftfall, rightfall, 0);

    return result;
}

private void helper(int n, boolean[] v, boolean[] l, boolean[] r, int row) {
    if (row == n) {
        result++;

        // 输出测试
        // System.out.println(new StringBuffer("result:" + result));
        return;
    }

    for (int col = 0; col < n; col++) {
        if (v[col] || l[row - col + n - 1] || r[row + col]) {
            continue;
        }

        v[col] = true;
        l[row - col + n - 1] = true;
        r[row + col] = true;

        System.out.println("row: " + row + ",v[" + col + "]"
                            + ",l[" + (row - col + n - 1) + "]"
                            + ",r[" + (row + col) + "]");
        helper(n, v, l, r, row + 1);

        v[col] = false;
        l[row - col + n - 1] = false;
        r[row + col] = false;
    }
}



```

**参考资料**
- [Java Solution](https://leetcode.com/problems/n-queens-ii/discuss/20058/Accepted-Java-Solution)
- [N Queen Problem Using Backtracking Algorithm](https://www.youtube.com/watch?v=xouin83ebxE)