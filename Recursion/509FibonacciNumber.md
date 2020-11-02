509. Fibonacci Number

### 题目地址
- [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Recursion with no cache *****/
// Time Complexity: O(2^N)
// Space Complexity: O(N)

public int fib(int n) {

    if (n <= 1) {
        return n;
    }

    return fib(n - 1) + fib(n - 2);
}


/***** Recursion with cache *****/
class Solution {
    int[] fibCache = new int[31];

    public int fib(int N) {
        if (N <= 1) {
            return N;
        } else if (fibCache[N] != 0) {
            return fibCache[N];
        } else {
            return fibCache[N] = fib[N - 1] + fib[N - 2];
        }
    }
}


/***** Dynamic Programming *****/
// Dynamic Programming: bottom-up
// Recursion: top-down

public int fib(int N) {
    if (N <= 1) {
        return N;
    }
    int[] f = new int[N + 1];
    f[0] = 0;
    f[1] = 1;
    for (int i = 2; i <= N; i++) {
        f[i] = f[i - 1] + f[i - 2];
    }
    return f[N];
}
```

**参考资料**
- [O(2^N) -> O(N) -> O(logN)](https://leetcode.com/problems/fibonacci-number/discuss/223199/Java-O(2N)-greater-O(N)-greater-O(logN))
- [Java Solutions](https://leetcode.com/problems/fibonacci-number/discuss/215992/Java-Solutions)