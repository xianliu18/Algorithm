977. Squares of a Sorted Array

### 题目地址
- [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

### 1,初步思路

```
/**
 * 1，取出每个值，求平方
 * 2，排序：
 *    2.1 冒泡排序
 */
 public int[] sortedSquares(int[] nums) {
     int[] result = new int[nums.length];
     // 求平方
     for (int i = 0; i < nums.length; i++) {
         result[i] = nums[i] * nums[i];
     }
     // 对result排序
     bubbleSort(result);
     return result;
 }

 public void bubbleSort(int[] arr) {
     int temp;
     for (int i = 0; i < arr.length - 1; i++) {
         for (int j = 0; j < arr.length - i - 1; j++) {
             if (arr[j + 1] < arr[j]) {
                 temp = arr[j];
                 arr[j] = arr[j + 1];
                 ar[j + 1] = temp;
             }
         }
     }
 }
```

### 2,正确解法

```
// 解法一
public int[] sortedSquares(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    int i = 0;
    int j = n - 1;
    for (int p = n - 1; p >= 0; p--) {
        if (Math.abs(nums[i]) > Math.abs(nums[j])) {
            result[p] = nums[i] * nums[i];
            i++;
        } else {
            result[p] = nums[j] * nums[j];
            j--;
        }
    }
    return result;
}

```