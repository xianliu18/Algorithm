70. Climbing Stairs

### 题目地址
- [Climging Stairs](https://leetcode.com/problems/climbing-stairs/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Based  Fibonacci *****/
public int climbStairs(int n) {
    int a = 1;
    int b = 1;
    while (n-- > 0) {
        a = (b += a) - a;
    }
    return a;
}


/***** Dynamic Programming *****/
public int climbStairs(int n) {
    if (n == 0 || n == 1 || n == 2) {
        return n;
    }
    int[] mem = new int[n];
    mem[0] = 1;
    mem[1] = 2;
    for (int i = 2; i < n; i++) {
        mem[i] = mem[i - 1] + mem[i - 2];
    }
    return mem[n - 1];
}
```

**参考资料**
- [3-4 short lines in every language](https://leetcode.com/problems/climbing-stairs/discuss/25296/3-4-short-lines-in-every-language)
- [Easy solutions for suggestions](https://leetcode.com/problems/climbing-stairs/discuss/25345/Easy-solutions-for-suggestions.)