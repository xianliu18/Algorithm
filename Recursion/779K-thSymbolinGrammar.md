779. K-th Symbol in Grammar

### 题目地址
- [K-th Symbol in Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** 根据规律解题 *****/
public int kthGrammar(int N, int K) {
    return Integer.bitCount(K - 1) & 1;
}

/***** Recursive ****/
public int kthGrammar(int N, int K) {
    if (N == 1) {
        return 0;
    }
    if (K % 2 == 0) {
        if (kthGrammar(N - 1, K/2) == 0) {
            return 1;
        } else {
            return 0;
        }
    } else {
        if (kthGrammar(N - 1, (K+1)/2) == 0) {
            return 0;
        } else {
            return 1;
        }
    }
}
```

**参考资料**
- [Easy 1-line Solution with detailed explanation](https://leetcode.com/problems/k-th-symbol-in-grammar/discuss/113736/PythonJavaC%2B%2B-Easy-1-line-Solution-with-detailed-explanation)
- [Java easy to understand recursion](https://leetcode.com/problems/k-th-symbol-in-grammar/discuss/365364/Java-easy-to-understand-recursion)