658. Find K Closest Elements

### 题目地址
- [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/)

### 1,初步思路

```

```

### 2,正确解法

```
/***** Solution 1: Binary Search *****/
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int left = 0;
    int right = arr.length - k;
    while (left < right) {
        int mid = (left + right ) / 2;
        if (x - arr[mid] > arr[mid + k] - x) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    return Arrays.stream(arr, left, left + k).boxed().collect(Collectors.toList());
}


/***** Solution 2 *****/
public List<Integer> findClosestEle(int[] arr, int k, int x) {
    int lo = 0;
    int hi = arr.length - 1;
    while (hi - lo >= k) {
        if (Math.abs(arr[lo] - x) > Math.abs(arr[hi] - x)) {
            lo++;
        } else {
            hi--;
        }
    }

    List<Integer> result = new ArrayList<>(k);
    for (int i = lo; i <= hi; i++) {
        result.add(arr[i]);
    }
    return result;
}
```

**参考资料**
- [Binary Search](https://leetcode.com/problems/find-k-closest-elements/discuss/106426/JavaC%2B%2BPython-Binary-Search-O(log(N-K)-%2B-K))
- [Very simple Java O(n) solution using two pointers](https://leetcode.com/problems/find-k-closest-elements/discuss/202785/Very-simple-Java-O(n)-solution-using-two-pointers)