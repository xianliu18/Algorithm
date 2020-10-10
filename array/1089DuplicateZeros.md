1089. Duplicate Zeros

### 题目地址
- [Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/)

### 1,初步思路

```
/**
 * 1, 需要遍历数组
 *    1.1 如果值为0， 考虑duplicate；
 *    1.2 如何保持后面的值不变，即不被覆盖
 *    1.3 统计存在多少个0，然后从后面开始做移动
 */
 public void duplicateZeros(int[] nums) {
     int m = 0;
     for (int i = 0; i < nums.length - m; i++) {
         if (nums[i] == 0) {
             m++;
         }
     }
     for (int j = nums.length - m - 1, n = nums.length - 1; j >= 0; j--, n--) {
         nums[n] = nums[j];
         if (nums[j] == 0) {
             nums[--n] = 0;
         }
     }
 }
```

### 2,正确解法

```
public void duplicateZeros2(int[] nums) {
    int countZero = 0;
    for (int i = 0; i < nums.length; i++) {
        countZero++;
    }
    int len = nums.length + countZero;
    // m point to the original array, j point to the new location
    for (int m = nums.length - 1, j = len - 1; i < j; i--, j--) {
        if (nums[m] != 0) {
            if (j < nums.length) {
                nums[j] = nums[m];
            }
        } else {
            if (j < nums.length) {
                nums[j] = nums[m];
            }
            j--;
            if (j < nums.length) {
                nums[j] = nums[m];
            }
        }
    }
}
```