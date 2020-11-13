278. First Bad Version

### 题目地址
- [First Bad Version](https://leetcode.com/problems/first-bad-version/)

### 1,初步思路

```
public int firstBadVersion(int n) {
    int start = 1;
    int end = n;
    while (start < end) {
        int mid = start + (end - start) / 2;
        if (!isBadVersion(mid)) {
            start = mid + 1;
        } else {
            end = mid;
        }
    }
    return start;
}
```

### 2,正确解法

```

```

**参考资料**
- [A Binary Search Template II](https://leetcode.com/explore/learn/card/binary-search/126/template-ii/937/)