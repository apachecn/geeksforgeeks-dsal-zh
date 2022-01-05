# 找到奇数索引处的元素之和大于偶数索引处的元素之和的数组置换

> 原文:[https://www . geeksforgeeks . org/find-the-array-排列-具有奇数索引的元素和-大于偶数索引的元素和/](https://www.geeksforgeeks.org/find-the-array-permutation-having-sum-of-elements-at-odd-indices-greater-than-sum-of-elements-at-even-indices/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到数组元素的[排列，使得奇数索引元素的和大于或等于偶数索引元素的和。](https://www.geeksforgeeks.org/permute-the-elements-of-an-array-following-given-order/)

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 1 4 2 3
> **解释:**
> 考虑给定数组的排列为{1，4，2，3}。
> 现在，奇数索引处的元素之和= (4 + 3) = 7，偶数索引处的元素之和= (1 + 2) = 3。
> 因为奇数指数元素的和大于偶数指数元素的和。因此，打印当前排列。
> 
> **输入:** arr[] = {123，45，67，89，60，33}
> **输出:** 33 123 45 89 60 67

**天真方法:**解决给定问题的最简单方法是[生成给定数组](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)的所有可能排列，并打印奇数索引元素之和大于或等于偶数索引元素之和的数组排列。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过[排序给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)并使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)进行优化。按照以下步骤解决问题:

*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定数组 **arr[]** 进行排序。
*   初始化两个变量，说 **i** 为 **0** 和 **j** 为**(N–1)**。
*   [使用变量 **K** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   如果 [**K** 的值为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则打印**arr【I】**的值，并将 **i** 的值增加 **1** 。
    *   否则，打印**arr【j】**的值，并通过 **1** 递减 **j** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation of
// array elements such that the sum of
// elements at odd āindices is greater
// than sum of elements at even indices
void rearrangeArray(int arr[], int n)
{
    // Sort the given array
    sort(arr, arr + n);

    // Initialize the two pointers
    int j = n - 1;
    int i = 0;

    // Traverse the array arr[]
    for (int k = 0; k < n; k++) {

        // Check if k is even
        if (k % 2 == 0) {
            cout << arr[i] << " ";

            // Increment the value
            // of i
            i++;
        }
        else {
            cout << arr[j] << " ";

            // Decrement the value
            // of j
            j--;
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 123, 45, 67, 89, 60, 33 };
    int N = sizeof(arr) / sizeof(arr[0]);
    rearrangeArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the permutation of
// array elements such that the sum of
// elements at odd āindices is greater
// than sum of elements at even indices
static void rearrangeArray(int arr[], int n)
{

    // Sort the given array
    Arrays.sort(arr);

    // Initialize the two pointers
    int j = n - 1;
    int i = 0;

    // Traverse the array arr[]
    for(int k = 0; k < n; k++)
    {

        // Check if k is even
        if (k % 2 == 0)
        {
            System.out.print(arr[i] + " ");

            // Increment the value
            // of i
            i++;
        }
        else
        {
            System.out.print(arr[j] + " ");

            // Decrement the value
            // of j
            j--;
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 123, 45, 67, 89, 60, 33 };
    int N = arr.length;

    rearrangeArray(arr, N);
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the permutation of
# array elements such that the sum of
# elements at odd āindices is greater
# than sum of elements at even indices
def rearrangeArray(arr, n):

    # Sort the given array
    arr = sorted(arr)

    # Initialize the two pointers
    j = n - 1
    i = 0

    # Traverse the array arr[]
    for k in range(n):

        # Check if k is even
        if (k % 2 == 0):
            print(arr[i], end = " ")

            # Increment the value
            # of i
            i += 1
        else:
            print(arr[j], end = " ")

            # Decrement the value
            # of j
            j -= 1

# Driver Code
if __name__ == '__main__':

    arr = [ 123, 45, 67, 89, 60, 33 ]
    N = len(arr)

    rearrangeArray(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the permutation of
// array elements such that the sum of
// elements at odd āindices is greater
// than sum of elements at even indices
static void rearrangeArray(int[] arr, int n)
{

    // Sort the given array
    Array.Sort(arr);

    // Initialize the two pointers
    int j = n - 1;
    int i = 0;

    // Traverse the array arr[]
    for(int k = 0; k < n; k++)
    {

        // Check if k is even
        if (k % 2 == 0)
        {
            Console.Write(arr[i] + " ");

            // Increment the value
            // of i
            i++;
        }
        else
        {
            Console.Write(arr[j] + " ");

            // Decrement the value
            // of j
            j--;
        }
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 123, 45, 67, 89, 60, 33 };
    int N = arr.Length;

    rearrangeArray(arr, N);
}
}

// This code is contributed by subham348
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the permutation of
// array elements such that the sum of
// elements at odd āindices is greater
// than sum of elements at even indices
function rearrangeArray(arr, n)
{

    // Sort the given array
    arr.sort((a, b) => a - b);

    // Initialize the two pointers
    let j = n - 1;
    let i = 0;

    // Traverse the array arr[]
    for(let k = 0; k < n; k++)
    {

        // Check if k is even
        if (k % 2 == 0)
        {
            document.write(arr[i] + " ");

            // Increment the value
            // of i
            i++;
        }
        else
        {
            document.write(arr[j] + " ");

            // Decrement the value
            // of j
            j--;
        }
    }
}

// Driver Code

    let arr = [ 123, 45, 67, 89, 60, 33 ];
    let N = arr.length;

    rearrangeArray(arr, N);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
33 123 45 89 60 67
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*