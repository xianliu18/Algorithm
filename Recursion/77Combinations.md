77. Combinations

### 题目地址
- [Combinations](https://leetcode.com/problems/combinations/)

### 1,初步思路

```

```

### 2,正确解法

```
// Backtracking
public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> result = new ArrayList<>();

    combine(result, new ArrayList<>(), 1, n, k);

    return result;
}

private static void combine(List<List<Integer>> result, List<Integer> comb, int start, int n, int k) {
    
    if (k == 0) {
        result.add(new ArrayList<>(comb));
        return;
    }

    for (int i = start; i <= n - k + 1; i++) {
        comb.add(i);
        combine(result, comb, i + 1, n, k - 1);
        comb.remove(comb.size() - 1);
    }
}

```

**参考资料**
- [Backtracking Solution Java](https://leetcode.com/problems/combinations/discuss/27002/Backtracking-Solution-Java)