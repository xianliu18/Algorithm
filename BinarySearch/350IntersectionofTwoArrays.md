350. Intersection of Two Arrays II

### 题目地址
- [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

### 1,初步思路

```
public int[] intersect(int[] nums1, int[] nums2) {
    int[] big;
    int[] small;
    if (nums1.length > nums2.length) {
        big = nums1;
        small = nums2;
    } else {
        big = nums2;
        small = nums1;
    }

    Set<Integer> set = new HashSet<>();
    for (int m : big) {
        set.add(m);
    }

    ArrayList<Integer> result = new ArrayList<>();
    for (int n : small) {
        if (set.contains(n)) {
            result.add(n);
        }
    }

    int[] arr = new int[result.size()];
    for (int i = 0; i < result.size(); i++) {
        arr[i] = result.get(i);
    }

    return arr;
}

// Test Case:
// [3, 1, 2]   和   [1, 1]
```

### 2,正确解法

```
public int[] intersection(int[] nums1, int[] nums2) {
    HashMap<Integer, Integer> map = new HashMap<>();
    ArrayList<Integer> result = new ArrayList<>();
    for (int i = 0; i < nums1.length; i++) {
        if (map.containsKey(nums1[i])) {
            map.put(nums1[i], map.get(nums1[i]) + 1);
        } else {
            map.put(nums1[i], 1);
        }
    }

    for (int i = 0; i < nums2.length; i++) {
        if (map.containsKey(nums2[i] && map.get(nums2[i]) > 0)) {
            result.add(nums2[i]);
            map.put(nums2[i], map.get(nums2[i]) - 1);
        }
    }

    int[] arr = new int[result.size()];
    for (int j = 0; j < result.size(); j++) {
        arr[j] = result.get(j)
    }

    return arr;
}
```

**参考资料**
- [AC solution using Java HashMap](https://leetcode.com/problems/intersection-of-two-arrays-ii/discuss/82241/AC-solution-using-Java-HashMap)