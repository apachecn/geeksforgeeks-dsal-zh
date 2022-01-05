# 二进制插入排序

> 原文:[https://www.geeksforgeeks.org/binary-insertion-sort/](https://www.geeksforgeeks.org/binary-insertion-sort/)

我们可以使用二分搜索法减少[正常插入排序](https://www.geeksforgeeks.org/insertion-sort/)中的比较次数。二进制插入排序在每次迭代中使用二分搜索法查找插入所选项目的正确位置。
在正常的插入排序中，最坏的情况下需要 O(n)次比较(第 n 次迭代)。我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)将其减少到 0(log n)。

## C++

```
// C program for implementation of
// binary insertion sort
#include <iostream>
using namespace std;

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    cout <<"Sorted array: \n";
    for (i = 0; i < n; i++)
        cout <<" "<< a[i];

    return 0;
}

// this code is contribution by shivanisinghss2110
```

## C

```
// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                 int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program implementing
// binary insertion sort

import java.util.Arrays;
class GFG
{

    public static void main(String[] args)
    {
        final int[] arr = { 37, 23, 0,   17, 12, 72,
                            31, 46, 100, 88, 54 };

        new GFG().sort(arr);

        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver Code
    public void sort(int array[])
    {
        for (int i = 1; i < array.length; i++)
        {
            int x = array[i];

            // Find location to insert
            // using binary search
            int j = Math.abs(
                Arrays.binarySearch(array, 0,
                                    i, x) + 1);

            // Shifting array to one
            // location right
            System.arraycopy(array, j,
                             array, j + 1, i - j);

            // Placing element at its
            // correct location
            array[j] = x;
        }
    }
}

// Code contributed by Mohit Gupta_OMG
```

## 计算机编程语言

```
# Python Program implementation
# of binary insertion sort

def binary_search(arr, val, start, end):

    # we need to distinugish whether we
    # should insert before or after the
    # left boundary. imagine [0] is the last
    # step of the binary search and we need
    # to decide where to insert -1
    if start == end:
        if arr[start] > val:
            return start
        else:
            return start+1

    # this occurs if we are moving
    # beyond left's boundary meaning
    # the left boundary is the least
    # position to find a number greater than val
    if start > end:
        return start

    mid = (start+end)//2
    if arr[mid] < val:
        return binary_search(arr, val, mid+1, end)
    elif arr[mid] > val:
        return binary_search(arr, val, start, mid-1)
    else:
        return mid

def insertion_sort(arr):
    for i in range(1, len(arr)):
        val = arr[i]
        j = binary_search(arr, val, 0, i-1)
        arr = arr[:j] + [val] + arr[j:i] + arr[i+1:]
    return arr

print("Sorted array:")
print(insertion_sort([37, 23, 0, 31, 22, 17, 12, 72, 31, 46, 100, 88, 54]))

# Code contributed by Mohit Gupta_OMG
```

## C#

```
// C# Program implementing
// binary insertion sort
using System;

class GFG {

    public static void Main()
    {
        int[] arr = { 37, 23, 0,   17, 12, 72,
                      31, 46, 100, 88, 54 };

        sort(arr);

        for (int i = 0; i < arr.Length; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void sort(int[] array)
    {
        for (int i = 1; i < array.Length; i++)
        {
            int x = array[i];

            // Find location to insert using
            // binary search
            int j = Math.Abs(
                Array.BinarySearch(array,
                                   0, i, x) + 1);

            // Shifting array to one location right
            System.Array.Copy(array, j,
                              array, j + 1,
                              i - j);

            // Placing element at its correct
            // location
            array[j] = x;
        }
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for implementation of
// binary insertion sort

// A binary search based function to find
// the position where item should be
// inserted in a[low..high]
function binarySearch($a, $item, $low, $high)
{

    if ($high <= $low)
        return ($item > $a[$low]) ?
                       ($low + 1) : $low;

    $mid = (int)(($low + $high) / 2);

    if($item == $a[$mid])
        return $mid + 1;

    if($item > $a[$mid])
        return binarySearch($a, $item,
                            $mid + 1, $high);

    return binarySearch($a, $item, $low,
                            $mid - 1);
}

// Function to sort an array a of size 'n'
function insertionSort(&$a, $n)
{
    $i; $loc; $j; $k; $selected;

    for ($i = 1; $i < $n; ++$i)
    {
        $j = $i - 1;
        $selected = $a[$i];

        // find location where selected
        // item should be inserted
        $loc = binarySearch($a, $selected, 0, $j);

        // Move all elements after location
        // to create space
        while ($j >= $loc)
        {
            $a[$j + 1] = $a[$j];
            $j--;
        }
        $a[$j + 1] = $selected;
    }
}

// Driver Code
$a = array(37, 23, 0, 17, 12, 72,
           31, 46, 100, 88, 54);

$n = sizeof($a);

insertionSort($a, $n);

echo "Sorted array:\n";
for ($i = 0; $i < $n; $i++)
    echo "$a[$i] ";

// This code is contributed by
// Adesh Singh
?>
```

## java 描述语言

```
<script>
// Javascript Program implementing
// binary insertion sort

function binarySearch(a, item, low, high)
{

    if (high <= low)
        return (item > a[low]) ?
                       (low + 1) : low;

    mid = Math.floor((low + high) / 2);

    if(item == a[mid])
        return mid + 1;

    if(item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);

    return binarySearch(a, item, low,
                            mid - 1);
}

function sort(array)
{
    for (let i = 1; i < array.length; i++)
        {
            let j = i - 1;
            let x = array[i];

            // Find location to insert
            // using binary search
            let loc = Math.abs(
                binarySearch(array, x,
                                    0, j));

            // Shifting array to one
            // location right

            while (j >= loc)
            {
                array[j + 1] = array[j];
                j--;
            }

            // Placing element at its
            // correct location
            array[j+1] = x;
        }
}

// Driver Code
let arr=[ 37, 23, 0,   17, 12, 72,
                            31, 46, 100, 88, 54];
sort(arr);

for (let i = 0; i < arr.length; i++)
    document.write(arr[i] + " ");

// This code is contributed by unknown2108
</script>
// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    r// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    // C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);
// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);// C program for implementation of
// binary insertion sort
#include <stdio.h>

// A binary search based function
// to find the position
// where item should be inserted
// in a[low..high]
int binarySearch(int a[], int item,
                int low, int high)
{
    if (high <= low)
        return (item > a[low]) ?
                (low + 1) : low;

    int mid = (low + high) / 2;

    if (item == a[mid])
        return mid + 1;

    if (item > a[mid])
        return binarySearch(a, item,
                            mid + 1, high);
    return binarySearch(a, item, low,
                        mid - 1);
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i])
```

**Output**

```
Sorted array: 
0 12 17 23 31 37 46 54 72 88 100 
```

**时间复杂度:**由于每次插入都需要一系列的交换，算法整体上仍然有一个运行最坏情况运行时间 O(n <sup>2</sup> )。

另一种方法:下面是上述递归代码的迭代实现

## C++

```
#include <iostream>
using namespace std;

// iterative implementation
int binarySearch(int a[], int item, int low, int high)
{
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (item == a[mid])
            return mid + 1;
        else if (item > a[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i) {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    cout <<"Sorted array: \n";
    for (i = 0; i < n; i++)
        cout <<" "<< a[i];

    return 0;
}

// This code is contributed by shivanisinghss2110.
```

## C

```
#include <stdio.h>

// iterative implementation
int binarySearch(int a[], int item, int low, int high)
{
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (item == a[mid])
            return mid + 1;
        else if (item > a[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}

// Function to sort an array a[] of size 'n'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i) {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
int main()
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = sizeof(a) / sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
// contributed by tmeid
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {

// iterative implementation
static int binarySearch(int a[], int item, int low, int high)
{
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (item == a[mid])
            return mid + 1;
        else if (item > a[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}

// Function to sort an array a[] of size 'n'
static void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i) {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
public static void main (String[] args)
{
    int a[]
        = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = a.length, i;

    insertionSort(a, n);

    System.out.println("Sorted array:");
    for (i = 0; i < n; i++)
        System.out.print(a[i] +" ");

}
}

// This code is contributed by shivanisinghss2110.
```

## 蟒蛇 3

```
# iterative implementation
def binarySearch(a, item, low, high):
    while (low <= high):
        mid = low + (high - low) // 2
        if (item == a[mid]):
            return mid + 1
        elif (item > a[mid]):
            low = mid + 1
        else:
            high = mid - 1
    return low

# Function to sort an array a[] of size 'n'
def insertionSort(a, n):
    for i in range (n):
        j = i - 1
        selected = a[i]

        # find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j)

        # Move all elements after location to create space
        while (j >= loc):
            a[j + 1] = a[j]
            j-=1
        a[j + 1] = selected

# Driver Code
a = [37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54]
n = len(a)
insertionSort(a, n)
print("Sorted array: ")
for i in range (n):
    print(a[i], end=" ")

# This code is contributed by shivanisinghss2110
```

## C#

```
using System;

class GFG {

// iterative implementation
static int binarySearch(int []a, int item, int low, int high)
{
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (item == a[mid])
            return mid + 1;
        else if (item > a[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}

// Function to sort an array a[] of size 'n'
static void insertionSort(int []a, int n)
{
    int i, loc, j, selected;

    for (i = 1; i < n; ++i) {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
public static void Main (String[] args)
{
    int []a = { 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 };
    int n = a.Length, i;

    insertionSort(a, n);

    Console.WriteLine("Sorted array:");
    for (i = 0; i < n; i++)
        Console.Write(a[i] +" ");

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// iterative implementation
function binarySearch( a,  item,  low,  high)
{
    while (low <= high) {
        var mid = low + (high - low) / 2;
        if (item == a[mid])
            return mid + 1;
        else if (item > a[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }

    return low;
}

// Function to sort an array a[] of size 'n'
function insertionSort(a, n)
{
    var i, loc, j, k, selected;

    for (i = 1; i < n; ++i) {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inseretd
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = selected;
    }
}

// Driver Code
    var a = [ 37, 23, 0, 17, 12, 72, 31, 46, 100, 88, 54 ];
    var n = a.length, i;

    insertionSort(a, n);

    document.write("Sorted array:" + "<br>");
    for (i = 0; i < n; i++)
        document.write(a[i] +" ");

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
Sorted array: 
0 12 17 23 31 37 46 54 72 88 100 
```

本文由**阿米特·奥迪**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论