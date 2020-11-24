367. Valid Perfect Square

### 题目地址
- [Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

### 1,初步思路

```
// Wrong Answer
public boolean isPerfectSquare(int num) {
    if (num < 0) {
        return false;
    }
    if (num == 1) {
        return true;
    }

    int result = 0;
    while (num > 1 && result == 0) {
        result = num % 2;
        num /= 2;
    }
    return result == 0 ? true : false;
}
```

### 2,正确解法

```
/***** Solution 1 *****/
public boolean isPerfectSquare(int num) {
    int i = 1;
    while (num > 0) {
        num -= i;
        i += 2;
    }
    return num == 0;
}


/***** Solution 2: Binary Search *****/
public boolean isPerfectSqare2(int num) {
    int low = 1;
    int high = num;
    while (low <= high) {
        long mid = (low + high) >> 1;
        if (mid * mid == num) {
            return true;
        } else if(mid * mid < num) {
            low = (int)mid + 1;
        } else {
            high = (int)mid - 1;
        }
    }
    return false;
}


/***** Newton Method *****/
public boolean isPerfectSqr(int num) {
    long x = num;
    while (x * x > num) {
        x = (x + num / x) >> 1;
    }
    return x * x == num;
}
```

**参考资料**
- [A square number is 1+3+5+7...](https://leetcode.com/problems/valid-perfect-square/discuss/83874/A-square-number-is-1%2B3%2B5%2B7%2B...-JAVA-code)