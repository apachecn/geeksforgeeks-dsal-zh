# 重新排列给定的数组，使得没有数组元素与其索引相同

> 原文:[https://www . geeksforgeeks . org/re 排列-给定-数组-这样-无数组-元素-与其索引相同/](https://www.geeksforgeeks.org/rearrange-given-array-such-that-no-array-element-is-same-as-its-index/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是重新排列数组，使得没有元素与其索引相同(基于 *1 的索引*)。如果存在多个解决方案，请打印其中任何一个。

**示例:**

> **输入:** arr[] = {4，2，3，1}
> **输出:** 3 1 4 2
> **说明:**索引{1，2，3，4}处的元素分别为{3，1，4，2}。
> 
> **输入:** arr[] = {10，20，30，40，6}
> **输出:** 6 10 20 30 40
> **说明:**指数{1，2，3，4，5}处的元素分别为{6，10，20，30，40}。

**方法:**思路是使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)，如果**arr【I】**等于 **i** ，则在任意索引 **i** 处交换每对相邻的索引。这是因为，如果 **arr[i] = i** 成立，那么肯定 **arr[i + 1] ≠ i** 和 **arr[i] ≠ i + 1** 因为 **arr[i + 1] > arr[i]** 。如果最后一个元素 **arr[N]** 等于 **N** ，则交换 **arr[N]** 和**arr[N–1]**。按照以下步骤解决问题:

*   [按递增顺序对数组 arr[]进行排序。](https://www.geeksforgeeks.org/sort-c-stl/)
*   [使用变量 **i** 在范围**【0，N–2】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**arr【I】**是否与 **(i + 1)** 相同。如果发现为真，则[交换](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)**arr【I】**和**arr【I+1】**。
*   现在，对于最后一个数组元素，如果 **arr[N]** 与 **N** 相同，那么交换 **arr[N]** 和**arr[N–1]**。
*   完成上述步骤后，打印修改后的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array a[]
// such that none of the array elements
// is same as its index
void rearrangeArray(int a[], int n)
{
    // Sort the array
    sort(a, a + n);

    // Traverse the indices [0, N - 2]
    // of the given array
    for (int i = 0; i < n - 1; i++) {

        // Check if the current element
        // is equal to its index
        if (a[i] == i + 1) {

            // If found to be true, swap
            // current element with the
            // next element
            swap(a[i], a[i + 1]);
        }
    }

    // Check if the last element is
    // same as its index
    if (a[n - 1] == n) {

        // If found to be true, swap
        // current element with the
        // previous element
        swap(a[n - 1], a[n - 2]);
    }

    // Print the modified array
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 3, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    rearrangeArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to rearrange the array a[]
// such that none of the array elements
// is same as its index
static void rearrangeArray(int a[], int n)
{

    // Sort the array
    Arrays.sort(a);

    // Traverse the indices [0, N - 2]
    // of the given array
    for(int i = 0; i < n - 1; i++)
    {

        // Check if the current element
        // is equal to its index
        if (a[i] == i + 1)
        {

            // If found to be true, swap
            // current element with the
            // next element
            int temp = a[i];
            a[i] = a[i + 1];
            a[i + 1] = temp;
        }
    }

    // Check if the last element is
    // same as its index
    if (a[n - 1] == n)
    {

        // If found to be true, swap
        // current element with the
        // previous element
        int temp = a[n - 1];
        a[n - 1] = a[n - 2];
        a[n - 2] = temp;
    }

    // Print the modified array
    for(int i = 0; i < n; i++)
    {
        System.out.print(a[i] + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 5, 3, 2, 4 };
    int N = arr.length;

    // Function Call
    rearrangeArray(arr, N);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange the array a[]
# such that none of the array elements
# is same as its index
def rearrangeArray(a, n):

    # Sort the array
    a = sorted(a)

    # Traverse the indices [0, N - 2]
    # of the given array
    for i in range(n - 1):

        # Check if the current element
        # is equal to its index
        if (a[i] == i + 1):

            # If found to be true, swap
            # current element with the
            # next element
            a[i], a[i + 1] = a[i + 1], a[i]

    # Check if the last element is
    # same as its index
    if (a[n - 1] == n):

        # If found to be true, swap
        # current element with the
        # previous element
        a[n - 1], a[n - 2] = a[n - 2], a[n - 1]

    # Print the modified array
    for i in range(n):
        print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [1, 5, 3, 2, 4]
    N = len(arr)

    # Function Call
    rearrangeArray(arr, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to rearrange the array []a
// such that none of the array elements
// is same as its index
static void rearrangeArray(int []a, int n)
{

    // Sort the array
    Array.Sort(a);

    // Traverse the indices [0, N - 2]
    // of the given array
    for(int i = 0; i < n - 1; i++)
    {

        // Check if the current element
        // is equal to its index
        if (a[i] == i + 1)
        {

            // If found to be true, swap
            // current element with the
            // next element
            int temp = a[i];
            a[i] = a[i + 1];
            a[i + 1] = temp;
        }
    }

    // Check if the last element is
    // same as its index
    if (a[n - 1] == n)
    {

        // If found to be true, swap
        // current element with the
        // previous element
        int temp = a[n - 1];
        a[n - 1] = a[n - 2];
        a[n - 2] = temp;
    }

    // Print the modified array
    for(int i = 0; i < n; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 1, 5, 3, 2, 4 };
    int N = arr.Length;

    // Function Call
    rearrangeArray(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to rearrange the array a[]
// such that none of the array elements
// is same as its index
function rearrangeArray(a, n)
{

    // Sort the array
    a.sort();

    // Traverse the indices [0, N - 2]
    // of the given array
    for(let i = 0; i < n - 1; i++)
    {

        // Check if the current element
        // is equal to its index
        if (a[i] == i + 1)
        {

            // If found to be true, swap
            // current element with the
            // next element
            let temp = a[i];
            a[i] = a[i + 1];
            a[i + 1] = temp;
        }
    }

    // Check if the last element is
    // same as its index
    if (a[n - 1] == n)
    {

        // If found to be true, swap
        // current element with the
        // previous element
        let temp = a[n - 1];
        a[n - 1] = a[n - 2];
        a[n - 2] = temp;
    }

    // Prlet the modified array
    for(let i = 0; i < n; i++)
    {
        document.write(a[i] + " ");
    }
}

// Driver code

     let arr = [ 1, 5, 3, 2, 4 ];
    let N = arr.length;

    // Function Call
    rearrangeArray(arr, N);

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
2 1 4 5 3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*