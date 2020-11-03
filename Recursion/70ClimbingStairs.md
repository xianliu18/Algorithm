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

```

**参考资料**
- [3-4 short lines in every language](https://leetcode.com/problems/climbing-stairs/discuss/25296/3-4-short-lines-in-every-language)