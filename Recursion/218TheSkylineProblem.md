218. The Skyline Problem

### 题目地址
- [The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/)

### 1,初步思路

```
// 计划使用 backtracking
public List<List<Integer>> getSkyline(int[][] buildings) {
    List<List<Integer>> result = new ArrayList<>();

    if (buildings == null || buildings.length == 0) {
        return result;
    }

    List<Integer> first = new ArrayList<>();
    first.add(buildings[0][0]);
    first.add(buildings[0][3]);
    result.add(first);

    return result;
}

private void backtrack(List<List<Integer>> result, List<Integer> subList, int start, int[][] buildings) {

    //不清楚如何处理逻辑关系
    if (subList.size() == 2) {
        result.add(subList);
        return;
    }

    for (int i = 1; i < buidlings.length; i++) {
        if (buildings[start][1] > buildings[i][0]) {
            int first = buildings[start][2] > buildings[i][2] ? 
        }
    }
}
```

### 2,正确解法

```
/***** Divide and Conquer *****/
public List<List<Integer>> getSkyline(int[][] buildings) {

    if (buildings.length == 0) {
        return new Linkedlist<List<Integer>>();
    }

    return recurSkyline(buildings, 0, buildings.length - 1);
}

private Linkedlist<List<Integer>> recurSkyline(int[][] buildings, int p, int q) {
    if (p < q) {
        int mid = p + (q - p) / 2;
        return merge(recurSkyline(buildings, p, mid), recurSkyline(buildings, mid + 1, q));
    } else {
        LinkedList<List<Integer>> rs = new LinkedList<>();
        List<Integer> first = new ArrayList<>();
        first.add(buildings[p][0]);
        first.add(buildings[p][2]);
        List<Integer> second = new ArrayList<>();
        second.add(buildings[p][1]);
        second.add(0);
        rs.add(first);
        rs.add(second);
        return rs;
    }
}

private LinkedList<List<Integer>> merge(LinkedList<List<Integer>> l1, LinkedList<List<Integer>> l2) {
    LinkedList<List<Integer>> rs = new LinkedList<>();

    int h1 = 0;
    int h2 = 0;

    while (l1.size() > 0 && l2.size() > 0) {
        int x = 0;
        int h = 0;
        if (l1.getFirst().get(0) < l2.getFirst().get(0)) {
            x = l1.getFirst().get(0);
            h1 = l1.getFirst().get(1);
            h = Math.max(h1, h2);
            l1.removeFirst();
        } else if (l1.getFirst().get(0) > l2.getFirst().get(0)) {
            x = l2.getFirst().get(0);
            h2 = l2.getFirst().get(1);
            h = Math.max(h1, h2);
            l2.removeFirst();
        } else {
            x = l1.getFirst().get(0);
            h1 = l1.getFirst().get(1);
            h2 = l2.getFirst().get(1);
            h = Math.max(h1, h2);
            l1.removeFirst();
            l2.removeFirst();
        }

        if (rs.size() == 0 || h != rs.getLast().get(1)) {
            List<Integer> temp = new ArrayList<>();
            temp.add(x);
            temp.add(h);
            rs.add(temp;)
        }
    }

    rs.addAll(l1);
    rs.addAll(l2);
    return rs;
}
```

**参考资料**
- [Divide and Conquer Solution](https://leetcode.com/problems/the-skyline-problem/discuss/61246/Share-my-divide-and-conquer-java-solution-464-ms)