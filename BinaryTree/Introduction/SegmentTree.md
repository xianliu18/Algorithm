### 1. Segment Tree


#### 1.1 Minimum Range Query

```
/**
 * A segment tree is a tree data structure for storing intervals, or segments. It allows
 * for faster querying(e.g sum or min) in these intervals. Lazy propagation is useful when there are
 * high number of updates in the input array.
 *
 *
 * Time complexity to create segment tree is O(N) since new array will be at max 4N size.
 * Space complexity to create segment tree is O(N) since new array will be at max 4N size.
 * Time complexity to search in segment tree is O(logN) since you would at max travel 4 depths.
 * Time complexity to update in segment tree is O(logN)
 * Time complexity to update range in segment tree is O(range)
 */

 public class SegmentTreeMinimumRangeQuery {

     /**
      * Creates a new segment tree based off input array.
      */
      public int[] createSegmentTree(int input[]) {
          NextPowerOf2 np2 = new NextPowerOf2();

          // if input len is pow of 2 then size of segment tree is 2 * len - 1,
          // otherwise size of segment tree is next (pow of 2 for len) * 2 - 1
          int nextPowOfTwo = np2.nextPowerOf2(input.length);
          int segmentTree[] = new int[nextPowOfTwo * 2 - 1];

          for (int i = 0; i < segmentTree.length; i++) {
              segmentTree[i] = Integer.MAX_VALUE;
          }
          constructMinSegmentTree(segmentTree, input, 0, input.length - 1, 0);
          return segmentTree;
      }

      /**
       * Updates segment tree for certain index by given delta
       */
       public void updateSegmentTree(int input[], int segmentTree[], int index, int delta) {
           input[index] += delta;
           updateSegmentTree(segmentTree, index, delta, 0, input.length - 1, 0);
       }

       /**
        * Updates segment tree for given range by given delta
        */
        public void updateSegmentTreeRange(int input[], int segmentTree[], int startRange, int endRange, int delta) {
            for (int i = startRange; i <= endRange; i++) {
                input[i] += delta;
            }
            updateSegmentTreeRange(segmentTree, startRange, endRange, delta, 0, input.length - 1, 0);
        }

        /**
         * Queries given range for minimum value.
         */
         public int rangeMinimumQuery(int segmentTree[], int qlow, int qhigh, int len) {
             return rangeMinimumQuery(segmentTree, 0, len - 1, qlow, qhigh, 0);
         }

         /**
          * Update given range by given delta lazily
          */
          public void updateSegmentTreeRangeLazy(int input[], int segmentTree[], int lazy[], int startRange, int endRange, int delta) {
              updateSegmentTreeRangeLazy(segmentTree, lazy, startRange, endRange, delta, 0, input.length - 1, 0);
          }

          /**
           * Queries given range lazily
           */
           public int rangeMinimumQueryLazy(int segmentTree[], int lazy[], int qlow, int qhigh, int len) {
               return rangeMinimumQueryLazy(segmentTree, lazy, qlow, qhigh, 0, len - 1, 0);
           }

           private void constructMinSegmentTree(int segmentTree[], int input[], int low, int high, int pos) {
               if (low == high) {
                   segmentTree[pos] = input[low];
                   return;
               }
               int mid = (low + high) / 2;
               // left child = 2 * pos + 1
               constructMinSegmentTree(segmentTree, input, low, mid, 2 * pos + 1);
               // right child = 2 * pos + 2
               constructMinSegmentTree(segmentTree, input, mid + 1, high, 2 * pos + 2);
               // parent 
               segmentTree[pos] = Math.min(segmentTree[2*pos + 1], segmentTree[2*pos+2]);
           }

           private void updateSegmentTree(int segmentTree[], int index, int delta, int low, int high, int pos) {
               // if index to be updated is less than low or higher than high just return.
               if (index < low || index > high) {
                   return;
               }

               // if low and high become equal, then index will be also equal to them and update
               // that value in segment tree at pos
               if (low == high) {
                   segmentTree[pos] += delta;
                   return;
               }

               // otherwise keep going left and right to find index to be updated
               // and then update current tree position if min of left or right has changed
               int mid = (low + high) / 2;
               updateSegmentTree(segmentTree, index, delta, low, mid, 2 * pos + 1);
               updateSegmentTree(segmentTree, index, delta, mid + 1, high, 2 * pos + 2);
               segmentTree[pos] = Math.min(segmentTree[2*pos+1], segmentTree[2*pos+2]);
           }

           private void updateSegmentTreeRange(int segmentTree[], int startRange, int endRange, int delta, int low, int high, int pos) {
               if (low > high || startRange > high || endRange < low) {
                   return;
               }

               if (low == high) {
                   segmentTree[pos] += delta;
                   return;
               }

               int mid = (low + high) / 2;
               updateSegmentTreeRange(segmentTree, startRange, endRange, delta, low, mid, 2 * pos + 1);
               updateSegmentTreeRange(segmentTree, startRange, endRange, delta, mid + 1, high, 2 * pos + 2);
               segmentTree[pos] = Math.min(segmentTree[2 * pos + 1], segmentTree[2 * pos + 2]);
           }

           private in rangeMinimumQuery(int segmentTree[], int low, int high, int qlow, int qhigh, int pos) {
               // total overlap
               if (qlow <= low && qhigh >= high) {
                   return segmentTree[pos];
               }

               // no overlap
               if (qlow > high || qhigh < low) {
                   return Integer.MAX_VALUE:
               }

               // partial overlap
               int mid = (low + high) / 2;
               return Math.min(rangeMinimumQuery(segmentTree, low, mid, qlow, qhigh, 2 * pos + 1),
                                rangeMinimumQuery(segmentTree, mid + 1, high, qlow, qhigh, 2 * pos + 2));
           }


           private void updateSegmentTreeRangeLazy(int segmentTree[],
                                                    int lazy[], int startRange, int endRange,
                                                    int delta, int low, int high, int pos) {
                if (low > high) {
                    return;
                }

                // make sure all propagation is done at pos. If not update tree
                // at pos and mark its children for lazy propagation.
                if (lazy[pos] != 0) {
                    segmentTree[pos] += lazy[pos];
                    if (low != high) { // not a leaf node
                        lazy[2 * pos + 1] += lazy[pos];
                        lazy[2 * pos + 2] += lazy[pos];
                    }
                    lazy[pos] = 0;
                }

                // no overlap condition
                if (startRange > high || endRange < low) {
                    return;
                }

                // total overlap condition
                if (startRange <= low && endRange >= high) {
                    segmentTree[pos] += delta;
                    if (low != high) {
                        lazy[2 * pos + 1] += delta;
                        lazy[2 * pos + 2] += delta;
                    }
                    return;
                }

                // otherwise partial overlap so look both left and right
                int mid = (low + high) / 2;
                updateSegmentTreeRangeLazy(segmentTree, lazy, startRange, endRange, delta, low, mid, 2 * pos + 1);
                update SegmentTreeRangeLayz(segmentTree, lazy, startRange, endRange, delta, mid + 1, high, 2 * pos + 2);
                segmentTree[pos] = Math.min(segmentTree[2 * pos + 1], segmentTree[2 * pos + 2]);
            }

            private int rangeMinimumQueryLazy(int segmentTree[], int lazy[], int qlow, int qhigh,
                                                int low, int high, int pos) {
                if (low > high) {
                    return Integer.MAX_VALUE;
                }

                // make sure all propagation is done at pos. If not update tree at pos
                // and mark its children for lazy propagation
                if (lazy[pos] != 0) {
                    segmentTree[pos] += lazy[pos];
                    if (low != high) {
                        lazy[2 * pos + 1] += lazy[pos];
                        lazy[2 * pos + 2] += lazy[pos];
                    }
                    lazy[pos] = 0;
                }

                // no overlap
                if (qlow > high || qhigh < low) {
                    return Integer.MAX_VALUE;
                }

                // total overlap
                if (qlow <= low && qhigh >= high) {
                    return segmentTree[pos];
                }

                // partial overlap
                int mid = (low + high) / 2;
                return Math.min(rangeMinimumQueryLazy(segmentTree, lazy, qlow, qhigh, low, mid, 2 * pos + 1),
                                rangeMinimumQueryLazy(segmentTree, lazy, qlow, qhigh, mid + 1, high, 2 * pos + 2));
            }
 }
```




**参考资料:**
- [Segment Tree Range Minimum Query](https://www.youtube.com/watch?v=ZBHKZF5w4YU&list=PLrmLmBdmIlpv_jNDXtJGYTPNQ2L1gdHxu&index=22&pbjreload=101)
- [Sum of given range](http://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
- [Range Minimum Query](http://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)