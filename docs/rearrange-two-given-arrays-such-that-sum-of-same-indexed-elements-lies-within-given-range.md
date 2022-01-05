# 重新排列两个给定的数组，使得相同的索引元素的和在给定的范围内

> 原文:[https://www . geeksforgeeks . org/relay-两个给定数组-相同索引元素的和-位于给定范围内/](https://www.geeksforgeeks.org/rearrange-two-given-arrays-such-that-sum-of-same-indexed-elements-lies-within-given-range/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**由 **N** 个正整数和一个偶数 **K** 组成，任务是在重新排列给定数组后，检查两个数组中相同索引元素的和是否在**【K/2，K】**的范围内。如果有可能得到这样的安排，那么打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr1[] = {1，4，3，5}，arr2[] = {0，2，1，1}，K = 6
> **输出:**是
> **解释:**将 arr1[]重新排列为{1，4，3，5}并将 arr2[]重新排列为{2，0，1，1}可确保相同索引元素的总和位于范围[3，6]内。因此，打印“是”。
> 
> **输入:** arr1[] = {2，0}，arr2[] = {3，4}，K = 2
> **输出:**否
> **说明:**不可能这样安排

**简单方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)的所有可能排列，并检查任何可能的排列是否满足给定条件。如果发现属实，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:** O((N！) <sup>2</sup> )*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，请按照以下步骤解决问题:

*   [按递增顺序排列数组 arr 1[]](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [按降序排列数组 arr 2[]](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并检查范围**【0，N–1】**内 **i** 所有可能值的[元素之和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) arr1[i]和 arr2[i]是否在范围**【K/2，K】**内。如果发现是真的，那么打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists any
// arrangements of the arrays such that
// sum of element lie in the range [K/2, K]
void checkArrangement(int A1[], int A2[],
                      int n, int k)
{
    // Sort the array arr1[] in
    // increasing order
    sort(A1, A1 + n);

    // Sort the array arr2[] in
    // decreasing order
    sort(A2, A2 + n, greater<int>());

    int flag = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If condition is not satisfied
        // break the loop
        if ((A1[i] + A2[i] > k)
            || (A1[i] + A2[i] < k / 2)) {

            flag = 1;
            break;
        }
    }

    // Print the result
    if (flag == 1)
        cout << "No";
    else
        cout << "Yes";
}

// Driver Code
int main()
{
    int arr1[] = { 1, 3, 4, 5 };
    int arr2[] = { 2, 0, 1, 1 };

    int K = 6;

    int N = sizeof(arr1)

            / sizeof(arr1[0]);

    checkArrangement(arr1, arr2, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if there exists any
// arrangements of the arrays such that
// sum of element lie in the range [K/2, K]
static void checkArrangement(Integer[] A1,
                             Integer[] A2,
                             int n, int k)
{

    // Sort the array arr1[] in
    // increasing order
    Arrays.sort(A1);

    // Sort the array arr2[] in
    // decreasing order
    Arrays.sort(A2, Collections.reverseOrder());

    int flag = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If condition is not satisfied
        // break the loop
        if ((A1[i] + A2[i] > k) ||
            (A1[i] + A2[i] < k / 2))
        {
            flag = 1;
            break;
        }
    }

    // Print the result
    if (flag == 1)
        System.out.println("No");
    else
        System.out.println("Yes");
}

// Driver Code
public static void main(String[] args)
{
    Integer[] arr1 = { 1, 3, 4, 5 };
    Integer[] arr2 = { 2, 0, 1, 1 };

    int K = 6;

    int N = arr1.length;

    checkArrangement(arr1, arr2, N, K);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exists any
# arrangements of the arrays such that
# sum of element lie in the range [K/2, K]
def checkArrangement(A1, A2, n, k):

    # Sort the array arr1[] in
    # increasing order
    A1 = sorted(A1)

    # Sort the array arr2[] in
    # decreasing order
    A2 = sorted(A2)

    A2 = A2[::-1]

    flag = 0

    # Traverse the array
    for i in range(n):

        # If condition is not satisfied
        # break the loop
        if ((A1[i] + A2[i] > k) or
            (A1[i] + A2[i] < k // 2)):
            flag = 1
            break

    # Print the result
    if (flag == 1):
        print("No")
    else:
        print("Yes")

# Driver Code
if __name__ == '__main__':

    arr1 = [ 1, 3, 4, 5 ]
    arr2 = [ 2, 0, 1, 1 ]

    K = 6

    N = len(arr1)

    checkArrangement(arr1, arr2, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG{

// Function to check if there exists any
// arrangements of the arrays such that
// sum of element lie in the range [K/2, K]
static void checkArrangement(int[] A1, int[] A2,
                             int n, int k)
{

    // Sort the array arr1[] in
    // increasing order
    Array.Sort(A1);

    // Sort the array arr2[] in
    // decreasing order
    Array.Sort(A2);
    Array.Reverse(A2);

    int flag = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If condition is not satisfied
        // break the loop
        if ((A1[i] + A2[i] > k) ||
            (A1[i] + A2[i] < k / 2))
        {
            flag = 1;
            break;
        }
    }

    // Print the result
    if (flag == 1)
        Console.WriteLine("No");
    else
        Console.WriteLine("Yes");
}

// Driver Code
public static void Main()
{
    int[] arr1 = { 1, 3, 4, 5 };
    int[] arr2 = { 2, 0, 1, 1 };

    int K = 6;

    int N = arr1.Length;

    checkArrangement(arr1, arr2, N, K);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to check if there exists any
// arrangements of the arrays such that
// sum of element lie in the range [K/2, K]
function checkArrangement( A1, A2, n, k)
{

    // Sort the array arr1[] in
    // increasing order
    A1.sort();

    // Sort the array arr2[] in
    // decreasing order
    A2.sort();
    A2.reverse();

    let flag = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // If condition is not satisfied
        // break the loop
        if ((A1[i] + A2[i] > k) ||
            (A1[i] + A2[i] < k / 2))
        {
            flag = 1;
            break;
        }
    }

    // Prlet the result
    if (flag == 1)
        document.write("No");
    else
        document.write("Yes");
}

// Driver Code

    let arr1 = [ 1, 3, 4, 5 ];
    let arr2 = [ 2, 0, 1, 1 ];

    let K = 6;

    let N = arr1.length;

    checkArrangement(arr1, arr2, N, K);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*