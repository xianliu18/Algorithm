374. Guess Number Higher or Lower

### 题目地址
- [Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/)

### 1,初步思路

```
/***** Binary Search *****/
public int guessNumber(int n) {
    int left = 1;
    int right = n;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (guess(mid) == 0) {
            return mid;
        } else if (guess(mid) > 0) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

```

### 2,正确解法

```

```

**参考资料**
- [Key Point About the problem](https://leetcode.com/problems/guess-number-higher-or-lower/discuss/84665/The-key-point-is-to-read-the-problem-carefully.)