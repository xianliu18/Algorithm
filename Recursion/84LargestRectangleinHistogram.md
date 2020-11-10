84. Largest Rectangle in Histogram

### 题目地址
- [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Iterative *****/
public int largestRectangleArea(int[] height) {

    if (height == null || height.length == 0) {
        return 0;
    }

    int[] lessFromLeft = new int[height.length];
    int[] lessFromRight = new int[height.length];
    lessFromRight[height.length - 1] = height.length;
    lessFromLeft[0] = -1;

    for (int i = 1; i < height.length; i++) {
        int p = i - 1;

        while (p >= 0 && height[p] >= height[i]) {
            p = lessFromLeft[p];
        }

        lessFromLeft[i] = p;
    }

    for (int i = height.length - 2; i >= 0; i--) {
        int p = i + 1;

        while (p < height.length && height[p] >= height[i]) {
            p = lessFromRight[p];
        }
        lessFromRight[i] = p;
    }

    int maxArea = 0;
    for (int i = 0; i < height.length; i++) {
        maxArea = Math.max(maxArea, height[i] * (lessFromRight[i] - lessFromLeft[i] - 1));
    }

    return maxArea;
}
```

**参考资料**
- [Java Solution](https://leetcode.com/problems/largest-rectangle-in-histogram/discuss/28902/5ms-O(n)-Java-solution-explained-(beats-96))