17. Letter Combinations of a Phone Number

### 题目地址
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

### 1,初步思路

```
/***** backtrack *****/
public List<String> letterCombinations(String digits) {
    String[] letters = {"", "", "abc", "def", "ghi",
                        "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    List<String> result = new ArrayList<>();
    if (digits.length == 0) {
        return result;
    }

    char[] strArr = digits.toCharArray();

    backtrack(result, strArr, 0, "", letters);

    return result;
}

private void backtrack(List<String> result, char[] strArr, int start, String comString, String[] letters) {

    // base case
    if (comString.length() == strArr.length) {
        result.add(comString);
        return;
    }

    // 将字符转换为数字
    // int index = Character.getNumericValue(strArr[start]);
    int index = strArr[start] - '0';

    for (int i = 0; i < letters[index].length(); i++) {
        comString = comString + letters[index].charAt(i);
        backtrack(result, strArr, start + 1, comString, letters);
        comString = comString.substring(0, comString.length() - 1);
    }
}
```

### 2,正确解法

```
/***** Iterative *****/
public List<String> letterCombinations(String digits) {
    LinkedList<String> result = new LinkedList<>();
    if (digits.isEmpty()) {
        return result;
    }

    String[] mapping = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

    result.add("");
    for (int i = 0; i < digits.length(); i++) {
        int index = digits.charAt(i) - '0';
        while (result.peek().length() == i) {
            String t = result.remove();
            for (char s : mapping[index].toCharArray()) {
                result.add(t + s);
            }
        }
    }
    return result;
}
```

**参考资料**
- [Iterative solution](https://leetcode.com/problems/letter-combinations-of-a-phone-number/discuss/8064/My-java-solution-with-FIFO-queue)