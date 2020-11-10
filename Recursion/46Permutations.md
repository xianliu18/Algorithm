46. Permutations

### 题目地址
- [Permutations](https://leetcode.com/problems/permutations/)

### 1,初步思路

```
/***** Backtrack *****/
public List<List<Integer>> permute(int[] nums) {

    List<List<Integer>> result = new ArrayList<>();
    helper(result, new ArrayList<Integer>(), 0, nums.length);
    return result;
}

private void helper(List<List<Integer>> result, List<Integer> subList, int start, int length) {

    if (subList.size() == length) {
        result.add(subList);
    }

    subList.add(start);

    helper(result, subList, start + 1, length);

    // 对于如何定义回溯函数,不是很清楚.
    // 什么时候调用回溯函数,以及调用完成后,怎么删除
}

```

### 2,正确解法

```
/***** Backtracking *****/
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();

    backtrack(result, new ArrayList<Integer>(), nums);

    return result;
}

private void backtrack(List<List<Integer>> result, List<Integer> subList, int[] nums) {

    if (subList.size() == nums.length) {
        result.add(new ArrayList<>(subList));
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        if (subList.contains(nums[i])) {
            continue;
        }
        subList.add(nums[i]);
        backtrack(result, subList, nums);
        subList.remove(subList.size() - 1);
    }
}

/***** solution 2 *****/
public List<List<Integer>> permute2(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new LinkedList<>(), result);
    return result;
}

private void backtrack2(int[] nums, int start, List<Integer> cur, List<List<Integer>> res) {
    if (cur.size() == nums.length) {
        res.add(new ArrayList<>(cur));
        return;
    }

    // 此处为 cur.size()
    for (int i = 0; i <=  cur.size(); i++) {
        cur.add(i, nums[start]);
        backtrack2(nums, start + 1, cur, res);
        cur.remove(i);
    }
}
```

**参考资料**
- [Backtracking in Java](https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning))
- [Two recursive solutions](https://leetcode.com/problems/permutations/discuss/18436/Java-Clean-Code-Two-recursive-solutions)