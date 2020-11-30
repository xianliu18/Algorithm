410. Split Array Largest Sum

### 题目地址
- [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

### 1,初步思路

```

```

### 2,正确解法

```

public int splitArray(int[] nums, int m) {
    int max = 0;
    long sum = 0;
    for (int num : nums) {
        max = Math.max(num, max);
        sum += num;
    }

    if (m == 1) {
        return (int)sum;
    }

    // binary search
    int low = max;
    long r = sum;
    while (low <= r) {
        long mid = (low + r) / 2;
        if (valid(mid, nums, m)) {
            r = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return (int)low;
}

public boolean valid(long target, int[] nums, int m) {
    int count = 1;
    long total = 0;
    for (int num : nums) {
        total += num;
        if (total > target) {
            total = num;
            count++;
            if (count > m) {
                return false;
            }
        }
    }
    return true;
}
```

**参考资料**
- [Clear Explanation: 8ms Binary Search Java](https://leetcode.com/problems/split-array-largest-sum/discuss/89817/Clear-Explanation%3A-8ms-Binary-Search-Java)