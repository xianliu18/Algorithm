22. Generate Parentheses

### 题目地址
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Backtracking *****/
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<>();
    backtrack(result, "", 0, 0, n);
    return result;
}

private void backtrack(List<String> list, String str, int open, int close, int max) {
    // base case
    if (str.length() == max * 2) {
        list.add(str);
        return;
    }

    if (open < max) {
        backtrack(list, str + "(", open + 1, close, max);
    }
    if (close < open) {
        backtrack(list, str + ")", open, close + 1, max);
    }
} 

// 优化版本: use StringBuilder, instead of string concatenation
private void backtrack(List<String> list, StringBuilder sb, int open, int close, int n) {
    // base case
    if (open == n && close == n) {
        list.add(sb.toString);
        return;
    }

    if (open < n) {
        sb.append("(");
        backtrack(list, sb, open + 1, close, n);
        
    }
}

```

**参考资料**
- [Backtracking solution](https://leetcode.com/problems/generate-parentheses/discuss/10100/Easy-to-understand-Java-backtracking-solution)