912. Sort an Array

### 题目地址
- [Sort an Array](https://leetcode.com/problems/sort-an-array/)

### 1,初步思路

```
/***** Divide and Conquer *****/
// Top-down merge sort algorithm
public int[] sortArray(int[] nums) {
    if (nums.length <= 1) {
        return nums;
    }
    int pivot = nums.length / 2;
    int[] leftList = sortArray(Arrays.copyOfRange(nums, 0, pivot));
    int[] rightList = sortArray(Arrays.copyOfRange(nums, pivot, nums.length));

    return merge(leftList, rightList);
}

private int[] merge(int[] leftList, int[] rightList) {

    int[] result = new int[leftList.length + rightList.length];

    int leftCursor = 0;
    int rightCursor = 0;
    int curr = 0;
    while (leftCursor < leftList.length && rightCursor < rightList.cursor) {
        if (leftList[leftCursor] < rightList[rightCursor]) {
            result[curr++] = leftList[leftCursor++];
        } else {
            result[curr++] = rightList[rightCursor++];
        }
    }

    while (leftCursor < leftList.length) {
        result[curr++] = leftList[leftCursor++];
    }

    while (rightCursor < rightList.length) {
        result[curr++] = rightList[rightCursor++];
    }
    return result;
}
```

### 2,正确解法

```
/***** Quick Sort *****/
public int[] sortArray(int[] nums) {
    if (nums.length <= 1) {
        return nums;
    }
    quickSort(nums, 0, nums.length - 1);
    return nums;
}

private void quickSort(int[] nums, int start, int end) {
    if (end <= start) {
        return;
    }
    int j = partition(nums, start, end);
    quickSort(nums, start, j - 1);
    quickSort(nums, j + 1, end);
}

private int partition(int[] nums, int low, int hi) {
    int i = low;
    int j = hi + 1;
    int pivot = nums[low];
    while (true) {
        while (nums[++i] < pivot) {
            if (i == hi) {
                break;
            }
        }
        while (pivot < nums[--j]) {
            if (j == low) {
                break;
            }
        }
        if (i >= j) {
            break;
        }
        swap(nums, i, j);
    }
    swap(nums, low, j);
    return j;
}

private void swap(int[] nums, int a, int b) {
    int temp = nums[a];
    nums[a] = nums[b];
    nums[b] = temp;
}
```

**参考资料**
- [Merge Sort(归并排序)](https://leetcode.com/explore/learn/card/recursion-ii/470/divide-and-conquer/2868/)