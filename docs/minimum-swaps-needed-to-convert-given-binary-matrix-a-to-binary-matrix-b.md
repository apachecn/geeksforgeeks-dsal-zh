# 将给定二进制矩阵 A 转换为二进制矩阵 B 所需的最小交换量

> 原文:[https://www . geesforgeks . org/minimum-互换-需要转换-给定-二进制-矩阵-a 到二进制-矩阵-b/](https://www.geeksforgeeks.org/minimum-swaps-needed-to-convert-given-binary-matrix-a-to-binary-matrix-b/)

给定两个[大小为 **N×M、**的](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)、 **A[][]** 和 **B[][]** 二进制矩阵，任务是找到将矩阵 **A** 转换为矩阵 **B** 所需的矩阵 A 元素互换的最小次数。如果不可能，则打印“ **-1** ”。

**示例:**

> ***输入:** A[][] = {{1，1，0}，{0，0，1}，{0，1，0}}，B[][] = {{0，0，1}，{0，1，0}，{1，1，0}}*
> ***输出:** 3*
> ***解释:***
> *将矩阵 A 转换为 B 的一种可能方式是:*
> 
> 1.  *用 A[0][2]交换元素 A[0][0]。此后矩阵 A 修改为{{0，1，1}，{ 0，0，1}，{ 0，1，0}}。*
> 2.  *用 A[1][1]交换元素 A[0][1]。此后矩阵 A 修改为{{0，0，1}，{ 0，1，1}，{ 0，1，0}}。*
> 3.  *用 A[2][0]交换元素 A[1][2]。此后矩阵 A 修改为{{ 0，0，1}，{ 0，1，0}，{1，1，0}}。*
> 
> *因此，需要的总移动次数是 3，也是需要的最小移动次数。*
> 
> ***输入:** A[][] = {{1，1}，{0，1}，{1，0}，{0，0}}，B[][] = {{1，1}，{1，1}，{0，1}，{0，0 } }*
> *T6】输出: -1*

**天真方法:**这个问题可以用 Hashing 来解决。要仅通过交换将矩阵 A 转换为矩阵 B，两个矩阵中的设置位和未设置位的计数必须相同。所以首先检查 A 中的设置位和未设置位是否与 B 中的相同。如果是，则找出 A 中元素与 b 中元素不同的位置数。这将是最终计数。

**高效方法:**上述方法可以进一步进行空间优化，借助于对元素数量进行计数的观察，使得 **A[i][j] = 0** 和 **B[i][j] = 1** 以及对元素数量进行计数，使得 **A[i][j] = 1** 和 **B[i][j] = 0** 必须相等，并且所需的最小移动次数等于获得的计数。按照以下步骤解决问题:

*   初始化两个变量，比如说 **count10** 和 **count01** ，它们分别计算元素的数量使得 **A[i][j] = 1** 和 **B[i][j] = 0** 以及元素的数量使得 **A{i][j] = 0** 和 **B[i][j] = 1** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，并执行以下步骤:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M-1】**，如果 **A[i][j] = 1** 和 **B[i][j] = 0** ，则将**计数 10** 增加 **1。**否则，如果 **A[i][j] = 0** 和 **B[i][j] = 1** ，则将**计数 01** 增加 **1** 。
*   如果 **count01** 等于 **count10** ，则打印 **count01** 的值作为答案。否则，打印 **-1** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of swaps required to convert matrix
// A to matrix B
int minSwaps(int N, int M, vector<vector<int> >& A,
             vector<vector<int> >& B)
{
    // Stores number of cells such that
    // matrix A contains 0 and matrix B
    // contains 1
    int count01 = 0;

    // Stores number of cells such that
    // matrix A contains 1 and matrix B
    // contains 0
    int count10 = 0;

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {
        // Iterate over the range [0, M-1]
        for (int j = 0; j < M; j++) {
            if (A[i][j] != B[i][j]) {

                // If A[i][j] = 1 and B[i][j] = 0
                if (A[i][j] == 1)
                    count10++;
                // If A[i][j] = 0 and B[i][j] = 1
                else
                    count01++;
            }
        }
    }

    // If count01 is equal to count10
    if (count01 == count10)
        return count01;

    // Otherwise,
    else
        return -1;
}

// Driver Code
int main()
{

    vector<vector<int> > A
        = { { 1, 1, 0 }, { 0, 0, 1 }, { 0, 1, 0 } };
    vector<vector<int> > B
        = { { 0, 0, 1 }, { 0, 1, 0 }, { 1, 1, 0 } };

    int N = A.size();
    int M = B[0].size();

    cout << minSwaps(N, M, A, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class MyClass
{

// Function to count the minimum number
// of swaps required to convert matrix
// A to matrix B
public static int minSwaps(int N, int M, int A[][], int B[][])
{
    // Stores number of cells such that
    // matrix A contains 0 and matrix B
    // contains 1
    int count01 = 0;

    // Stores number of cells such that
    // matrix A contains 1 and matrix B
    // contains 0
    int count10 = 0;

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {
        // Iterate over the range [0, M-1]
        for (int j = 0; j < M; j++) {
            if (A[i][j] != B[i][j]) {

                // If A[i][j] = 1 and B[i][j] = 0
                if (A[i][j] == 1)
                    count10++;
                // If A[i][j] = 0 and B[i][j] = 1
                else
                    count01++;
            }
        }
    }

    // If count01 is equal to count10
    if (count01 == count10)
        return count01;

    // Otherwise,
    else
        return -1;
}

// Driver Code
  public static void main(String args[])
{

    int [][] A = { { 1, 1, 0 }, { 0, 0, 1 }, { 0, 1, 0 } };
    int [][] B = { { 0, 0, 1 }, { 0, 1, 0 }, { 1, 1, 0 } };

    int N = A.length;
    int M = B[0].length;

    System.out.println(minSwaps(N, M, A, B));
}}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of swaps required to convert matrix
# A to matrix B
def minSwaps(N, M, A, B):

    # Stores number of cells such that
    # matrix A contains 0 and matrix B
    # contains 1
    count01 = 0

    # Stores number of cells such that
    # matrix A contains 1 and matrix B
    # contains 0
    count10 = 0

    # Iterate over the range[0, N-1]
    for i in range(0, N):

        # Iterate over the range[0, M-1]
        for j in range(0, M):
            if (A[i][j] != B[i][j]):

                # If A[i][j] = 1 and B[i][j] = 0
                if (A[i][j] == 1):
                    count10 += 1

                # If A[i][j] = 0 and B[i][j] = 1
                else:
                    count01 += 1

    # If count01 is equal to count10
    if (count01 == count10):
        return count01

    # Otherwise,
    else:
        return -1

# Driver Code
A = [ [ 1, 1, 0 ], [ 0, 0, 1 ], [ 0, 1, 0 ] ]
B = [ [ 0, 0, 1 ], [ 0, 1, 0 ], [ 1, 1, 0 ] ]
N = len(A)
M = len(B[0])

print(minSwaps(N, M, A, B))

# This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to count the minimum number
        // of swaps required to convert matrix
        // A to matrix B
        function minSwaps(N, M, A, B)
        {

            // Stores number of cells such that
            // matrix A contains 0 and matrix B
            // contains 1
            let count01 = 0;

            // Stores number of cells such that
            // matrix A contains 1 and matrix B
            // contains 0
            let count10 = 0;

            // Iterate over the range [0, N-1]
            for (let i = 0; i < N; i++) {
                // Iterate over the range [0, M-1]
                for (let j = 0; j < M; j++) {
                    if (A[i][j] != B[i][j]) {

                        // If A[i][j] = 1 and B[i][j] = 0
                        if (A[i][j] == 1)
                            count10++;
                        // If A[i][j] = 0 and B[i][j] = 1
                        else
                            count01++;
                    }
                }
            }

            // If count01 is equal to count10
            if (count01 == count10)
                return count01;

            // Otherwise,
            else
                return -1;
        }

        // Driver Code
        let A
            = [[1, 1, 0], [0, 0, 1], [0, 1, 0]];
        let B
            = [[0, 0, 1], [0, 1, 0], [1, 1, 0]];

        let N = A.length;
        let M = B[0].length;

        document.write(minSwaps(N, M, A, B));

  // This code is contributed by Potta Lokesh
    </script>
```

## C#

```
// C# program for the above approach

using System;

class GFG {

// Function to count the minimum number
// of swaps required to convert matrix
// A to matrix B
public static int minSwaps(int N, int M, int[,] A, int[,] B)
{
    // Stores number of cells such that
    // matrix A contains 0 and matrix B
    // contains 1
    int count01 = 0;

    // Stores number of cells such that
    // matrix A contains 1 and matrix B
    // contains 0
    int count10 = 0;

    // Iterate over the range [0, N-1]
    for (int i = 0; i < N; i++) {
        // Iterate over the range [0, M-1]
        for (int j = 0; j < M; j++) {
            if (A[i,j] != B[i, j]) {

                // If A[i][j] = 1 and B[i][j] = 0
                if (A[i, j] == 1)
                    count10++;
                // If A[i][j] = 0 and B[i][j] = 1
                else
                    count01++;
            }
        }
    }

    // If count01 is equal to count10
    if (count01 == count10)
        return count01;

    // Otherwise,
    else
        return -1;
}

  // Driver code
  public static void Main (String[] args)
  {
    int [,] A = { { 1, 1, 0 }, { 0, 0, 1 }, { 0, 1, 0 } };
    int [,] B = { { 0, 0, 1 }, { 0, 1, 0 }, { 1, 1, 0 } };

    int N = A.GetLength(0);
    int M = 3;

    Console.Write(minSwaps(N, M, A, B));
  }
}
```

**Output**

```
3
```

***时间复杂度:** O(N*M)。*
***辅助空间:** O(1)*