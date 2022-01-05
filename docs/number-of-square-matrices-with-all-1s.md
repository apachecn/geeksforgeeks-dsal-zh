# 全为 1 的方阵数

> 原文:[https://www . geesforgeks . org/全 1 方阵数/](https://www.geeksforgeeks.org/number-of-square-matrices-with-all-1s/)

给定一个只包含 0 和 1 的 **N*M** 矩阵，任务是计算包含所有 1 的正方形子矩阵的数量。
**例:**

> **输入:** arr[][] = {{0，1，1，1}，
> {1，1，1，1}，
> {0，1，1，1}}
> **输出:** 15
> **说明:**
> 边长 1 的方块有 10 个。
> 边长 2 的正方形有 4 个。
> 边长 3 的 1 平方。
> 方块总数= 10 + 4 + 1 = 15。
> **输入:** arr[][] = {{1，0，1}，
> {1，1，0}，
> {1，1，0}}
> **输出:** 7

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

1.  让数组***arr【I】【j】***存储以 ***(i，j)*** 结束的方阵数量
2.  求以 ***(i，j)*** 结束的方块数的递推关系可由下式给出:
    *   如果 arr[i][j]是 1:
        *   **arr[I][j]= min(min(arr[I-1][j]，arr[i][j-1])，arr[i-1][j-1]) + 1**
    *   否则如果 arr[i][j]为 0:
        *   **arr[i][j] = 0**
3.  计算数组的和，等于全为 1 的正方形子矩阵的数量。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to return the number of
// square submatrices with all 1s
#include <bits/stdc++.h>
using namespace std;

#define n 3
#define m 3

// Function to return the number of
// square submatrices with all 1s
int countSquareMatrices(int a[][m],
                        int N, int M)
{
    // Initialize count variable
    int count = 0;

    for (int i = 1; i < N; i++) {
        for (int j = 1; j < M; j++) {
            // If a[i][j] is equal to 0
            if (a[i][j] == 0)
                continue;

            // Calculate number of
            // square submatrices
            // ending at (i, j)
            a[i][j] = min(min(a[i - 1][j],
                              a[i][j - 1]),
                          a[i - 1][j - 1])
                      + 1;
        }
    }

    // Calculate the sum of the array
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
            count += a[i][j];

    return count;
}

// Driver code
int main()
{
    int arr[][m] = { { 1, 0, 1 },
                     { 1, 1, 0 },
                     { 1, 1, 0 } };

    cout << countSquareMatrices(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to return the number of
// square submatrices with all 1s
class GFG
{

    final static int n = 3;
    final static int m = 3;

    // Function to return the number of
    // square submatrices with all 1s
    static int countSquareMatrices(int a[][], int N, int M)
    {
        // Initialize count variable
        int count = 0;

        for (int i = 1; i < N; i++)
        {
            for (int j = 1; j < M; j++)
            {
                // If a[i][j] is equal to 0
                if (a[i][j] == 0)
                    continue;

                // Calculate number of
                // square submatrices
                // ending at (i, j)
                a[i][j] = Math.min(Math.min(a[i - 1][j], a[i][j - 1]),
                            a[i - 1][j - 1]) + 1;
            }
        }

        // Calculate the sum of the array
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
                count += a[i][j];

        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[][] = { { 1, 0, 1 },
                        { 1, 1, 0 },
                        { 1, 1, 0 } };

        System.out.println(countSquareMatrices(arr, n, m));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 program to return the number of
# square submatrices with all 1s
n = 3
m = 3

# Function to return the number of
# square submatrices with all 1s
def countSquareMatrices(a, N, M):

    # Initialize count variable
    count = 0

    for i in range(1, N):
        for j in range(1, M):

            # If a[i][j] is equal to 0
            if (a[i][j] == 0):
                continue

            # Calculate number of
            # square submatrices
            # ending at (i, j)
            a[i][j] = min([a[i - 1][j],
                      a[i][j - 1], a[i - 1][j - 1]])+1

    # Calculate the sum of the array
    for i in range(N):
        for j in range(M):
            count += a[i][j]

    return count

# Driver code

arr = [ [ 1, 0, 1],
    [ 1, 1, 0 ],
    [ 1, 1, 0 ] ]

print(countSquareMatrices(arr, n, m))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to return the number of
// square submatrices with all 1s
using System;

class GFG
{

    static int n = 3;
    static int m = 3;

    // Function to return the number of
    // square submatrices with all 1s
    static int countSquareMatrices(int [,]a, int N, int M)
    {
        // Initialize count variable
        int count = 0;

        for (int i = 1; i < N; i++)
        {
            for (int j = 1; j < M; j++)
            {
                // If a[i][j] is equal to 0
                if (a[i, j] == 0)
                    continue;

                // Calculate number of
                // square submatrices
                // ending at (i, j)
                a[i, j] = Math.Min(Math.Min(a[i - 1, j], a[i, j - 1]),
                            a[i - 1, j - 1]) + 1;
            }
        }

        // Calculate the sum of the array
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
                count += a[i, j];

        return count;
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = { { 1, 0, 1 },
                        { 1, 1, 0 },
                        { 1, 1, 0 } };

        Console.WriteLine(countSquareMatrices(arr, n, m));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to return the number of
// square submatrices with all 1s

var n = 3
var m = 3

// Function to return the number of
// square submatrices with all 1s
function countSquareMatrices(a, N, M)
{
    // Initialize count variable
    var count = 0;

    for (var i = 1; i < N; i++) {
        for (var j = 1; j < M; j++) {
            // If a[i][j] is equal to 0
            if (a[i][j] == 0)
                continue;

            // Calculate number of
            // square submatrices
            // ending at (i, j)
            a[i][j] = Math.min(Math.min(a[i - 1][j],
                              a[i][j - 1]),
                          a[i - 1][j - 1])
                      + 1;
        }
    }

    // Calculate the sum of the array
    for (var i = 0; i < N; i++)
        for (var j = 0; j < M; j++)
            count += a[i][j];

    return count;
}

// Driver code
var arr = [ [ 1, 0, 1 ],
                 [ 1, 1, 0 ],
                 [ 1, 1, 0 ] ];
document.write( countSquareMatrices(arr, n, m));

</script>
```

**输出:**

```
7
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(1)