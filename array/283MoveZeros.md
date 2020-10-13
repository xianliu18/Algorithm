283. Move Zeroes

### 题目地址
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/)

### 1,初步思路

```
/**
* Move Zeros
*
* 1, Two-pointers tech
* 		- readPointer
* 		- writePointer
* 2, 以{0,1,0,3,12}为例
* 		第一步:{1,0,0,3,12}
* 	    第二步:{1,3,0,0,12}
* 	    第三步:{1,3,12,0,0}
*/

public void moveZeros(int[] nums) {
    int writePointer = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == 0 && nums[writePointer] != 0) {
            writePointer = i;
        }
        if (nums[i] != 0 && nums[writePointer] == 0) {
            nums[writePointer] = nums[i];
            nums[i] = 0;
            writePointer++;
        }
    }
}
```

### 2,正确解法

```
// 只要不等于0, 就可以交换
public void moveZeros(int[] nums) {
    int j = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) {
            int temp = nums[j];
            nums[j] = nums[i];
            nums[i] = temp;
            j++;
        }
    }
}
```