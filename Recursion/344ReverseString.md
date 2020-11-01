344. Reverse String

### 题目地址
- [Reverse String](https://leetcode.com/problems/reverse-string/)

### 1,初步思路

```
/***** Two Pointers *****/
public void reverString(char[] s) {
    int i = 0;
    int j = s.length - 1;
    while (i < j) {
        char temp = s[i];
        s[i] = s[j];
        s[j] = temp;
        i++;
        j--;
    }
}
```

### 2,正确解法

```
/***** Recursive *****/
public String reverseString(String s) {
    // base case
    if (s.length() == 0 || s.length() == 1) {
        return s;
    }
    return s.substring(length - 1) + reverseString(s.substring(0, length - 1));
}

```

**参考资料**
- [Simple and Clean with Explanations](https://leetcode.com/problems/reverse-string/discuss/80937/JAVA-Simple-and-Clean-with-Explanations-6-Solutions)
- [ Is recursion not an efficient solution?](https://leetcode.com/problems/reverse-string/discuss/81121/Java-Is-recursion-not-an-efficient-solution)