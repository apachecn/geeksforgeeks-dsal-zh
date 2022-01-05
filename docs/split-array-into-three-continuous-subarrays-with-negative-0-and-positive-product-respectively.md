# 将阵列拆分成三个连续的子阵列，分别为负积、0 积和正积

> 原文:[https://www . geeksforgeeks . org/split-array-in-three-continuous-subarray-with-negative-0-和-positive-product-分别/](https://www.geeksforgeeks.org/split-array-into-three-continuous-subarrays-with-negative-0-and-positive-product-respectively/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**大小 **N** 使得每个数组元素要么是 **-1，0，**要么是 **1** ，任务是检查是否有可能将数组拆分为 3 个连续的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得第一、第二和第三子数组的乘积分别为负、0 和正。

**示例:**

> **输入:** arr[] = {-1，0，1}，N = 3
> **输出:** -1
> 0
> 1
> **说明:**将阵列拆分为子阵列{-1}、{0}、{1}。
> 
> **输入:** arr[] = {1，-1，1，-1}，N = 4
> T3】输出:不可能

**方法:**这个问题可以通过[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)选择直到第一个“ **-1** ”没有**0′**s 的元素作为第一个子阵列，然后从最后一个子阵列中选择元素，直到产品变成 1 作为第三个子阵列，剩余的元素作为第二个子阵列来解决。按照以下步骤解决问题:

*   初始化两个变量，说 **l** 和 **r** 为 **-1** ，存储第一子阵列最后一个元素和第三子阵列第一个元素的索引。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果 **l** 为**-1****arr【I】**为 **0** ，则打印**“不可能”**。否则，如果**arr【I】**为 **-1** ，则将 **i** 分配给 **l** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   [按](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[倒序](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)遍历数组**arr【】**，如果**【I，N–1】**范围内的产品大于 **0** ，则将 **i** 分配给 **r** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   检查值 **l** 或 **r** 是否为 **-1** 或 **l ≥ r** 或[范围内的 0 计数](https://www.geeksforgeeks.org/find-the-occurrences-of-y-in-the-range-of-x/)**【l，r】**是否为 **0** 。如果任一条件为真，打印**“不可能”**。
*   打印第一个超范围子阵列**【0，l】**，第二个超范围子阵列**【l+1，r-1】**，然后打印最后一个超范围子阵列**【r，N-1】**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split an array into 3 contiguous
// subarrays satisfying the given condition
void PrintAllArrays(int arr[], int N)
{
    // Store the index of rightmost
    // element of the first and leftmost
    // element of the third subarray
    int l = -1, r = -1;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If l is equal to -1
        if (l == -1) {

            // If arr[i] is -1
            if (arr[i] == -1) {

                l = i;
                break;
            }

            // If arr[i] is 0
            if (arr[i] == 0) {

                cout << "Not Possible" << endl;
                return;
            }
        }
    }

    // Stores the product
    // of the last subarray
    int p = 1;

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {

        // Update the product
        p *= arr[i];

        // If p is greater than 0,
        // assign i to r and break
        if (p > 0) {
            r = i;
            break;
        }
    }

    // If l or r is -1 or l to r, there
    // P are no 0's, print "Not possible"
    if (l == -1 || r == -1 || l >= r
        || count(arr + l, arr + r + 1, 0) == 0) {

        cout << "Not Possible" << endl;
        return;
    }

    // Print the three subarrays
    for (int i = 0; i <= l; i++)
        cout << arr[i] << " ";

    cout << "\n";

    for (int i = l + 1; i < r; i++)
        cout << arr[i] << " ";
    cout << "\n";

    for (int i = r; i < N; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { -1, 0, 1 };
    int N = sizeof(arr) / sizeof(int);

    PrintAllArrays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to split an array into 3 contiguous
// subarrays satisfying the given condition
static void PrintAllArrays(int arr[], int N)
{

    // Store the index of rightmost
    // element of the first and leftmost
    // element of the third subarray
    int l = -1, r = -1;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If l is equal to -1
        if (l == -1)
        {

            // If arr[i] is -1
            if (arr[i] == -1)
            {
                l = i;
                break;
            }

            // If arr[i] is 0
            if (arr[i] == 0)
            {
                System.out.println("Not Possible");
                return;
            }
        }
    }

    // Stores the product
    // of the last subarray
    int p = 1;

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {

        // Update the product
        p *= arr[i];

        // If p is greater than 0,
        // assign i to r and break
        if (p > 0)
        {
            r = i;
            break;
        }
    }

    // If l or r is -1 or l to r, there
    // P are no 0's, print "Not possible"
    if (l == -1 || r == -1 || l >= r ||
       count(arr, l, r + 1, 0) == 0)
    {
        System.out.println("Not Possible");
        return;
    }

    // Print the three subarrays
    for(int i = 0; i <= l; i++)
        System.out.print(arr[i] + " ");

    System.out.println();

    for(int i = l + 1; i < r; i++)
        System.out.print(arr[i] + " ");

    System.out.println();

    for(int i = r; i < N; i++)
        System.out.print(arr[i] + " ");
}

// Function to return the number of occurrence of
// the element 'val' in the range [start, end).
static int count(int arr[], int start,
                 int end, int val)
{
    int count = 0;
    for(int i = start; i < end; i++)
    {
        if (arr[i] == val)
        {
            count++;
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { -1, 0, 1 };
    int N = arr.length;

    PrintAllArrays(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split an array into 3 contiguous
# subarrays satisfying the given condition
def PrintAllArrays(arr, N):

    # Store the index of rightmost
    # element of the first and leftmost
    # element of the third subarray
    l = -1
    r = -1

    # Traverse the array arr[]
    for i in range(N):

        # If l is equal to -1
        if (l == -1):

            # If arr[i] is -1
            if (arr[i] == -1):
                l = i
                break

            # If arr[i] is 0
            if (arr[i] == 0):
                print("Not Possible")
                return

    # Stores the product
    # of the last subarray
    p = 1

    # Traverse the array in reverse
    for i in range(N - 1, -1, -1):

        # Update the product
        p *= arr[i]

        # If p is greater than 0,
        # assign i to r and break
        if (p > 0):
            r = i
            break

    # If l or r is -1 or l to r, there
    # P are no 0's, pr"Not possible"
    if (l == -1 or r == -1 or l >= r or
       count(arr, l, r + 1, 0) == 0):
        print("Not Possible")
        return

    # Printthe three subarrays
    for i in range(0, l + 1, 1):
        print(arr[i], end = " ")

    print()

    for i in range(l + 1, r, 1):
        print(arr[i], end = " ")

    print()

    for i in range(r, N, 1):
        print(arr[i], end = " ")

# Function to return the number of occurrence of
# the element 'val' in the range [start, end).
def count(arr, start, end, val):

    count = 0
    for i in range(start, end, 1):
        if (arr[i] == val):
            count += 1

    return count

# Driver Code

# Given Input
arr = [ -1, 0, 1 ]
N = len(arr)

PrintAllArrays(arr, N)

# This code is contriobuted by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to split an array into 3 contiguous
// subarrays satisfying the given condition
static void PrintAllArrays(int[] arr, int N)
{

    // Store the index of rightmost
    // element of the first and leftmost
    // element of the third subarray
    int l = -1, r = -1;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // If l is equal to -1
        if (l == -1)
        {

            // If arr[i] is -1
            if (arr[i] == -1)
            {
                l = i;
                break;
            }

            // If arr[i] is 0
            if (arr[i] == 0)
            {
                Console.WriteLine("Not Possible");
                return;
            }
        }
    }

    // Stores the product
    // of the last subarray
    int p = 1;

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {

        // Update the product
        p *= arr[i];

        // If p is greater than 0,
        // assign i to r and break
        if (p > 0)
        {
            r = i;
            break;
        }
    }

    // If l or r is -1 or l to r, there
    // P are no 0's, print "Not possible"
    if (l == -1 || r == -1 || l >= r ||
       count(arr, l, r + 1, 0) == 0)
    {
        Console.WriteLine("Not Possible");
        return;
    }

    // Print the three subarrays
    for(int i = 0; i <= l; i++)
        Console.Write(arr[i] + " ");

    Console.WriteLine();

    for(int i = l + 1; i < r; i++)
        Console.Write(arr[i] + " ");

    Console.WriteLine();

    for(int i = r; i < N; i++)
        Console.Write(arr[i] + " ");
}

// Function to return the number of occurrence of
// the element 'val' in the range [start, end).
static int count(int[] arr, int start,
                 int end, int val)
{
    int count = 0;
    for(int i = start; i < end; i++)
    {
        if (arr[i] == val)
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void Main(String []args)
{

    // Given Input
    int[] arr = { -1, 0, 1 };
    int N = arr.Length;

    PrintAllArrays(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to split an array into 3 contiguous
// subarrays satisfying the given condition
function PrintAllArrays(arr, N)
{

    // Store the index of rightmost
    // element of the first and leftmost
    // element of the third subarray
    let l = -1, r = -1;

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // If l is equal to -1
        if (l == -1)
        {

            // If arr[i] is -1
            if (arr[i] == -1)
            {
                l = i;
                break;
            }

            // If arr[i] is 0
            if (arr[i] == 0)
            {
                document.write("Not Possible" + "<br/>");
                return;
            }
        }
    }

    // Stores the product
    // of the last subarray
    let p = 1;

    // Traverse the array in reverse
    for(let i = N - 1; i >= 0; i--)
    {

        // Update the product
        p *= arr[i];

        // If p is greater than 0,
        // assign i to r and break
        if (p > 0)
        {
            r = i;
            break;
        }
    }

    // If l or r is -1 or l to r, there
    // P are no 0's, print "Not possible"
    if (l == -1 || r == -1 || l >= r ||
       count(arr, l, r + 1, 0) == 0)
    {
        document.write("Not Possible" + "<br/>");
        return;
    }

    // Print the three subarrays
    for(let i = 0; i <= l; i++)
        document.write(arr[i] + " ");

    document.write("<br/>");

    for(let i = l + 1; i < r; i++)
        document.write(arr[i] + " ");

    document.write("<br/>");

    for(let i = r; i < N; i++)
        document.write(arr[i] + " ");
}

// Function to return the number of occurrence of
// the element 'val' in the range [start, end).
function count(arr, start, end, val)
{
    let count = 0;
    for(let i = start; i < end; i++)
    {
        if (arr[i] == val)
        {
            count++;
        }
    }
    return count;
}

// Driver Code

     // Given Input
    let arr = [ -1, 0, 1 ];
    let N = arr.length;

    PrintAllArrays(arr, N);

</script>
```

**Output:** 

```
-1 
0 
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)