1346. Check If N and Its Double Exist

### 题目地址
- [Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/)

### 1,初步思路

```
/**
 * 顺序遍历数组
 *    取出当前值,判断当前值*2,是否存在于数组中;
 *    当前值的索引,与当前值*2的索引不能相同;
 */
 public boolean checkIfExist(int[] nums) {
     for (int i = 0; i < nums.length; i++) {
         int val = nums[i];
         for (int j = 0; j < arr.length; j++) {
             if (arr[j] == val * 2 && i != j) {
                 return true;
             }
         }
     }
     return false;
 }
```

### 2,正确解法

```
// HashSet
public boolean checkIfExist(int[] nums) {
    Set<Integer> result = new HashSet<>();
    for (int val : nums) {
        if (result.contains(val * 2) || val % 2 == 0 && result.contains(val / 2)) {
            return true;
        }
        result.add(val);
    }
    return false;
}
```