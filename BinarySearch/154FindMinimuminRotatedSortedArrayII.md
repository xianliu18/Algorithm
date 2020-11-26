154. Find Minimum in Rotated Sorted Array II

### 题目地址
- [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

### 1,初步思路

```
// Wrong Answer
public int findMin(int[] nums) {
    if (nums == null || nums.length == 0) {
        return -1;
    }

    int lo = 0;
    int hi = nums.length - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo)/2;
        if (nums[mid] <= nums[hi]) {
            hi = mid;
        } else {
            lo = mid + 1;
        }
    }
    return nums[lo];
}

// Test Case:  {3, 3, 1, 3}
```

### 2,正确解法

```
public int findMin(int[] nums) {
    if(nums == null || nums.length == 0) {
        return -1;
    }

    int lo = 0;
    int hi = nums.length - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;
        if (nums[mid] > nums[hi]) {
            lo = mid + 1;
        } else if (nums[mid] < nums[hi]) {
            hi = mid;
        } else {
            // when nums[mid] equals nums[hi]
            hi--;
        }
    }
    return nums[lo];
}

```

**参考资料**
- [My Pretty simple code to solve it](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/discuss/48808/My-pretty-simple-code-to-solve-it)