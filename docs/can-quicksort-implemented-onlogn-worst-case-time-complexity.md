# 快速排序能否在 O(nLogn)最坏情况时间复杂度下实现？

> 原文:[https://www . geesforgeks . org/can-quick sort-implemented-onlogn-最坏情况-时间复杂度/](https://www.geeksforgeeks.org/can-quicksort-implemented-onlogn-worst-case-time-complexity/)

[快速排序](http://geeksquiz.com/quick-sort/)的典型实现的最坏情况时间复杂度是 O(n <sup>2</sup> )。当拾取的轴始终是一个极端(最小或最大)元素时，会出现最坏的情况。当输入数组被排序或反向排序，并且第一个或最后一个元素被选作透视时，就会出现这种情况。

尽管随机快速排序即使在对数组进行排序时也能很好地工作，但仍然有可能随机选取的元素总是极端的。最坏的情况可以简化为 O(nLogn)吗？

答案是肯定的，我们可以实现 O(nLogn)最坏的情况。这个想法是基于这样一个事实，即未排序数组的[中值元素可以在线性时间](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)中找到。所以我们先求中值，然后围绕中值元素对数组进行划分。
以下是基于上述思想的 C++实现。以下程序中的大部分函数都是从[未排序数组中第 K 个最小/最大元素|集合 3(最坏情况线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)复制而来的

## C++

```
/* A worst case O(nLogn) implementation of quicksort */
#include<cstring>
#include<iostream>
#include<algorithm>
#include<climits>
using namespace std;

// Following functions are taken from http://goo.gl/ih05BF
int partition(int arr[], int l, int r, int k);
int kthSmallest(int arr[], int l, int r, int k);

/* A O(nLogn) time complexity function for sorting arr[l..h] */
void quickSort(int arr[], int l, int h)
{
    if (l < h)
    {
        // Find size of current subarray
        int n = h-l+1;

        // Find median of arr[].
        int med = kthSmallest(arr, l, h, n/2);

        // Partition the array around median
        int p = partition(arr, l, h, med);

        // Recur for left and right of partition
        quickSort(arr, l, p - 1);
        quickSort(arr, p + 1, h);
    }
}

// A simple function to find median of arr[].  This is called
// only for an array of size 5 in this program.
int findMedian(int arr[], int n)
{
    sort(arr, arr+n);  // Sort the array
    return arr[n/2];   // Return middle element
}

// Returns k'th smallest element in arr[l..r] in worst case
// linear time. ASSUMPTION: ALL ELEMENTS IN ARR[] ARE DISTINCT
int kthSmallest(int arr[], int l, int r, int k)
{
    // If k is smaller than number of elements in array
    if (k > 0 && k <= r - l + 1)
    {
        int n = r-l+1; // Number of elements in arr[l..r]

        // Divide arr[] in groups of size 5, calculate median
        // of every group and store it in median[] array.
        int i, median[(n+4)/5]; // There will be floor((n+4)/5) groups;
        for (i=0; i<n/5; i++)
            median[i] = findMedian(arr+l+i*5, 5);
        if (i*5 < n) //For last group with less than 5 elements
        {
            median[i] = findMedian(arr+l+i*5, n%5);
            i++;
        }

        // Find median of all medians using recursive call.
        // If median[] has only one element, then no need
        // of recursive call
        int medOfMed = (i == 1)? median[i-1]:
                                 kthSmallest(median, 0, i-1, i/2);

        // Partition the array around a random element and
        // get position of pivot element in sorted array
        int pos = partition(arr, l, r, medOfMed);

        // If position is same as k
        if (pos-l == k-1)
            return arr[pos];
        if (pos-l > k-1)  // If position is more, recur for left
            return kthSmallest(arr, l, pos-1, k);

        // Else recur for right subarray
        return kthSmallest(arr, pos+1, r, k-pos+l-1);
    }

    // If k is more than number of elements in array
    return INT_MAX;
}

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// It searches for x in arr[l..r], and partitions the array
// around x.
int partition(int arr[], int l, int r, int x)
{
    // Search for x in arr[l..r] and move it to end
    int i;
    for (i=l; i<r; i++)
        if (arr[i] == x)
           break;
    swap(&arr[i], &arr[r]);

    // Standard partition algorithm
    i = l;
    for (int j = l; j <= r - 1; j++)
    {
        if (arr[j] <= x)
        {
            swap(&arr[i], &arr[j]);
            i++;
        }
    }
    swap(&arr[i], &arr[r]);
    return i;
}

/* Function to print an array */
void printArray(int arr[], int size)
{
    int i;
    for (i=0; i < size; i++)
        cout << arr[i] << " ";
    cout << endl;
}

// Driver program to test above functions
int main()
{
    int arr[] = {1000, 10, 7, 8, 9, 30, 900, 1, 5, 6, 20};
    int n = sizeof(arr)/sizeof(arr[0]);
    quickSort(arr, 0, n-1);
    cout << "Sorted array is\n";
    printArray(arr, n);
    return 0;
}
```

**输出:**

```
Sorted array is
1 5 6 7 8 9 10 20 30 900 1000
```

**快速排序在实践中是如何实现的——是否使用了上述方法？**
虽然上述方法的最坏情况时间复杂度为 O(nLogn)，但在实际实现中从未使用过。与普通快速排序相比，这种方法中的隐藏常数较高。以下是快速排序的实际实现中使用的一些技术。
1)随机选取以减少最坏情况发生的可能性(随机快速排序)
2)为小规模数组调用插入排序以减少递归调用。
3) QuickSort 是[尾递归](https://www.geeksforgeeks.org/tail-recursion/)，所以尾调用优化完成。

因此，上面讨论的方法更像是一种理论方法，具有 O(nLogn)最坏情况时间复杂度。

本文由**希瓦姆**整理。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息