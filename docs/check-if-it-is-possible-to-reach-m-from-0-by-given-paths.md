# 检查给定路径是否可以从 0 到达 M

> 原文:[https://www . geeksforgeeks . org/check-如果有可能，请按给定路径从 0 到达 m-/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-m-from-0-by-given-paths/)

给定由整数的 **N** [对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中每对 **(a，b)** 代表从 **a** 到 **b** 的路径，任务是检查是否有可能使用数组 **arr[]** 中的给定路径从 **0** 到达 **M** 。如果可能，那么打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {{0，2}、{2，2}、{2，5}、{4，5}}，M = 5
> **输出:**是
> **说明:**使用对{(0，2)、(2，5)}可以从 0 达到 5。
> 
> **输入:** arr[] = {{0，1}，{1，2}，{2，4}}，M = 5
> **输出:**否

**方法:**给定的问题可以通过使用给定的路径数组作为一对从 **0** 找到最右边的点来解决，然后如果最右边的点大于或等于 **M** ，这意味着在 **0** 到 **M** 之间有一条路径。否则就不是了。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如**最右边的[]** 和 **dp[]** ，分别存储从 **1** 点到最远点的距离，并用 **0** 初始化**最右边的[]** 的每个值。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**并将**最右边的【a[I][0]】**更新为**最右边的【a[I][0]】**和**的[最大值](https://www.geeksforgeeks.org/stdmax_element-in-cpp/)**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【M，0】**:
    *   将**DP【I】**的值更新为 **i** 。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【min(m，最右[i])，I 1】**，并将 **dp[i]** 更新为 **dp[i]** 和 **dp[j]** 的最大值。
*   如果**DP【0】**的值至少为**M**，则有可能达到从 **0** 到 **M** ，因此打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is
// possible to reach M from 0
void canReach0toM(int a[][2], int n,
                  int m)
{
    // Stores the farther point that
    // can reach from 1 point
    int rightMost[m + 1];

    // Stores the farthest point it
    // can go for each index i
    int dp[m + 1];

    // Initialize rightMost[i] with 0
    for (int i = 0; i <= m; i++) {
        rightMost[i] = 0;
    }

    // Traverse the array
    for (int i = 0; i < n; i++) {

        int a1 = a[i][0];
        int b1 = a[i][1];

        // Update the rightMost
        // position reached from a1
        rightMost[a1] = max(
            rightMost[a1], b1);
    }

    for (int i = m; i >= 0; i--) {

        dp[i] = i;

        // Find the farthest point
        // it can reach from i
        for (int j = min(m, rightMost[i]);
             j > i; j--) {
            dp[i] = max(dp[i], dp[j]);
        }
    }

    // If point < can be reached
    if (dp[0] >= m) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int arr[][2] = { { 0, 2 }, { 2, 2 },
                     { 2, 5 }, { 4, 5 } };
    int M = 5;
    int N = sizeof(arr) / sizeof(arr[0]);
    canReach0toM(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to check if it is
    // possible to reach M from 0
    static void canReach0toM(int[][] a, int n, int m)
    {

        // Stores the farther point that
        // can reach from 1 point
        int[] rightMost = new int[m + 1];

        // Stores the farthest point it
        // can go for each index i
        int[] dp = new int[m + 1];

        // Initialize rightMost[i] with 0
        for (int i = 0; i <= m; i++) {
            rightMost[i] = 0;
        }

        // Traverse the array
        for (int i = 0; i < n; i++) {

            int a1 = a[i][0];
            int b1 = a[i][1];

            // Update the rightMost
            // position reached from a1
            rightMost[a1] = Math.max(rightMost[a1], b1);
        }

        for (int i = m; i >= 0; i--) {

            dp[i] = i;

            // Find the farthest point
            // it can reach from i
            for (int j = Math.min(m, rightMost[i]); j > i;
                 j--) {
                dp[i] = Math.max(dp[i], dp[j]);
            }
        }

        // If point < can be reached
        if (dp[0] >= m) {
            System.out.print("Yes");
        }
        else {
            System.out.print("No");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] arr
            = { { 0, 2 }, { 2, 2 }, { 2, 5 }, { 4, 5 } };
        int M = 5;
        int N = arr.length;
        canReach0toM(arr, N, M);
    }
}

// This code is contributed by subhammahato348.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is
# possible to reach M from 0
def canReach0toM(a, n, m):

    # Stores the farther point that
    # can reach from 1 point
    rightMost = [0 for i in range(m + 1)]

    # Stores the farthest point it
    # can go for each index i
    dp = [0 for i in range(m + 1)]

    # Initialize rightMost[i] with 0
    for i in range(m + 1):
        rightMost[i] = 0

    # Traverse the array
    for i in range(n):
        a1 = a[i][0]
        b1 = a[i][1]

        # Update the rightMost
        # position reached from a1
        rightMost[a1] = max(rightMost[a1], b1)

    i = m

    while(i >= 0):
        dp[i] = i

        # Find the farthest point
        # it can reach from i
        j = min(m, rightMost[i])
        while(j > i):
            dp[i] = max(dp[i], dp[j])
            j -= 1

        i -= 1

    # If point < can be reached
    if (dp[0] >= m):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    arr = [ [ 0, 2 ], [ 2, 2 ],
            [ 2, 5 ], [ 4, 5 ] ]
    M = 5
    N = len(arr)

    canReach0toM(arr, N, M)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is
// possible to reach M from 0
static void canReach0toM(int[,] a, int n, int m)
{

    // Stores the farther point that
    // can reach from 1 point
    int[] rightMost = new int[m + 1];

    // Stores the farthest point it
    // can go for each index i
    int[] dp = new int[m + 1];

    // Initialize rightMost[i] with 0
    for(int i = 0; i <= m; i++)
    {
        rightMost[i] = 0;
    }

    // Traverse the array
    for(int i = 0; i < n; i++)
    {
        int a1 = a[i, 0];
        int b1 = a[i, 1];

        // Update the rightMost
        // position reached from a1
        rightMost[a1] = Math.Max(rightMost[a1], b1);
    }

    for(int i = m; i >= 0; i--)
    {
        dp[i] = i;

        // Find the farthest point
        // it can reach from i
        for(int j = Math.Min(m, rightMost[i]); j > i; j--)
        {
            dp[i] = Math.Max(dp[i], dp[j]);
        }
    }

    // If point < can be reached
    if (dp[0] >= m)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver Code
public static void Main()
{
    int[,] arr = { { 0, 2 }, { 2, 2 },
                   { 2, 5 }, { 4, 5 } };
    int M = 5;
    int N = arr.GetLength(0);

    canReach0toM(arr, N, M);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if it is
// possible to reach M from 0
function canReach0toM(a, n, m)
{
    // Stores the farther point that
    // can reach from 1 point
    let rightMost = new Array(m + 1);

    // Stores the farthest point it
    // can go for each index i
    let dp = new Array(m + 1);

    // Initialize rightMost[i] with 0
    for (let i = 0; i <= m; i++) {
        rightMost[i] = 0;
    }

    // Traverse the array
    for (let i = 0; i < n; i++) {

        let a1 = a[i][0];
        let b1 = a[i][1];

        // Update the rightMost
        // position reached from a1
        rightMost[a1] = Math.max(
            rightMost[a1], b1);
    }

    for (let i = m; i >= 0; i--) {

        dp[i] = i;

        // Find the farthest point
        // it can reach from i
        for (let j = Math.min(m, rightMost[i]);
             j > i; j--) {
            dp[i] = Math.max(dp[i], dp[j]);
        }
    }

    // If point < can be reached
    if (dp[0] >= m) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }
}

// Driver Code
    let arr = [[ 0, 2 ], [ 2, 2 ],
                     [ 2, 5 ], [ 4, 5 ]];
    let M = 5;
    let N = arr.length;
    canReach0toM(arr, N, M);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)