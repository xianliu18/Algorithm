27. Remove Element

### 题目地址
- [Remove Element](https://leetcode.com/problems/remove-element/)

### 1,初步思路

```
/**
 * 遍历数组
 *    1.1 如果数组值与指定值相等,则最终数组长度减1
 *    1.2 最繁琐的方式:找到一个值,然后将后面的全部向前移动一位
 *    1.3 另外,由于不用关注最终数组的排序时,可以双向遍历:
 *         从前往后遍历,碰到等于val的值,使用末尾值替换
 */

 // 解法一:繁琐方式
 public int removeElement(int[] nums, int val) {
     int len = nums.length;
     for (int i = 0; i < len; i++) {
         if (nums[i] == val) {
             for (int j = i; j < len - 1; j++) {
                 nums[j] = nums[j + 1];
             }
             len--;
             // 仍然需要重新开始判断nums[i]是否等于val
             i--;
         }
     }
     return len;
 }

 // 解法二:将nums[i]=val的值,用末尾的值替换
 // 特殊的case:
 // {1}, {2,2,3}
 public int removeEle2(int[] nums, int val) {
     int len = nums.length;
     for (int i = 0, j = nums.length - 1; i < nums.length; i++) {
         if (nums[i] == val) {
             while (j >= 0 && j >= i && nums[j] == val) {
                 j--;
                 len--;
             }
             if (j > 0 && i <= j) {
                 nums[i] = nums[j];
                 j--;
                 len--;
             }
         }
     }
     return len;
 }
```

### 2,正确解法

```
public int removeEle3(int[] nums, int val) {
    int i = 0;
    for (int j = 0; j < nums.length; j++) {
        if (nums[j] != val) {
            nums[i++] = nums[j];
        }
    }
    return i;
}
```