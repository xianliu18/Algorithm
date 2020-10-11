26. Remove Duplicates from Sorted Array

### 题目地址
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

### 1,初步思路

```

/**
 * 如何找到duplicate的值,保留一个?
 *     记录第一次出现的值,然后移除后面出现的相同值, 如何做到不再遍历已经移除的值?
 */


```

### 2,正确解法

```
// 注意题目中的Sorted Array
// 由于是有序数组,所以不会出现{1,2,3,1,4}的情况
public int removeDup(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    int i = 0;
    for (int j = 0; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            nums[++i] = nums[j];
        }
    }
    // 返回的为下一个数值添加位置,即数组长度
    return (i+1);
}
```