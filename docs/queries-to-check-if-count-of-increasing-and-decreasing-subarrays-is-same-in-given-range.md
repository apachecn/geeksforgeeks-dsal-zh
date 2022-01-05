# 查询在给定范围内增加和减少子阵列的计数是否相同

> 原文:[https://www . geeksforgeeks . org/query-to-check-count-of-递增和递减子阵列-在给定范围内是否相同/](https://www.geeksforgeeks.org/queries-to-check-if-count-of-increasing-and-decreasing-subarrays-is-same-in-given-range/)

给定一个由 **N** 个整数和一个数组**Q【】【】**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其中每一行都是 **{L，R}** 形式的查询。每个查询的任务是检查**【L，R】**范围内增加和减少子阵列的计数是否相同。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {11，13，12，14}，Q[][] = {{1，4}，{2，4}}
> **输出:**
> 否
> 是
> **说明:**
> **查询 1:** 在[1，4]范围内有两个递增的子阵列{11，13}和{12，14}。但是在范围[1，4]中只有一个递减的子阵列{13，12}。
> 因此，打印编号
> **查询 2:** 范围【2，4】内只有一个递增子阵列{12，14}和一个递减子阵列{13，12}。
> 因此，打印是。
> 
> **输入:** arr[] = {16，24，32，18，14}，Q = {{1，5}，{2，3}，{2，4 } }
> T3】输出:T5】是
> 否
> 是

**天真法:**解决这个问题最简单的方法是[从子阵 **{arr[L]，arr[R]}** 生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，检查增减子阵的个数是否相同。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:**O(Q * N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，观察到每个增加的子阵列后面跟着一个减少的子阵列，反之亦然，即它们交替增加或减少。因此，增减子阵的数量最多相差**1**。因此，想法是检查范围中的第一对和最后一对元素是否都形成递增对。如果发现属实，则打印**“否”**。否则，打印**“是”**。对每个查询执行上述步骤，得到 ***O(1)*** 中的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if given range
// have equal number of increasing
// as well as decreasing subarrays
void checkCount(int A[], int Q[][2],
                int q)
{

    // Traverse each query
    for (int i = 0; i < q; i++) {

        int L = Q[i][0];
        int R = Q[i][1];

        // For 0-based indexing
        L--, R--;

        // Condition for same count of
        // increasing & decreasing subarray
        if ((A[L] < A[L + 1])
            != (A[R - 1] < A[R])) {
            cout << "Yes\n";
        }
        else {
            cout << "No\n";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 11, 13, 12, 14 };
    int Q[][2] = { { 1, 4 }, { 2, 4 } };

    int q = sizeof(Q) / sizeof(Q[0]);

    checkCount(arr, Q, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if given range
// have equal number of increasing
// as well as decreasing subarrays
static void checkCount(int A[], int Q[][],
                       int q)
{

    // Traverse each query
    for(int i = 0; i < q; i++)
    {
        int L = Q[i][0];
        int R = Q[i][1];

        // For 0-based indexing
        L--;
        R--;

        // Condition for same count of
        // increasing & decreasing subarray
        if ((A[L] < A[L + 1]) !=
            (A[R - 1] < A[R]))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 11, 13, 12, 14 };
    int Q[][] = { { 1, 4 }, { 2, 4 } };

    int q = Q.length;

    checkCount(arr, Q, q);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if given range
# have equal number of increasing
# as well as decreasing subarrays
def checkCount(A, Q, q):

    # Traverse each query
    for i in range(q):
        L = Q[i][0]
        R = Q[i][1]

        # For 0-based indexing
        L -= 1
        R -= 1

        # Condition for same count of
        # increasing & decreasing subarray
        if ((A[L] < A[L + 1]) !=
            (A[R - 1] < A[R])):
            print("Yes")
        else:
            print("No")

# Driver Code
if __name__ == '__main__':

    arr = [ 11, 13, 12, 14 ]
    Q = [ [ 1, 4 ], [ 2, 4 ] ]

    q = len(Q)

    checkCount(arr, Q, q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if given range
// have equal number of increasing
// as well as decreasing subarrays
static void checkCount(int[] A, int[,] Q,
                       int q)
{

    // Traverse each query
    for(int i = 0; i < q; i++)
    {
        int L = Q[i, 0];
        int R = Q[i, 1];

        // For 0-based indexing
        L--;
        R--;

        // Condition for same count of
        // increasing & decreasing subarray
        if ((A[L] < A[L + 1]) !=
            (A[R - 1] < A[R]))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 11, 13, 12, 14 };
    int[,] Q = { { 1, 4 }, { 2, 4 } };

    int q = Q.GetLength(0);

    checkCount(arr, Q, q);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if given range
// have equal number of increasing
// as well as decreasing subarrays
function checkCount(A, Q, q)
{

    // Traverse each query
    for(let i = 0; i < q; i++)
    {
        let L = Q[i][0];
        let R = Q[i][1];

        // For 0-based indexing
        L--;
        R--;

        // Condition for same count of
        // increasing & decreasing subarray
        if ((A[L] < A[L + 1]) !=
            (A[R - 1] < A[R]))
        {
            document.write("Yes" + "<br/>");
        }
        else
        {
            document.write("No" + "<br/>");
        }
    }
}

// Driver Code

    let arr = [ 11, 13, 12, 14 ];
    let Q = [[ 1, 4 ], [ 2, 4 ]];

    let q = Q.length;

    checkCount(arr, Q, q);

</script>
```

**Output:** 

```
No
Yes
```

***时间复杂度:**O(Q)*
T5**辅助空间:** O(1)