# 重新排列一个数组，使相同索引元素与另一个数组的按位“与”之和最大化

> 原文:[https://www . geeksforgeeks . org/重排一个数组以最大化同一个索引元素与另一个数组的按位求和/](https://www.geeksforgeeks.org/rearrange-an-array-to-maximize-sum-of-bitwise-and-of-same-indexed-elements-with-another-array/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是找出数组**A【】**和**B【】**中相同索引元素的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的最大和，该和可以通过以任何顺序重新排列数组****B【】**来获得。**

****示例:****

> ****输入:** A[] = {1，2，3，4}，B[] = {3，4，1，2}
> **输出:** 10
> **解释:**获得最大值的一种可能方法是将数组 B[]重新排列为{1，2，3，4}。
> 因此，数组 A[]和 B[]的同索引元素的按位 AND 之和= { 1&1+2&2+3&3+4&4 = 10)，这是最大可能。**
> 
> ****输入:** A[] = {3，5，7，11}，B[] = {2，6，10，12 }
> T3】输出: 22**

****天真法:**解决问题最简单的方法是[生成数组](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/) **B[]** 的所有可能排列，对于每个排列，计算数组 **A[]** 和 **B[]** 中相同索引元素的**位 AND** 之和，并相应更新最大可能和。最后，打印最大可能的总和。**

****时间复杂度:** O(N！* N)
T3】辅助空间: O(1)**

****高效方法:**上述方法也可以基于以下观察进行优化:**

> ***   For each array element of **a []** , the idea is to use [bit mask](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/) to select the unselected array elements of **b []** , which will give the maximum bitwise AND sum of the current index.*   The idea is to use [bit to mask dynamic programming](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/) , because it has multiple [overlapping subproblems](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/) and [optimal substructure](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/) .*   Let's assume that **DP (I, mask)** represents the maximum bit sum of arrays **a []** and **I** , and the selected element of array **b []** is represented by the bit position of **mask** .*   Then the transition from one state to another can be defined as:
>     *   For the range [T0】 【0 [0, n]:
>         *   If [T4】 jT41] bit of **mask** is not set, **DP (I, mask) = max(dp(i, mask | (1 < < J))****

**按照以下步骤解决问题:**

*   **用值 **-1** 定义向量的[向量表示维度**N * 2<sup>N</sup>T7 的 **dp** ，以存储所有 dp 状态。**](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)**
*   **定义一个[递归 Dp 函数](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)比如**maximizeandtil(I，mask)** 来求两个数组中相同位置元素的按位 AND 的最大和 **A[]** 和 **B[]** :

    *   基本情况下，如果 **i** 等于 **N** ，则返回 **0** 。
    *   如果 **dp[i][mask]** 不等于 **-1** 即已经访问过，则返回 **dp[i][mask]。**
    *   使用变量 **j** 迭代范围**【0，N-1】**，在每次迭代中，如果未设置掩码中的 **j <sup>第</sup>** 位，则将**DP【I】【掩码】**更新为**DP【I】【掩码】= max(DP【I】【掩码】，maximizeUtil(i+1，掩码| 2 <sup>j</sup> )。**
    *   最后，返回 **dp[i][mask]。**** 
*   **调用[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **maximizeAnd(0，0)** 并打印其返回值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement recursive DP
int maximizeAnd(int i, int mask,
                int* A, int* B, int N,
                vector<vector<int> >& dp)
{
    // If i is equal to N
    if (i == N)
        return 0;

    // If dp[i][mask] is not
    // equal to -1
    if (dp[i][mask] != -1)
        return dp[i][mask];

    // Iterate over the array B[]
    for (int j = 0; j < N; ++j) {

        // If current element
        // is not yet selected
        if (!(mask & (1 << j))) {

            // Update dp[i][mask]
            dp[i][mask] = max(
                dp[i][mask],
                (A[i] & B[j])
                    + maximizeAnd(i + 1, mask | (1 << j), A,
                                  B, N, dp));
        }
    }
    // Return dp[i][mask]
    return dp[i][mask];
}

// Function to obtain maximum sum
// of Bitwise AND of same-indexed
// elements from the arrays A[] and B[]
int maximizeAndUtil(int* A, int* B, int N)
{
    // Stores all dp-states
    vector<vector<int> > dp(
        N, vector<int>(1 << N + 1, -1));

    // Returns the maximum value
    // returned by the function maximizeAnd()
    return maximizeAnd(0, 0, A, B, N, dp);
}

// Driver Code
int main()
{
    int A[] = { 3, 5, 7, 11 };
    int B[] = { 2, 6, 10, 12 };
    int N = sizeof A / sizeof A[0];

    cout << maximizeAndUtil(A, B, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to implement recursive DP
    static int maximizeAnd(int i, int mask, int A[],
                           int B[], int N, int[][] dp)
    {
        // If i is equal to N
        if (i == N)
            return 0;

        // If dp[i][mask] is not
        // equal to -1
        if (dp[i][mask] != -1)
            return dp[i][mask];

        // Iterate over the array B[]
        for (int j = 0; j < N; ++j) {

            // If current element
            // is not yet selected
            if ((mask & (1 << j)) == 0) {

                // Update dp[i][mask]
                dp[i][mask] = Math.max(
                    dp[i][mask],
                    (A[i] & B[j])
                        + maximizeAnd(i + 1,
                                      mask | (1 << j), A, B,
                                      N, dp));
            }
        }
        // Return dp[i][mask]
        return dp[i][mask];
    }

    // Function to obtain maximum sum
    // of Bitwise AND of same-indexed
    // elements from the arrays A[] and B[]
    static int maximizeAndUtil(int A[], int B[], int N)
    {

        // Stores all dp-states
        int dp[][] = new int[N][(1 << N) + 1];
        for (int dd[] : dp)
            Arrays.fill(dd, -1);

        // Returns the maximum value
        // returned by the function maximizeAnd()
        return maximizeAnd(0, 0, A, B, N, dp);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 3, 5, 7, 11 };
        int B[] = { 2, 6, 10, 12 };
        int N = A.length;

        System.out.print(maximizeAndUtil(A, B, N));
    }
}

// This code is contributed by Kingash.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to implement recursive DP
def maximizeAnd(i, mask, A, B, N, dp):

    # If i is equal to N
    if (i == N):
        return 0

    # If dp[i][mask] is not
    # equal to -1
    if (dp[i][mask] != -1):
        return dp[i][mask]

    # Iterate over the array B[]
    for j in range(N):

        # If current element
        # is not yet selected
        if ((mask & (1 << j)) == 0):

            # Update dp[i][mask]
            dp[i][mask] = max(
                dp[i][mask],(A[i] & B[j]) +
                maximizeAnd(i + 1, mask | (1 << j),
                            A, B, N, dp))

    # Return dp[i][mask]
    return dp[i][mask]

# Function to obtain maximum sum
# of Bitwise AND of same-indexed
# elements from the arrays A[] and B[]
def maximizeAndUtil(A, B, N):

    # Stores all dp-states
    temp = [-1 for i in range(1 << N + 1)]
    dp = [temp for i in range(N)]

    # Returns the maximum value
    # returned by the function maximizeAnd()
    return maximizeAnd(0, 0, A, B, N, dp)

# Driver Code
if __name__ == '__main__':

    A = [ 3, 5, 7, 11 ]
    B = [ 2, 6, 10, 12 ]
    N = len(A)

    print(maximizeAndUtil(A, B, N))

# This code is contributed by ipg2016107
```

## **C#**

```
// C# program for the above approach
using System;

class GFG {

    // Function to implement recursive DP
    static int maximizeAnd(int i, int mask, int[] A,
                           int[] B, int N, int[,] dp)
    {
        // If i is equal to N
        if (i == N)
            return 0;

        // If dp[i][mask] is not
        // equal to -1
        if (dp[i, mask] != -1)
            return dp[i, mask];

        // Iterate over the array B[]
        for (int j = 0; j < N; ++j) {

            // If current element
            // is not yet selected
            if ((mask & (1 << j)) == 0) {

                // Update dp[i][mask]
                dp[i, mask] = Math.Max(
                    dp[i, mask],
                    (A[i] & B[j])
                        + maximizeAnd(i + 1,
                                      mask | (1 << j), A, B,
                                      N, dp));
            }
        }
        // Return dp[i][mask]
        return dp[i, mask];
    }

    // Function to obtain maximum sum
    // of Bitwise AND of same-indexed
    // elements from the arrays A[] and B[]
    static int maximizeAndUtil(int[] A, int[] B, int N)
    {

        // Stores all dp-states
        int[,] dp = new int[N, (1 << N) + 1];
        for(int i = 0; i<N; i++)
        {
            for(int j =0 ; j<(1 << N) + 1; j++)
            {
                dp[i, j] = -1;
            }
        }

        // Returns the maximum value
        // returned by the function maximizeAnd()
        return maximizeAnd(0, 0, A, B, N, dp);
    }

    // Driver Code
    static void Main()
    {
        int[] A = { 3, 5, 7, 11 };
        int[] B = { 2, 6, 10, 12 };
        int N = A.Length;

        Console.Write(maximizeAndUtil(A, B, N));
    }
}

// This code is contributed by sanjoy_62.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to implement recursive DP
function maximizeAnd(i, mask, A, B, N, dp)
{

    // If i is equal to N
    if (i == N)
        return 0;

    // If dp[i][mask] is not
    // equal to -1
    if (dp[i][mask] != -1)
        return dp[i][mask];

    // Iterate over the array B[]
    for(var j = 0; j < N; ++j)
    {

        // If current element
        // is not yet selected
        if (!(mask & (1 << j)))
        {

            // Update dp[i][mask]
            dp[i][mask] = Math.max(
                dp[i][mask], (A[i] & B[j]) +
                maximizeAnd(i + 1, mask | (1 << j), A,
                            B, N, dp));
        }
    }

    // Return dp[i][mask]
    return dp[i][mask];
}

// Function to obtain maximum sum
// of Bitwise AND of same-indexed
// elements from the arrays A[] and B[]
function maximizeAndUtil(A, B, N)
{

    // Stores all dp-states
    var dp = Array.from(
        Array(N), () => Array(1 << N + 1).fill(-1));

    // Returns the maximum value
    // returned by the function maximizeAnd()
    return maximizeAnd(0, 0, A, B, N, dp);
}

// Driver Code
var A = [ 3, 5, 7, 11 ];
var B = [ 2, 6, 10, 12 ];
var N = A.length

document.write(maximizeAndUtil(A, B, N));

// This code is contributed by rrrtnx

</script>
```

****Output:** 

```
22
```** 

****时间复杂度:**O(N<sup>2</sup>* 2<sup>N)</sup>
**辅助空间:** O(N * 2 <sup>N</sup>**