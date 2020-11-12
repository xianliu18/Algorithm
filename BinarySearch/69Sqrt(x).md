69. Sqrt(x)

### 题目地址
- [Sqrt(x)](https://leetcode.com/problems/sqrtx/)

### 1,初步思路

```
public int mySqrt(int x) {
    // x 为0,1 特殊处理
    if (x == 0 || x == 1) {
        return x;
    }

    int temp = (int)Math.floor(x / 2);
    while (temp >= 1) {
        if (temp * temp > x) {
            temp = (int)Math.floor(temp/2) + 1;
            continue;
        } else {
            break;
        }
    }
}

// 测试用例:
Input:  1024

```

### 2,正确解法

```
/***** Binary Search *****/
public int mySqrt(int x) {
    int left = 1;
    int right = x;
    while (left <= right) {
        int mid = left + (right - left)/2;
        if (mid == x/mid) {
            return mid;
        } else if (mid < x/mid) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return right;
}


/***** Integer Newton *****/
public int mySqrt(int x) {
    long r = x;
    while (r * r > x) {
        r = (r + x / r) / 2;
    }
    return (int)r;
}
```

**参考资料**
- [A Binary Search Solution](https://leetcode.com/problems/sqrtx/discuss/25047/A-Binary-Search-Solution)
- [Integer Newton](https://leetcode.com/problems/sqrtx/discuss/25057/3-4-short-lines-Integer-Newton-Every-Language)