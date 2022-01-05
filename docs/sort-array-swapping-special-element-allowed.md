# 通过仅交换特殊元素来排序数组是允许的

> 原文:[https://www . geeksforgeeks . org/sort-array-swapping-special-element-allowed/](https://www.geeksforgeeks.org/sort-array-swapping-special-element-allowed/)

给定一个长度为 n + 1 的数组，包含元素 1 到 n 和一个空格，需要使用给定的交换(index i，index j)函数对数组进行排序，你只能交换间隙和一个数字，最后，把间隙放在最后。
数组中会有一个数字 999 作为间隙或空格。

示例:

```
Input  : arr = {1, 5, 4, 999, 3, 2}
Output : arr = {1, 2, 3, 4, 5, 999}
We need to sort only by moving 

Input  : arr = {1, 5, 4, 3, 2, 8, 7, 999, 6}
Output : arr = {1, 2, 3, 4, 5, 6, 7, 8, 999}
```

我们遵循递归方法来解决这个问题。因为我们只能用空格交换数字。首先我们找到空间的指数。如果索引是数组的开始，那么通过与它右边的每个数字交换，将这个空间移到倒数第二个索引。
如果空间既不是数组的开始，也不是数组的最后一个元素，并且它之前的元素大于空间旁边的元素，则执行以下操作。

> 第一步:交换空间和空间旁边的元素
> 在{3，999，2}的情况下，使其成为{3，2，999}
> 第二步:交换空间和更大的元素
> 例如-将{3，2，999}转换为{999，2，3}

否则，索引旁边的元素将被排序，并与前一个元素交换。再次调用排序函数，数组的大小减少 1，空间的索引为-1，因为我们每次都会得到一个排序的元素。

## C++

```
// CPP program to sort an array by moving one
// space around.
#include <bits/stdc++.h>
using namespace std;

// n is total number of elements.
// index is index of 999 or space.
// k is number of elements yet to be sorted.
void sortRec(int arr[], int index, int k, int n)
{
    // print the sorted array when loop reaches
    // the base case
    if (k == 0) {
        for (int i = 1; i < n; i++)
            cout << arr[i] << " ";
        cout << 999;
        return;
    }

    // else if k>0 and space is at 0th index swap
    // each number with space and store index at
    // second last index
    else if (k > 0 && index == 0) {
        index = n - 2;
        for (int i = 1; i <= index; i++) {
            arr[i - 1] = arr[i];
        }
        arr[index] = 999;
    }

    // if space is neither start of array nor last
    // element of array and element before it greater
    // than/ the element next to space
    if (index - 1 >= 0 && index + 1 < n &&
       arr[index - 1] > arr[index + 1]) {

        // first swap space and element next to space
        // in case of {3, 999, 2} make it {3, 2, 999}
        swap(arr[index], arr[index + 1]);

        // than swap space and greater element
        // convert {3, 2, 999} to {999, 2, 3}
        swap(arr[index - 1], arr[index + 1]);
    }

    else
        swap(arr[index], arr[index - 1]);

    sortRec(arr, index - 1, k - 1, n);
}

// Wrapper over sortRec.
void sort(int arr[], int n)
{
    // Find index of space (or 999)
    int index = -1;
    for (int i = 0; i < n; i++) {
        if (arr[i] == 999) {
            index = i;
            break;
        }
    }

    // Invalid input
    if (index == -1)
        return;

    sortRec(arr, index, n, n);
}

// driver program
int main()
{
    int arr[] = { 3, 2, 999, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    sort(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array by moving one
// space around.

class GFG
{

// n is total number of elements.
// index is index of 999 or space.
// k is number of elements yet to be sorted.
static void sortRec(int arr[], int index, int k, int n)
{
    // print the sorted array when loop reaches
    // the base case
    if (k == 0)
    {
        for (int i = 1; i < n; i++)
                        System.out.print(arr[i] + " ");
                System.out.println(999);
        return;
    }

    // else if k>0 and space is at 0th index swap
    // each number with space and store index at
    // second last index
    else if (k > 0 && index == 0)
    {
        index = n - 2;
        for (int i = 1; i <= index; i++)
        {
            arr[i - 1] = arr[i];
        }
        arr[index] = 999;
    }

    // if space is neither start of array nor last
    // element of array and element before it greater
    // than/ the element next to space
    if (index - 1 >= 0 && index + 1 < n &&
    arr[index - 1] > arr[index + 1])
    {

        // first swap space and element next to space
        // in case of {3, 999, 2} make it {3, 2, 999}
        swap(arr,index, index + 1);

        // than swap space and greater element
        // convert {3, 2, 999} to {999, 2, 3}
        swap(arr,index - 1, index + 1);
    }

    else
        swap(arr,index, index - 1);

    sortRec(arr, index - 1, k - 1, n);
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Wrapper over sortRec.
static void sort(int arr[], int n)
{
    // Find index of space (or 999)
    int index = -1;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 999)
        {
            index = i;
            break;
        }
    }

    // Invalid input
    if (index == -1)
        return;

    sortRec(arr, index, n, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 999, 1 };
    int n = arr.length;
    sort(arr, n);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to sort an array
# by moving one space around.

# n is total number of elements.
# index is index of 999 or space.
# k is number of elements yet to be sorted.
def sortRec(arr, index, k, n):

    # Print the sorted array when loop reaches
    # the base case
    if (k == 0):
        for i in range(1,n):
            print(arr[i],end=" ")
        print(999,end="")

    # Else if k>0 and space is at 0th index swap
    # each number with space and store index at
    # second last index
    elif(k > 0 and index == 0):
        index = n - 2

        for i in range(1,index+1):
            arr[i - 1] = arr[i]
        arr[index] = 999

    # If space is neither start of array nor last
    # element of array and element before it greater
    # than/ the element next to space
    if (index - 1 >= 0 and index + 1 < n and arr[index - 1] > arr[index + 1]):

        # First swap space and element next to space
        # in case of {3, 999, 2} make it {3, 2, 999}
        arr[index],arr[index+1] = arr[index+1],arr[index]

        # Than swap space and greater element
        # convert {3, 2, 999} to {999, 2, 3}
        arr[index-1],arr[index+1] = arr[index+1],arr[index-1]

    else:
        if(index-1<0):
            return
        arr[index],arr[index-1] = arr[index-1],arr[index]

    sortRec(arr, index - 1, k - 1, n)

# Wrapper over sortRec.
def sort(arr, n):

    # Find index of space (or 999)
    index = -1

    for i in range(n):
        if (arr[i] == 999):
            index = i
            break
    #  Invalid input
    if (index == -1):
        return
    sortRec(arr, index, n, n)

# Driver Code
arr = [ 3, 2, 999, 1 ]
n=len(arr)
sort(arr, n)

# This code is contributed by rag2127.
```

## C#

```
// C# program to sort an array by moving one
// space around.
using System;

class GFG
{

// n is total number of elements.
// index is index of 999 or space.
// k is number of elements yet to be sorted.
static void sortRec(int []arr, int index, int k, int n)
{
    // print the sorted array when loop reaches
    // the base case
    if (k == 0)
    {
        for (int i = 1; i < n; i++)
                        Console.Write(arr[i] + " ");
                Console.WriteLine(999);
        return;
    }

    // else if k>0 and space is at 0th index swap
    // each number with space and store index at
    // second last index
    else if (k > 0 && index == 0)
    {
        index = n - 2;
        for (int i = 1; i <= index; i++)
        {
            arr[i - 1] = arr[i];
        }
        arr[index] = 999;
    }

    // if space is neither start of array nor last
    // element of array and element before it greater
    // than/ the element next to space
    if (index - 1 >= 0 && index + 1 < n &&
    arr[index - 1] > arr[index + 1])
    {

        // first swap space and element next to space
        // in case of {3, 999, 2} make it {3, 2, 999}
        swap(arr,index, index + 1);

        // than swap space and greater element
        // convert {3, 2, 999} to {999, 2, 3}
        swap(arr,index - 1, index + 1);
    }

    else
        swap(arr,index, index - 1);

    sortRec(arr, index - 1, k - 1, n);
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Wrapper over sortRec.
static void sort(int []arr, int n)
{
    // Find index of space (or 999)
    int index = -1;
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 999)
        {
            index = i;
            break;
        }
    }

    // Invalid input
    if (index == -1)
        return;

    sortRec(arr, index, n, n);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 999, 1 };
    int n = arr.Length;
    sort(arr, n);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to sort an array
// by moving one space around.

// n is total number of elements.
// index is index of 999 or space.
// k is number of elements yet to be sorted.
function sortRec(arr, index, k, n)
{

    // Print the sorted array when loop reaches
    // the base case
    if (k == 0)
    {
        for(let i = 1; i < n; i++)
           document.write(arr[i] + " ");

        document.write(999);
        return;
    }

    // Else if k>0 and space is at 0th index swap
    // each number with space and store index at
    // second last index
    else if (k > 0 && index == 0)
    {
        index = n - 2;
        for(let i = 1; i <= index; i++)
        {
            arr[i - 1] = arr[i];
        }
        arr[index] = 999;
    }

    // If space is neither start of array nor last
    // element of array and element before it greater
    // than/ the element next to space
    if (index - 1 >= 0 && index + 1 < n &&
     arr[index - 1] > arr[index + 1])
    {

        // First swap space and element next to space
        // in case of {3, 999, 2} make it {3, 2, 999}
        swap(arr, index, index + 1);

        // Than swap space and greater element
        // convert {3, 2, 999} to {999, 2, 3}
        swap(arr, index - 1, index + 1);
    }
    else
        swap(arr,index, index - 1);

    sortRec(arr, index - 1, k - 1, n);
}

function swap(arr, i, j)
{
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Wrapper over sortRec.
function sort(arr, n)
{

    // Find index of space (or 999)
    let index = -1;
    for(let i = 0; i < n; i++)
    {
        if (arr[i] == 999)
        {
            index = i;
            break;
        }
    }

    // Invalid input
    if (index == -1)
        return;

    sortRec(arr, index, n, n);
}

// Driver Code
let arr = [ 3, 2, 999, 1 ];
let n = arr.length;

sort(arr, n);

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
1 2 3 999
```

**时间复杂度-** O(n <sup>2</sup> )