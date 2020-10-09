485. Max Consecutive Ones

### 题目地址
- [Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/)

### 1,初步思路

```
class Solution {
    /*
    * 1,记录最长的连续1为多少
    * 2，记录当前连续1为多少
    * 3，求出两者最大值
    */
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
		 int current = 0;
		 for(int i = 0; i < nums.length; i++) {
			 if (nums[i] == 1) {
				 current++;
			 }
             // 缺乏考虑的点：i == nums.length - 1
             // 在遍历数组完成后，需要比较此时current和max的大小
			 if (nums[i] == 0 || i == nums.length - 1) {
				 max = Integer.max(current, max);
				 current = 0;
			 }
		 }
		 return max;
    }
}
```

### 2,正确解法

```
public int findMaxConsecutiveOnes(int[] nums) {
    int maxHere = 0;
    int max = 0;
    for (int n : nums) {
        max = Math.max(max, maxHere = n == 0 : 0 ? maxHere + 1);
    }
    return max;
}
```