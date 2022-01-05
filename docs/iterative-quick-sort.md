# 迭代快速排序

> 原文:[https://www.geeksforgeeks.org/iterative-quick-sort/](https://www.geeksforgeeks.org/iterative-quick-sort/)

以下是[快速排序](http://geeksquiz.com/quick-sort/)的典型递归实现，它使用最后一个元素作为轴心。

## C++

```
// CPP code for recursive function of Quicksort
#include <bits/stdc++.h>

using namespace std;

// Function to swap numbers
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

/* This function takes last element as pivot,
   places the pivot element at its correct
   position in sorted  array, and places
   all smaller (smaller than pivot) to left
   of pivot and all greater elements to
   right of pivot */
int partition(int arr[], int l, int h)
{
    int x = arr[h];
    int i = (l - 1);

    for (int j = l; j <= h - 1; j++) {
        if (arr[j] <= x) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[h]);
    return (i + 1);
}

/* A[] --> Array to be sorted,
l --> Starting index,
h --> Ending index */
void quickSort(int A[], int l, int h)
{
    if (l < h) {
        /* Partitioning index */
        int p = partition(A, l, h);
        quickSort(A, l, p - 1);
        quickSort(A, p + 1, h);
    }
}

// Driver code
int main()
{

    int n = 5;
    int arr[n] = { 4, 2, 6, 9, 2 };

    quickSort(arr, 0, n - 1);

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of QuickSort
import java.util.*;

class QuickSort {
    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    static int partition(int arr[], int low, int high)
    {
        int pivot = arr[high];
        int i = (low - 1); // index of smaller element
        for (int j = low; j <= high - 1; j++) {
            // If current element is smaller than or
            // equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (or pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* The main function that implements QuickSort()
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    static void qSort(int arr[], int low, int high)
    {
        if (low < high) {
            /* pi is partitioning index, arr[pi] is
            now at right place */
            int pi = partition(arr, low, high);

            // Recursively sort elements before
            // partition and after partition
            qSort(arr, low, pi - 1);
            qSort(arr, pi + 1, high);
        }
    }

    // Driver code
    public static void main(String args[])
    {

        int n = 5;
        int arr[] = { 4, 2, 6, 9, 2 };

        qSort(arr, 0, n - 1);

        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

## 蟒蛇 3

```
# A typical recursive Python
# implementation of QuickSort

# Function takes last element as pivot,
# places the pivot element at its correct
# position in sorted array, and places all
# smaller (smaller than pivot) to left of
# pivot and all greater elements to right
# of pivot
def partition(arr, low, high):
    i = (low - 1)         # index of smaller element
    pivot = arr[high]     # pivot

    for j in range(low, high):

        # If current element is smaller
        # than or equal to pivot
        if arr[j] <= pivot:

            # increment index of
            # smaller element
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return (i + 1)

# The main function that implements QuickSort
# arr[] --> Array to be sorted,
# low --> Starting index,
# high --> Ending index

# Function to do Quick sort
def quickSort(arr, low, high):
    if low < high:

        # pi is partitioning index, arr[p] is now
        # at right place
        pi = partition(arr, low, high)

        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi-1)
        quickSort(arr, pi + 1, high)

# Driver Code
if __name__ == '__main__' :

    arr = [4, 2, 6, 9, 2]
    n = len(arr)

    # Calling quickSort function
    quickSort(arr, 0, n - 1)

    for i in range(n):
        print(arr[i], end = " ")
```

## C#

```
// C# program for implementation of
// QuickSort
using System;

class GFG {

    /* This function takes last element
    as pivot, places the pivot element
    at its correct position in sorted
    array, and places all smaller
    (smaller than pivot) to left of
    pivot and all greater elements to
    right of pivot */
    static int partition(int[] arr,
                         int low, int high)
    {
        int temp;
        int pivot = arr[high];

        // index of smaller element
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++) {

            // If current element is
            // smaller than or
            // equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high]
        // (or pivot)
        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* The main function that implements
    QuickSort() arr[] --> Array to be
    sorted,
    low --> Starting index,
    high --> Ending index */
    static void qSort(int[] arr, int low,
                      int high)
    {
        if (low < high) {
            /* pi is partitioning index,
            arr[pi] is now at right place */
            int pi = partition(arr, low, high);

            // Recursively sort elements
            // before partition and after
            // partition
            qSort(arr, low, pi - 1);
            qSort(arr, pi + 1, high);
        }
    }

    // Driver code
    public static void Main()
    {

        int n = 5;
        int[] arr = { 4, 2, 6, 9, 2 };

        qSort(arr, 0, n - 1);

        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for recursive function
// of Quicksort

// Function to swap numbers
function swap(&$a, &$b)
{
    $temp = $a;
    $a = $b;
    $b = $temp;
}

/* This function takes last element as pivot,
places the pivot element at its correct
position in sorted array, and places
all smaller (smaller than pivot) to left
of pivot and all greater elements to
right of pivot */
function partition (&$arr, $l, $h)
{
    $x = $arr[$h];
    $i = ($l - 1);

    for ($j = $l; $j <= $h - 1; $j++)
    {
        if ($arr[$j] <= $x)
        {
            $i++;
            swap ($arr[$i], $arr[$j]);
        }
    }
    swap ($arr[$i + 1], $arr[$h]);
    return ($i + 1);
}

/* A[] --> Array to be sorted,
l --> Starting index,
h --> Ending index */
function quickSort(&$A, $l, $h)
{
    if ($l < $h)
    {
        /* Partitioning index */
        $p = partition($A, $l, $h);
        quickSort($A, $l, $p - 1);
        quickSort($A, $p + 1, $h);
    }

}

// Driver code
$n = 5;
$arr = array(4, 2, 6, 9, 2);

quickSort($arr, 0, $n - 1);

for($i = 0; $i < $n; $i++)
{
    echo $arr[$i] . " ";
}

// This code is contributed by
// rathbhupendra
?>
```

## java 描述语言

```
<script>

    // JavaScript program for implementation of QuickSort

    /* This function takes last element
    as pivot, places the pivot element
    at its correct position in sorted
    array, and places all smaller
    (smaller than pivot) to left of
    pivot and all greater elements to
    right of pivot */
    function partition(arr, low, high)
    {
        let temp;
        let pivot = arr[high];

        // index of smaller element
        let i = (low - 1);
        for (let j = low; j <= high - 1; j++) {

            // If current element is
            // smaller than or
            // equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high]
        // (or pivot)
        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* The main function that implements
    QuickSort() arr[] --> Array to be
    sorted,
    low --> Starting index,
    high --> Ending index */
    function qSort(arr, low, high)
    {
        if (low < high) {
            /* pi is partitioning index,
            arr[pi] is now at right place */
            let pi = partition(arr, low, high);

            // Recursively sort elements
            // before partition and after
            // partition
            qSort(arr, low, pi - 1);
            qSort(arr, pi + 1, high);
        }
    }

    let n = 5;
    let arr = [ 4, 2, 6, 9, 2 ];

    qSort(arr, 0, n - 1);

    for (let i = 0; i < n; i++)
      document.write(arr[i] + " ");

</script>
```

**输出:**

```
2 2 4 6 9
```

以上实现可以通过多种方式进行优化
1)以上实现使用最后一个索引作为枢纽。这导致已经排序的数组出现最坏的情况，这是经常发生的情况。这个问题可以通过为透视选择随机索引或者选择分区的中间索引或者为透视选择分区的第一个、中间和最后一个元素的中间值来解决。(详见[本](https://www.geeksforgeeks.org/when-does-the-worst-case-of-quicksort-occur/))
2)要减少递归深度，先对数组的小一半递归，用一个尾调用递归到另一半。
3)插入排序更适合小型子阵列。插入排序可用于调用这样的小数组(即长度小于实验确定的阈值 t)。例如，[快速排序的这个](http://code.google.com/p/dexandroid/source/browse/trunk/bionic/libc/stdlib/qsort.c?r=2)库实现使用小于 7 的插入排序。
尽管进行了上述优化，该函数仍然是递归的，并使用[函数调用堆栈](http://en.wikipedia.org/wiki/Call_stack)来存储 l 和 h 的中间值。该函数调用堆栈将其他簿记信息与参数一起存储。此外，函数调用涉及到一些开销，比如存储调用方函数的激活记录，然后恢复执行。
借助辅助栈，可以很容易地将上述函数转换为迭代版本。下面是上述递归代码的迭代实现。

## C++

```
// An iterative implementation of quick sort
#include <bits/stdc++.h>
using namespace std;

// A utility function to swap two elements
void swap(int* a, int* b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

/* This function is same in both iterative and recursive*/
int partition(int arr[], int l, int h)
{
    int x = arr[h];
    int i = (l - 1);

    for (int j = l; j <= h - 1; j++) {
        if (arr[j] <= x) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[h]);
    return (i + 1);
}

/* A[] --> Array to be sorted,
l --> Starting index,
h --> Ending index */
void quickSortIterative(int arr[], int l, int h)
{
    // Create an auxiliary stack
    int stack[h - l + 1];

    // initialize top of stack
    int top = -1;

    // push initial values of l and h to stack
    stack[++top] = l;
    stack[++top] = h;

    // Keep popping from stack while is not empty
    while (top >= 0) {
        // Pop h and l
        h = stack[top--];
        l = stack[top--];

        // Set pivot element at its correct position
        // in sorted array
        int p = partition(arr, l, h);

        // If there are elements on left side of pivot,
        // then push left side to stack
        if (p - 1 > l) {
            stack[++top] = l;
            stack[++top] = p - 1;
        }

        // If there are elements on right side of pivot,
        // then push right side to stack
        if (p + 1 < h) {
            stack[++top] = p + 1;
            stack[++top] = h;
        }
    }
}

// A utility function to print contents of arr
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 5, 2, 1, 3, 2, 3 };
    int n = sizeof(arr) / sizeof(*arr);
    quickSortIterative(arr, 0, n - 1);
    printArr(arr, n);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// An iterative implementation of quick sort
#include <stdio.h>

// A utility function to swap two elements
void swap(int* a, int* b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

/* This function is same in both iterative and recursive*/
int partition(int arr[], int l, int h)
{
    int x = arr[h];
    int i = (l - 1);

    for (int j = l; j <= h - 1; j++) {
        if (arr[j] <= x) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[h]);
    return (i + 1);
}

/* A[] --> Array to be sorted,
   l  --> Starting index,
   h  --> Ending index */
void quickSortIterative(int arr[], int l, int h)
{
    // Create an auxiliary stack
    int stack[h - l + 1];

    // initialize top of stack
    int top = -1;

    // push initial values of l and h to stack
    stack[++top] = l;
    stack[++top] = h;

    // Keep popping from stack while is not empty
    while (top >= 0) {
        // Pop h and l
        h = stack[top--];
        l = stack[top--];

        // Set pivot element at its correct position
        // in sorted array
        int p = partition(arr, l, h);

        // If there are elements on left side of pivot,
        // then push left side to stack
        if (p - 1 > l) {
            stack[++top] = l;
            stack[++top] = p - 1;
        }

        // If there are elements on right side of pivot,
        // then push right side to stack
        if (p + 1 < h) {
            stack[++top] = p + 1;
            stack[++top] = h;
        }
    }
}

// A utility function to print contents of arr
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        printf("%d ", arr[i]);
}

// Driver program to test above functions
int main()
{
    int arr[] = { 4, 3, 5, 2, 1, 3, 2, 3 };
    int n = sizeof(arr) / sizeof(*arr);
    quickSortIterative(arr, 0, n - 1);
    printArr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of QuickSort
import java.util.*;

class QuickSort {
    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    static int partition(int arr[], int low, int high)
    {
        int pivot = arr[high];

        // index of smaller element
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++) {
            // If current element is smaller than or
            // equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (or pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* A[] --> Array to be sorted,
   l  --> Starting index,
   h  --> Ending index */
    static void quickSortIterative(int arr[], int l, int h)
    {
        // Create an auxiliary stack
        int[] stack = new int[h - l + 1];

        // initialize top of stack
        int top = -1;

        // push initial values of l and h to stack
        stack[++top] = l;
        stack[++top] = h;

        // Keep popping from stack while is not empty
        while (top >= 0) {
            // Pop h and l
            h = stack[top--];
            l = stack[top--];

            // Set pivot element at its correct position
            // in sorted array
            int p = partition(arr, l, h);

            // If there are elements on left side of pivot,
            // then push left side to stack
            if (p - 1 > l) {
                stack[++top] = l;
                stack[++top] = p - 1;
            }

            // If there are elements on right side of pivot,
            // then push right side to stack
            if (p + 1 < h) {
                stack[++top] = p + 1;
                stack[++top] = h;
            }
        }
    }
    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 4, 3, 5, 2, 1, 3, 2, 3 };
        int n = 8;

        // Function calling
        quickSortIterative(arr, 0, n - 1);

        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
```

## 计算机编程语言

```
# Python program for implementation of Quicksort

# This function is same in both iterative and recursive
def partition(arr, l, h):
    i = ( l - 1 )
    x = arr[h]

    for j in range(l, h):
        if   arr[j] <= x:

            # increment index of smaller element
            i = i + 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[h] = arr[h], arr[i + 1]
    return (i + 1)

# Function to do Quick sort
# arr[] --> Array to be sorted,
# l  --> Starting index,
# h  --> Ending index
def quickSortIterative(arr, l, h):

    # Create an auxiliary stack
    size = h - l + 1
    stack = [0] * (size)

    # initialize top of stack
    top = -1

    # push initial values of l and h to stack
    top = top + 1
    stack[top] = l
    top = top + 1
    stack[top] = h

    # Keep popping from stack while is not empty
    while top >= 0:

        # Pop h and l
        h = stack[top]
        top = top - 1
        l = stack[top]
        top = top - 1

        # Set pivot element at its correct position in
        # sorted array
        p = partition( arr, l, h )

        # If there are elements on left side of pivot,
        # then push left side to stack
        if p-1 > l:
            top = top + 1
            stack[top] = l
            top = top + 1
            stack[top] = p - 1

        # If there are elements on right side of pivot,
        # then push right side to stack
        if p + 1 < h:
            top = top + 1
            stack[top] = p + 1
            top = top + 1
            stack[top] = h

# Driver code to test above
arr = [4, 3, 5, 2, 1, 3, 2, 3]
n = len(arr)
quickSortIterative(arr, 0, n-1)
print ("Sorted array is:")
for i in range(n):
    print ("% d" % arr[i]),

# This code is contributed by Mohit Kumra
```

## C#

```
// C# program for implementation of QuickSort
using System;

class GFG {

    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    static int partition(int[] arr, int low,
                         int high)
    {
        int temp;
        int pivot = arr[high];

        // index of smaller element
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++) {
            // If current element is smaller
            // than or equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high]
        // (or pivot)

        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* A[] --> Array to be sorted,
    l --> Starting index,
    h --> Ending index */
    static void quickSortIterative(int[] arr,
                                   int l, int h)
    {
        // Create an auxiliary stack
        int[] stack = new int[h - l + 1];

        // initialize top of stack
        int top = -1;

        // push initial values of l and h to
        // stack
        stack[++top] = l;
        stack[++top] = h;

        // Keep popping from stack while
        // is not empty
        while (top >= 0) {
            // Pop h and l
            h = stack[top--];
            l = stack[top--];

            // Set pivot element at its
            // correct position in
            // sorted array
            int p = partition(arr, l, h);

            // If there are elements on
            // left side of pivot, then
            // push left side to stack
            if (p - 1 > l) {
                stack[++top] = l;
                stack[++top] = p - 1;
            }

            // If there are elements on
            // right side of pivot, then
            // push right side to stack
            if (p + 1 < h) {
                stack[++top] = p + 1;
                stack[++top] = h;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 4, 3, 5, 2, 1, 3, 2, 3 };
        int n = 8;

        // Function calling
        quickSortIterative(arr, 0, n - 1);

        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An iterative implementation of quick sort

// A utility function to swap two elements
function swap ( &$a, &$b )
{
    $t = $a;
    $a = $b;
    $b = $t;
}

/* This function is same in both iterative and recursive*/
function partition (&$arr, $l, $h)
{
    $x = $arr[$h];
    $i = ($l - 1);

    for ($j = $l; $j <= $h- 1; $j++)
    {
        if ($arr[$j] <= $x)
        {
            $i++;
            swap ($arr[$i], $arr[$j]);
        }
    }
    swap ($arr[$i + 1], $arr[$h]);
    return ($i + 1);
}

/* A[] --> Array to be sorted,
l --> Starting index,
h --> Ending index */
function quickSortIterative (&$arr, $l, $h)
{
    // Create an auxiliary stack
    $stack=array_fill(0, $h - $l + 1, 0);

    // initialize top of stack
    $top = -1;

    // push initial values of l and h to stack
    $stack[ ++$top ] = $l;
    $stack[ ++$top ] = $h;

    // Keep popping from stack while is not empty
    while ( $top >= 0 )
    {
        // Pop h and l
        $h = $stack[ $top-- ];
        $l = $stack[ $top-- ];

        // Set pivot element at its correct position
        // in sorted array
        $p = partition( $arr, $l, $h );

        // If there are elements on left side of pivot,
        // then push left side to stack
        if ( $p-1 > $l )
        {
            $stack[ ++$top ] = $l;
            $stack[ ++$top ] = $p - 1;
        }

        // If there are elements on right side of pivot,
        // then push right side to stack
        if ( $p+1 < $h )
        {
            $stack[ ++$top ] = $p + 1;
            $stack[ ++$top ] = $h;
        }
    }
}

// A utility function to print contents of arr
function printArr( $arr, $n )
{
    for ( $i = 0; $i < $n; ++$i )
        echo $arr[$i]." ";
}

// Driver code
    $arr = array(4, 3, 5, 2, 1, 3, 2, 3);
    $n = count($arr);
    quickSortIterative($arr, 0, $n - 1 );
    printArr($arr, $n );

// This is code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
    // Javascript program for implementation of QuickSort

    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    function partition(arr, low, high)
    {
        let temp;
        let pivot = arr[high];

        // index of smaller element
        let i = (low - 1);
        for (let j = low; j <= high - 1; j++) {
            // If current element is smaller
            // than or equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high]
        // (or pivot)

        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    /* A[] --> Array to be sorted,
    l --> Starting index,
    h --> Ending index */
    function quickSortIterative(arr, l, h)
    {
        // Create an auxiliary stack
        let stack = new Array(h - l + 1);
        stack.fill(0);

        // initialize top of stack
        let top = -1;

        // push initial values of l and h to
        // stack
        stack[++top] = l;
        stack[++top] = h;

        // Keep popping from stack while
        // is not empty
        while (top >= 0) {
            // Pop h and l
            h = stack[top--];
            l = stack[top--];

            // Set pivot element at its
            // correct position in
            // sorted array
            let p = partition(arr, l, h);

            // If there are elements on
            // left side of pivot, then
            // push left side to stack
            if (p - 1 > l) {
                stack[++top] = l;
                stack[++top] = p - 1;
            }

            // If there are elements on
            // right side of pivot, then
            // push right side to stack
            if (p + 1 < h) {
                stack[++top] = p + 1;
                stack[++top] = h;
            }
        }
    }

    let arr = [ 4, 3, 5, 2, 1, 3, 2, 3 ];
    let n = 8;

    // Function calling
    quickSortIterative(arr, 0, n - 1);

    for (let i = 0; i < n; i++)
      document.write(arr[i] + " ");

// This code is contributed by mukesh07.
</script>
```

**输出:**

```
1 2 2 3 3 3 4 5
```

上述针对递归快速排序的优化也可以应用于迭代版本。
1)划分过程在递归和迭代上都是一样的。选择最佳枢轴的相同技术也可以应用于迭代版本。
2)要减小堆栈大小，先推小一半的索引。
3)当大小减少到实验计算的阈值以下时，使用插入排序。
**参考文献:**
[http://en.wikipedia.org/wiki/Quicksort](http://en.wikipedia.org/wiki/Quicksort)
本文由**aashis Barnwal**编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。