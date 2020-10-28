### 1, Fenwick Or Binary Indexed Tree

```
/**
 * 
 * A Fenwick tree or binary indexed tree is a data structure provicing effecient methods
 * for calculating and manipulation of the prefix sums of a table of values.
 *
 * Space complexity for fenwick tree is O(n)
 * Time complexity to create fenwick tree is O(nlogn)
 * Time complexity to update value is O(logn)
 * Time complexity to get prefix sum is O(logn)
 *
 */

 public class FenwickTree {

     /**
      * Start from index + 1 if you updating index in original array. Keep adding this value
      * for next node till you reach outside range of tree
      */
      public void updateBinaryIndexedTree(int binaryIndexedTree[], int val, int index) {
          while (index < binaryIndexedTree.length) {
              binaryIndexedTree[index] += val;
              index = getNext(index);
          }
      }

      /**
       * Start from index + 1 if you want prefix sum 0 to index. Keep adding value till you reach 0
       */
       public int getSum(int binaryIndexedTree[], int index) {
           index = index + 1;
           int sum = 0;
           while (index > 0) {
               sum += binaryIndexedTree[index];
               index = getParent(index);
           }
           return sum;
       }


     /**
      * Creating tree is like updating Fenwick tree for every value in array
      */
      public int[] createTree(int input[]) {
          int binaryIndexedTree[] = new int[input.length + 1];
          for (int i = 1; i <= input.length; i++) {
              updateBinaryIndexedTree(binaryIndexedTree, input[i-1], i);
          }
          return binaryIndexedTree;
      }
    
    /**
     * To get parent
     * 1) 2's complement to get minus of index
     * 2) AND this with index
     * 3) Subtract that from index
     */
     private int getParent(int index) {
         return index - (index & -index);
     }

     /**
      * To get next
      * 1) 2's complement of get minus of index
      * 2) AND this with index
      * 3) Add it to index
      */
      private int getNext(int index) {
          return index + (index & -index);
      }
 }
```

**参考资料:**
- [Fenwick Tree or Binary Indexed Tree](https://www.youtube.com/watch?v=CWDQJGaN1gY&list=PLrmLmBdmIlpv_jNDXtJGYTPNQ2L1gdHxu&index=24)
- [Binary Indexed Tree or Fenwick](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
- [Binary Indexed Trees](https://www.topcoder.com/community/competitive-programming/tutorials/binary-indexed-trees/)
- [Fenwick Tree](http://en.wikipedia.org/wiki/Fenwick_tree)