# 了解你的排序算法|集合 2 (Introsort- C++的排序武器)

> 原文:[https://www . geesforgeks . org/know-your-sorting-algorithm-set-2-intro sort-cs-sorting-armor/](https://www.geeksforgeeks.org/know-your-sorting-algorithm-set-2-introsort-cs-sorting-weapon/)

我们在之前的文章中已经讨论过[整理不同语言使用的武器](https://www.geeksforgeeks.org/know-sorting-algorithm-set-1-sorting-weapons-used-programming-languages/)。本文讨论了 C++的排序武器，Introsort。

**什么是 Introsort？**
简单来说，就是身边最好的排序算法。它是一种混合排序算法，这意味着它使用多个排序算法作为例程。

**intro Sort 中使用了哪些标准排序算法**
Introsort 是一种混合排序算法，使用三种排序算法来最小化运行时间，[quick Sort](https://www.geeksforgeeks.org/quick-sort/)[heap Sort](https://www.geeksforgeeks.org/heap-sort/)和[insert Sort](https://www.geeksforgeeks.org/insertion-sort/)

**它是如何工作的？**
Introsort 以快速排序开始，如果递归深度超过特定限制，它会切换到 Heapsort，以避免快速排序更糟糕的情况 O(N <sup>2</sup> )时间复杂度。当要排序的元素数量很少时，它也使用插入排序。
所以首先它创建一个分区。三种情况由此产生。

1.  如果分区大小有可能超过最大深度限制，则 Introsort 会切换到 Heapsort。我们将最大深度限制定义为 2*log(N)
2.  如果分区太小，则快速排序会衰减为插入排序。我们将这个截止值定义为 16(根据研究)。因此，如果分区大小小于 16，那么我们将进行插入排序。
3.  如果分区大小低于限制且不太小(即介于 16 和 2*log(N)之间)，则它会执行简单的快速排序。

**为什么比简单的快速排序好或者为什么需要 Introsort？**
由于快速排序可能会有更差的情况 O(N <sup>2</sup> )时间复杂度，并且还会增加递归堆栈空间(如果应用尾部递归，则为 O(log N))，因此为了避免所有这些情况，如果有更差情况的可能，我们需要将算法从快速排序切换到另一个。所以 Introsort 通过切换到 Heapsort 来解决这个问题。

同样由于较大的常数因子，当 N 足够小时，快速排序的性能甚至比 O(N2)排序算法差。因此，它切换到插入排序，以减少排序的运行时间。

此外，如果做了一个糟糕的枢轴选择，那么快速排序并不比冒泡排序做得好。

**为什么使用插入排序(而不是冒泡排序等)？**
插入排序具有以下优点。

1.  众所周知，插入排序是小数组中基于比较的最优排序算法。
2.  它有很好的参考价值
3.  这是一种自适应排序算法，即如果数组元素被部分排序，它的性能优于所有其他算法。

**为什么使用 Heapsort(而不是 Mergesort 等)？**
这完全是因为内存需求。合并排序需要 0(N)空间，而堆排序是一种就地 0(1)空间算法。

**分区大小在限制之下，为什么不用 Heapsort 代替 Quicksort？**
这个问题和为什么 Quicksort 普遍跑赢 Heapsort 一样？

答案是，虽然 Heapsort 平均也是 O(N log N)，最坏的情况下也是 O(1)空间，但当分区大小低于极限时，我们仍然不使用它，因为 Heapsort 中额外的隐藏常数因子比 Quicksort 大得多。

 **为什么从快速排序切换到插入排序的截止 16，从快速排序切换到堆排序的截止 2*logN？**
这些值是根据经验选择的近似值，因为进行了各种测试和研究。

```
/* A Program to sort the array using Introsort.
  The most popular C++ STL Algorithm- sort()
  uses Introsort. */

#include<bits/stdc++.h>
using namespace std;

// A utility function to swap the values pointed by
// the two pointers
void swapValue(int *a, int *b)
{
    int *temp = a;
    a = b;
    b = temp;
    return;
}

/* Function to sort an array using insertion sort*/
void InsertionSort(int arr[], int *begin, int *end)
{
    // Get the left and the right index of the subarray
    // to be sorted
    int left = begin - arr;
    int right = end - arr;

    for (int i = left+1; i <= right; i++)
    {
        int key = arr[i];
        int j = i-1;

       /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= left && arr[j] > key)
        {
            arr[j+1] = arr[j];
            j = j-1;
        }
        arr[j+1] = key;
   }

   return;
}

// A function to partition the array and return
// the partition point
int* Partition(int arr[], int low, int high)
{
    int pivot = arr[high];    // pivot
    int i = (low - 1);  // Index of smaller element

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller than or
        // equal to pivot
        if (arr[j] <= pivot)
        {
            // increment index of smaller element
            i++;

            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (arr + i + 1);
}

// A function that find the middle of the
// values pointed by the pointers a, b, c
// and return that pointer
int *MedianOfThree(int * a, int * b, int * c)
{
    if (*a < *b && *b < *c)
        return (b);

    if (*a < *c && *c <= *b)
        return (c);

    if (*b <= *a && *a < *c)
        return (a);

    if (*b < *c && *c <= *a)
        return (c);

    if (*c <= *a && *a < *b)
        return (a);

    if (*c <= *b && *b <= *a)
        return (b);
}

// A Utility function to perform intro sort
void IntrosortUtil(int arr[], int * begin,
                  int * end, int depthLimit)
{
    // Count the number of elements
    int size = end - begin;

      // If partition size is low then do insertion sort
    if (size < 16)
    {
        InsertionSort(arr, begin, end);
        return;
    }

    // If the depth is zero use heapsort
    if (depthLimit == 0)
    {
        make_heap(begin, end+1);
        sort_heap(begin, end+1);
        return;
    }

    // Else use a median-of-three concept to
    // find a good pivot
    int * pivot = MedianOfThree(begin, begin+size/2, end);

    // Swap the values pointed by the two pointers
    swapValue(pivot, end);

   // Perform Quick Sort
    int * partitionPoint = Partition(arr, begin-arr, end-arr);
    IntrosortUtil(arr, begin, partitionPoint-1, depthLimit - 1);
    IntrosortUtil(arr, partitionPoint + 1, end, depthLimit - 1);

    return;
}

/* Implementation of introsort*/
void Introsort(int arr[], int *begin, int *end)
{
    int depthLimit = 2 * log(end-begin);

    // Perform a recursive Introsort
    IntrosortUtil(arr, begin, end, depthLimit);

      return;
}

// A utility function ot print an array of size n
void printArray(int arr[], int n)
{
   for (int i=0; i < n; i++)
       printf("%d ", arr[i]);
   printf("\n");
}

// Driver program to test Introsort
int main()
{
    int arr[] = {3, 1, 23, -9, 233, 23, -313, 32, -9};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Pass the array, the pointer to the first element and
    // the pointer to the last element
    Introsort(arr, arr, arr+n-1);
    printArray(arr, n);

    return(0);
}
```

**Output:**

```
-313 -9 -9 1 3 23 23 32 233

```

 **intro sort 稳定吗？**
由于 Quicksort 也不稳定，所以 Introsort 也是<u>而不是</u>稳定。

**时间复杂度**
最佳情况-O(N log N)
平均情况- O(N log N)
较差情况- O(N log N)
其中，N =要排序的元素数量。

**辅助空间**
就像快速排序一样，可能会用到 O(log N)辅助递归栈空间。

[了解你的排序算法|集合 2 (Introsort- C++的排序武器)](https://www.geeksforgeeks.org/know-your-sorting-algorithm-set-2-introsort-cs-sorting-weapon/)

**参考**
[https://en . Wikipedia . org/wiki/intru rt](https://en.wikipedia.org/wiki/Introsort)

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论