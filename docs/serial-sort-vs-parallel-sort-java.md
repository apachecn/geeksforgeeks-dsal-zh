# Java 中串行排序 v/s 并行排序

> 原文:[https://www . geesforgeks . org/serial-sort-vs-parallel-sort-Java/](https://www.geeksforgeeks.org/serial-sort-vs-parallel-sort-java/)

我们经常需要在编程时对数组进行排序。为此，我们在 Arrays 类中使用 Java 提供的内置方法，即 sort()。sort()方法使用合并排序或 Tim Sort 对数组元素进行排序。在这两种情况下，sort()方法按顺序对数组的元素进行排序。

在 Java 8 中，引入了一个新的排序 API，这就是并行排序。

并行排序使用 Java 7 中引入的 [Fork/Join](http://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) 框架，将排序任务分配给线程池中可用的多个线程。Fork/Join 实现了一个[工作窃取算法](https://en.wikipedia.org/wiki/Work_stealing)，在这个算法中，一个空闲线程可以窃取另一个线程中排队的任务。

例如，下面的代码是一个使用 [**Arrays.sort()**](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) 和**arrays . parallels art()**对随机化的双精度数组进行排序的程序。这个程序只是测量这两种方法之间的性能差异。：

```
// Java program to demonstrate time taken by sort()
// and parallelSort() methods.
import java.util.Arrays;

public class ParallelSortTest
{
    private static final int BASE_ARRAY_SIZE = 10000;

    // A utility function to generate and return an
    // an array of given size filled with randomly
    // generated elements.
    public static double[] generateArray(int size)
    {
        if (size <= 0 || size > Integer.MAX_VALUE)
            return null;

        double[] result = new double[size];
        for (int i = 0; i < size; i++)
            result[i] = Math.random();

        return result;
    }

    // Driver code to compare two sortings
    public static void main(String[] args)
    {
        for (int i = 1; i < 10000; i *= 10)
        {
            int size = BASE_ARRAY_SIZE * i;
            double[] arr1 = generateArray(size);

            // Creating a copy of arr1 so that we can
            // use same content for both sortings.
            double[] arr2 = Arrays.copyOf(arr1, arr1.length);
            System.out.println("Array Size: " + size);

            // Sorting arr1[] using serial sort
            long startTime = System.currentTimeMillis();
            Arrays.sort(arr1);
            long endTime = System.currentTimeMillis();
            System.out.println("Time take in serial: " +
                             (endTime - startTime) + "ms.");

            // Sorting arr2[] using serial sort
            startTime = System.currentTimeMillis();
            Arrays.parallelSort(arr2);
            endTime = System.currentTimeMillis();
            System.out.println("Time take in parallel: "
                            + (endTime - startTime) + "ms.");
            System.out.println();
        }
    }
}
```

环境:

```
2.6 GHz Intel Core i7
java version "1.8.0_25"

```

**注意:**所需时间可能因数组中的随机值而异。

这两种算法的主要区别如下:

1) **Arrays.sort()** :是顺序排序。

*   该应用编程接口使用单线程进行操作。
*   执行这项操作需要稍长的时间。

2.**数组。parallels art():**是一个并行排序。

*   该应用编程接口使用多个线程进行操作。
*   有很多元素时速度更快，而较少元素时速度更慢。

**分析:**
结果显示，多核机器上的并行排序可以在 100 万个或更多元素上实现性能提升。当低于该阈值时，它实际上可能比顺序排序慢。这个结果符合预期，这里合适的大小可能是 100 万。您的里程可能会有所不同，这取决于您的环境。

**解释:**
现在，让我们看一下代码，了解一下这种并行排序是如何工作的。

```
    public static void parallelSort(double[] a) {
        int n = a.length, p, g;
        if (n <= MIN_ARRAY_SORT_GRAN ||
            (p = ForkJoinPool.getCommonPoolParallelism()) == 1)
            DualPivotQuicksort.sort(a, 0, n - 1, null, 0, 0);
        else
            new ArraysParallelSortHelpers.FJDouble.Sorter
                (null, a, new double[n], 0, n, 0,
                 ((g = n / (p << 2)) <= MIN_ARRAY_SORT_GRAN) ?
                 MIN_ARRAY_SORT_GRAN : g).invoke();
    }

```

我们可以看到，有一个最小粒度(Java . util . arrays . min _ ARRAY _ SORT _ GRAN = 8192[0x 2000])，如果数组的长度小于最小粒度，则直接使用 DualPivotQuicksort.sort 而不是排序任务分区进行排序。通常，使用较小的大小会导致任务之间的内存争用，这使得并行加速不太可能。

另一个值得注意的判断是 forkjoinpool . getcommonpoolparallelism()返回公共池的目标并行度(默认情况下，等于可用处理器的数量 Runtime.getRuntime()。availableProcessors())。如果你的机器只有一个工作线程，它也不会使用并行任务。

当数组长度达到最小粒度，并且有 1 个以上的工作线程时，使用**并行排序方法**对数组进行排序。这里使用 ForkJoin 公共池来执行并行任务。

**参考:**
[http://download . Java . net/lambda/b84/docs/API/Java/util/arrays . html # parallels art % 28 int](http://download.java.net/lambda/b84/docs/api/java/util/Arrays.html#parallelSort%28int)

本文由 **[索米亚米什拉](https://www.facebook.com/profile.php?id=100009911175839&fref=ts)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。