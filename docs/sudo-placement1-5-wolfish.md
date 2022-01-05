# Sudo 放置【1.5】| Wolfish

> 原文:[https://www.geeksforgeeks.org/sudo-placement1-5-wolfish/](https://www.geeksforgeeks.org/sudo-placement1-5-wolfish/)

给定一个 N×N 矩阵，其中单元格(I，j)处的值是从单元格(I，j)移动到单元格(I–1，j–1)、(I–1，j)或(I，j–1)的成本。您的任务是在 N×N 矩阵(基于 0 的索引)中找到从(N-1，N-1)单元格到(0，0)单元格的最大成本路径。但是，从一个单元格到另一个单元格的移动有一些限制。如果你在(I，j)单元，并且(i + j)是 2 的幂，你只能移动到(I–1，j–1)单元。如果(i + j)不是 2 的幂，那么你可以移到(I–1，j)或(I，j–1)
**示例:**

```
Input :[1 2 3 1
        4 5 6 1
        7 8 9 1
        1 1 1 1]
Output: 16 
The maximum cost path is: 
(3, 3) -> (3, 2) -> (2, 2) -> (1, 1) -> (0, 0).
Cost pathwise is: 
1 + 1 + 9 + 5 = 16.

Input: [1 2 
        3 4]
Output: 4 
```

**最优子结构:**
这个问题是[最小成本](https://www.geeksforgeeks.org/dynamic-programming-set-6-min-cost-path/)问题的变种。从(n-1，n-1)到达(0，0)的路径必须通过三个单元(I，j-1)或(i-1，j)或(i-1，j-1)。将调用自顶向下的递归函数，对于 m 和 n 的每个值，检查(m+n)是否是 2 的幂。如果是 2 的幂，则移动到单元格(m-1，n-1)并将该值加到 a[m][n]处。因此成本为:

> 成本= a[m][n] +最大成本(a，m–1，n–1)

如果不是 2 的幂，那么我们可以移到(m-1，n)和(m，n-1)两个单元格。所以成本会是:

> 成本= a[m][n] +最大值(最大成本(a，m–1，n)，最大成本(a，m，n–1))

下面是上述方法的递归实现:

## C++

```
// C++ program for
// SP - Wolfish
#include <bits/stdc++.h>
using namespace std;

const int size = 1000;

// Function to find the maxCost of path from
// (n-1, n-1) to (0, 0) | recursive approach
int maxCost(int a[][size], int m, int n)
{
    // base condition
    if (n < 0 || m < 0)
        return -1e9;

    // reaches the point
    else if (m == 0 && n == 0)
        return 0;

    else {

        // i + j
        int num = m + n;

        // check if it is a power of 2,
        // then only move diagonally
        if ((num & (num - 1)) == 0)
            return a[m][n] + maxCost(a, m - 1, n - 1);

        // if not a power of 2
        // then move side-wise
        else
            return a[m][n] + max(maxCost(a, m - 1, n),
                                 maxCost(a, m, n - 1));
    }
}

// Function to return the maximum cost
int answer(int a[][size], int n)
{
    // calling dp function to get the answer
    return maxCost(a, n - 1, n - 1);
}

// Driver Code
int main()
{
    int a[][size] = { { 1, 2, 3, 1 },
                      { 4, 5, 6, 1 },
                      { 7, 8, 9, 1 },
                      { 1, 1, 1, 1 } };
    int n = 4;

    // Function calling to get the answer
    cout << answer(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for SP - Wolfish
class GFG {

    static int size = 1000;

    // Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0) | recursive approach
    public static int maxCost(int[][] a, int m, int n)
    {
        // base condition
        if (n < 0 || m < 0) {
            return -1;
        }

        // reaches the point
        else if (m == 0 && n == 0) {
            return 0;
        }
        else {

            // i + j
            int num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0) {
                return a[m][n] + maxCost(a, m - 1, n - 1);
            }

            // if not a power of 2
            // then move side-wise
            else {
                return a[m][n] + Math.max(maxCost(a, m - 1, n), maxCost(a, m, n - 1));
            }
        }
    }

    // Function to return the maximum cost
    public static int answer(int[][] a, int n)
    {
        // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] a = new int[][] { { 1, 2, 3, 1 },
                                  { 4, 5, 6, 1 },
                                  { 7, 8, 9, 1 },
                                  { 1, 1, 1, 1 } };
        int n = 4;

        System.out.println(answer(a, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python program for
# SP - Wolfish
size = 1000

# Function to find the maxCost of path from
# (n-1, n-1) to (0, 0) | recursive approach
def maxCost(a: list, m: int, n: int) -> int:

    # base condition
    if n < 0 or m < 0:
        return int(-1e9)

    # reaches the point
    elif m == 0 and n == 0:
        return 0
    else:

        # i + j
        num = m + n

        # check if it is a power of 2,
        # then only move diagonally
        if (num & (num - 1)) == 0:
            return a[m][n] + maxCost(a, m - 1, n - 1)

        # if not a power of 2
        # then move side-wise
        else:
            return a[m][n] + max(maxCost(a, m - 1, n), maxCost(a, m, n - 1))

# Function to return the maximum cost
def answer(a: list, n: int) -> int:

    # calling dp function to get the answer
    return maxCost(a, n - 1, n - 1)

# Driver Code
if __name__ == "__main__":

    a = [[1, 2, 3, 1],
        [4, 5, 6, 1],
        [7, 8, 9, 1],
        [1, 1, 1, 1]]
    n = 4

    # Function calling to get the answer
    print(answer(a, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for
// SP - Wolfish
using System;

class GFG {
    static int size = 1000;

    // Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0) | recursive approach
    public static int maxCost(int[, ] a, int m, int n)
    {
        // base condition
        if (n < 0 || m < 0)
            return -1;

        // reaches the point
        else if (m == 0 && n == 0)
            return 0;

        else {

            // i + j
            int num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0)
                return a[m, n] + maxCost(a, m - 1, n - 1);

            // if not a power of 2
            // then move side-wise
            else
                return a[m, n] + Math.Max(maxCost(a, m - 1, n), maxCost(a, m, n - 1));
        }
    }

    // Function to return the maximum cost
    public static int answer(int[, ] a, int n)
    {
        // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1);
    }

    // Driver Code
    static void Main()
    {
        int[, ] a = new int[, ] { { 1, 2, 3, 1 },
                                  { 4, 5, 6, 1 },
                                  { 7, 8, 9, 1 },
                                  { 1, 1, 1, 1 } };
        int n = 4;

        // Function calling to get the answer
        Console.Write(answer(a, n));
    }
    // This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>
// Javascript program for SP - Wolfish

let size = 1000;

// Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0) | recursive approach
function maxCost(a,m,n)
{
    // base condition
        if (n < 0 || m < 0) {
            return -1;
        }

        // reaches the point
        else if (m == 0 && n == 0) {
            return 0;
        }
        else {

            // i + j
            let num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0) {
                return a[m][n] + maxCost(a, m - 1, n - 1);
            }

            // if not a power of 2
            // then move side-wise
            else {
                return a[m][n] + Math.max(maxCost(a, m - 1, n), maxCost(a, m, n - 1));
            }
        }
}

// Function to return the maximum cost
function answer(a,n)
{
    // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1);
}

// Driver Code
let a=[[ 1, 2, 3, 1 ],[ 4, 5, 6, 1 ],
                                  [ 7, 8, 9, 1 ],
                                  [ 1, 1, 1, 1 ]];
let  n = 4;
document.write(answer(a, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
16
```

**时间复杂度:** O(2 <sup>N</sup> )

使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)的方法

在上面的递归中，很多子问题被反复调用。为了减少重复呼叫的次数，使用了记忆。常见的观察点是，每次函数调用时，只有两个参数值发生变化。因此，如果我们记住 dp[][]数组中的返回值，调用的次数将减少到 N^2.因此，将每个 maxCost(m，n)的计算值存储在 dp[m][n]中。如果 maxCost(m，n)被多次调用，那么通过返回存储在 dp[m][n]中的值，将减少该函数的额外调用。
以下是上述方法的高效实现:

## C++

```
// C++ program for SP - Wolfish
#include <bits/stdc++.h>
using namespace std;

const int size = 1000;

// Function to find the maxCost of path from
// (n-1, n-1) to (0, 0)
int maxCost(int a[][size], int m, int n, int dp[][size])
{
    // base condition
    if (n < 0 || m < 0)
        return -1e9;

    // reaches the point
    else if (m == 0 && n == 0)
        return 0;

    // if the state has been visited previously
    else if (dp[m][n] != -1)
        return dp[m][n];
    else {

        // i + j
        int num = m + n;

        // check if it is a power of 2,
        // then only move diagonally
        if ((num & (num - 1)) == 0)
            return dp[m][n] = a[m][n] + maxCost(a, m - 1, n - 1, dp);

        // if not a power of 2
        // then move side-wise
        else
            return dp[m][n] = (a[m][n] + max(maxCost(a, m - 1, n, dp),
                                             maxCost(a, m, n - 1, dp)));
    }
}

// Function to return the maximum cost
int answer(int a[][size], int n)
{
    int dp[size][size];
    memset(dp, -1, sizeof dp);

    // calling dp function to get the answer
    return maxCost(a, n - 1, n - 1, dp);
}

// Driver Code
int main()
{
    int a[][size] = { { 1, 2, 3, 1 },
                      { 4, 5, 6, 1 },
                      { 7, 8, 9, 1 },
                      { 1, 1, 1, 1 } };
    int n = 4;

    // Function calling to get the answer
    cout << answer(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for SP - Wolfish

class GFG {

    static int size = 1000;

    // Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0)
    static int maxCost(int a[][], int m, int n, int dp[][])
    {
        // base condition
        if (n < 0 || m < 0)
            return (int)-1e9;

        // reaches the point
        else if (m == 0 && n == 0)
            return 0;

        // if the state has been visited previously
        else if (dp[m][n] != -1)
            return dp[m][n];
        else {

            // i + j
            int num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0)
                return dp[m][n] = a[m][n] + maxCost(a, m - 1, n - 1, dp);

            // if not a power of 2
            // then move side-wise
            else
                return dp[m][n] = (a[m][n] + Math.max(maxCost(a, m - 1, n, dp),
                                                      maxCost(a, m, n - 1, dp)));
        }
    }

    // Function to return the maximum cost
    static int answer(int a[][], int n)
    {
        int dp[][] = new int[size][size];
        for (int i = 0; i < size; i++) {
            for (int j = 0; j < size; j++) {
                dp[i][j] = -1;
            }
        }

        // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1, dp);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[][] = { { 1, 2, 3, 1 },
                      { 4, 5, 6, 1 },
                      { 7, 8, 9, 1 },
                      { 1, 1, 1, 1 } };
        int n = 4;

        // Function calling to get the answer
        System.out.println(answer(a, n));
    }
}
// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for SP - Wolfish

size = 1000;

# Function to find the maxCost of path from
# (n-1, n-1) to (0, 0)
def maxCost(a, m, n, dp):
    # base condition
    if (n < 0 or m < 0):
        return int(-1e9);

    # reaches the point
    elif(m == 0 and n == 0):
        return 0;

    # if the state has been visited previously
    elif(dp[m][n] != -1):
        return dp[m][n];
    else:

        # i + j
        num = m + n;

        # check if it is a power of 2,
        # then only move diagonally
        if ((num & (num - 1)) == 0):
            dp[m][n] = a[m][n] + maxCost(a, m - 1, n - 1, dp);
            return dp[m][n];

        # if not a power of 2
        # then move side-wise
        else:
            dp[m][n] = (a[m][n] + max(maxCost(a, m - 1, n, dp), maxCost(a, m, n - 1, dp)));
            return dp[m][n];

# Function to return the maximum cost
def answer(a, n):
    dp = [[0 for i in range(size)] for j in range(size)] ;
    for i in range(size):
        for j in range(size):
            dp[i][j] = -1;

    # calling dp function to get the answer
    return maxCost(a, n - 1, n - 1, dp);

# Driver Code
if __name__ == '__main__':
    a = [[ 1, 2, 3, 1 ],[ 4, 5, 6, 1 ],[ 7, 8, 9, 1 ],[ 1, 1, 1, 1 ]];
    n = 4;

    # Function calling to get the answer
    print(answer(a, n));

# This code contributed by Rajput-Ji
```

## C#

```
// C# program for SP - Wolfish
using System;

class GFG
{

    static int size = 1000;

    // Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0)
    static int maxCost(int [,]a, int m, int n, int [,]dp)
    {
        // base condition
        if (n < 0 || m < 0)
            return (int)-1e9;

        // reaches the point
        else if (m == 0 && n == 0)
            return 0;

        // if the state has been visited previously
        else if (dp[m, n] != -1)
            return dp[m,n];
        else {

            // i + j
            int num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0)
                return dp[m, n] = a[m, n] + maxCost(a, m - 1, n - 1, dp);

            // if not a power of 2
            // then move side-wise
            else
                return dp[m,n] = (a[m,n] + Math.Max(maxCost(a, m - 1, n, dp),
                                                    maxCost(a, m, n - 1, dp)));
        }
    }

    // Function to return the maximum cost
    static int answer(int [,]a, int n)
    {
        int [,]dp = new int[size,size];
        for (int i = 0; i < size; i++)
        {
            for (int j = 0; j < size; j++)
            {
                dp[i, j] = -1;
            }
        }

        // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1, dp);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int [,]a = { { 1, 2, 3, 1 },
                    { 4, 5, 6, 1 },
                    { 7, 8, 9, 1 },
                    { 1, 1, 1, 1 } };
        int n = 4;

        // Function calling to get the answer
        Console.WriteLine(answer(a, n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program for SP - Wolfish

let size = 1000;

// Function to find the maxCost of path from
    // (n-1, n-1) to (0, 0)
function maxCost(a,m,n,dp)
{
    // base condition
        if (n < 0 || m < 0)
            return -1e9;

        // reaches the point
        else if (m == 0 && n == 0)
            return 0;

        // if the state has been visited previously
        else if (dp[m][n] != -1)
            return dp[m][n];
        else {

            // i + j
            let num = m + n;

            // check if it is a power of 2,
            // then only move diagonally
            if ((num & (num - 1)) == 0)
                return dp[m][n] = a[m][n] + maxCost(a, m - 1, n - 1, dp);

            // if not a power of 2
            // then move side-wise
            else
                return dp[m][n] = (a[m][n] + Math.max(maxCost(a, m - 1, n, dp),
                                                      maxCost(a, m, n - 1, dp)));
        }
}

// Function to return the maximum cost
function answer(a,n)
{
    let dp = new Array(size);
        for (let i = 0; i < size; i++) {
            dp[i]=new Array(size);
            for (let j = 0; j < size; j++) {
                dp[i][j] = -1;
            }
        }

        // calling dp function to get the answer
        return maxCost(a, n - 1, n - 1, dp);
}

// Driver Code
let a=[[ 1, 2, 3, 1 ],
                      [ 4, 5, 6, 1 ],
                      [ 7, 8, 9, 1 ],
                      [ 1, 1, 1, 1 ]];
let n = 4;

// Function calling to get the answer
document.write(answer(a, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
16
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N <sup>2</sup> )
**注:**要实现自下而上的方法，我们需要检查((m+1) + (n+1))是否是 2 的幂，而不是(m+n)，因为移动是自上而下的。