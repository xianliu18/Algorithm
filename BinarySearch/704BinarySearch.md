704. Binary Search

### 题目地址
- [Binary Search](https://leetcode.com/problems/binary-search/)

### 1,初步思路

```
/***** Binary Search *****/
public int search(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }

    int start = 0;
    int end = nums.length - 1;
    
    // Attention:"=", when nums contain only one element, like {5} 
    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] > target) {
            end = mid - 1;
        } else if (nums[mid] < target) {
            start = mid + 1;
        } else {
            return mid;
        }
    }

    return -1;
}

```

### 2,正确解法

```

```

**参考资料**
- []()