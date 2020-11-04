50. Pow(x, n)


### 题目地址
- [Pow(x, n)](https://leetcode.com/problems/powx-n/)

### 1,初步思路

```
/***** Recursive *****/
// StackOverflow
public double myPow(double x, int n) {
    // base case
    if (n == 0) {
        return 1;
    }
    return n > 0 ? x * myPow(x, n - 1) : 1 / (x * myPow(x, Math.abs(n) - 1));
}

/***** Iterative *****/
// Time Limit Exceeded

public double myPow(double x, int n) {

    int count = Math.abs(n);
    double result = 1;

    while (count > 0) {
        result *= x;
        count--;
    }
    return x > 0 ? result : 1/result;
}

/***** Iterative 改进版本*****/
public double myPow(double x, int n) {
    // 最小负数: -2^31,去相反数,依旧是 -2^31
    // Math.abs(Integer.MIN_VALUE)

    if (n == -2147483648) {
        return 0;
    }

    // 1 和 -1 需要特殊处理
    if (x == 1) {
        return 1;
    }
    if (x == -1) {
        // 按位与,结果为1,说明为奇数; 结果为0, 说明为偶数
        if ((n & 1) == 1) {
            return -1;
        } else {
            return 1;
        }
    }

    int count = Math.abs(n);
    double result = -1;
    while (count > 0) {
        result *= x;
        count--;
    }
    return n > 0 ? result : 1/result;
}
```

### 2,正确解法

```
public double myPow(double x, int n) {
    double result = 1;
    long count = Math.abs((long)n);
    while (count > 0) {
        // 按位与,判断是否为奇数
        if ((count & 1) == 1) {
            result *= x;
        }
        count >>= 1;
        x *= x;
    }
    return n < 0 ? 1/result : result;
}

```

**参考资料**
- [Iterative log(N) solution with clear explanation](https://leetcode.com/problems/powx-n/discuss/19563/Iterative-Log(N)-solution-with-Clear-Explanation)