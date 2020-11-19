153. Find Minimum in Rotated Sorted Array

### 题目地址
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

### 1,初步思路

```

```

### 2,正确解法

```
         5   5                           5
        / \ / \                         / \
       4   4   4                       4  -∞
      /         \                     /
     3           3           3       3
    /             \         / \     /
   2               2       2   2   2
  /                 \     /     \ /
-∞                   1   1       1
                      \ /
                       0  

public int findMin(int[] nums) {

    if (nums == null || nums.length == 0) {
        return -1;
    }

    int left = 0;
    int right = nums.length - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < nums[right]) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return nums[left];
}
```

**参考资料**
- [Java solution and explanation using invariants](https://leetcode.com/problems/find-peak-element/discuss/50239/Java-solution-and-explanation-using-invariants)
- [A concise solution with proof in the comment](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/discuss/48484/A-concise-solution-with-proof-in-the-comment)