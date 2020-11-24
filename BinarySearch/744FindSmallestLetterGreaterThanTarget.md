744. Find Smallest Letter Greater Than Target

### 题目地址
- [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Solution 1 *****/
public char nextGreatestLetter(char[] letters, char target) {
    int len = letters.length;
    if (target >= letters[len - 1]) {
        target = letters[0];
    } else {
        target++;
    }

    int lo = 0;
    int hi = len - 1;
    while (lo < hi) {
        int mid = lo + (hi - lo)/2;
        if (letters[mid] == target) {
            return letters[mid];
        } else if (letters[mid] < target) {
            lo = mid + 1;
        } else {
            hi = mid;
        }
    }
    return letters[hi];
}


/***** Solution2 *****/
public char nextGreatestLetters(char[] letters, char t) {
    int n = letters.length;

    int lo = 0;
    int hi = n;
    while (lo < hi) {
        int mid = lo + (hi - lo)/2;
        if (letters[mid] > target) {
            hi = mid;
        } else {
            lo = mid + 1;
        }
    }
    return letters[lo%n];
}

```

**参考资料**
- [Easy Binary Search in Java - O(log(n)) time](https://leetcode.com/problems/find-smallest-letter-greater-than-target/discuss/110005/Easy-Binary-Search-in-Java-O(log(n))-time)