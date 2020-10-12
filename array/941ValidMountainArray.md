941. Valid Mountain Array

### 题目地址
- [Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array/)

### 1,初步思路

```
/**
 * 1, 边界条件:nums.length > 3;
 * 2, 从左到右,找到最大值(即前一个比后一个小),后面的只能前一个比后一个大;
 */

 // 存在问题: 不知道如何进行前后比较?

public boolean validMountain(int[] nums) {

		if (nums.length < 3) {
			return false;
		}

		int topIndex = 0;


		for (int i = 0; i < nums.length - 1; i++) {
			if (nums[i] > nums[i + 1]) {
				topIndex = i;
				break;
			}
		}
		if (topIndex == nums.length - 1) {
			return false;
		}
		for (int i = topIndex; i < nums.length - 1; i++) {
			if (nums[i] < nums[i + 1]) {
				return false;
			} else {
				return true;
			}
		}

		return true;
	}
```

### 2,正确解法

```

public boolean validMount2(int[] nums) {
    if (nums.length < 3) {
        return false;
    }
    int start = 0;
    int end = nums.length - 1;
    while (start < end) {
        if (nums[start + 1] > nums[start]) {
            start++;
        } else if (nums[end - 1] > nums[end]) {
            end--;
        } else {
            break;
        }
    }
    return start != 0 && end != nums.length - 1 && start == end;
}
```