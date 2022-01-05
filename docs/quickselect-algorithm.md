# 快速选择算法

> 原文:[https://www.geeksforgeeks.org/quickselect-algorithm/](https://www.geeksforgeeks.org/quickselect-algorithm/)

[快速选择](https://en.wikipedia.org/wiki/Quickselect)是一种在无序列表中寻找第 k 个最小元素的选择算法。与[快速排序](https://www.geeksforgeeks.org/quick-sort/)排序算法有关。
**例:**

```
Input: arr[] = {7, 10, 4, 3, 20, 15}
           k = 3
Output: 7

Input: arr[] = {7, 10, 4, 3, 20, 15}
           k = 4
Output: 10
```

算法类似于快速排序。不同的是，它不是在两侧重复出现(找到枢轴后)，而是只在包含第 k 个最小元素的部分重复出现。逻辑很简单，如果分区元素的索引大于 k，那么我们对左边部分进行递归。如果索引与 k 相同，我们找到了第 k 个最小的元素，然后返回。如果指数小于 k，那么我们对右半部分重复。这将预期的复杂性从 O(n log n)降低到 O(n)，最坏的情况是 O(n^2).

```
function quickSelect(list, left, right, k)

   if left = right
      return list[left]

   Select a pivotIndex between left and right

   pivotIndex := partition(list, left, right, 
                                  pivotIndex)
   if k = pivotIndex
      return list[k]
   else if k < pivotIndex
      right := pivotIndex - 1
   else
      left := pivotIndex + 1 
```

## C++14

```
// CPP program for implementation of QuickSelect
#include <bits/stdc++.h>
using namespace std;

// Standard partition process of QuickSort().
// It considers the last element as pivot
// and moves all smaller element to left of
// it and greater elements to right
int partition(int arr[], int l, int r)
{
    int x = arr[r], i = l;
    for (int j = l; j <= r - 1; j++) {
        if (arr[j] <= x) {
            swap(arr[i], arr[j]);
            i++;
        }
    }
    swap(arr[i], arr[r]);
    return i;
}

// This function returns k'th smallest
// element in arr[l..r] using QuickSort
// based method.  ASSUMPTION: ALL ELEMENTS
// IN ARR[] ARE DISTINCT
int kthSmallest(int arr[], int l, int r, int k)
{
    // If k is smaller than number of
    // elements in array
    if (k > 0 && k <= r - l + 1) {

        // Partition the array around last
        // element and get position of pivot
        // element in sorted array
        int index = partition(arr, l, r);

        // If position is same as k
        if (index - l == k - 1)
            return arr[index];

        // If position is more, recur
        // for left subarray
        if (index - l > k - 1)
            return kthSmallest(arr, l, index - 1, k);

        // Else recur for right subarray
        return kthSmallest(arr, index + 1, r,
                            k - index + l - 1);
    }

    // If k is more than number of
    // elements in array
    return INT_MAX;
}

// Driver program to test above methods
int main()
{
    int arr[] = { 10, 4, 5, 8, 6, 11, 26 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    cout << "K-th smallest element is "
        << kthSmallest(arr, 0, n - 1, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of Quick Select
import java.util.Arrays;

class GFG {

    // partition function similar to quick sort
    // Considers last element as pivot and adds
    // elements with less value to the left and
    // high value to the right and also changes
    // the pivot position to its respective position
    // in the final array.
    public static int partition(int[] arr, int low,
                                int high)
    {
        int pivot = arr[high], pivotloc = low;
        for (int i = low; i <= high; i++) {
            // inserting elements of less value
            // to the left of the pivot location
            if (arr[i] < pivot) {
                int temp = arr[i];
                arr[i] = arr[pivotloc];
                arr[pivotloc] = temp;
                pivotloc++;
            }
        }

        // swapping pivot to the final pivot location
        int temp = arr[high];
        arr[high] = arr[pivotloc];
        arr[pivotloc] = temp;

        return pivotloc;
    }

    // finds the kth position (of the sorted array)
    // in a given unsorted array i.e this function
    // can be used to find both kth largest and
    // kth smallest element in the array.
    // ASSUMPTION: all elements in arr[] are distinct
    public static int kthSmallest(int[] arr, int low,
                                  int high, int k)
    {
        // find the partition
        int partition = partition(arr, low, high);

        // if partition value is equal to the kth position,
        // return value at k.
        if (partition == k - 1)
            return arr[partition];

        // if partition value is less than kth position,
        // search right side of the array.
        else if (partition < k - 1)
            return kthSmallest(arr, partition + 1, high, k);

        // if partition value is more than kth position,
        // search left side of the array.
        else
            return kthSmallest(arr, low, partition - 1, k);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] array = new int[] { 10, 4, 5, 8, 6, 11, 26 };
        int[] arraycopy
            = new int[] { 10, 4, 5, 8, 6, 11, 26 };

        int kPosition = 3;
        int length = array.length;

        if (kPosition > length) {
            System.out.println("Index out of bound");
        }
        else {
            // find kth smallest value
            System.out.println(
                "K-th smallest element in array : "
                + kthSmallest(arraycopy, 0, length - 1,
                              kPosition));
        }
    }
}

// This code is contributed by Saiteja Pamulapati
```

## 蟒蛇 3

```
# Python3 program of Quick Select

# Standard partition process of QuickSort().
# It considers the last element as pivot
# and moves all smaller element to left of
# it and greater elements to right
def partition(arr, l, r):

    x = arr[r]
    i = l
    for j in range(l, r):

        if arr[j] <= x:
            arr[i], arr[j] = arr[j], arr[i]
            i += 1

    arr[i], arr[r] = arr[r], arr[i]
    return i

# finds the kth position (of the sorted array)
# in a given unsorted array i.e this function
# can be used to find both kth largest and
# kth smallest element in the array.
# ASSUMPTION: all elements in arr[] are distinct
def kthSmallest(arr, l, r, k):

    # if k is smaller than number of
    # elements in array
    if (k > 0 and k <= r - l + 1):

        # Partition the array around last
        # element and get position of pivot
        # element in sorted array
        index = partition(arr, l, r)

        # if position is same as k
        if (index - l == k - 1):
            return arr[index]

        # If position is more, recur
        # for left subarray
        if (index - l > k - 1):
            return kthSmallest(arr, l, index - 1, k)

        # Else recur for right subarray
        return kthSmallest(arr, index + 1, r,
                            k - index + l - 1)
    print("Index out of bound")

# Driver Code
arr = [ 10, 4, 5, 8, 6, 11, 26 ]
n = len(arr)
k = 3
print("K-th smallest element is ", end = "")
print(kthSmallest(arr, 0, n - 1, k))

# This code is contributed by Muskan Kalra.
```

## C#

```
// C# program of Quick Select
using System;

class GFG
{

    // partition function similar to quick sort
    // Considers last element as pivot and adds
    // elements with less value to the left and
    // high value to the right and also changes
    // the pivot position to its respective position
    // in the readonly array.
    static int partitions(int []arr,int low, int high)
    {
        int pivot = arr[high], pivotloc = low, temp;
        for (int i = low; i <= high; i++)
        {
            // inserting elements of less value
            // to the left of the pivot location
            if(arr[i] < pivot)
            {        
                temp = arr[i];
                arr[i] = arr[pivotloc];
                arr[pivotloc] = temp;
                pivotloc++;
            }
        }

        // swapping pivot to the readonly pivot location
        temp = arr[high];
        arr[high] = arr[pivotloc];
        arr[pivotloc] = temp;

        return pivotloc;
    }

    // finds the kth position (of the sorted array)
    // in a given unsorted array i.e this function
    // can be used to find both kth largest and
    // kth smallest element in the array.
    // ASSUMPTION: all elements in []arr are distinct
    static int kthSmallest(int[] arr, int low,
                                int high, int k)
    {
        // find the partition
        int partition = partitions(arr,low,high);

        // if partition value is equal to the kth position,
        // return value at k.
        if(partition == k)
            return arr[partition];

        // if partition value is less than kth position,
        // search right side of the array.
        else if(partition < k )
            return kthSmallest(arr, partition + 1, high, k );

        // if partition value is more than kth position,
        // search left side of the array.
        else
            return kthSmallest(arr, low, partition - 1, k );        
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] array = {10, 4, 5, 8, 6, 11, 26};
        int[] arraycopy = {10, 4, 5, 8, 6, 11, 26};

        int kPosition = 3;
        int length = array.Length;

        if(kPosition > length)
        {
            Console.WriteLine("Index out of bound");
        }
        else
        {
            // find kth smallest value
            Console.WriteLine("K-th smallest element in array : " +
                                kthSmallest(arraycopy, 0, length - 1,
                                                        kPosition - 1));
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program of Quick Select

// partition function similar to quick sort
    // Considers last element as pivot and adds
    // elements with less value to the left and
    // high value to the right and also changes
    // the pivot position to its respective position
    // in the final array.
function _partition(arr, low, high)
{
    let pivot = arr[high], pivotloc = low;
        for (let i = low; i <= high; i++)
        {

            // inserting elements of less value
            // to the left of the pivot location
            if (arr[i] < pivot)
            {
                let temp = arr[i];
                arr[i] = arr[pivotloc];
                arr[pivotloc] = temp;
                pivotloc++;
            }
        }

        // swapping pivot to the final pivot location
        let temp = arr[high];
        arr[high] = arr[pivotloc];
        arr[pivotloc] = temp;

        return pivotloc;
}

// finds the kth position (of the sorted array)
    // in a given unsorted array i.e this function
    // can be used to find both kth largest and
    // kth smallest element in the array.
    // ASSUMPTION: all elements in arr[] are distinct
function kthSmallest(arr, low, high, k)
{

    // find the partition
        let partition = _partition(arr, low, high);

        // if partition value is equal to the kth position,
        // return value at k.
        if (partition == k - 1)
            return arr[partition];

        // if partition value is less than kth position,
        // search right side of the array.
        else if (partition < k - 1)
            return kthSmallest(arr, partition + 1, high, k);

        // if partition value is more than kth position,
        // search left side of the array.
        else
            return kthSmallest(arr, low, partition - 1, k);
}

// Driver Code
let array = [ 10, 4, 5, 8, 6, 11, 26];
let arraycopy = [10, 4, 5, 8, 6, 11, 26 ];
let kPosition = 3;
let length = array.length;

if (kPosition > length) {
    document.write("Index out of bound<br>");
}
else
{

// find kth smallest value
document.write(
"K-th smallest element in array : "
+ kthSmallest(arraycopy, 0, length - 1,
              kPosition)+"<br>");
}

// This code is contributed by rag2127
</script>
```

**输出:**

```
K-th smallest element is 6
```

**要点:**

1.  像 quicksort 一样，它在实践中速度很快，但最坏情况下的性能很差。它用于
2.  分区过程与快速排序相同，只是递归代码不同。
3.  有一种算法可以在最差 cas e 中找到 O(n)中的第 k 个最小元素[，但快速选择的平均性能更好。](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/) 

相关 C++函数:[STD::n th _ element in c++](https://www.geeksforgeeks.org/stdnth_element-in-cpp/)
本文由 [Sahil Chhabra](https://www.facebook.com/sahil.chhabra.965) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。