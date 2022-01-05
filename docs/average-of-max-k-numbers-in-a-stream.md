# 一个流中最大 K 个数的平均值

> 原文:[https://www . geesforgeks . org/max-k-numbers in-a-stream/](https://www.geeksforgeeks.org/average-of-max-k-numbers-in-a-stream/)

给定一列“N”个数字和一个整数“K”。任务是在每次查询后打印最大“K”数的平均值，其中查询由需要添加到元素列表中的整数元素组成。
**注意:**查询是用整数数组‘q’定义的

**示例:**

> **输入:** N = 4，K = 3，arr = {1，2，3，4}，q = {7，2，1，5}
> **输出:**4.666666
> 4.66666
> 4.66666
> 5.333333
> 查询 1 后，arr = {1，2，3，4，7}和最大 K 的平均值(即{3，4
> 查询 2 后，arr = {1，2，3，4，7，2}，{3，4，7}的平均值为 4.666666。
> 查询 3 后，arr = {1，2，3，4，7，2，1}，{3，4，7}的平均值为 4.666666。
> 查询 4 后，arr = {1，2，3，4，7，2，5}，{4，5，7}的平均值为 5.333333。
> 
> **输入:** N = 5，K = 4，arr = {1，2，2，3，3}，q = {2，5，1 }
> T3】输出: 2.5
> 3.25
> 3.25

**方法:** [堆](https://www.geeksforgeeks.org/binary-heap/) (Min Heap)数据结构可以用来解决类似这样的问题，其中元素的插入和删除可以在 O(log n)时间内执行。

*   最初，将给定元素列表中的最大 k 个元素存储在最小堆中。
*   如果传入的元素小于或等于当前位于最小堆根的元素，则丢弃该元素，因为它对平均值没有影响。
*   否则，如果数字大于根元素，则移除最小堆的根，然后插入新元素，然后计算堆中当前元素的平均值。
*   打印平均值，并对所有输入元素重复上述两个步骤。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function that returns the
    // average of max k elements in
    // the list after each query
    static void max_average_k_numbers(int n,
                                      int k,
                                      int m,
                                      int[] arr,
                                      int[] query)
    {
        double max_avg = 0.0;

        // min-heap to maintain
        // the max k elements at
        // any point of time;
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

        // Sort the array
        // in ascending order
        Arrays.sort(arr);

        // add max k elements
        // to the heap
        double sum = 0;
        for (int i = n - 1; i >= n - k; i--) {
            pq.add(arr[i]);
            sum = sum + arr[i];
        }

        // perform offline queries
        for (int i = 0; i < m; i++) {

            // if the minimum element in
            // the heap is less than
            // the incoming element
            if (query[i] > pq.peek()) {
                int polled = pq.poll();
                pq.add(query[i]);

                // decrement the current
                // sum by the polled element
                sum = sum - polled;

                // increment sum by the
                // incoming element
                sum = sum + query[i];
            }

            // compute the average
            max_avg = sum / (double)k;
            System.out.println(max_avg);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        int k = 3;
        int m = 4;
        int[] arr = new int[] { 1, 2, 3, 4 };
        int[] query = new int[] { 7, 2, 1, 5 };

        max_average_k_numbers(n, k, m, arr, query);
    }
}
```

**Output:**

```
4.666666666666667
4.666666666666667
4.666666666666667
5.333333333333333

```