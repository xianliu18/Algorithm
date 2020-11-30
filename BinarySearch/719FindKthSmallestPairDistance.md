719. Find K-th Smallest Pair Distance

### 题目地址
- [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/)

### 1,初步思路

```

```

### 2,正确解法

```
// Returns number of pairs with absolute difference less than or equal to mid
private int countPairs(int[] nums, int mid) {
    int n = nums.length;
    int res = 0;
    for (int i = 0; i < n; i++) {
        int j = i;
        while (j < n && nums[j] - nums[i] <= mid) {
            j++;
        }
        res += j - i - 1;
    }
    return res;
}

public int smallestDistancePair(int nums[], int k) {
    int n = nums.length;
    Arrays.sort(nums);

    // Minimum absolute difference
    int low = nums[1] - nums[0];
    for (int i = 1; i < n - 1; i++) {
        low = Math.min(low, nums[i+1] - nums[i]);
    }

    // Maximum absolute difference
    int high = nums[n - 1] - nums[0];

    // Do binary search for k-th absolute difference
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (countPairs(nums, mid) < k) {
            low = mid + 1;
        } else {
            high = mid;
        }
    }

    return low;
}
```

**参考资料**
- [Java solution, Binary Search](https://leetcode.com/problems/find-k-th-smallest-pair-distance/discuss/109075/Java-solution-Binary-Search)