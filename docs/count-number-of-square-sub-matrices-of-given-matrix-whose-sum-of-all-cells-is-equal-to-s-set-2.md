# 统计给定矩阵中所有单元格之和等于 S 的正方形子矩阵的个数|集合 2

> 原文:[https://www . geesforgeks . org/count-给定矩阵的子矩阵的平方数-其所有单元的和等于 s-set-2/](https://www.geeksforgeeks.org/count-number-of-square-sub-matrices-of-given-matrix-whose-sum-of-all-cells-is-equal-to-s-set-2/)

给定一个尺寸为 **M*N、**的[矩阵](https://www.geeksforgeeks.org/matrix/)、 **arr[][]** 和一个整数 **S** ，任务是打印矩阵子方块数的[计数，其和等于 **S** 。](https://www.geeksforgeeks.org/count-of-submatrix-with-sum-x-in-a-given-matrix/)

**示例:**

> ***输入:** M = 4，N = 5，S = 10，arr[][]={{2，4，3，2，10}，{3，1，1，1，5}，{1，1，2，1，4}，{2，1，1，3}}*
> ***输出:** 3*
> ***解释:***
> *子方块{10*
> 
> ***输入:** M = 3，N = 4，S = 8，arr[][]={{3，1，5，3}，{2，2，2，6}，{1，2，2，4}}*
> ***输出:** 2*
> ***解释:***
> *子方块{{2，2}，{2，2}}和{{3，1}，}*

**天真方法:**解决问题最简单的方法是生成所有可能的子正方形，并检查子正方形所有元素的[和](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/)是否等于 **S** 。

***时间复杂度:**O(N<sup>3</sup>* M<sup>3</sup>)*
***辅助空间:** O(1)*

**替代方法:**上述方法可以通过找到矩阵的[前缀和来优化，这导致子矩阵的所有元素的和的恒定时间计算。按照以下步骤解决问题:](https://www.geeksforgeeks.org/prefix-sum-2d-array/)

*   找到矩阵**arr【】【】**的[前缀和，并将其存储在维度 **(M + 1)*(N + 1)的**](https://www.geeksforgeeks.org/prefix-sum-2d-array/) **[2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)表示 **dp** 中。**
*   初始化一个变量，说**计数**为 **0** ，用和 **S.** 存储子方块的计数
*   使用变量 **x** 迭代范围**【1，min(N，M)】**，并执行以下操作:
    *   使用变量 **i** 和 **j** 迭代矩阵 **arr[][]** 的每个元素，并执行以下操作:
        *   如果 **i** 和 **j** 大于或等于 **x** ，则求尺寸 **x * x** 的子正方形之和，其中 **(i，j)** 为变量的右下顶点，如 **Sum。**
        *   将 **Sum** 变量更新为**，Sum = DP[I][j]–DP[I–x][j]–DP[I][j–x]+DP[I–x][j–x]。**
        *   如果**之和**等于 **S，**则将**计数**增加 1。
*   最后，完成以上步骤后，打印**中的数值，将**算作答案**。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to compute prefix sum
void find_prefixsum(int M, int N, vector<vector<int> >& arr,
                    vector<vector<int> >& dp)
{
    // Assign 0 to first column
    for (int i = 0; i <= M; i++) {
        dp[i][0] = 0;
    }

    // Assign 0 to first row
    for (int j = 0; j <= N; j++) {
        dp[0][j] = 0;
    }
    // Iterate over the range
    //[1, M]
    for (int i = 1; i <= M; i++) {

        // Iterate over the range
        //[1, N]
        for (int j = 1; j <= N; j++) {

            // Update
            dp[i][j] = dp[i][j - 1] + arr[i - 1][j - 1];
        }
    }

    // Iterate over the range
    //[1, M]
    for (int i = 1; i <= M; i++) {

        // Iterate over the range
        //[1, N]
        for (int j = 1; j <= N; j++) {

            // Update
            dp[i][j] = dp[i][j] + dp[i - 1][j];
        }
    }
}

// Function to find sub-squares
// with given sum S
int findSubsquares(vector<vector<int> > arr, int M, int N,
                   int S)
{
    // Stores the prefix sum of
    // matrix
    vector<vector<int> > dp(M + 1, vector<int>(N + 1));

    // Function call to find
    // prefix Sum of matrix
    find_prefixsum(M, N, arr, dp);

    // Stores the count of
    // subsquares with sum S
    int cnt = 0;

    for (int x = 1; x <= min(N, M); x++) {

        // Iterate over every
        // element of the matrix
        for (int i = x; i <= M; i++) {
            for (int j = x; j <= N; j++) {

                // Stores the sum of
                // subsquare of dimension
                // x*x formed with i, j as
                // the bottom-right
                // vertex

                int sum = dp[i][j] - dp[i - x][j]
                          - dp[i][j - x] + dp[i - x][j - x];

                // If sum is equal to S

                if (sum == S) {

                    // Increment cnt by 1
                    cnt++;
                }
            }
        }
    }

    // Return the result
    return cnt;
}

// Driver Code
int main()
{
    // Input
    int M = 4, N = 5;
    vector<vector<int> > arr = { { 2, 4, 3, 2, 10 },
                                 { 3, 1, 1, 1, 5 },
                                 { 1, 1, 2, 1, 4 },
                                 { 2, 1, 1, 1, 3 } };
    int S = 10;

    // Function call
    cout << findSubsquares(arr, M, N, S);
    return 0;
}
```

## 蟒蛇 3

```
# python program for the above approach

# Function to compute prefix sum
def find_prefixsum(M, N, arr, dp):

    # Assign 0 to first column
    for i in range(0, M+1):
        dp[i][0] = 0

    # Assign 0 to first row
    for j in range(0, N+1):
        dp[0][j] = 0

    # Iterate over the range
    # [1, M]
    for i in range(1, M+1):

        # Iterate over the range
        # [1, N]
        for j in range(1, N+1):
            dp[i][j] = dp[i][j - 1] + arr[i - 1][j - 1]

    # Iterate over the range
    # [1, M]
    for i in range(1, M+1):

        # Iterate over the range
        #  [1, N]
        for j in range(1, N+1):
            # Update
            dp[i][j] = dp[i][j] + dp[i - 1][j]

# Function to find sub-squares
# with given sum S
def findSubsquares(arr, M,  N, S):

    # Stores the prefix sum of
    # matrix
    dp = [[0 for i in range(N + 1)] for col in range(M + 1)]

    # Function call to find
    # prefix Sum of matrix
    find_prefixsum(M, N, arr, dp)

    # Stores the count of
    # subsquares with sum S
    cnt = 0
    for x in range(1, min(N, M)):

        # Iterate over every
        # element of the matrix
        for i in range(x, M + 1):
            for j in range(x, N + 1):

                # Stores the sum of
                # subsquare of dimension
                # x*x formed with i, j as
                # the bottom-right
                # vertex
                sum = dp[i][j] - dp[i - x][j] - dp[i][j - x] + dp[i - x][j - x]

                # If sum is equal to S

                if (sum == S):
                    # Increment cnt by 1
                    cnt += 1

    # Return the result
    return cnt

# Driver Code
# Input
M = 4
N = 5
arr = [[2, 4, 3, 2, 10],
       [3, 1, 1, 1, 5],
       [1, 1, 2, 1, 4],
       [2, 1, 1, 1, 3]]
S = 10

# Function call
print(findSubsquares(arr, M, N, S))

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to compute prefix sum
    static void find_prefixsum(int M, int N, int[, ] arr,
                               int[, ] dp)
    {

        // Assign 0 to first column
        for (int i = 0; i <= M; i++) {
            dp[i, 0] = 0;
        }

        // Assign 0 to first row
        for (int j = 0; j <= N; j++) {
            dp[0, j] = 0;
        }
        // Iterate over the range
        //[1, M]
        for (int i = 1; i <= M; i++) {

            // Iterate over the range
            //[1, N]
            for (int j = 1; j <= N; j++) {

                // Update
                dp[i, j] = dp[i, j - 1] + arr[i - 1, j - 1];
            }
        }

        // Iterate over the range
        //[1, M]
        for (int i = 1; i <= M; i++) {

            // Iterate over the range
            //[1, N]
            for (int j = 1; j <= N; j++) {

                // Update
                dp[i, j] = dp[i, j] + dp[i - 1, j];
            }
        }
    }

    // Function to find sub-squares
    // with given sum S
    static int findSubsquares(int[, ] arr, int M, int N,
                              int S)
    {
        // Stores the prefix sum of
        // matrix
        int[, ] dp = new int[M + 1, N + 1];

        // Function call to find
        // prefix Sum of matrix
        find_prefixsum(M, N, arr, dp);

        // Stores the count of
        // subsquares with sum S
        int cnt = 0;

        for (int x = 1; x <= Math.Min(N, M); x++) {

            // Iterate over every
            // element of the matrix
            for (int i = x; i <= M; i++) {
                for (int j = x; j <= N; j++) {

                    // Stores the sum of
                    // subsquare of dimension
                    // x*x formed with i, j as
                    // the bottom-right
                    // vertex

                    int sum = dp[i, j] - dp[i - x, j]
                              - dp[i, j - x]
                              + dp[i - x, j - x];

                    // If sum is equal to S

                    if (sum == S) {

                        // Increment cnt by 1
                        cnt++;
                    }
                }
            }
        }

        // Return the result
        return cnt;
    }

    // Driver Code
    public static void Main()
    {
        // Input
        int M = 4, N = 5;
        int[, ] arr = { { 2, 4, 3, 2, 10 },
                        { 3, 1, 1, 1, 5 },
                        { 1, 1, 2, 1, 4 },
                        { 2, 1, 1, 1, 3 } };
        int S = 10;

        // Function call
        Console.WriteLine(findSubsquares(arr, M, N, S));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to compute prefix sum
function find_prefixsum(M, N, arr, dp)
{
    // Assign 0 to first column
    for (var i = 0; i <= M; i++) {
        dp[i][0] = 0;
    }

    // Assign 0 to first row
    for (var j = 0; j <= N; j++) {
        dp[0][j] = 0;
    }
    // Iterate over the range
    //[1, M]
    for (var i = 1; i <= M; i++) {

        // Iterate over the range
        //[1, N]
        for (var j = 1; j <= N; j++) {

            // Update
            dp[i][j] = dp[i][j - 1] + arr[i - 1][j - 1];
        }
    }

    // Iterate over the range
    //[1, M]
    for (var i = 1; i <= M; i++) {

        // Iterate over the range
        //[1, N]
        for (var j = 1; j <= N; j++) {

            // Update
            dp[i][j] = dp[i][j] + dp[i - 1][j];
        }
    }
}

// Function to find sub-squares
// with given sum S
function findSubsquares(arr, M, N, S)
{
    // Stores the prefix sum of
    // matrix
    var dp = Array.from(Array(M+1), ()=>Array(N+1));

    // Function call to find
    // prefix Sum of matrix
    find_prefixsum(M, N, arr, dp);

    // Stores the count of
    // subsquares with sum S
    var cnt = 0;

    for (var x = 1; x <= Math.min(N, M); x++) {

        // Iterate over every
        // element of the matrix
        for (var i = x; i <= M; i++) {
            for (var j = x; j <= N; j++) {

                // Stores the sum of
                // subsquare of dimension
                // x*x formed with i, j as
                // the bottom-right
                // vertex

                var sum = dp[i][j] - dp[i - x][j]
                          - dp[i][j - x] + dp[i - x][j - x];

                // If sum is equal to S

                if (sum == S) {

                    // Increment cnt by 1
                    cnt++;
                }
            }
        }
    }

    // Return the result
    return cnt;
}

// Driver Code
// Input
var M = 4, N = 5;
var arr = [ [ 2, 4, 3, 2, 10 ],
                             [ 3, 1, 1, 1, 5 ],
                             [ 1, 1, 2, 1, 4 ],
                             [ 2, 1, 1, 1, 3 ] ];
var S = 10;
// Function call
document.write( findSubsquares(arr, M, N, S));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(M * N * min(M，N))*
***辅助空间:** O(N * M)*

**有效方法:**上述方法可以使用[二分搜索法算法](https://www.geeksforgeeks.org/binary-search/)进一步优化。请参考链接，了解给定矩阵中求和为 X 的子矩阵的有效解[ [计数]。](https://www.geeksforgeeks.org/count-of-submatrix-with-sum-x-in-a-given-matrix/)