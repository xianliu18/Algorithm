1.Smallest power of 2 greater than or equal to n

### 题目地址
- [Smallest power of 2 greater than or equal to n](https://practice.geeksforgeeks.org/problems/smallest-power-of-2-greater-than-or-equal-to-n2630/1#topicTags)

### 1,初步思路

```
// 无思路
```

### 2,正确解法

```
public int nextPowerOf2(int n) {
    int count = 0;

    if (n > 0 && (n & (n - 1)) == 0) {
        return n;
    }

    while (n != 0) {
        n >>= 1;
        count += 1;
    }

    return 1 << count;
}
```

**参考资料**
- [Smallest power of 2](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/)