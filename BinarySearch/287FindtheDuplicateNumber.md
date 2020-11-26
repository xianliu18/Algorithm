287. Find the Duplicate Number

### 题目地址
- [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

### 1,初步思路

```
public int findDuplicate(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i])) {
            return nums[i];
        } else {
            map.put(nums[i], 1);
        }
    }

    return -1;
}


```

### 2,正确解法

```
public int findDuplicate(int[] nums) {

    if (nums.length > 1) {
        int slow = nums[0];
        int fast = nums[nums[0]];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[nums[fast]];
        }

        fast = 0;
        while (fast != slow) {
            fast = nums[fast];
            slow = nums[slow];
        }
        return slow;
    }
}
```

**参考资料**
- [My easy understood solution with O(n) time and O(1) space](https://leetcode.com/problems/find-the-duplicate-number/discuss/72846/My-easy-understood-solution-with-O(n)-time-and-O(1)-space-without-modifying-the-array.-With-clear-explanation.)