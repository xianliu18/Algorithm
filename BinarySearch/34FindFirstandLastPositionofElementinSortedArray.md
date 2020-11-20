34. Find First and Last Position of Element in Sorted Array

### 题目地址
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Solution 1: Binary Search Template III *****/
public int[] searchRange(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return new int[]{-1, -1};
    }

    int start = firstGreaterOrEqual(nums, target);
    if (start == nums.length || nums[start] != target) {
        return new int[]{-1, -1};
    }

    int end = firstGreaterOrEqual(nums, target + 1);
    return new int[]{start, nums[end] == target ? end : end - 1};
}

public int firstGreaterOrEqual(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;

    while (left + 1 < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }

    if (nums[left] == target) {
        return left;
    }
    return right;
}
```

**参考资料**
- [A very simple Java solution, with only one binary search algorithm](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/discuss/14701/A-very-simple-Java-solution-with-only-one-binary-search-algorithm)