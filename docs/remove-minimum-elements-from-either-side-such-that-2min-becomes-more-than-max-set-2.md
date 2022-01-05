# 从任一侧移除最小元素，使 2*min 大于 max |设置 2

> 原文:[https://www . geesforgeks . org/remove-从任一侧移除最小元素-这样-2 分钟就变成大于最大集-2/](https://www.geeksforgeeks.org/remove-minimum-elements-from-either-side-such-that-2min-becomes-more-than-max-set-2/)

给定一个未排序的数组，修剪数组，使最小值的两倍大于修剪数组中的最大值。元素应该从数组的任何一端移除。移除的数量应该是最小的。

**示例:**

> **输入:** arr[] = {4，5，100，9，10，11，12，15，200}
> **输出:** 4
> 我们需要去掉 4 个元素(4，5，100，200)
> 这样 2*min 就变得大于 max 了。
> 
> **输入:** arr[] = {4，7，5，6}
> **输出:** 0
> 我们不需要移除任何元素作为
> 4*2 > 7
> 
> **输入:** arr[] = {20，7，5，6}
> **输出:** 1

**方式:**我们在[上一篇](https://www.geeksforgeeks.org/remove-minimum-elements-either-side-2min-max/)中的 O(n <sup>3</sup> )、O(n <sup>2</sup> * logn)和 O(n <sup>2</sup> 时间中讨论了解决这个问题的各种方式。在本文中，我们将讨论使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)和[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)概念的 O(n * logn)时间解决方案。

1.  为给定输入数组的范围最小值查询和范围最大值查询构造段树。
2.  取两个指针**开始**和**结束**，将两者初始化为 **0** 。
3.  当**结束**小于输入数组的长度时，执行以下操作:
    *   使用步骤 1 中构建的分段树在当前窗口中找到**最小值**和**最大值**。
    *   检查 **2 * min ≤ max** ，如果是，则递增**开始**指针，否则更新到目前为止的最大有效长度(如果需要)
    *   增量**结束**
4.  **长度(arr[])–maxValidLength**为必选项。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the minimum removals
    // required so that the array satisfy
    // the given condition
    public int removeMinElements(int[] a)
    {
        int n = a.length;

        RangeMinimumQuery rMimQ = new RangeMinimumQuery();
        int[] minTree = rMimQ.createSegmentTree(a);

        RangeMaximumQuery rMaxQ = new RangeMaximumQuery();
        int[] maxTree = rMaxQ.createSegmentTree(a);

        int start = 0, end = 0;

        // To store min and max in the current window
        int min, max;
        int maxValidLen = 0;

        while (end < n) {
            min = rMimQ.rangeMinimumQuery(minTree,
                                          start, end, n);
            max = rMaxQ.rangeMaximumQuery(maxTree,
                                          start, end, n);
            if (2 * min <= max)
                start++;
            else
                maxValidLen = Math.max(maxValidLen,
                                       end - start + 1);
            end++;
        }
        return n - maxValidLen;
    }

    class RangeMinimumQuery {

        // Creates a new segment tree from
        // the given input array
        public int[] createSegmentTree(int[] input)
        {
            int n = input.length;
            int segTreeSize = 2 * getNextPowerOfTwo(n) - 1;
            int[] segmentTree = new int[segTreeSize];

            createSegmentTreeUtil(segmentTree, input,
                                  0, n - 1, 0);
            return segmentTree;
        }

        private void createSegmentTreeUtil(int[] segmentTree,
                                           int[] input, int low,
                                           int high, int pos)
        {
            if (low == high) {

                // Its a leaf node
                segmentTree[pos] = input[low];
                return;
            }

            // Construct left and right subtrees and then
            // update value for current node
            int mid = (low + high) / 2;
            createSegmentTreeUtil(segmentTree, input, low,
                                  mid, (2 * pos + 1));
            createSegmentTreeUtil(segmentTree, input,
                                  mid + 1, high, (2 * pos + 2));
            segmentTree[pos] = Math.min(segmentTree[2 * pos + 1],
                                        segmentTree[2 * pos + 2]);
        }

        public int rangeMinimumQuery(int[] segmentTree, int from,
                                     int to, int inputSize)
        {
            return rangeMinimumQueryUtil(segmentTree, 0,
                                         inputSize - 1, from, to, 0);
        }

        private int rangeMinimumQueryUtil(int[] segmentTree, int low,
                                        int high, int from, int to, int pos)
        {
            // Total overlap
            if (from <= low && to >= high) {
                return segmentTree[pos];
            }

            // No overlap
            if (from > high || to < low) {
                return Integer.MAX_VALUE;
            }

            // Partial overlap
            int mid = (low + high) / 2;
            int left = rangeMinimumQueryUtil(segmentTree, low,
                                             mid, from, to,
                                             (2 * pos + 1));
            int right = rangeMinimumQueryUtil(segmentTree,
                                              mid + 1, high, from,
                                              to, (2 * pos + 2));
            return Math.min(left, right);
        }
    }

    class RangeMaximumQuery {

        // Creates a new segment tree from given input array
        public int[] createSegmentTree(int[] input)
        {
            int n = input.length;
            int segTreeSize = 2 * getNextPowerOfTwo(n) - 1;
            int[] segmentTree = new int[segTreeSize];

            createSegmentTreeUtil(segmentTree, input, 0, n - 1, 0);
            return segmentTree;
        }

        private void createSegmentTreeUtil(int[] segmentTree, int[] input,
                                           int low, int high, int pos)
        {
            if (low == high) {

                // Its a leaf node
                segmentTree[pos] = input[low];
                return;
            }

            // Construct left and right subtrees and then
            // update value for current node
            int mid = (low + high) / 2;
            createSegmentTreeUtil(segmentTree, input, low,
                                  mid, (2 * pos + 1));
            createSegmentTreeUtil(segmentTree, input,
                                  mid + 1, high, (2 * pos + 2));
            segmentTree[pos] = Math.max(segmentTree[2 * pos + 1],
                                        segmentTree[2 * pos + 2]);
        }

        public int rangeMaximumQuery(int[] segmentTree,
                                     int from, int to, int inputSize)
        {
            return rangeMaximumQueryUtil(segmentTree, 0,
                                         inputSize - 1, from, to, 0);
        }

        private int rangeMaximumQueryUtil(int[] segmentTree, int low,
                                 int high, int from, int to, int pos)
        {
            // Total overlap
            if (from <= low && to >= high) {
                return segmentTree[pos];
            }

            // No overlap
            if (from > high || to < low) {
                return Integer.MIN_VALUE;
            }

            // Partial overlap
            int mid = (low + high) / 2;
            int left = rangeMaximumQueryUtil(segmentTree, low,
                                             mid, from, to,
                                             (2 * pos + 1));
            int right = rangeMaximumQueryUtil(segmentTree,
                                              mid + 1, high, from,
                                              to, (2 * pos + 2));
            return Math.max(left, right);
        }
    }

    // Function to return the minimum power of 2
    // which is greater than n
    private int getNextPowerOfTwo(int n)
    {
        int logPart = (int)Math.ceil(Math.log(n)
                                     / Math.log(2));
        return (int)Math.pow(2, logPart);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 4, 5, 100, 9, 10, 11, 12, 15, 200 };
        GFG gfg = new GFG();
        System.out.println(gfg.removeMinElements(a));
    }
}
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum removals
    // required so that the array satisfy
    // the given condition
    static int removeMinElements(int[] a)
    {
        int n = a.Length;

        RangeMinimumQuery rMimQ = new RangeMinimumQuery();
        int[] minTree = rMimQ.createSegmentTree(a);

        RangeMaximumQuery rMaxQ = new RangeMaximumQuery();
        int[] maxTree = rMaxQ.createSegmentTree(a);

        int start = 0, end = 0;

        // To store min and max in the current window
        int min, max;
        int maxValidLen = 0;

        while (end < n) 
        {
            min = rMimQ.rangeMinimumQuery(minTree,
                                        start, end, n);
            max = rMaxQ.rangeMaximumQuery(maxTree,
                                        start, end, n);
            if (2 * min <= max)
                start++;
            else
                maxValidLen = Math.Max(maxValidLen,
                                    end - start + 1);
            end++;
        }
        return n - maxValidLen;
    }

    class RangeMinimumQuery {

        // Creates a new segment tree from
        // the given input array
        public int[] createSegmentTree(int[] input)
        {
            int n = input.Length;
            int segTreeSize = 2 * getNextPowerOfTwo(n) - 1;
            int[] segmentTree = new int[segTreeSize];

            createSegmentTreeUtil(segmentTree, input,
                                0, n - 1, 0);
            return segmentTree;
        }

        public void createSegmentTreeUtil(int[] segmentTree,
                                        int[] input, int low,
                                        int high, int pos)
        {
            if (low == high) {

                // Its a leaf node
                segmentTree[pos] = input[low];
                return;
            }

            // Construct left and right subtrees and then
            // update value for current node
            int mid = (low + high) / 2;
            createSegmentTreeUtil(segmentTree, input, low,
                                mid, (2 * pos + 1));
            createSegmentTreeUtil(segmentTree, input,
                                mid + 1, high, (2 * pos + 2));
            segmentTree[pos] = Math.Min(segmentTree[2 * pos + 1],
                                        segmentTree[2 * pos + 2]);
        }

        public int rangeMinimumQuery(int[] segmentTree, int from,
                                    int to, int inputSize)
        {
            return rangeMinimumQueryUtil(segmentTree, 0,
                                        inputSize - 1, from, to, 0);
        }

        static int rangeMinimumQueryUtil(int[] segmentTree, int low,
                                        int high, int from, int to, int pos)
        {
            // Total overlap
            if (from <= low && to >= high) {
                return segmentTree[pos];
            }

            // No overlap
            if (from > high || to < low) {
                return int.MaxValue;
            }

            // Partial overlap
            int mid = (low + high) / 2;
            int left = rangeMinimumQueryUtil(segmentTree, low,
                                            mid, from, to,
                                            (2 * pos + 1));
            int right = rangeMinimumQueryUtil(segmentTree,
                                            mid + 1, high, from,
                                            to, (2 * pos + 2));
            return Math.Min(left, right);
        }
    }

    class RangeMaximumQuery {

        // Creates a new segment tree from given input array
        public int[] createSegmentTree(int[] input)
        {
            int n = input.Length;
            int segTreeSize = 2 * getNextPowerOfTwo(n) - 1;
            int[] segmentTree = new int[segTreeSize];

            createSegmentTreeUtil(segmentTree, input, 0, n - 1, 0);
            return segmentTree;
        }

        public void createSegmentTreeUtil(int[] segmentTree, int[] input,
                                        int low, int high, int pos)
        {
            if (low == high) {

                // Its a leaf node
                segmentTree[pos] = input[low];
                return;
            }

            // Construct left and right subtrees and then
            // update value for current node
            int mid = (low + high) / 2;
            createSegmentTreeUtil(segmentTree, input, low,
                                mid, (2 * pos + 1));
            createSegmentTreeUtil(segmentTree, input,
                                mid + 1, high, (2 * pos + 2));
            segmentTree[pos] = Math.Max(segmentTree[2 * pos + 1],
                                        segmentTree[2 * pos + 2]);
        }

        public int rangeMaximumQuery(int[] segmentTree,
                                    int from, int to, int inputSize)
        {
            return rangeMaximumQueryUtil(segmentTree, 0,
                                        inputSize - 1, from, to, 0);
        }

        public int rangeMaximumQueryUtil(int[] segmentTree, int low,
                                int high, int from, int to, int pos)
        {
            // Total overlap
            if (from <= low && to >= high) {
                return segmentTree[pos];
            }

            // No overlap
            if (from > high || to < low) {
                return int.MinValue;
            }

            // Partial overlap
            int mid = (low + high) / 2;
            int left = rangeMaximumQueryUtil(segmentTree, low,
                                            mid, from, to,
                                            (2 * pos + 1));
            int right = rangeMaximumQueryUtil(segmentTree,
                                            mid + 1, high, from,
                                            to, (2 * pos + 2));
            return Math.Max(left, right);
        }
    }

    // Function to return the minimum power of 2
    // which is greater than n
    static int getNextPowerOfTwo(int n)
    {
        int logPart = (int)Math.Ceiling(Math.Log(n)
                                    / Math.Log(2));
        return (int)Math.Pow(2, logPart);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 4, 5, 100, 9, 10, 11, 12, 15, 200 };
        Console.WriteLine(removeMinElements(a));
    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
4

```