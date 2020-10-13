448. Find All Numbers Disappeared in an Array

### 题目地址
- [ Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

### 1,初步思路

```

 

```

### 2,正确解法

```
/**
 * 链接:https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/discuss/92957/2ms-O(n)-In-Space-Java
 */
 
 1, Negate each number while traversiing
 2, Run again and find the index that is not negated

 public List<Integer> findDisapearNum(int[] nums) {
     List<Integer> result = new ArrayList<>();
     for (int i = 0; i < nums.length; i++) {
         int index = nums[i];
         if (nums[Math.abs(index) - 1] > 0) {
             nums[Math.abs(index) - 1] = -nums[Math.abs(index) - 1];
         }
     }
     for (int j = 0; j < nums.length; j++) {
         if (nums[j] > 0) {
             result.add(j + 1);
         }
     }
     return result;
 }
```