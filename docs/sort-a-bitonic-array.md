# 排序双离子阵列

> 原文:[https://www.geeksforgeeks.org/sort-a-bitonic-array/](https://www.geeksforgeeks.org/sort-a-bitonic-array/)

给定一个[双离子数组](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-bitonic-or-not/) **arr[]** ，任务是对给定的双离子数组进行排序。

> 一个[双音素序列](https://www.geeksforgeeks.org/longest-bitonic-subsequence-onlogn/)是一个数字序列，它首先严格递增，然后经过一个严格递减的点。

**例:**

> **输入:** arr[] = {5，10，15，25，20，3，2，1}
> **输出:** 1 2 3 5 10 15 20 25
> **输入:** arr[] = {5，20，30，40，36，33，25，15，10}
> **输出:** 5 10 15 20 25 30 33 36 40

**进场:**

*   其思想是将一个变量 **K** 初始化为数组大小为 2 的**最高幂，例如比较相距 **K** 的元素。**
*   如果元素不是按升序排列，则交换元素。
*   将 **K** 减少一半，重复该过程，直到 **K** 变为零。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Sort a Bitonic array
// in constant space
void sortArr(int a[], int n)
{
    int i, k;

    // Initialize the value of k
    k = (int)log2(n);
    k = pow(2, k);

    // In each iteration compare elements
    // k distance apart and swap if
    // they are not in order
    while (k > 0) {
        for (i = 0; i + k < n; i++)
            if (a[i] > a[i + k])
                swap(a[i], a[i + k]);

        // k is reduced to half
        // after every iteration
        k = k / 2;
    }

    // Print the array elements
    for (i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 20, 30, 40, 36, 33, 25, 15, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to Sort a Bitonic array
// in constant space
static void sortArr(int a[], int n)
{
    int i, k;

    // Initialize the value of k
    k = (int)(Math.log(n) / Math.log(2));
    k = (int) Math.pow(2, k);

    // In each iteration compare elements
    // k distance apart and swap if
    // they are not in order
    while (k > 0)
    {
        for(i = 0; i + k < n; i++)
            if (a[i] > a[i + k])
            {
                int tmp = a[i];
                a[i] = a[i + k];
                a[i + k] = tmp;
            }

        // k is reduced to half
        // after every iteration
        k = k / 2;
    }

    // Print the array elements
    for(i = 0; i < n; i++)
    {
        System.out.print(a[i] + " ");
    }
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 5, 20, 30, 40, 36,
                  33, 25, 15, 10 };
    int n = arr.length;

    // Function call
    sortArr(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
import math

# Function to sort bitonic
# array in constant space
def sortArr(a, n):

    # Initialize thevalue of k
    k = int(math.log(n, 2))
    k = int(pow(2, k))

    # In each iteration compare elements
    # k distance apart and swap it
    # they are not in order
    while(k > 0):
        i = 0
        while i + k < n:
            if a[i] > a[i + k]:
                a[i], a[i + k] = a[i + k], a[i]
            i = i + 1

        # k is reduced to half after
        # every iteration
        k = k // 2

    # Print the array elements    
    for i in range(n):
        print(a[i], end = " ")

# Driver code

# Given array
a = [ 5, 20, 30, 40, 36, 33, 25, 15, 10 ]
n = len(a)

# Function call
sortArr(a, n)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to Sort a Bitonic array
// in constant space
static void sortArr(int []a, int n)
{
    int i, k;

    // Initialize the value of k
    k = (int)(Math.Log(n) / Math.Log(2));
    k = (int) Math.Pow(2, k);

    // In each iteration compare elements
    // k distance apart and swap if
    // they are not in order
    while (k > 0)
    {
        for(i = 0; i + k < n; i++)
            if (a[i] > a[i + k])
            {
                int tmp = a[i];
                a[i] = a[i + k];
                a[i + k] = tmp;
            }

        // k is reduced to half
        // after every iteration
        k = k / 2;
    }

    // Print the array elements
    for(i = 0; i < n; i++)
    {
        Console.Write(a[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 5, 20, 30, 40, 36,
                  33, 25, 15, 10 };
    int n = arr.Length;

    // Function call
    sortArr(arr, n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Java script program for the above approach

// Function to Sort a Bitonic array
// in constant space
function sortArr(a,n)
{
    let i, k;

    // Initialize the value of k
    k = parseInt(Math.log(n) / Math.log(2));
    k = parseInt( Math.pow(2, k));

    // In each iteration compare elements
    // k distance apart and swap if
    // they are not in order
    while (k > 0)
    {
        for(i = 0; i + k < n; i++)
            if (a[i] > a[i + k])
            {
                let tmp = a[i];
                a[i] = a[i + k];
                a[i + k] = tmp;
            }

        // k is reduced to half
        // after every iteration
        k = k / 2;
    }

    // Print the array elements
    for(i = 0; i < n; i++)
    {
        document.write(a[i] + " ");
    }
}

// Driver code

    // Given array arr[]
    let arr = [ 5, 20, 30, 40, 36,
                33, 25, 15, 10 ];
    let n = arr.length;

    // Function call
    sortArr(arr, n);

// This code is contributed by sravan kumar
</script>
```

**Output**

```
5 10 15 20 25 30 33 36 40 
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*

**高效方式:**使用合并排序的**二分搜索法**和**合并功能**。

1.  在给定数组中使用二分搜索法查找峰值元素索引。
2.  将数组分成两部分，第一部分从索引 0 到峰值，第二部分从索引峰值+1 到 N-1
    ，并以升序遍历两个数组，并执行以下操作，直到任何一个
    数组耗尽:
    (i)如果第一个数组的元素少于第二个数组的元素，则将其存储到 tmp 数组
    中，并增加两个数组的索引(tmp 和第一个)。
    (ii)否则将第二个数组的元素存储到 tmp 数组中，并增加两个
    数组(tmp 和第二个)的索引。
3.  检查数组和未完全遍历的数组，将剩余的元素存储到
    tmp 数组中。
4.  将 tmp 数组的所有元素复制回原始数组。

<u>以下是上述方法的实施</u>:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG {

    // Function to Sort a Bitonic array
    static void sortArr(int arr[], int n)
    {

       // Auxiliary array to store the sorted elements
       int tmp[] = new int[n];

       // Index of peak element in the bitonic array
       int peak = -1, low = 0, high = n-1, k=0;

       // Modified Binary search to find the index of peak element
       while (low <= high){

           int mid = (low + high) / 2;

           // Condition for checking element at index mid is peak element or not
           if (( mid == 0 || arr[mid - 1] < arr[mid] )
                   && ( mid == n - 1 || arr[mid + 1] < arr[mid]
              ))
           {
               peak = mid;
               break;
           }

           // If elements before mid element
           // are in increasing order it means
           // peak is present after the mid index
           if (arr[mid] < arr[mid + 1]) low = mid + 1;

           // If elements after mid element
           // are in decreasing order it means
           // peak is present before the mid index
           else high = mid - 1;
       }

       // Merging both the sorted arrays present
       // before after the peak element
       low = 0;
       high = n - 1;

       // Loop until any of both arrays is exhausted
       while (low <= peak && high > peak){

           // Storing less value element in tmp array
           if (arr[low] < arr[high]) tmp[k++] = arr[low++];
           else tmp[k++] = arr[high--];
       }

       // Storing remaining elements of array which is
       // present before peak element in tmp array
       while (low <= peak) tmp[k++] = arr[low++];

       // Storing remaining elements of array which is
       // present after peak element in tmp array
       while (high > peak) tmp[k++] = arr[high--];

       // Storing all elements of tmp array back in
       // original array
       for (int i = 0; i < n; i++) arr[i] = tmp[i];
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given array arr[]
        int arr[] = { 5, 20, 30, 40, 36, 33, 25, 15, 10 };
        int n = arr.length;

        // Function call
        sortArr(arr, n);

        for (int x : arr) System.out.print(x + " ");
    }
}
```

**Output**

```
5 10 15 20 25 30 33 36 40 
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)* (也可以在 O(1)中完成)