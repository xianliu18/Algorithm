905. Sort Array By Parity

### 题目地址
- [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/)

### 1,初步思路

```

/**
 * 和283类似
 */
 public int[] sortArrayByParity(int[] nums) {
     int j = 0;
     for (int i = 0; i < nums.length; i++) {
         if (nums[i] % 2 == 0) {
            int temp = nums[j];
            nums[j] = nums[i];
            nums[i] = temp;
            j++;
         }
     }
     return nums;
 }
```

### 2,正确解法

```


```