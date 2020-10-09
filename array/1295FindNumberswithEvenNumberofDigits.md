1295. Find Numbers with Even Number of Digits

### 题目地址
- [Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)

### 1,初步思路

```
/**
 * 1, 统计数字位数
 *     1.1 数字/10 > 0
 * 2, 判断位数是奇数还是偶数
 */
public int findNumbers(int[] nums) {
    int digitNum = 0;
    int result = 0;
    int current = 0;
    int[] resultArray = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        current = nums[i];
        do {
            current = current / 10;
            if (current >= 0) {
                digitNum++;
            }
        } while (current > 0);
        resultArray[i] = digitNum;
        digitNum = 0;
    }
    for (int n : resultArray) {
        if (n % 2 == 0) {
            result++;
        }
    }
    return result;
}
```

### 2,正确解法

```
public int findNumbers(int[] nums) {
    // 起始数字，从1开始
    int digitNum = 1;
    int result = 0;
    int current = 0;
    for (int i = 0; i < nums.length; i++) {
        current = nums[i];
        while((current = current / 10) != 0) {
            digitNum++;
        }
        if (digitNum % 2 == 0) {
            result++;
        }
        // 此处，恢复为1
        digitNum = 1;
    }
    return result;
}
```