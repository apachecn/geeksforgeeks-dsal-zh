# 3 向快速通道(荷兰国旗)

> 原文:[https://www . geesforgeks . org/3 路-quick sort-Dutch-national-flag/](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)

在[简单快速排序](http://geeksquiz.com/quick-sort/)算法中，我们选择一个元素作为轴，围绕一个轴对数组进行分区，并在轴的左右两边重复出现子数组。
考虑一个有许多冗余元素的阵列。例如，{1，4，2，4，2，4，1，2，4，1，2，2，2，2，4，1，4，4，4}。如果在简单快速排序中选择 4 作为轴心，我们只修复一个 4，并递归处理剩余的出现。
3 路快速排序的思想是处理枢轴的所有出现，并且基于[荷兰国旗算法。](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-and-2s/)

```
In 3 Way QuickSort, an array arr[l..r] is divided in 3 parts:
a) arr[l..i] elements less than pivot.
b) arr[i+1..j-1] elements equal to pivot.
c) arr[j..r] elements greater than pivot.
```

下面是上述算法的实现。

## C++

```
// C++ program for 3-way quick sort
#include <bits/stdc++.h>
using namespace std;

/* This function partitions a[] in three parts
   a) a[l..i] contains all elements smaller than pivot
   b) a[i+1..j-1] contains all occurrences of pivot
   c) a[j..r] contains all elements greater than pivot */
void partition(int a[], int l, int r, int& i, int& j)
{
    i = l - 1, j = r;
    int p = l - 1, q = r;
    int v = a[r];

    while (true) {
        // From left, find the first element greater than
        // or equal to v. This loop will definitely
        // terminate as v is last element
        while (a[++i] < v)
            ;

        // From right, find the first element smaller than
        // or equal to v
        while (v < a[--j])
            if (j == l)
                break;

        // If i and j cross, then we are done
        if (i >= j)
            break;

        // Swap, so that smaller goes on left greater goes
        // on right
        swap(a[i], a[j]);

        // Move all same left occurrence of pivot to
        // beginning of array and keep count using p
        if (a[i] == v) {
            p++;
            swap(a[p], a[i]);
        }

        // Move all same right occurrence of pivot to end of
        // array and keep count using q
        if (a[j] == v) {
            q--;
            swap(a[j], a[q]);
        }
    }

    // Move pivot element to its correct index
    swap(a[i], a[r]);

    // Move all left same occurrences from beginning
    // to adjacent to arr[i]
    j = i - 1;
    for (int k = l; k < p; k++, j--)
        swap(a[k], a[j]);

    // Move all right same occurrences from end
    // to adjacent to arr[i]
    i = i + 1;
    for (int k = r - 1; k > q; k--, i++)
        swap(a[i], a[k]);
}

// 3-way partition based quick sort
void quicksort(int a[], int l, int r)
{
    if (r <= l)
        return;

    int i, j;

    // Note that i and j are passed as reference
    partition(a, l, r, i, j);

    // Recur
    quicksort(a, l, j);
    quicksort(a, i, r);
}

// A utility function to print an array
void printarr(int a[], int n)
{
    for (int i = 0; i < n; ++i)
        printf("%d  ", a[i]);
    printf("\n");
}

// Driver code
int main()
{
    int a[] = { 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 };
    int size = sizeof(a) / sizeof(int);

      // Function Call
    printarr(a, size);
    quicksort(a, 0, size - 1);
    printarr(a, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for 3-way quick sort
import java.util.*;
class GFG
{

    static int i, j;

/* This function partitions a[] in three parts
   a) a[l..i] contains all elements smaller than pivot
   b) a[i+1..j-1] contains all occurrences of pivot
   c) a[j..r] contains all elements greater than pivot */
static void partition(int a[], int l, int r)
{

    i = l - 1; j = r;
    int p = l - 1, q = r;
    int v = a[r];

    while (true)
    {

        // From left, find the first element greater than
        // or equal to v. This loop will definitely
        // terminate as v is last element
        while (a[++i] < v)
            ;

        // From right, find the first element smaller than
        // or equal to v
        while (v < a[--j])
            if (j == l)
                break;

        // If i and j cross, then we are done
        if (i >= j)
            break;

        // Swap, so that smaller goes on left greater goes
        // on right
        int temp = a[i];
          a[i] = a[j];
          a[j] = temp;

        // Move all same left occurrence of pivot to
        // beginning of array and keep count using p
        if (a[i] == v) {
            p++;
            temp = a[i];
            a[i] = a[p];
            a[p] = temp;

        }

        // Move all same right occurrence of pivot to end of
        // array and keep count using q
        if (a[j] == v) {
            q--;
            temp = a[q];
            a[q] = a[j];
            a[j] = temp;
        }
    }

    // Move pivot element to its correct index
    int temp = a[i];
      a[i] = a[r];
      a[r] = temp;

    // Move all left same occurrences from beginning
    // to adjacent to arr[i]
    j = i - 1;
    for (int k = l; k < p; k++, j--)
    {
        temp = a[k];
          a[k] = a[j];
          a[j] = temp;
    }

    // Move all right same occurrences from end
    // to adjacent to arr[i]
    i = i + 1;
    for (int k = r - 1; k > q; k--, i++)
    {
        temp = a[i];
          a[i] = a[k];
          a[k] = temp;
    }
}

// 3-way partition based quick sort
static void quicksort(int a[], int l, int r)
{
    if (r <= l)
        return;

   i = 0; j = 0;

    // Note that i and j are passed as reference
    partition(a, l, r);

    // Recur
    quicksort(a, l, j);
    quicksort(a, i, r);
}

// A utility function to print an array
static void printarr(int a[], int n)
{
    for (int i = 0; i < n; ++i)
        System.out.printf("%d  ", a[i]);
    System.out.printf("\n");
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 };
    int size = a.length;

      // Function Call
    printarr(a, size);
    quicksort(a, 0, size - 1);
    printarr(a, size);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program for 3-way quick sort
using System;

class GFG {
    // A function which is used to swap values
    static void swap<T>(ref T lhs, ref T rhs)
    {
        T temp;
        temp = lhs;
        lhs = rhs;
        rhs = temp;
    }
    /* This function partitions a[] in three parts
       a) a[l..i] contains all elements smaller than pivot
       b) a[i+1..j-1] contains all occurrences of pivot
       c) a[j..r] contains all elements greater than pivot
     */
    public static void partition(int[] a, int l, int r,
                                 ref int i, ref int j)
    {
        i = l - 1;
        j = r;
        int p = l - 1, q = r;
        int v = a[r];

        while (true) {
            // From left, find the first element greater
            // than or equal to v. This loop will definitely
            // terminate as v is last element
            while (a[++i] < v)
                ;

            // From right, find the first element smaller
            // than or equal to v
            while (v < a[--j])
                if (j == l)
                    break;

            // If i and j cross, then we are done
            if (i >= j)
                break;

            // Swap, so that smaller goes on left greater
            // goes on right
            swap(ref a[i], ref a[j]);

            // Move all same left occurrence of pivot to
            // beginning of array and keep count using p
            if (a[i] == v) {
                p++;
                swap(ref a[p], ref a[i]);
            }

            // Move all same right occurrence of pivot to
            // end of array and keep count using q
            if (a[j] == v) {
                q--;
                swap(ref a[j], ref a[q]);
            }
        }

        // Move pivot element to its correct index
        swap(ref a[i], ref a[r]);

        // Move all left same occurrences from beginning
        // to adjacent to arr[i]
        j = i - 1;
        for (int k = l; k < p; k++, j--)
            swap(ref a[k], ref a[j]);

        // Move all right same occurrences from end
        // to adjacent to arr[i]
        i = i + 1;
        for (int k = r - 1; k > q; k--, i++)
            swap(ref a[i], ref a[k]);
    }

    // 3-way partition based quick sort
    public static void quicksort(int[] a, int l, int r)
    {
        if (r <= l)
            return;

        int i = 0, j = 0;

        // Note that i and j are passed as reference
        partition(a, l, r, ref i, ref j);

        // Recur
        quicksort(a, l, j);
        quicksort(a, i, r);
    }

    // A utility function to print an array
    public static void printarr(int[] a, int n)
    {
        for (int i = 0; i < n; ++i)
            Console.Write(a[i] + " ");
        Console.Write("\n");
    }

    // Driver code
    static void Main()
    {
        int[] a = { 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 };
        int size = a.Length;

          // Function Call
          printarr(a, size);
        quicksort(a, 0, size - 1);
        printarr(a, size);
    }
    // This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>
// javascript program for 3-way quick sort

    var i, j;

    /*
     * This function partitions a in three parts a) a[l..i] contains all elements
     * smaller than pivot b) a[i+1..j-1] contains all occurrences of pivot c)
     * a[j..r] contains all elements greater than pivot
     */
    function partition(a , l , r) {

        i = l - 1;
        j = r;
        var p = l - 1, q = r;
        var v = a[r];

        while (true) {

            // From left, find the first element greater than
            // or equal to v. This loop will definitely
            // terminate as v is last element
            while (a[++i] < v)
                ;

            // From right, find the first element smaller than
            // or equal to v
            while (v < a[--j])
                if (j == l)
                    break;

            // If i and j cross, then we are done
            if (i >= j)
                break;

            // Swap, so that smaller goes on left greater goes
            // on right
            var temp = a[i];
            a[i] = a[j];
            a[j] = temp;

            // Move all same left occurrence of pivot to
            // beginning of array and keep count using p
            if (a[i] == v) {
                p++;
                temp = a[i];
                a[i] = a[p];
                a[p] = temp;

            }

            // Move all same right occurrence of pivot to end of
            // array and keep count using q
            if (a[j] == v) {
                q--;
                temp = a[q];
                a[q] = a[j];
                a[j] = temp;
            }
        }

        // Move pivot element to its correct index
        var temp = a[i];
        a[i] = a[r];
        a[r] = temp;

        // Move all left same occurrences from beginning
        // to adjacent to arr[i]
        j = i - 1;
        for (k = l; k < p; k++, j--) {
            temp = a[k];
            a[k] = a[j];
            a[j] = temp;
        }

        // Move all right same occurrences from end
        // to adjacent to arr[i]
        i = i + 1;
        for (k = r - 1; k > q; k--, i++) {
            temp = a[i];
            a[i] = a[k];
            a[k] = temp;
        }
    }

    // 3-way partition based quick sort
    function quicksort(a , l , r) {
        if (r <= l)
            return;

        i = 0;
        j = 0;

        // Note that i and j are passed as reference
        partition(a, l, r);

        // Recur
        quicksort(a, l, j);
        quicksort(a, i, r);
    }

    // A utility function to print an array
    function printarr(a , n) {
        for (i = 0; i < n; ++i)
            document.write(" "+ a[i]);
        document.write("<br/>");
    }

    // Driver code   
        var a = [ 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 ];
        var size = a.length;

        // Function Call
        printarr(a, size);
        quicksort(a, 0, size - 1);
        printarr(a, size);
// This code contributed by aashish1995
</script>
```

## 蟒蛇 3

```
'''
This function partitions a[] in three parts
   a) a[first..start] contains all elements smaller than pivot
   b) a[start+1..mid-1] contains all occurrences of pivot
   c) a[mid..last] contains all elements greater than pivot

'''
def partition(arr, first, last, start, mid):

    pivot = arr[last]
    end = last

    # Iterate while mid is not greater than end.
    while (mid[0] <= end):

        # Inter Change position of element at the starting if it's value is less than pivot.
        if (arr[mid[0]] < pivot):

            arr[mid[0]], arr[start[0]] = arr[start[0]], arr[mid[0]]

            mid[0] = mid[0] + 1
            start[0] = start[0] + 1

        # Inter Change position of element at the end if it's value is greater than pivot.
        elif (arr[mid[0]] > pivot):

            arr[mid[0]], arr[end] = arr[end], arr[mid[0]]

            end = end - 1

        else:
            mid[0] = mid[0] + 1

# Function to sort the array elements in 3 cases
def quicksort(arr,first,last):
    # First case when an array contain only 1 element
    if (first >= last):
        return

    # Second case when an array contain only 2 elements
    if (last == first + 1):

        if (arr[first] > arr[last]):

            arr[first], arr[last] = arr[last], arr[first]

            return

    # Third case when an array contain more than 2 elements
    start = [first]
    mid = [first]

    # Function to partition the array.
    partition(arr, first, last, start, mid)

    # Recursively sort sublist containing elements that are less than the pivot.
    quicksort(arr, first, start[0] - 1)

    # Recursively sort sublist containing elements that are more than the pivot
    quicksort(arr, mid[0], last)

# Code Start from here
arr = [4,9,4,4,1,9,4,4,9,4,4,1,4]

# Call the quicksort function.
quicksort(arr,0,len(arr) - 1)

# print arr after sorting the elements
print(arr)
```

**Output**

```
4  9  4  4  1  9  4  4  9  4  4  1  4  
1  1  4  4  4  4  4  4  4  4  9  9  9  
```

**时间复杂度** : <u>O(N * log(N))</u>

其中“N”是给定数组/列表中的元素数量

对快速排序函数进行递归调用的平均次数是 log N，每次调用该函数时，我们都会遍历给定的数组/列表，这需要 O(N)个时间。因此，总时间复杂度为 O(N * log (N))。

**空间复杂度:** <u>O(对数 N)</u>

其中“N”是给定数组/列表中的元素数量。

感谢 [Utkarsh](http://qa.geeksforgeeks.org/user/utkarsh111) 提出以上实施建议。

另一个使用[荷兰国旗算法](https://www.geeksforgeeks.org/sort-an-array-of-0s-1s-and-2s/)的实现

## C++

```
// C++ program for 3-way quick sort
#include <bits/stdc++.h>
using namespace std;

void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// A utility function to print an array
void printarr(int a[], int n)
{
    for (int i = 0; i < n; ++i)
        printf("%d ", a[i]);
    printf("\n");
}

/* This function partitions a[] in three parts
a) a[l..i] contains all elements smaller than pivot
b) a[i+1..j-1] contains all occurrences of pivot
c) a[j..r] contains all elements greater than pivot */

// It uses Dutch National Flag Algorithm
void partition(int a[], int low, int high, int& i, int& j)
{
    // To handle 2 elements
    if (high - low <= 1) {
        if (a[high] < a[low])
            swap(&a[high], &a[low]);
        i = low;
        j = high;
        return;
    }

    int mid = low;
    int pivot = a[high];
    while (mid <= high) {
        if (a[mid] < pivot)
            swap(&a[low++], &a[mid++]);
        else if (a[mid] == pivot)
            mid++;
        else if (a[mid] > pivot)
            swap(&a[mid], &a[high--]);
    }

    // update i and j
    i = low - 1;
    j = mid; // or high+1
}

// 3-way partition based quick sort
void quicksort(int a[], int low, int high)
{
    if (low >= high) // 1 or 0 elements
        return;

    int i, j;

    // Note that i and j are passed as reference
    partition(a, low, high, i, j);

    // Recur two halves
    quicksort(a, low, i);
    quicksort(a, j, high);
}

// Driver Code
int main()
{
    int a[] = { 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 };
    // int a[] = {4, 39, 54, 14, 31, 89, 44, 34, 59, 64, 64,
    // 11, 41}; int a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    // int a[] = {91, 82, 73, 64, 55, 46, 37, 28, 19, 10};
    // int a[] = {4, 9, 4, 4, 9, 1, 1, 1};
    int size = sizeof(a) / sizeof(int);

    // Function Call
    printarr(a, size);
    quicksort(a, 0, size - 1);
    printarr(a, size);
    return 0;
}
```

## C#

```
// C# program for 3-way quick sort
using System;

class GFG {
    // A function which is used to swap values
    static void swap<T>(ref T lhs, ref T rhs)
    {
        T temp;
        temp = lhs;
        lhs = rhs;
        rhs = temp;
    }

    // A utility function to print an array
    public static void printarr(int[] a, int n)
    {
        for (int i = 0; i < n; ++i)
            Console.Write(a[i] + " ");
        Console.Write("\n");
    }

    /* This function partitions a[] in three parts
    a) a[l..i] contains all elements smaller than pivot
    b) a[i+1..j-1] contains all occurrences of pivot
    c) a[j..r] contains all elements greater than pivot */

    // It uses Dutch National Flag Algorithm
    public static void partition(int[] a, int low, int high,
                                 ref int i, ref int j)
    {
        // To handle 2 elements
        if (high - low <= 1) {
            if (a[high] < a[low])
                swap(ref a[high], ref a[low]);
            i = low;
            j = high;
            return;
        }

        int mid = low;
        int pivot = a[high];
        while (mid <= high) {
            if (a[mid] < pivot)
                swap(ref a[low++], ref a[mid++]);
            else if (a[mid] == pivot)
                mid++;
            else if (a[mid] > pivot)
                swap(ref a[mid], ref a[high--]);
        }

        // update i and j
        i = low - 1;
        j = mid; // or high+1
    }

    // 3-way partition based quick sort
    public static void quicksort(int[] a, int low, int high)
    {
        if (low >= high) // 1 or 0 elements
            return;

        int i = 0, j = 0;

        // Note that i and j are passed as reference
        partition(a, low, high, ref i, ref j);

        // Recur two halves
        quicksort(a, low, i);
        quicksort(a, j, high);
    }

    // Driver code
    static void Main()
    {
        int[] a = { 4, 9, 4, 4, 1, 9, 4, 4, 9, 4, 4, 1, 4 };
        // int[] a = {4, 39, 54, 14, 31, 89, 44, 34, 59, 64,
        // 64, 11, 41}; int[] a = {1, 2, 3, 4, 5, 6, 7, 8, 9,
        // 10}; int[] a = {91, 82, 73, 64, 55, 46, 37, 28,
        // 19, 10}; int[] a = {4, 9, 4, 4, 9, 1, 1, 1};
        int size = a.Length;

          // Function Call
        printarr(a, size);
        quicksort(a, 0, size - 1);
        printarr(a, size);
    }
    // This code is contributed by DrRoot_
}
```

**Output**

```
4 9 4 4 1 9 4 4 9 4 4 1 4 
1 1 4 4 4 4 4 4 4 4 9 9 9 
```

感谢 [Aditya Goel](http://qa.geeksforgeeks.org/user/aditya.goel) 的这个实现。
**参考:**
[http://alg S4 . cs . Princeton . edu/讲课/23 demo partitioning . pdf](http://algs4.cs.princeton.edu/lectures/23DemoPartitioning.pdf)
[http://www.sorting-algorithms.com/quick-sort-3-way](http://www.sorting-algorithms.com/quick-sort-3-way)
如发现有不正确的地方，或想分享更多关于以上讨论话题的信息，请写评论。