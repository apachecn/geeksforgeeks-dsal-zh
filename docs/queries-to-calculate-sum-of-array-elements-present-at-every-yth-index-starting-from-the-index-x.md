# 从索引 X 开始计算每个 Yth 索引处存在的数组元素的总和的查询

> 原文:[https://www . geesforgeks . org/query-to-compute-sum-array-elements-every-at-yth-index-from-index-x/](https://www.geeksforgeeks.org/queries-to-calculate-sum-of-array-elements-present-at-every-yth-index-starting-from-the-index-x/)

给定一个大小为 **N** 的[数组**arr【】**和一个数组**Q【】【】**，每行代表一个形式为 **{ X，Y }** 的查询，每个查询的任务是找到存在于索引 **X** ， **X + Y** ， **X + 2 * Y** + …](https://www.geeksforgeeks.org/array-data-structure/)

**示例:**

> **输入:** arr[] = { 1，2，7，5，4 }，Q[][] = { { 2，1 }，{ 3，2 } }
> **输出:**16 5
> T6】解释:T8】查询 1:arr[2]+arr[2+1]+arr[2+2]= 7+5+4 = 16。
> 查询 2: arr[3] = 5。
> 
> **输入:** arr[] = { 3，6，1，8，0 } Q[][] = { { 0，2 } }
> **输出:** 4

**天真方法:**解决这个问题最简单的方法是[遍历每个查询的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并打印**arr[x]+arr[x+y]+arr[x+2 * y]+…**的和

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
void querySum(int arr[], int N,
              int Q[][2], int M)
{

    // Iterate over each query
    for (int i = 0; i < M; i++) {

        int x = Q[i][0];
        int y = Q[i][1];

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        int sum = 0;

        // Traverse the array and calculate
        // the sum of the expression
        while (x < N) {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }

        cout << sum << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 7, 5, 4 };
    int Q[][2] = { { 2, 1 }, { 3, 2 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    int M = sizeof(Q) / sizeof(Q[0]);

    querySum(arr, N, Q, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
static void querySum(int arr[], int N,
                     int Q[][], int M)
{

    // Iterate over each query
    for(int i = 0; i < M; i++)
    {
        int x = Q[i][0];
        int y = Q[i][1];

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        int sum = 0;

        // Traverse the array and calculate
        // the sum of the expression
        while (x < N)
        {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }
        System.out.print(sum + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 7, 5, 4 };
    int Q[][] = { { 2, 1 }, { 3, 2 } };

    int N = arr.length;
    int M = Q.length;

    querySum(arr, N, Q, M);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to Find the sum of
# arr[x]+arr[x+y]+arr[x+2*y] + ...
# for all queries
def querySum(arr, N, Q, M):

    # Iterate over each query
    for i in range(M):
        x = Q[i][0]
        y = Q[i][1]

        # Stores the sum of
        # arr[x]+arr[x+y]+arr[x+2*y] + ...
        sum = 0

        # Traverse the array and calculate
        # the sum of the expression
        while (x < N):

            # Update sum
            sum += arr[x]

            # Update x
            x += y
        print(sum, end=" ")

# Driver Code
if __name__ == '__main__':
    arr = [ 1, 2, 7, 5, 4 ];
    Q = [ [ 2, 1 ], [3, 2 ] ]
    N = len(arr)
    M = len(Q)
    querySum(arr, N, Q, M)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

  // Function to Find the sum of
  // arr[x]+arr[x+y]+arr[x+2*y] + ...
  // for all queries
  static void querySum(int []arr, int N,
                       int [,]Q, int M)
  {

    // Iterate over each query
    for(int i = 0; i < M; i++)
    {
      int x = Q[i, 0];
      int y = Q[i, 1];

      // Stores the sum of
      // arr[x]+arr[x+y]+arr[x+2*y] + ...
      int sum = 0;

      // Traverse the array and calculate
      // the sum of the expression
      while (x < N)
      {

        // Update sum
        sum += arr[x];

        // Update x
        x += y;
      }
      Console.Write(sum + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 1, 2, 7, 5, 4 };
    int [,]Q = { { 2, 1 }, { 3, 2 } };
    int N = arr.Length;
    int M = Q.GetLength(0);
    querySum(arr, N, Q, M);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
function querySum(arr, N, Q, M)
{

    // Iterate over each query
    for (let i = 0; i < M; i++) {

        let x = Q[i][0];
        let y = Q[i][1];

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        let sum = 0;

        // Traverse the array and calculate
        // the sum of the expression
        while (x < N) {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }
        document.write(sum + " ");
    }
}

// Driver Code
    let arr = [ 1, 2, 7, 5, 4 ];
    let Q = [ [ 2, 1 ], [ 3, 2 ] ];
    let N = arr.length;
    let M = Q.length;
    querySum(arr, N, Q, M);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
16 5
```

***时间复杂度:** O(|Q| * O(N))*
***辅助空间:** O(1)*

**有效方法:**使用[动态规划技术](https://www.geeksforgeeks.org/dynamic-programming/)和[平方根分解技术](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)对 **{ X，Y }** 的所有可能值预计算给定表达式的值，可以解决该问题。以下是循环关系:

> 如果 I+j< N
> DP[I][j]= DP[I+j][j]+arr[I]
> 否则，
> dp[i][j] = arr[i]
> 
> dp[i][j]:存储给定表达式的和，其中 X = i，Y = j

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如 **dp[][]** ，存储 **X** 和 **Y** 所有可能值的表达式之和，其中 **Y** 小于等于 **sqrt(N)** 。
*   使用[制表方法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)填充 **dp[][]** 数组。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** 。对于每个查询，检查 **Q[i][1]** 的值是否小于或等于 **sqrt(N)** 。如果发现为真，则打印**DP[Q[I][0]][Q[I][1]]【T9]的值。**
*   否则，使用上述简单方法计算表达式的值，并打印计算值。

以下是我们方法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const int sz = 20;
const int sqr = int(sqrt(sz)) + 1;

// Function to sum of arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all possible values of X and Y, where Y is
// less than or equal to sqrt(N).
void precomputeExpressionForAllVal(int arr[], int N,
                                   int dp[sz][sqr])
{

    // Iterate over all possible values of X
    for (int i = N - 1; i >= 0; i--) {

        // Precompute for all possible values
        // of an expression such that y <= sqrt(N)
        for (int j = 1; j <= sqrt(N); j++) {

            // If i + j less than N
            if (i + j < N) {

                // Update dp[i][j]
                dp[i][j] = arr[i] + dp[i + j][j];
            }
            else {

                // Update dp[i][j]
                dp[i][j] = arr[i];
            }
        }
    }
}

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
int querySum(int arr[], int N,
             int Q[][2], int M)
{

    // dp[x][y]: Stores sum of
    // arr[x]+arr[x+y]+arr[x+2*y] + ...
    int dp[sz][sqr];

    precomputeExpressionForAllVal(arr, N, dp);
    // Traverse the query array, Q[][]
    for (int i = 0; i < M; i++) {

        int x = Q[i][0];
        int y = Q[i][1];

        // If y is less than or equal
        // to sqrt(N)
        if (y <= sqrt(N)) {
            cout << dp[x][y] << " ";
            continue;
        }

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        int sum = 0;

        // Traverse the array, arr[]
        while (x < N) {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }

        cout << sum << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 7, 5, 4 };
    int Q[][2] = { { 2, 1 }, { 3, 2 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    int M = sizeof(Q) / sizeof(Q[0]);

    querySum(arr, N, Q, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int sz = 20;
static int sqr = (int)(Math.sqrt(sz)) + 1;

// Function to sum of arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all possible values of X and Y, where Y is
// less than or equal to Math.sqrt(N).
static void precomputeExpressionForAllVal(int arr[],
                                          int N,
                                          int dp[][])
{

    // Iterate over all possible values of X
    for(int i = N - 1; i >= 0; i--)
    {

        // Precompute for all possible values
        // of an expression such that y <= Math.sqrt(N)
        for(int j = 1; j <= Math.sqrt(N); j++)
        {

            // If i + j less than N
            if (i + j < N)
            {

                // Update dp[i][j]
                dp[i][j] = arr[i] + dp[i + j][j];
            }
            else
            {

                // Update dp[i][j]
                dp[i][j] = arr[i];
            }
        }
    }
}

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
static void querySum(int arr[], int N,
                     int Q[][], int M)
{

    // dp[x][y]: Stores sum of
    // arr[x]+arr[x+y]+arr[x+2*y] + ...
    int [][]dp = new int[sz][sqr];

    precomputeExpressionForAllVal(arr, N, dp);

    // Traverse the query array, Q[][]
    for(int i = 0; i < M; i++)
    {
        int x = Q[i][0];
        int y = Q[i][1];

        // If y is less than or equal
        // to Math.sqrt(N)
        if (y <= Math.sqrt(N))
        {
            System.out.print(dp[x][y] + " ");
            continue;
        }

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        int sum = 0;

        // Traverse the array, arr[]
        while (x < N)
        {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }
        System.out.print(sum + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 7, 5, 4 };
    int Q[][] = { { 2, 1 }, { 3, 2 } };

    int N = arr.length;
    int M = Q.length;

    querySum(arr, N, Q, M);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach
import math
sz = 20
sqr = int(math.sqrt(sz)) + 1

# Function to sum of arr[x]+arr[x+y]+arr[x+2*y] + ...
# for all possible values of X and Y, where Y is
# less than or equal to sqrt(N).
def precomputeExpressionForAllVal(arr, N, dp):

    # Iterate over all possible values of X
    for i in range(N - 1, -1, -1) :

        # Precompute for all possible values
        #  of an expression such that y <= sqrt(N)
        for j in range (1,int(math.sqrt(N)) + 1):

            # If i + j less than N
            if (i + j < N):

                # Update dp[i][j]
                dp[i][j] = arr[i] + dp[i + j][j]
            else:

                # Update dp[i][j]
                dp[i][j] = arr[i]

# Function to Find the sum of
# arr[x]+arr[x+y]+arr[x+2*y] + ...
# for all queries
def querySum(arr, N, Q,  M):

    # dp[x][y]: Stores sum of
    # arr[x]+arr[x+y]+arr[x+2*y] + ...
    dp = [ [0 for x in range(sz)]for x in range(sqr)]
    precomputeExpressionForAllVal(arr, N, dp)

    # Traverse the query array, Q[][]
    for i in range (0,M):
        x = Q[i][0]
        y = Q[i][1]

        # If y is less than or equal
        #  to sqrt(N)
        if (y <= math.sqrt(N)):
            print(dp[x][y])
            continue

        # Stores the sum of
        # arr[x]+arr[x+y]+arr[x+2*y] + ...
        sum = 0

        # Traverse the array, arr[]
        while (x < N):

            # Update sum
            sum += arr[x]

            # Update x
            x += y
        print(sum)

# Driver Code
arr = [ 1, 2, 7, 5, 4 ]
Q = [ [ 2, 1 ], [ 3, 2]]

N = len(arr)

M = len(Q[0])
querySum(arr, N, Q, M)

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int sz = 20;
static int sqr = (int)(Math.Sqrt(sz)) + 1;

// Function to sum of arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all possible values of X and Y, where Y is
// less than or equal to Math.Sqrt(N).
static void precomputeExpressionForAllVal(int []arr,
                                          int N,
                                          int [,]dp)
{

    // Iterate over all possible values of X
    for(int i = N - 1; i >= 0; i--)
    {

        // Precompute for all possible values
        // of an expression such that y <= Math.Sqrt(N)
        for(int j = 1; j <= Math.Sqrt(N); j++)
        {

            // If i + j less than N
            if (i + j < N)
            {

                // Update dp[i,j]
                dp[i, j] = arr[i] + dp[i + j, j];
            }
            else
            {

                // Update dp[i,j]
                dp[i, j] = arr[i];
            }
        }
    }
}

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
static void querySum(int []arr, int N,
                     int [,]Q, int M)
{

    // dp[x,y]: Stores sum of
    // arr[x]+arr[x+y]+arr[x+2*y] + ...
    int [,]dp = new int[sz, sqr];

    precomputeExpressionForAllVal(arr, N, dp);

    // Traverse the query array, Q[,]
    for(int i = 0; i < M; i++)
    {
        int x = Q[i, 0];
        int y = Q[i, 1];

        // If y is less than or equal
        // to Math.Sqrt(N)
        if (y <= Math.Sqrt(N))
        {
            Console.Write(dp[x, y] + " ");
            continue;
        }

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        int sum = 0;

        // Traverse the array, []arr
        while (x < N)
        {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }
        Console.Write(sum + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 7, 5, 4 };
    int [,]Q = { { 2, 1 }, { 3, 2 } };

    int N = arr.Length;
    int M = Q.GetLength(0);

    querySum(arr, N, Q, M);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program of the above approach

 let sz = 20;
 let sqr = (Math.sqrt(sz)) + 1;

// Function to sum of arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all possible values of X and Y, where Y is
// less than or equal to Math.sqrt(N).
function precomputeExpressionForAllVal(arr, N, dp)
{

    // Iterate over all possible values of X
    for(let i = N - 1; i >= 0; i--)
    {

        // Precompute for all possible values
        // of an expression such that y <= Math.sqrt(N)
        for(let j = 1; j <= Math.sqrt(N); j++)
        {

            // If i + j less than N
            if (i + j < N)
            {

                // Update dp[i][j]
                dp[i][j] = arr[i] + dp[i + j][j];
            }
            else
            {

                // Update dp[i][j]
                dp[i][j] = arr[i];
            }
        }
    }
}

// Function to Find the sum of
// arr[x]+arr[x+y]+arr[x+2*y] + ...
// for all queries
function querySum(arr, N, Q, M)
{
    let dp = new Array(sz);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    precomputeExpressionForAllVal(arr, N, dp);

    // Traverse the query array, Q[][]
    for(let i = 0; i < M; i++)
    {
        let x = Q[i][0];
        let y = Q[i][1];

        // If y is less than or equal
        // to Math.sqrt(N)
        if (y <= Math.sqrt(N))
        {
            document.write(dp[x][y] + " ");
            continue;
        }

        // Stores the sum of
        // arr[x]+arr[x+y]+arr[x+2*y] + ...
        let sum = 0;

        // Traverse the array, arr[]
        while (x < N)
        {

            // Update sum
            sum += arr[x];

            // Update x
            x += y;
        }
        Sdocument.write(sum + " ");
    }
}

    // Driver Code

   // Given array
    let arr = [ 1, 2, 7, 5, 4 ];
    let Q= [[ 2, 1 ], [ 3, 2 ]]

    let N = arr.length;
    let M = Q.length;

    querySum(arr, N, Q, M);

 // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
16 5
```

***时间复杂度:**O(N * sqrt(N)+| Q | * sqrt(N))*
***辅助空间:** O(N * sqrt(N))*