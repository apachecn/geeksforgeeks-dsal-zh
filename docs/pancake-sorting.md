# 煎饼分拣

> 原文:[https://www.geeksforgeeks.org/pancake-sorting/](https://www.geeksforgeeks.org/pancake-sorting/)

给定一个未排序的数组，对给定数组进行排序。您只能对数组执行以下操作。

```
flip(arr, i): Reverse array from 0 to i 
```

与试图用尽可能少的比较进行排序的传统排序算法不同，它的目标是以尽可能少的反转对序列进行排序。
想法是做一些类似[选择排序](http://en.wikipedia.org/wiki/Selection_sort)的事情。我们一个接一个地将最大元素放在末尾，并将当前数组的大小减少一。
详细步骤如下。假设给定的数组是 arr[]，数组的大小是 n。

*   从当前大小等于 n 开始，当当前大小大于 1 时，将当前大小减少 1。让当前大小为 curr_size。对每种货币大小执行以下操作
    *   查找 arr[0]中最大元素的索引..curr_szie-1]。让索引为“mi”
    *   呼叫翻转(arr，mi)
    *   呼叫翻转(arr，curr_size-1)

关于上述算法的可视化，请参见以下视频。
[http://www.youtube.com/embed/kk-_DDgoXfk](http://www.youtube.com/embed/kk-_DDgoXfk)

## C

```
// C program to
// sort array using
// pancake sort
#include <stdio.h>
#include <stdlib.h>

/* Reverses arr[0..i] */
void flip(int arr[], int i)
{
    int temp, start = 0;
    while (start < i) {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

// Returns index of the
// maximum element in
// arr[0..n-1]
int findMax(int arr[], int n)
{
    int mi, i;
    for (mi = 0, i = 0; i < n; ++i)
        if (arr[i] > arr[mi])
            mi = i;
    return mi;
}

// The main function that
// sorts given array using
// flip operations
void pancakeSort(int* arr, int n)
{
    // Start from the complete
    // array and one by one
    // reduce current size
    // by one
    for (int curr_size = n; curr_size > 1;
                                 --curr_size)
    {
        // Find index of the
        // maximum element in
        // arr[0..curr_size-1]
        int mi = findMax(arr, curr_size);

        // Move the maximum
        // element to end of
        // current array if
        // it's not already
        // at the end
        if (mi != curr_size - 1) {
            // To move at the end,
            // first move maximum
            // number to beginning
            flip(arr, mi);

            // Now move the maximum
            // number to end by
            // reversing current array
            flip(arr, curr_size - 1);
        }
    }
}

// A utility function to print
// n array of size n
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        printf("%d ", arr[i]);
}

// Driver program to test above function
int main()
{
    int arr[] = { 23, 10, 20, 11, 12, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pancakeSort(arr, n);

    puts("Sorted Array ");
    printArray(arr, n);

    return 0;
}
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to
// sort array using
// pancake sort
#include<bits/stdc++.h>
using namespace std;

/* Reverses arr[0..i] */
void flip(int arr[], int i)
{
    int temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

// Returns index of the
// maximum element in
// arr[0..n-1]
int findMax(int arr[], int n)
{
int mi, i;
for (mi = 0, i = 0; i < n; ++i)
    if (arr[i] > arr[mi])
            mi = i;
return mi;
}

// The main function that
// sorts given array using
// flip operations
void pancakeSort(int *arr, int n)
{
    // Start from the complete
    // array and one by one
    // reduce current size
    // by one
    for (int curr_size = n; curr_size > 1;
                               --curr_size)
    {
        // Find index of the
        // maximum element in
        // arr[0..curr_size-1]
        int mi = findMax(arr, curr_size);

        // Move the maximum
        // element to end of
        // current array if
        // it's not already
        // at the end
        if (mi != curr_size-1)
        {
            // To move at the end,
            // first move maximum
            // number to beginning
            flip(arr, mi);

            // Now move the maximum
            // number to end by
            // reversing current array
            flip(arr, curr_size-1);
        }
    }
}

// A utility function to print
// n array of size n
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout<< arr[i]<<" ";
}

// Driver program to test above function
int main()
{
    int arr[] = {23, 10, 20, 11, 12, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);

    pancakeSort(arr, n);

    cout<<"Sorted Array "<<endl;
    printArray(arr, n);

    return 0;
}

//This code is contributed by rathbhupendra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// sort array using
// pancake sort
import java.io.*;

class PancakeSort {

    /* Reverses arr[0..i] */
    static void flip(int arr[], int i)
    {
        int temp, start = 0;
        while (start < i)
        {
            temp = arr[start];
            arr[start] = arr[i];
            arr[i] = temp;
            start++;
            i--;
        }
    }

    // Returns index of the
    // maximum element in
    // arr[0..n-1]
    static int findMax(int arr[], int n)
    {
        int mi, i;
        for (mi = 0, i = 0; i < n; ++i)
            if (arr[i] > arr[mi])
                mi = i;
        return mi;
    }

    // The main function that
    // sorts given array using
    // flip operations
    static int pancakeSort(int arr[], int n)
    {
        // Start from the complete
        // array and one by one
        // reduce current size by one
        for (int curr_size = n; curr_size > 1;
                                 --curr_size)
        {
            // Find index of the
            // maximum element in
            // arr[0..curr_size-1]
            int mi = findMax(arr, curr_size);

            // Move the maximum element
            // to end of current array
            // if it's not already at
            // the end
            if (mi != curr_size-1)
            {
                // To move at the end,
                // first move maximum
                // number to beginning
                flip(arr, mi);

                // Now move the maximum
                // number to end by
                // reversing current array
                flip(arr, curr_size-1);
            }
        }
        return 0;
    }

    /* Utility function to print array arr[] */
    static void printArray(int arr[], int arr_size)
    {
        for (int i = 0; i < arr_size; i++)
            System.out.print(arr[i] + " ");
        System.out.println("");
    }

    /* Driver function to check for above functions*/
    public static void main (String[] args)
    {
        int arr[] = {23, 10, 20, 11, 12, 6, 7};
        int n = arr.length;

        pancakeSort(arr, n);

        System.out.println("Sorted Array: ");
        printArray(arr, n);
    }
}
/* This code is contributed by Devesh Agrawal*/
```

## 蟒蛇 3

```
# Python3 program to
# sort array using
# pancake sort

# Reverses arr[0..i] */
def flip(arr, i):
    start = 0
    while start < i:
        temp = arr[start]
        arr[start] = arr[i]
        arr[i] = temp
        start += 1
        i -= 1

# Returns index of the maximum
# element in arr[0..n-1] */
def findMax(arr, n):
    mi = 0
    for i in range(0,n):
        if arr[i] > arr[mi]:
            mi = i
    return mi

# The main function that
# sorts given array
# using flip operations
def pancakeSort(arr, n):

    # Start from the complete
    # array and one by one
    # reduce current size
    # by one
    curr_size = n
    while curr_size > 1:
        # Find index of the maximum
        # element in
        # arr[0..curr_size-1]
        mi = findMax(arr, curr_size)

        # Move the maximum element
        # to end of current array
        # if it's not already at
        # the end
        if mi != curr_size-1:
            # To move at the end,
            # first move maximum
            # number to beginning
            flip(arr, mi)

            # Now move the maximum
            # number to end by
            # reversing current array
            flip(arr, curr_size-1)
        curr_size -= 1

# A utility function to
# print an array of size n
def printArray(arr, n):
    for i in range(0,n):
        print ("%d"%( arr[i]),end=" ")

# Driver program
arr = [23, 10, 20, 11, 12, 6, 7]
n = len(arr)
pancakeSort(arr, n);
print ("Sorted Array ")
printArray(arr,n)

# This code is contributed by shreyanshi_arun.
```

## C#

```
// C# program to sort array using
// pancake sort
using System;

class GFG {

    // Reverses arr[0..i]
    static void flip(int []arr, int i)
    {
        int temp, start = 0;
        while (start < i)
        {
            temp = arr[start];
            arr[start] = arr[i];
            arr[i] = temp;
            start++;
            i--;
        }
    }

    // Returns index of the
    // maximum element in
    // arr[0..n-1]
    static int findMax(int []arr, int n)
    {
        int mi, i;
        for (mi = 0, i = 0; i < n; ++i)
            if (arr[i] > arr[mi])
                mi = i;

        return mi;
    }

    // The main function that
    // sorts given array using
    // flip operations
    static int pancakeSort(int []arr, int n)
    {

        // Start from the complete
        // array and one by one
        // reduce current size by one
        for (int curr_size = n; curr_size > 1;
                                  --curr_size)
        {

            // Find index of the
            // maximum element in
            // arr[0..curr_size-1]
            int mi = findMax(arr, curr_size);

            // Move the maximum element
            // to end of current array
            // if it's not already at
            // the end
            if (mi != curr_size - 1)
            {
                // To move at the end,
                // first move maximum
                // number to beginning
                flip(arr, mi);

                // Now move the maximum
                // number to end by
                // reversing current array
                flip(arr, curr_size - 1);
            }
        }

        return 0;
    }

    // Utility function to print
    // array arr[]
    static void printArray(int []arr,
                           int arr_size)
    {
        for (int i = 0; i < arr_size; i++)
            Console.Write(arr[i] + " ");

        Console.Write("");
    }

    // Driver function to check for
    // above functions
    public static void Main ()
    {
        int []arr = {23, 10, 20, 11, 12, 6, 7};
        int n = arr.Length;

        pancakeSort(arr, n);

        Console.Write("Sorted Array: ");
        printArray(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// sort array using
// pancake sort

/* Reverses arr[0..i] */
function flip(&$arr, $i)
{
    $start = 0;
    while ($start < $i)
    {
        $temp = $arr[$start];
        $arr[$start] = $arr[$i];
        $arr[$i] = $temp;
        $start++;
        $i--;
    }
}

// Returns index of the
// maximum element in
// arr[0..n-1]
function findMax($arr, $n)
{
    $mi = 0;
    for ($i = 0; $i < $n; ++$i)
        if ($arr[$i] > $arr[$mi])
                $mi = $i;
    return $mi;
}

// The main function that
// sorts given array using
// flip operations
function pancakeSort(&$arr, $n)
{
    // Start from the complete
    // array and one by one
    // reduce current size
    // by one
    for ($curr_size = $n; $curr_size > 1;
                              --$curr_size)
    {
        // Find index of the
        // maximum element in
        // arr[0..curr_size-1]
        $mi = findMax($arr, $curr_size);

        // Move the maximum
        // element to end of
        // current array if
        // it's not already
        // at the end
        if ($mi != $curr_size-1)
        {
            // To move at the end,
            // first move maximum
            // number to beginning
            flip($arr, $mi);

            // Now move the maximum
            // number to end by
            // reversing current array
            flip($arr, $curr_size-1);
        }
    }
}

// A utility function to print
// n array of size n
function printArray($arr, $n)
{
    for ($i = 0; $i < $n; ++$i)
        print($arr[$i]." ");
}

// Driver code
$arr = array(23, 10, 20, 11, 12, 6, 7);
$n = count($arr);

pancakeSort($arr, $n);

echo("Sorted Array \n");
printArray($arr, $n);

return 0;

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript program to sort array using pancake sort

    // Reverses arr[0..i]
    function flip(arr, i)
    {
        let temp, start = 0;
        while (start < i)
        {
            temp = arr[start];
            arr[start] = arr[i];
            arr[i] = temp;
            start++;
            i--;
        }
    }

    // Returns index of the
    // maximum element in
    // arr[0..n-1]
    function findMax(arr, n)
    {
        let mi, i;
        for (mi = 0, i = 0; i < n; ++i)
            if (arr[i] > arr[mi])
                mi = i;

        return mi;
    }

    // The main function that
    // sorts given array using
    // flip operations
    function pancakeSort(arr, n)
    {

        // Start from the complete
        // array and one by one
        // reduce current size by one
        for (let curr_size = n; curr_size > 1; --curr_size)
        {

            // Find index of the
            // maximum element in
            // arr[0..curr_size-1]
            let mi = findMax(arr, curr_size);

            // Move the maximum element
            // to end of current array
            // if it's not already at
            // the end
            if (mi != curr_size - 1)
            {
                // To move at the end,
                // first move maximum
                // number to beginning
                flip(arr, mi);

                // Now move the maximum
                // number to end by
                // reversing current array
                flip(arr, curr_size - 1);
            }
        }

        return 0;
    }

    // Utility function to print
    // array arr[]
    function printArray(arr, arr_size)
    {
        for (let i = 0; i < arr_size; i++)
            document.write(arr[i] + " ");

        document.write("");
    }

    let arr = [23, 10, 20, 11, 12, 6, 7];
    let n = arr.length;

    pancakeSort(arr, n);

    document.write("Sorted Array: " + "</br>");
    printArray(arr, n);

</script>
```

**输出:**

```
Sorted Array
6 7 10 11 12 20 23
```

在上面的代码中，总共执行了 O(n)个翻转操作。总的时间复杂度是 O(n^2).
**参考文献:**
[【http://en.wikipedia.org/wiki/Pancake_sorting】](http://en.wikipedia.org/wiki/Pancake_sorting)
发现有不正确的地方请写评论，或者想分享以上讨论话题的更多信息。