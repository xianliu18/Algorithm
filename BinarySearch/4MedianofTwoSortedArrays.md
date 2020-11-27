4. Median of Two Sorted Arrays

### 题目地址
- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Solution1 *****/
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int m = nums1.length;
    int n = nums2.length;
    if (m > n) {
        int[] temp = nums1;
        int val = m;
        nums1 = nums2;
        nums2 = temp;
        m = n;
        n = val;
    }

    if (n == 0) {
        return -1;
    }

    int imin = 0;
    int imax = m;
    int mid = (m + n + 1) / 2;
    while (imin <= imax) {
        int i = (imin + imax)/2;
        int j = mid - i;
        if (i < m && nums2[j - 1] > nums1[i]) {
            // i is too small, must increase it
            imax = i + 1;
        } else if (i > 0 && nums1[i - 1] > nums2[j]) {
            // i is too big, must decrease it
            imax = i - 1;
        } else {
            // i is perfect
            double maxLeft = 0;
            double minRigth = 0;
            if (i == 0) {
                maxLeft = nums2[j - 1];
            } else if (j == 0) {
                maxLeft = Math.max(nums1[i - 1], nums2[j - 1]);
            }
            if ((m+n) % 2 == 1) {
                return maxLeft;
            }

            if (i == m) {
                minRight = nums2[j];
            } else if (j == n) {
                minRight = nums1[i];
            } else {
                minRight = Math.min(nums1[i], nums2[j]);
            }

            return (maxLeft + minRight)/2;
        }
    }
    return -1;
}
```

**参考资料**
- [Share my O(log(min(m,n))) solution with explanation](https://leetcode.com/problems/median-of-two-sorted-arrays/discuss/2481/Share-my-O(log(min(mn)))-solution-with-explanation)