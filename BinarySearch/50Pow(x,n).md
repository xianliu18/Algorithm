50. Pow(x, n)

### 题目地址
- [Pow(x, n)](https://leetcode.com/problems/powx-n/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Solution 1 *****/
public double myPow(double x, int n) {
    double result = 1;
    long absN = Math.abs((long)n);
    while (absN > 0) {
        if ((absN & 1) == 1) {
            result *= x;
        }
        absN >>= 1;
        x *= x;
    }
    return n < 0 ? 1/result : result;
}

```

**参考资料**
- [Iterative Log(N) solution with clear Explanation](https://leetcode.com/problems/powx-n/discuss/19563/Iterative-Log(N)-solution-with-Clear-Explanation)