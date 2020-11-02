119. Pascal's Triangle II

### 题目地址
- [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)

### 1,初步思路

```
/***** Recursive: Time Limit Exceeded *****/
public List<Integer> getRow(int rowIndex) {
    List<Integer> result = new ArrayList<>(rowIndex + 1);
    result.add(1);
    if (rowIndex == 0) {
        return result;
    }
    for (int i = 1; i < rowIndex; i++) {
        result.add(indexNum(rowIndex + 1, i + 1));
    }
    result.add(1);
    return result;
}

private Integer indexNum(int row, int col) {
    if (col == 1 || row == col) {
        return 1;
    }
    return indexNum(row - 1, col - 1) + indexNum(row - 1, col);
}

```

### 2,正确解法

```
/***** *****/
public List<Integer> getRow(int rowIndex) {
    List<Integer> result = new ArrayList<>();
    result.add(1);
    for (int i = 1; i <= rowIndex; i++) {
        for (int j = i - 1; j >= 1; j--) {
            int temp = result.get(j - 1) + result.get(j);
            result.set(j, temp);
        }
        result.add(1);
    }
    return result;
}


/***** Recursive *****/
class Solution {
    int[][] cache;

    public List<Integer> getRow(int rowIndex) {
        
        // 2D cache, representing pascals triangle, will store values that have already been calculated
        cache = new int[rowIndex + 1][];

        // Fill each row in cache with a new array
        for (int i = 0; i < cache.length; i++) {
            cache[i] = new int[i+1];
        }

        // Array list to store final result
        List<Integer> result = new ArrayList<>();

        for (int i = 0; i <= rowIndex; i++) {
            result.add(getTriangleValue(rowIndex, i));
        }
        return result;
    }


    // Recursive function that takes in the row of the triangle and the index in that row
    public int getTriangleValue(int row, int col) {
        if (col == 0 || row == col) {
            return 1;
        }

        // If the value isnt in cache, calculate and store it
        if (cache[row][col] == 0) {
            cache[row][col] = getTriangleValue(row - 1, col - 1) + getTriangleValue(row - 1, col);
        }
        return cache[row][col];
    }
}
```

**参考资料**
- [Here is my brief O(k) solution](https://leetcode.com/problems/pascals-triangle-ii/discuss/38420/Here-is-my-brief-O(k)-solution)
- [Recursive solution java](https://leetcode.com/problems/pascals-triangle-ii/discuss/38516/Recursive-solution-Java.-3ms)