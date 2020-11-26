167. Two Sum II - Input array is sorted

### 题目地址
- [Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

### 1,初步思路

```

```

### 2,正确解法

```
public int[] twoSum(int[] nums, int target) {
    int[] result = new int[2];
    if (nums == null || nums.length < 2) {
        return result;
    }
    int left = 0;
    int right = nums.length - 1;
    while (left < right) {
        int v = nums[left] + nums[right];
        if (v == target) {
            result[0] = left + 1;
            result[1] = right + 1;
            break;
        } else if (v > target) {
            right--;
        } else {
            left++;
        }
    }
    return result;
}
```

**参考资料**
- [Share my java AC solution](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/discuss/51239/Share-my-java-AC-solution.)