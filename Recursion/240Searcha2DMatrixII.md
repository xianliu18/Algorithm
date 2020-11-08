240. Search a 2D Matrix II

### 题目地址
- [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Iterative *****/
// Time Complexity: O(m + n)

public boolean searchMatrix(int[][]matrix, int target) {
    if (matrix == null || matrix.length < 1 || matrix[0].length < 1) {
        return false;
    }
    int col = matrix[0].length-1;
    int row = 0;
    while (col >= 0 && row <= matrix.length - 1) {
        if (target == matrix[row][col]) {
            return true;
        } else if (target < matrix[row][col]) {
            col--;
        } else if (target > matrix[row][col]) {
            row++;
        }
    }
    return false;
}


/***** Divide and Conquer *****/
public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length;
    if (m < 1) {
        return false;
    }
    int n = matrix[0].length;

    return searchMatrix(matrix, new int[]{0, 0}, new int[]{m - 1, n - 1}, target);
}

private boolean searchMatrix(int[][] matrix, int[] upperLeft, int[] lowerRight, int target) {
    if (upperLeft[0] > lowerRight[0] || upperLeft[1] > lowerRight[1]
        || lowerRight[0] >= matrix.length || lowerRight[1] >= matrix[0].length) {
            return false;
    }

    if (lowerRight[0] - upperLeft[0] == 0 && lowerRight[1] - upperLeft[1] == 0) {
        return matrix[upperLeft[0]][upperLeft[1]] == target;
    }

    int rowMid = (upperLeft[0] + lowerRight[0]) >> 1;
    int colMid = (upperLeft[1] + lowerRight[1]) >> 1;
    int diff = matrix[rowMid][colMid] - target;
    if (diff > 0) {
        return searchMatrix(matrix, upperLeft, new int[]{rowMid, colMid}, target)
                || searchMatrix(matrix, new int[]{upperLeft[0], colMid + 1}, new int[]{rowMid, lowerRight[1]}, target)
                || searchMatrix(matrix, new int[]{rowMid + 1, upperLeft[1]}, new int[]{lowerRight[0], colMid}, target);
    } else if (diff < 0) {
        return searchMatrix(matrix, new int[]{upperLeft[0], colMid + 1}, new int[]{rowMid, lowerRight[1]}, target)
                || searchMatrix(matrix, new int[]{rowMid + 1, upperLeft[1]}, new int[]{lowerRight[0], colMid}, target)
                || searchMatrix(matrix, new int[]{rowMid + 1, colMid + 1}, lowerRight, target);
    } else {
        return true;
    }
}
```

**参考资料**
- [My concise O(m + n) java solution](https://leetcode.com/problems/search-a-2d-matrix-ii/discuss/66140/My-concise-O(m%2Bn)-Java-solution)
- [an easy-to-understand divide and conquer method](https://leetcode.com/problems/search-a-2d-matrix-ii/discuss/66147/*Java*-an-easy-to-understand-divide-and-conquer-method)