# 多线程快速排序

> 原文:[https://www . geeksforgeeks . org/quick-sort-use-multi-threading/](https://www.geeksforgeeks.org/quick-sort-using-multi-threading/)

[快速排序](https://www.geeksforgeeks.org/quick-sort/)是一种流行的基于分治算法的排序技术。在这种技术中，选择一个元素作为轴，并围绕它划分数组。分区的目标是，给定一个数组和数组的元素 x 作为轴心，将 x 放在排序数组的正确位置，将所有较小的元素(小于 x)放在 x 之前，将所有较大的元素(大于 x)放在 x 之后。
[**【多线程】**](https://www.geeksforgeeks.org/multithreading-in-java/) 允许并发执行程序的两个或多个部分，以最大限度地利用 CPU。这种程序的每个部分称为[线程](https://www.geeksforgeeks.org/thread-in-operating-system/)。因此，线程是进程中的轻量级进程。
**举例:**

> **输入:** arr[] = {10，9，8，7，6，5，4，3，2，1}
> **输出:** 1 2 3 4 5 6 7 8 9 10
> **输入:** arr[] = {54，64，95，82，1 2，32，63}
> **输出:** 12 32 54 63 64 82 95

**进场:**进场的主要思路是:

1.  主线程调用 quicksort 方法。
2.  方法对数组进行分区，并检查当前线程的数量。
3.  下一步使用相同的并行方法调用新线程。
4.  使用单一正常快速排序方法。

下面是程序使用 *ForkJoinPool* 线程池保持线程数与 CPU 数相同并重用线程:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Random;
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.RecursiveTask;

public class QuickSortMutliThreading
    extends RecursiveTask<Integer> {

    int start, end;
    int[] arr;

    /**
     * Finding random pivoted and partition
     * array on a pivot.
     * There are many different
     * partitioning algorithms.
     * @param start
     * @param end
     * @param arr
     * @return
     */
    private int partition(int start, int end,
                        int[] arr)
    {

        int i = start, j = end;

        // Decide random pivot
        int pivote = new Random()
                         .nextInt(j - i)
                     + i;

        // Swap the pivote with end
        // element of array;
        int t = arr[j];
        arr[j] = arr[pivote];
        arr[pivote] = t;
        j--;

        // Start partitioning
        while (i <= j) {

            if (arr[i] <= arr[end]) {
                i++;
                continue;
            }

            if (arr[j] >= arr[end]) {
                j--;
                continue;
            }

            t = arr[j];
            arr[j] = arr[i];
            arr[i] = t;
            j--;
            i++;
        }

        // Swap pivote to its
        // correct position
        t = arr[j + 1];
        arr[j + 1] = arr[end];
        arr[end] = t;
        return j + 1;
    }

    // Function to implement
    // QuickSort method
    public QuickSortMutliThreading(int start,
                                   int end,
                                   int[] arr)
    {
        this.arr = arr;
        this.start = start;
        this.end = end;
    }

    @Override
    protected Integer compute()
    {
        // Base case
        if (start >= end)
            return null;

        // Find partition
        int p = partition(start, end, arr);

        // Divide array
        QuickSortMutliThreading left
            = new QuickSortMutliThreading(start,
                                          p - 1,
                                          arr);

        QuickSortMutliThreading right
            = new QuickSortMutliThreading(p + 1,
                                          end,
                                          arr);

        // Left subproblem as separate thread
        left.fork();
        right.compute();

        // Wait untill left thread complete
        left.join();

        // We don't want anything as return
        return null;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 7;
        int[] arr = { 54, 64, 95, 82, 12, 32, 63 };

        // Forkjoin ThreadPool to keep
        // thread creation as per resources
        ForkJoinPool pool
            = ForkJoinPool.commonPool();

        // Start the first thread in fork
        // join pool for range 0, n-1
        pool.invoke(
            new QuickSortMutliThreading(
                0, n - 1, arr));

        // Print shorted elements
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}
```

**Output:** 

```
12 32 54 63 64 82 95
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(N)*