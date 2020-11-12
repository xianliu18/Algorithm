33. Search in Rotated Sorted Array

### 题目地址
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

### 1,初步思路

```
public int search(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    int pivot = 0;
    for (int i = 0, j = i + 1; j < nums.length; i++,j++) {
        if (nums[j] < nums[i]) {
            pivot = i;
            brreak;
        }
    }

    int start = 0;
    int end = nums.length - 1;
    /*****/
    if (nums[0] == target) {
        return 0;
    }
    /*****/
    if (nums[pivot] == target) {
        return pivot;
    }
    
    if (nums[0] > target) {
        start = pivot + 1;
    } else if (nums[0] < target && nums[pivot] > target) {
        end = pivot - 1;

    /***** } else if (nums[pivot] < target) { *****/
    } else if (nums[pivot] < target && pivot != 0) {}
        return -1;
    }

    while (start <= end) {
        int mid = start + (end - start)/2;
        if (nums[mid] < target) {
            start = mid + 1;
        } else if (nums[mid] > target) {
            end = mid - 1;
        } else {
            return mid;
        }
    }
    return -1;
}

// 测试用例:
Input: {1, 3}  target: 3

Input: {6,7,1,2,3,4,5}   target: 6
```

### 2,正确解法

```
public int search(int[] nums, int target) {
    // find the index of the smallest value using binary search
    int minIdx = findMinIdx(nums);
    if (nums[minIdx] == target) {
        return minIdx;
    }

    int hi = nums.length - 1;
    int start = (target <= nums[hi]) ? minIdx : 0;
    int end = (target > nums[hi]) ? minIdx - 1 : hi;

    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }
    return -1;
}

private int findMinIdx(int[] nums) {
    int start = 0;
    int end = nums.length - 1;
    while (start < end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] > nums[end]) {
            start = mid + 1;
        } else {
            end = mid;
        }
    }
    return start;
}
```

**参考资料**
- [O(logN) Binary search solution](https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14425/Concise-O(log-N)-Binary-search-solution)