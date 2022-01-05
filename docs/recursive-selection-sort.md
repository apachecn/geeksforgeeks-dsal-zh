# 递归选择排序

> 原文:[https://www.geeksforgeeks.org/recursive-selection-sort/](https://www.geeksforgeeks.org/recursive-selection-sort/)

[选择排序](https://www.geeksforgeeks.org/selection-sort/)算法排序维护两部分。

1.  已经排序的第一部分
2.  第二部分尚待整理。

该算法的工作原理是从未排序的部分重复寻找最小元素(考虑升序)，并将其放在排序部分的末尾。

```
arr[] = 64 25 12 22 11

// Find the minimum element in arr[0...4]
// and place it at beginning
11 25 12 22 64

// Find the minimum element in arr[1...4]
// and place it at beginning of arr[1...4]
11 12 25 22 64

// Find the minimum element in arr[2...4]
// and place it at beginning of arr[2...4]
11 12 22 25 64

// Find the minimum element in arr[3...4]
// and place it at beginning of arr[3...4]
11 12 22 25 64 
```

我们已经讨论过[迭代选择排序](https://www.geeksforgeeks.org/selection-sort/)。本文讨论递归方法。递归求解的思想是逐个递增排序部分，递归调用剩余(尚待排序)部分。

## C++

```
// Recursive C++ program to sort an array
// using selection sort
#include <iostream>
using namespace std;

// Return minimum index
int minIndex(int a[], int i, int j)
{
    if (i == j)
        return i;

    // Find minimum of remaining elements
    int k = minIndex(a, i + 1, j);

    // Return minimum of current and remaining.
    return (a[i] < a[k])? i : k;
}

// Recursive selection sort. n is size of a[] and index
// is index of starting element.
void recurSelectionSort(int a[], int n, int index = 0)
{
    // Return when starting and size are same
    if (index == n)
       return;

    // calling minimum index function for minimum index
    int k = minIndex(a, index, n-1);

    // Swapping when index nd minimum index are not same
    if (k != index)
       swap(a[k], a[index]);

    // Recursively calling selection sort function
    recurSelectionSort(a, n, index + 1);
}

// Driver code
int main()
{
    int arr[] = {3, 1, 5, 2, 7, 0};
    int n = sizeof(arr)/sizeof(arr[0]);

    // Calling function
    recurSelectionSort(arr, n);

    //printing sorted array
    for (int i = 0; i<n ; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to sort an array
// using selection sort

class Test
{
    // Return minimum index
    static int minIndex(int a[], int i, int j)
    {
        if (i == j)
            return i;

        // Find minimum of remaining elements
        int k = minIndex(a, i + 1, j);

        // Return minimum of current and remaining.
        return (a[i] < a[k])? i : k;
    }

    // Recursive selection sort. n is size of a[] and index
    // is index of starting element.
    static void recurSelectionSort(int a[], int n, int index)
    {

        // Return when starting and size are same
        if (index == n)
           return;

        // calling minimum index function for minimum index
        int k = minIndex(a, index, n-1);

        // Swapping when index nd minimum index are not same
        if (k != index){
           // swap
           int temp = a[k];
           a[k] = a[index];
           a[index] = temp;
        }
        // Recursively calling selection sort function
        recurSelectionSort(a, n, index + 1);
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = {3, 1, 5, 2, 7, 0};

        // Calling function
        recurSelectionSort(arr, arr.length, 0);

        //printing sorted array
        for (int i = 0; i< arr.length; i++)
            System.out.print(arr[i] + " ");
    }
}
```

## 蟒蛇 3

```
# Recursive Python3 code to sort
# an array using selection sort

# Return minimum index
def minIndex( a , i , j ):
    if i == j:
        return i

    # Find minimum of remaining elements
    k = minIndex(a, i + 1, j)

    # Return minimum of current
    # and remaining.
    return (i if a[i] < a[k] else k)

# Recursive selection sort. n is
# size of a[] and index is index of
# starting element.
def recurSelectionSort(a, n, index = 0):

    # Return when starting and
    # size are same
    if index == n:
        return -1

    # calling minimum index function
    # for minimum index
    k = minIndex(a, index, n-1)

    # Swapping when index and minimum
    # index are not same
    if k != index:
        a[k], a[index] = a[index], a[k]

    # Recursively calling selection
    # sort function
    recurSelectionSort(a, n, index + 1)

# Driver code
arr = [3, 1, 5, 2, 7, 0]
n = len(arr)

# Calling function
recurSelectionSort(arr, n)

# printing sorted array
for i in arr:
    print(i, end = ' ')

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// Recursive C# program to sort an array
// using selection sort
using System;

class GFG
{
    // Return minimum index
    static int minIndex(int []a, int i, int j)
    {
        if (i == j)
            return i;

        // Find minimum of remaining elements
        int k = minIndex(a, i + 1, j);

        // Return minimum of current and remaining.
        return (a[i] < a[k])? i : k;
    }

    // Recursive selection sort. n is size of
    // a[] and index is index of starting element.
    static void recurSelectionSort(int []a, int n,
                                   int index)
    {

        // Return when starting and size are same
        if (index == n)
        return;

        // calling minimum index function
        // for minimum index
        int k = minIndex(a, index, n - 1);

        // Swapping when index and minimum index
        // are not same
        if (k != index)
        {
            // swap
            int temp = a[k];
            a[k] = a[index];
            a[index] = temp;
        }

        // Recursively calling selection sort function
        recurSelectionSort(a, n, index + 1);
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = {3, 1, 5, 2, 7, 0};

        // Calling function
        recurSelectionSort(arr, arr.Length, 0);

        //printing sorted array
        for (int i = 0; i< arr.Length; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by Princi Singh
```

**输出:**

```
0 1 2 3 5 7 
```

本文由 [**萨赫勒拉吉普特**](https://www.linkedin.com/in/sahil-rajput-3ba2b3134/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。