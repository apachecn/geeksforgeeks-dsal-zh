# 给定坐标下最大矩形的面积

> 原文:[https://www . geeksforgeeks . org/给定坐标的最大矩形面积/](https://www.geeksforgeeks.org/area-of-the-largest-rectangle-possible-from-given-coordinates/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和**arr 2[]****N**表示 **N** 表格的坐标 **(arr1[i]，0)** 和 **M** 正整数表示 **M** 表格的坐标 **(arr2[j]，1** )，其中 **1 ≤ i ≤ N** 和**任务是找到使用这些坐标可以形成的最大矩形的面积。如果不能形成矩形，打印 **0** 。**

**示例:**

> **输入:** arr1[] = {1，2，4}，arr2[] = {1，3，4}
> **输出:** 3
> **解释:**最大的矩形可能是{(1，0)，(1，1)，(4，0)，(4，1)}。
> 因此，矩形的面积=长度*宽度=(4–1)*(1–0)= 3
> 
> **输入:** arr1[] = {1，3，5}，arr2[] = {4，2，10}
> **输出:** 0
> **说明:**不能形成矩形。因此，答案是零。

**简单方法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr1[]** ，对于每个 **i** ，使用变量 **j** 遍历 **arr2[]** 中的点。如果 **arr1[i]** 等于 **arr2[j]** ，则将值 **arr1[i]** 存储在单独的数组中，比如 **ans[]** 。找到所有这些值后，对 **ans[]** 数组进行排序，将最大面积打印为**ans[L]–ans[0]**，其中 **L** 是 **ans[]** 最后一个元素的索引，因为矩形的宽度始终为 **1** 。

***时间复杂度:** O(N*M)*
***辅助空间:** O(M + N)*

**高效方法:**思路是使用[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)和[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。观察矩形的宽度始终为 **1** 。因此，最大面积可以通过最大化其长度来找到。按照以下步骤解决问题:

*   [排序给定的数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr1[]** 和 **arr2[]** 。
*   初始化变量，**用 **0** 开始**和**结束**来存储长度的起点和终点。另外，初始化变量 **i** 和 **j** 分别遍历数组 **arr1[]** 和 **arr2[]** 。
*   当 **i** 小于 **N** 和 **j** 小于 **M** 时，检查以下情况:
    *   如果 **arr1[i]** 与 **arr2[j]** 相同，且 start 为 **0** ，则将 **start** 更新为 **start = arr1[i]** 。否则，将 **end** 更新为 **end = arr1[i]** ，然后将 **i** 和 **j** 增加 **1** 。
    *   如果 **arr1[i]** 大于 **arr2[j]** ，则将 **j** 增加 **1** 。否则，将 **i** 增加 **1** 。
*   如果**开始**或**结束**是 **0** ，打印 **0** 。否则，打印**(结束–开始)**作为最大可能区域。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible
// area of a rectangle
int largestArea(int arr1[], int n,
                int arr2[], int m)
{
    // Initialize variables
    int end = 0, start = 0, i = 0, j = 0;

    // Sort array arr1[]
    sort(arr1, arr1 + n);

    // Sort array arr2[]
    sort(arr2, arr2 + m);

    // Traverse arr1[] and arr2[]
    while (i < n and j < m) {

        // If arr1[i] is same as arr2[j]
        if (arr1[i] == arr2[j]) {

            // If no starting point
            // is found yet
            if (start == 0)
                start = arr1[i];
            else
                // Update maximum end
                end = arr1[i];
            i++;
            j++;
        }

        // If arr[i] > arr2[j]
        else if (arr1[i] > arr2[j])
            j++;
        else
            i++;
    }

    // If no rectangle is found
    if (end == 0 or start == 0)
        return 0;
    else
        // Return the area
        return (end - start);
}

// Driver Code
int main()
{
    // Given point
    int arr1[] = { 1, 2, 4 };

    // Given length
    int N = sizeof(arr1) / sizeof(arr1[0]);

    // Given points
    int arr2[] = { 1, 3, 4 };

    // Given length
    int M = sizeof(arr2) / sizeof(arr2[0]);

    // Function Call
    cout << largestArea(arr1, N, arr2, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum possible
// area of a rectangle
static int largestArea(int arr1[], int n,
                       int arr2[], int m)
{

    // Initialize variables
    int end = 0, start = 0, i = 0, j = 0;

    // Sort array arr1[]
    Arrays.sort(arr1);

    // Sort array arr2[]
    Arrays.sort(arr1);

    // Traverse arr1[] and arr2[]
    while (i < n && j < m)
    {

        // If arr1[i] is same as arr2[j]
        if (arr1[i] == arr2[j])
        {

            // If no starting point
            // is found yet
            if (start == 0)
                start = arr1[i];
            else

                // Update maximum end
                end = arr1[i];

            i++;
            j++;
        }

        // If arr[i] > arr2[j]
        else if (arr1[i] > arr2[j])
            j++;
        else
            i++;
    }

    // If no rectangle is found
    if (end == 0 || start == 0)
        return 0;
    else

        // Return the area
        return (end - start);
}

// Driver Code
public static void main(String args[])
{

    // Given point
    int arr1[] = { 1, 2, 4 };

    // Given length
    int N = arr1.length;

    // Given points
    int arr2[] = { 1, 3, 4 };

    // Given length
    int M = arr2.length;

    // Function Call
    System.out.println(largestArea(arr1, N,
                                   arr2, M));
}
}

// This code is contributed by bolliranadheer
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum possible
# area of a rectangle
def largestArea(arr1, n, arr2, m):

    # Initialize variables
    end = 0
    start = 0
    i = 0
    j = 0

    # Sort array arr1[]
    arr1.sort(reverse = False)

    # Sort array arr2[]
    arr2.sort(reverse = False)

    # Traverse arr1[] and arr2[]
    while (i < n and j < m):

        # If arr1[i] is same as arr2[j]
        if (arr1[i] == arr2[j]):

            # If no starting point
            # is found yet
            if (start == 0):
                start = arr1[i]
            else:

                # Update maximum end
                end = arr1[i]

            i += 1
            j += 1

        # If arr[i] > arr2[j]
        elif (arr1[i] > arr2[j]):
            j += 1
        else:
            i += 1

    # If no rectangle is found
    if (end == 0 or start == 0):
        return 0
    else:

        # Return the area
        return (end - start)

# Driver Code
if __name__ == '__main__':

    # Given point
    arr1 = [ 1, 2, 4 ]

    # Given length
    N = len(arr1)

    # Given points
    arr2 = [ 1, 3, 4 ]

    # Given length
    M =  len(arr2)

    # Function Call
    print(largestArea(arr1, N, arr2, M))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum possible
// area of a rectangle
static int largestArea(int[] arr1, int n,
                       int[] arr2, int m)
{

    // Initialize variables
    int end = 0, start = 0, i = 0, j = 0;

    // Sort array arr1[]
    Array.Sort(arr1);

    // Sort array arr2[]
    Array.Sort(arr2);

    // Traverse arr1[] and arr2[]
    while (i < n && j < m)
    {

        // If arr1[i] is same as arr2[j]
        if (arr1[i] == arr2[j])
        {

            // If no starting point
            // is found yet
            if (start == 0)
                start = arr1[i];
            else

                // Update maximum end
                end = arr1[i];

            i++;
            j++;
        }

        // If arr[i] > arr2[j]
        else if (arr1[i] > arr2[j])
            j++;
        else
            i++;
    }

    // If no rectangle is found
    if (end == 0 || start == 0)
        return 0;
    else

        // Return the area
        return (end - start);
}

// Driver code
static void Main()
{

    // Given point
    int[] arr1 = { 1, 2, 4 };

    // Given length
    int N = arr1.Length;

    // Given points
    int[] arr2 = { 1, 3, 4 };

    // Given length
    int M = arr2.Length;

    // Function Call
    Console.WriteLine(largestArea(arr1, N,
                                  arr2, M));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum possible
// area of a rectangle
function largestArea(arr1, n,
                    arr2, m)
{

    // Initialize variables
    var end = 0, start = 0, i = 0, j = 0;

    // Sort array arr1[]
    arr1.sort();

    // Sort array arr2[]
    arr2.sort();

    // Traverse arr1[] and arr2[]
    while (i < n && j < m) {

        // If arr1[i] is same as arr2[j]
        if (arr1[i] == arr2[j]) {

            // If no starting point
            // is found yet
            if (start == 0)
                start = arr1[i];
            else
                // Update maximum end
                end = arr1[i];
            i++;
            j++;
        }

        // If arr[i] > arr2[j]
        else if (arr1[i] > arr2[j])
            j++;
        else
            i++;
    }

    // If no rectangle is found
    if (end == 0 || start == 0)
        return 0;
    else
        // Return the area
        return (end - start);
}

// Driver Code

// Given point
var arr1 = [ 1, 2, 4 ];

// Given length
var N = arr1.length;

// Given points
var arr2 = [ 1, 3, 4 ];

// Given length
var M = arr2.length;

// Function Call
document.write(largestArea(arr1, N, arr2, M));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * log N+M * log M)*
T5**辅助空间:** O(M+N)