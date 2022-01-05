# 查询以检查来自索引[L，R]的数组元素是否形成算术级数

> 原文:[https://www . geesforgeks . org/query-to-check-if-array-elements-from-indexs-l-r-forms-a-算术级数-or-not/](https://www.geeksforgeeks.org/queries-to-check-if-array-elements-from-indices-l-r-forms-an-arithmetic-progression-or-not/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由 **M** 个查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**Q【】【2】**形式的 **{L，R}** ，每个查询的任务是检查数组元素是否在**【L，R】**范围内形成[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)。如果发现**为真**，打印**“是”**。否则，打印**“否”。**

**示例:**

> **输入:** arr[] = {1，3，5，7，6，5，4，1}，Q[][] = {{0，3}，{3，4}，{2，4}}
> **输出:**
> 是
> 是
> 否
> T9】解释:
> **查询 1:** 范围内的数组元素是{1，3，5，7}，它们构成一个算术因此，打印“是”。
> **查询 2:** 数组在[3，4]范围内的元素是{7，6}，形成一个公差为-1 的算术数列。因此，打印“是”。
> **查询 3:** 数组在[2，4]范围内的元素为{5，7，6}，不构成算术级数。因此，打印“是”。
> 
> **输入:** arr[] = {1，2}，Q[][] = {{0，0}，{0，1}，{0，1}}
> **输出:**
> 是
> 是
> 是

**天真方法:**解决这个问题最简单的方法是在每个查询的**【L，R】**范围内遍历给定的数组，检查所有相邻元素之间的公共差异是否相同。如果差异相同，则打印**“是”**。否则，打印**“否”**。

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   其思想是使用[双指针算法](https://www.geeksforgeeks.org/two-pointers-technique/)对辅助数组中数组的每个 **i <sup>第</sup>元素**从任意索引 **i** 开始预计算形成 AP 的子数组的最长长度。
*   对于给定的范围**【L，R】**，如果**DP【L】**的值大于或等于**(R–L)**，则该范围将始终形成一个 **AP** ，因为**(R–L)**是元素的当前范围，**DP【L】**存储从索引 **L** 开始形成 AP 的最长子阵列的[长度，然后](https://www.geeksforgeeks.org/longest-subarray-forming-an-arithmetic-progression-ap/)

按照以下步骤解决问题:

*   初始化一个数组，比如 **dp[]** ，以存储从该索引处每个元素的每个索引开始的最长子数组的长度。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   将变量 say **j** 初始化为 **(i + 1)** 以存储从索引 **i** 形成[等差数列](https://www.geeksforgeeks.org/progressions-ap-gp-hp/)的最后一个索引数组。
    *   增加 **j** 的值，直到 **(j + 1 < N)** 和**(arr[j]–arr[j–1])**与**(arr[I+1]–arr[I])相同。**
    *   使用变量迭代范围**【I，j–1】**，比如 **K** ，并将**DP【K】**的值更新为**(j–K)**。
    *   将 **i** 的值更新为 **j** 。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q[]**，对于每个查询 **{L，R}** ，如果**DP【L】**的值大于或等于**(R–L)**，则打印**“是”**。否则，打印**“否”。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the given range
// of queries form an AP or not in the
// given array arr[]
void findAPSequence(int arr[], int N,
                    int Q[][2], int M)
{
    // Stores length of the longest
    // subarray forming AP for every
    // array element
    int dp[N + 5] = { 0 };

    // Iterate over the range [0, N]
    for (int i = 0; i + 1 < N;) {

        // Stores the index of the last
        // element of forming AP
        int j = i + 1;

        // Iterate until the element at
        // index (j, j + 1) forms AP
        while (j + 1 < N
               && arr[j + 1] - arr[j]
                      == arr[i + 1] - arr[i])

            // Increment j by 1
            j++;

        // Traverse the current subarray
        // over the range [i, j - 1]
        for (int k = i; k < j; k++) {

            // Update the length of the
            // longest subarray at index k
            dp[k] = j - k;
        }

        // Update the value of i
        i = j;
    }

    // Traverse the given queries
    for (int i = 0; i < M; i++) {

        // Print the result
        if (dp[Q[i][0]]
            >= Q[i][1] - Q[i][0]) {
            cout << "Yes" << endl;
        }

        // Otherwise
        else {
            cout << "No" << endl;
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 7, 6, 5, 4, 1 };
    int Q[][2] = { { 0, 3 }, { 3, 4 }, { 2, 4 } };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(Q) / sizeof(Q[0]);

    findAPSequence(arr, N, Q, M);

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

// Function to check if the given range
// of queries form an AP or not in the
// given array arr[]
static void findAPSequence(int arr[], int N,
                           int Q[][], int M)
{

    // Stores length of the longest
    // subarray forming AP for every
    // array element
    int dp[] = new int[N + 5];

    // Iterate over the range [0, N]
    for(int i = 0; i + 1 < N;)
    {

        // Stores the index of the last
        // element of forming AP
        int j = i + 1;

        // Iterate until the element at
        // index (j, j + 1) forms AP
        while (j + 1 < N && arr[j + 1] - arr[j] ==
                            arr[i + 1] - arr[i])

            // Increment j by 1
            j++;

        // Traverse the current subarray
        // over the range [i, j - 1]
        for(int k = i; k < j; k++)
        {

            // Update the length of the
            // longest subarray at index k
            dp[k] = j - k;
        }

        // Update the value of i
        i = j;
    }

    // Traverse the given queries
    for(int i = 0; i < M; i++)
    {

        // Print the result
        if (dp[Q[i][0]] >= Q[i][1] - Q[i][0])
        {
            System.out.println("Yes");
        }

        // Otherwise
        else
        {
            System.out.println("No");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 5, 7, 6, 5, 4, 1 };
    int Q[][] = { { 0, 3 }, { 3, 4 }, { 2, 4 } };
    int N = arr.length;
    int M = Q.length;

    findAPSequence(arr, N, Q, M);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given range
# of queries form an AP or not in the
# given array arr[]
def findAPSequence(arr, N, Q, M):

    # Stores length of the longest
    # subarray forming AP for every
    # array element
    dp = [0] * (N + 5)

    # Iterate over the range [0, N]
    i = 0

    while i + 1 < N:

        # Stores the index of the last
        # element of forming AP
        j = i + 1

        # Iterate until the element at
        # index (j, j + 1) forms AP
        while (j + 1 < N and
           arr[j + 1] - arr[j] ==
           arr[i + 1] - arr[i]):

            # Increment j by 1
            j += 1

        # Traverse the current subarray
        # over the range [i, j - 1]
        for k in range(i, j):

            # Update the length of the
            # longest subarray at index k
            dp[k] = j - k

        # Update the value of i
        i = j

    # Traverse the given queries
    for i in range(M):

        # Print the result
        if (dp[Q[i][0]] >= Q[i][1] - Q[i][0]):
            print("Yes")

        # Otherwise
        else:
            print("No")

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 3, 5, 7, 6, 5, 4, 1 ]
    Q = [ [ 0, 3 ], [ 3, 4 ], [ 2, 4 ] ]
    N = len(arr)
    M = len(Q)

    findAPSequence(arr, N, Q, M)

# This code is contributed by ukasp
```

## C#

```
// C# code for above approach
using System;

public class GFG
{

    // Function to check if the given range
// of queries form an AP or not in the
// given array arr[]
static void findAPSequence(int[] arr, int N,
                           int[, ] Q, int M)
{

    // Stores length of the longest
    // subarray forming AP for every
    // array element
    int[] dp = new int[N + 5];

    // Iterate over the range [0, N]
    for(int i = 0; i + 1 < N;)
    {

        // Stores the index of the last
        // element of forming AP
        int j = i + 1;

        // Iterate until the element at
        // index (j, j + 1) forms AP
        while (j + 1 < N && arr[j + 1] - arr[j] ==
                            arr[i + 1] - arr[i])

            // Increment j by 1
            j++;

        // Traverse the current subarray
        // over the range [i, j - 1]
        for(int k = i; k < j; k++)
        {

            // Update the length of the
            // longest subarray at index k
            dp[k] = j - k;
        }

        // Update the value of i
        i = j;
    }

    // Traverse the given queries
    for(int i = 0; i < M; i++)
    {

        // Print the result
        if (dp[Q[i, 0]] >= Q[i, 1] - Q[i, 0])
        {
            Console.WriteLine("Yes");
        }

        // Otherwise
        else
        {
            Console.WriteLine("No");
        }
    }
}

    static public void Main (){
      int[] arr = { 1, 3, 5, 7, 6, 5, 4, 1 };
    int[, ] Q = { { 0, 3 }, { 3, 4 }, { 2, 4 } };
    int N = arr.Length;
    int M = Q.GetLength(0);

    findAPSequence(arr, N, Q, M);
    }
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// javascript program for the above approach
    // Function to check if the given range
    // of queries form an AP or not in the
    // given array arr
    function findAPSequence(arr , N , Q , M) {

        // Stores length of the longest
        // subarray forming AP for every
        // array element
        var dp = Array(N + 5).fill(0);

        // Iterate over the range [0, N]
        for (i = 0; i + 1 < N;) {

            // Stores the index of the last
            // element of forming AP
            var j = i + 1;

            // Iterate until the element at
            // index (j, j + 1) forms AP
            while (j + 1 < N && arr[j + 1] - arr[j] == arr[i + 1] - arr[i])

                // Increment j by 1
                j++;

            // Traverse the current subarray
            // over the range [i, j - 1]
            for (k = i; k < j; k++) {

                // Update the length of the
                // longest subarray at index k
                dp[k] = j - k;
            }

            // Update the value of i
            i = j;
        }

        // Traverse the given queries
        for (i = 0; i < M; i++) {

            // Print the result
            if (dp[Q[i][0]] >= Q[i][1] - Q[i][0]) {
                document.write("Yes <br/>");
            }

            // Otherwise
            else {
                document.write("No <br/>");
            }
        }
    }

    // Driver Code

        var arr = [ 1, 3, 5, 7, 6, 5, 4, 1 ];
        var Q = [ [ 0, 3 ], [ 3, 4 ], [ 2, 4 ] ];
        var N = arr.length;
        var M = Q.length;

        findAPSequence(arr, N, Q, M);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
Yes
Yes
No
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*