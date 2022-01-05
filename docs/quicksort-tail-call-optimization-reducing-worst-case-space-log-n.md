# 快速排序尾呼优化(将最坏情况空间减少到日志 n )

> 原文:[https://www . geesforgeks . org/quick sort-tail-call-optimization-reducing-最坏情况-space-log-n/](https://www.geeksforgeeks.org/quicksort-tail-call-optimization-reducing-worst-case-space-log-n/)

**先决条件:** [尾呼淘汰](https://www.geeksforgeeks.org/tail-call-elimination/)

在[快速排序](http://geeksquiz.com/quick-sort/)中，分区函数已经就位，但是我们需要额外的空间来进行递归函数调用。快速排序的一个简单实现对自身进行两次调用，在最坏的情况下，需要函数调用堆栈上有 O(n)个空间。

最糟糕的情况发生在选定的轴总是划分数组，使得一部分有 0 个元素，另一部分有 n-1 个元素。例如，在下面的代码中，如果我们选择最后一个元素作为轴心，我们会得到排序数组的最坏情况(可视化见[这个](http://www.cs.nthu.edu.tw/~wkhon/algo08-tutorials/tutorial2b.pdf)

## C

```
/* A Simple implementation of QuickSort that makes two
   two recursive calls. */
void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
// See below link for complete running code
// http://geeksquiz.com/quick-sort/
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple implementation of QuickSort that
// makes two recursive calls.
static void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {

        // pi is partitioning index, arr[p] is
        // now at right place
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach
def quickSort(arr, low, high):

    if (low < high):

        # pi is partitioning index, arr[p] is now
        # at right place
        pi = partition(arr, low, high)

        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi - 1)
        quickSort(arr, pi + 1, high)

# This code is contributed by sanjoy_62
```

## C#

```
// A Simple implementation of QuickSort that
// makes two recursive calls.
static void quickSort(int []arr, int low, int high)
{
    if (low < high)
    {

        // pi is partitioning index, arr[p] is
        // now at right place
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// This code is contributed by pratham76.
```

## java 描述语言

```
<script>
// A Simple implementation of QuickSort that
// makes two recursive calls.
function quickSort(arr , low , high)
{
    if (low < high)
    {

        // pi is partitioning index, arr[p] is
        // now at right place
        var pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

// This code is contributed by umadevi9616.
</script>
```

**能不能减少函数调用栈的辅助空间？**
我们可以把辅助空间限制为 O(Log n)。这个想法是基于[尾叫淘汰](https://www.geeksforgeeks.org/tail-call-elimination/)。正如在[之前的帖子](https://www.geeksforgeeks.org/tail-call-elimination/)中看到的，我们可以转换代码，使其进行一次递归调用。例如，在下面的代码中，我们将上面的代码转换为使用 while 循环，并减少了递归调用的数量。

## C

```
/* QuickSort after tail call elimination using while loop */
void quickSort(int arr[], int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);

        low = pi+1;
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/qrlM31
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* QuickSort after tail call elimination using while loop */
static void quickSort(int arr[], int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);

        low = pi+1;
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/qrlM31

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# QuickSort after tail call elimination using while loop '''
def quickSort(arr, low, high):
    while (low < high):

        # pi is partitioning index, arr[p] is now
        #  at right place '''
        pi = partition(arr, low, high)

        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi - 1)

        low = pi+1

# See below link for complete running code
# https:#ide.geeksforgeeks.org/qrlM31

# This code is contributed by gauravrajput1
```

## C#

```
/* QuickSort after tail call elimination using while loop */
static void quickSort(int []arr, int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);

        low = pi+1;
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/qrlM31

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>
/* QuickSort after tail call elimination using while loop */
function quickSort(arr , low , high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        var pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);

        low = pi+1;
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/qrlM31

// This code is contributed by gauravrajput1
</script>
```

虽然我们减少了递归调用的次数，但在最坏的情况下，上面的代码仍然可以使用 O(n)个辅助空间。在最坏的情况下，有可能数组的第一部分总是有 n-1 个元素。例如，当最后一个元素被选择为透视元素并且数组按降序排序时，可能会发生这种情况。

我们可以优化上面的代码，只对分区后的较小部分进行递归调用。下面是这个想法的实现。

**进一步优化:**

## C

```
/* This QuickSort requires O(Log n) auxiliary space in
   worst case. */
void quickSort(int arr[], int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // If left part is smaller, then recur for left
        // part and handle right part iteratively
        if (pi - low < high - pi)
        {
            quickSort(arr, low, pi - 1);
            low = pi + 1;
        }

        // Else recur for right part
        else
        {
            quickSort(arr, pi + 1, high);
            high = pi - 1;
        }
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/LHxwPk
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* This QuickSort requires O(Log n) auxiliary space in
   worst case. */
static void quickSort(int arr[], int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // If left part is smaller, then recur for left
        // part and handle right part iteratively
        if (pi - low < high - pi)
        {
            quickSort(arr, low, pi - 1);
            low = pi + 1;
        }

        // Else recur for right part
        else
        {
            quickSort(arr, pi + 1, high);
            high = pi - 1;
        }
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/LHxwPk

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
''' This QuickSort requires O(Log n) auxiliary space in
   worst case. '''
def quickSort(arr, low, high)
{
    while (low < high):
        ''' pi is partitioning index, arr[p] is now
           at right place '''
        pi = partition(arr, low, high);

        # If left part is smaller, then recur for left
        # part and handle right part iteratively
        if (pi - low < high - pi):
            quickSort(arr, low, pi - 1);
            low = pi + 1;

        # Else recur for right part
        else:
            quickSort(arr, pi + 1, high);
            high = pi - 1;

# See below link for complete running code
# https:#ide.geeksforgeeks.org/LHxwPk

# This code is contributed by gauravrajput1
```

## C#

```
/* This QuickSort requires O(Log n) auxiliary space in
   worst case. */
static void quickSort(int []arr, int low, int high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // If left part is smaller, then recur for left
        // part and handle right part iteratively
        if (pi - low < high - pi)
        {
            quickSort(arr, low, pi - 1);
            low = pi + 1;
        }

        // Else recur for right part
        else
        {
            quickSort(arr, pi + 1, high);
            high = pi - 1;
        }
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/LHxwPk

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
/* This QuickSort requires O(Log n) auxiliary space in
   worst case. */
function quickSort(arr , low , high)
{
    while (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        var pi = partition(arr, low, high);

        // If left part is smaller, then recur for left
        // part and handle right part iteratively
        if (pi - low < high - pi)
        {
            quickSort(arr, low, pi - 1);
            low = pi + 1;
        }

        // Else recur for right part
        else
        {
            quickSort(arr, pi + 1, high);
            high = pi - 1;
        }
    }
}
// See below link for complete running code
// https://ide.geeksforgeeks.org/LHxwPk

// This code contributed by gauravrajput1
</script>
```

在上面的代码中，如果左半部分变小，那么我们对左半部分进行递归调用。其他合适的部分。在最坏的情况下(对于空间)，当两个部分在所有递归调用中大小相等时，我们使用 O(Log n)额外空间。

**参考:**
[http://www . cs . nthu . edu . tw/~ wk hon/algo 08-tutorial2b . pdf](http://www.cs.nthu.edu.tw/~wkhon/algo08-tutorials/tutorial2b.pdf)

本文由 **Dheeraj Jain** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息