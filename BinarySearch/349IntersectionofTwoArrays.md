349. Intersection of Two Arrays

### 题目地址
- [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)

### 1,初步思路

```

```

### 2,正确解法

```
public int[] intersection(int[] nums1, int[] nums2) {
    Set<Integer> numbers = new HashSet<>();
    for (int n : nums1) {
        numbers.add(n);
    }

    ArrayList<Integer> result = new ArrayList<>();
    for (int m : nums2) {
        if (numbers.contains(m)) {
            result.add(m);
            numbers.remove(m);
        }
    }

    // convert arraylist to array
    int[] arr = new int[result.size()];
    for (int i = 0; i < result.size(); i++) {
        arr[i] = result.get(i);
    }

    return arr;
}
```

**参考资料**
- [5ms Java Using 1 hashset and time complexity of O(m+n)](https://leetcode.com/problems/intersection-of-two-arrays/discuss/81974/5ms-Java-Using-1-hashset-and-time-complexity-of-O(m%2Bn))