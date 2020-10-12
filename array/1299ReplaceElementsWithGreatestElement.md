1299. Replace Elements with Greatest Element on Right Side

### 题目地址
- [Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)

### 1,初步思路

```
/**
* Replace Element
*
* 1,遍历
* 		如果后一个值比前一个值大, 前一个的值替换为后一个值;
* 		如果后一个值比前一个值小,则不做替换;
* 	忽略第一个值,直接从第二个值开始, 末尾的值为-1
*
* 	2, 如何找到右侧最大值?
* 	3, 找到后,如何进行替换?
*/

public int[] replaceElements(int[] arr) {
		if (arr.length == 0) {
			return arr;
		}
		int start = 0;
		int end = arr.length - 1;
		for (int i = 1; i < arr.length - 1; i++) {
			if (arr[i+1] < arr[i]) {
				end = i;
				while (end >= start) {
					arr[end] = arr[i];
					end--;
				}
				start = i + 1;
			}
		}
		arr[arr.length - 1] = -1;
		return arr;
	}

```

### 2,正确解法

```
// 从反方向考虑
public int[] replaceEle2(int[] nums) {
    int max = -1;
    int len = nums.length;
    int temp;
    for (int i = len - 1; i >= 0; --i) {
        temp = nums[i];
        nums[i] = max;
        max = Math.max(temp, max);
    }
    return nums;
}
```