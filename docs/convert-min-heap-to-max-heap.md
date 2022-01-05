# 将最小堆转换为最大堆

> 原文:[https://www.geeksforgeeks.org/convert-min-heap-to-max-heap/](https://www.geeksforgeeks.org/convert-min-heap-to-max-heap/)

给定最小堆的数组表示，在 O(n)时间内将其转换为最大堆。
**例:**

```
Input: arr[] = [3 5 9 6 8 20 10 12 18 9]
         3
      /     \
     5       9
   /   \    /  \
  6     8  20   10
 /  \   /
12   18 9 

Output: arr[] = [20 18 10 12 9 9 3 5 6 8] OR 
       [any Max Heap formed from input elements]

         20
       /    \
     18      10
   /    \    /  \
  12     9  9    3
 /  \   /
5    6 8 
```

这个问题乍一看可能很复杂。但是我们的最终目标是只构建最大堆。这个想法很简单——我们只需构建最大堆，而不考虑输入。我们从最小堆的最底部和最右边的内部模式开始，以自下而上的方式堆化所有内部模式来构建最大堆。
下面是它的实现

## C++

```
// A C++ program to convert min Heap to max Heap
#include<bits/stdc++.h>
using namespace std;

// to heapify a subtree with root at given index
void MaxHeapify(int arr[], int i, int n)
{
    int l = 2*i + 1;
    int r = 2*i + 2;
    int largest = i;
    if (l < n && arr[l] > arr[i])
        largest = l;
    if (r < n && arr[r] > arr[largest])
        largest = r;
    if (largest != i)
    {
        swap(arr[i], arr[largest]);
        MaxHeapify(arr, largest, n);
    }
}

// This function basically builds max heap
void convertMaxHeap(int arr[], int n)
{
    // Start from bottommost and rightmost
    // internal mode and heapify all internal
    // modes in bottom up way
    for (int i = (n-2)/2; i >= 0; --i)
        MaxHeapify(arr, i, n);
}

// A utility function to print a given array
// of given size
void printArray(int* arr, int size)
{
    for (int i = 0; i < size; ++i)
        printf("%d ", arr[i]);
}

// Driver program to test above functions
int main()
{
    // array representing Min Heap
    int arr[] = {3, 5, 9, 6, 8, 20, 10, 12, 18, 9};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Min Heap array : ");
    printArray(arr, n);

    convertMaxHeap(arr, n);

    printf("\nMax Heap array : ");
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert min Heap to max Heap

class GFG
{
    // To heapify a subtree with root at given index
    static void MaxHeapify(int arr[], int i, int n)
    {
        int l = 2*i + 1;
        int r = 2*i + 2;
        int largest = i;
        if (l < n && arr[l] > arr[i])
            largest = l;
        if (r < n && arr[r] > arr[largest])
            largest = r;
        if (largest != i)
        {
            // swap arr[i] and arr[largest]
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;
            MaxHeapify(arr, largest, n);
        }
    }

    // This function basically builds max heap
    static void convertMaxHeap(int arr[], int n)
    {
        // Start from bottommost and rightmost
        // internal mode and heapify all internal
        // modes in bottom up way
        for (int i = (n-2)/2; i >= 0; --i)
            MaxHeapify(arr, i, n);
    }

    // A utility function to print a given array
    // of given size
    static void printArray(int arr[], int size)
    {
        for (int i = 0; i < size; ++i)
            System.out.print(arr[i]+" ");
    }

    // driver program
    public static void main (String[] args)
    {
        // array representing Min Heap
        int arr[] = {3, 5, 9, 6, 8, 20, 10, 12, 18, 9};
        int n = arr.length;

        System.out.print("Min Heap array : ");
        printArray(arr, n);

        convertMaxHeap(arr, n);

        System.out.print("\nMax Heap array : ");
        printArray(arr, n);
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A Python3 program to convert min Heap
# to max Heap

# to heapify a subtree with root
# at given index
def MaxHeapify(arr, i, n):
    l = 2 * i + 1
    r = 2 * i + 2
    largest = i
    if l < n and arr[l] > arr[i]:
        largest = l
    if r < n and arr[r] > arr[largest]:
        largest = r
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        MaxHeapify(arr, largest, n)

# This function basically builds max heap
def convertMaxHeap(arr, n):

    # Start from bottommost and rightmost
    # internal mode and heapify all
    # internal modes in bottom up way
    for i in range(int((n - 2) / 2), -1, -1):
        MaxHeapify(arr, i, n)

# A utility function to print a
# given array of given size
def printArray(arr, size):
    for i in range(size):
        print(arr[i], end = " ")
    print()

# Driver Code
if __name__ == '__main__':

    # array representing Min Heap
    arr = [3, 5, 9, 6, 8, 20, 10, 12, 18, 9]
    n = len(arr)

    print("Min Heap array : ")
    printArray(arr, n)

    convertMaxHeap(arr, n)

    print("Max Heap array : ")
    printArray(arr, n)

# This code is contributed by PranchalK
```

## C#

```
// C# program to convert
// min Heap to max Heap
using System;

class GFG
{
    // To heapify a subtree with
    // root at given index
    static void MaxHeapify(int []arr,
                           int i, int n)
    {
        int l = 2 * i + 1;
        int r = 2 * i + 2;
        int largest = i;
        if (l < n && arr[l] > arr[i])
            largest = l;
        if (r < n && arr[r] > arr[largest])
            largest = r;
        if (largest != i)
        {
            // swap arr[i] and arr[largest]
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;
            MaxHeapify(arr, largest, n);
        }
    }

    // This function basically
    // builds max heap
    static void convertMaxHeap(int []arr,
                               int n)
    {
        // Start from bottommost and
        // rightmost internal mode and
        // heapify all internal modes
        // in bottom up way
        for (int i = (n - 2) / 2; i >= 0; --i)
            MaxHeapify(arr, i, n);
    }

    // A utility function to print
    // a given array of given size
    static void printArray(int []arr,
                           int size)
    {
        for (int i = 0; i < size; ++i)
            Console.Write(arr[i]+" ");
    }

    // Driver Code
    public static void Main ()
    {
        // array representing Min Heap
        int []arr = {3, 5, 9, 6, 8,
                     20, 10, 12, 18, 9};
        int n = arr.Length;

        Console.Write("Min Heap array : ");
        printArray(arr, n);

        convertMaxHeap(arr, n);

        Console.Write("\nMax Heap array : ");
        printArray(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to convert min Heap to max Heap

// utility swap function
function swap(&$a,&$b)
{
    $tmp=$a;
    $a=$b;
    $b=$tmp;
}

// to heapify a subtree with root at given index
function MaxHeapify(&$arr, $i, $n)
{
    $l = 2*$i + 1;
    $r = 2*$i + 2;
    $largest = $i;
    if ($l < $n && $arr[$l] > $arr[$i])
        $largest = $l;
    if ($r < $n && $arr[$r] > $arr[$largest])
        $largest = $r;
    if ($largest != $i)
    {
        swap($arr[$i], $arr[$largest]);
        MaxHeapify($arr, $largest, $n);
    }
}

// This function basically builds max heap
function convertMaxHeap(&$arr, $n)
{
    // Start from bottommost and rightmost
    // internal mode and heapify all internal
    // modes in bottom up way
    for ($i = (int)(($n-2)/2); $i >= 0; --$i)
        MaxHeapify($arr, $i, $n);
}

// A utility function to print a given array
// of given size
function printArray($arr, $size)
{
    for ($i = 0; $i <$size; ++$i)
        print($arr[$i]." ");
}

    // Driver code

    // array representing Min Heap
    $arr = array(3, 5, 9, 6, 8, 20, 10, 12, 18, 9);
    $n = count($arr);

    print("Min Heap array : ");
    printArray($arr, $n);

    convertMaxHeap($arr, $n);

    print("\nMax Heap array : ");
    printArray($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to convert min Heap to max Heap   
// To heapify a subtree with root at given index
function MaxHeapify(arr , i , n)
{
    var l = 2*i + 1;
    var r = 2*i + 2;
    var largest = i;
    if (l < n && arr[l] > arr[i])
        largest = l;
    if (r < n && arr[r] > arr[largest])
        largest = r;
    if (largest != i)
    {
        // swap arr[i] and arr[largest]
        var temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        MaxHeapify(arr, largest, n);
    }
}

// This function basically builds max heap
function convertMaxHeap(arr , n)
{
    // Start from bottommost and rightmost
    // internal mode and heapify all internal
    // modes in bottom up way
    for (i = (n-2)/2; i >= 0; --i)
        MaxHeapify(arr, i, n);
}

// A utility function to print a given array
// of given size
function printArray(arr , size)
{
    for (i = 0; i < size; ++i)
        document.write(arr[i]+" ");
}

// driver program
// array representing Min Heap
var arr = [3, 5, 9, 6, 8, 20, 10, 12, 18, 9];
var n = arr.length;

document.write("Min Heap array : ");
printArray(arr, n);

convertMaxHeap(arr, n);

document.write("<br>Max Heap array : ");
printArray(arr, n);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
Min Heap array : 3 5 9 6 8 20 10 12 18 9 
Max Heap array : 20 18 10 12 9 9 3 5 6 8 
```

上述解决方案的复杂性看起来像 O(nLogn)，但实际上是 O(n)。更多详情请参考本 [G-Fact](https://www.geeksforgeeks.org/g-fact-85/) 。
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息