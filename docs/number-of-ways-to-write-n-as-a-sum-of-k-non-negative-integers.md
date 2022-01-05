# 将 N 写成 K 个非负整数之和的方式数

> 原文:[https://www . geesforgeks . org/n 作为非负整数 k 的和的写入方式数/](https://www.geeksforgeeks.org/number-of-ways-to-write-n-as-a-sum-of-k-non-negative-integers/)

给定两个正整数 **N** 和 **K** ，任务是统计将 **N** 写成 **K** 个非负整数之和的方式数。

**示例:**

> **输入:** N = 2，K = 3
> **输出:** 6
> **说明:**
> 2 可拆分为 K 个非负整数的总方式为:
> 1。(0，0，2)
> 2。(0，2，0)
> 3。(2，0，0)
> 4。(0，1，1)
> 5。(1，0，1)
> 6。(1, 1, 0)
> 
> **输入:** N = 3，K = 2
> **输出:** 4
> **说明:**
> 将 3 拆分为 2 个非负整数的总方式为:
> 1。(0，3)
> 2。(3，0)
> 3。(1，2)
> 4。(2, 1)

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。以下是步骤:

1.  将 2D 数组初始化为 **dp[K+1][N+1]** ，其中行对应于我们选取的元素的数量，列对应于相应的总和。
2.  在上表 **dp[][]** 中，以和为 **K** 开始填充第一行和第一列。
3.  假设我们到达第行第**列第**列的第**处，即我们可以选择的元素，我们需要得到总和 j。要计算直到 dp[i][j]的路数，请首先选择**(I–1)**元素，然后选择**(j–x)**元素，其中 x 是第一个**(I–1)**元素的总和。**
4.  重复以上步骤填充 dp[][]数组。
5.  值 **dp[n][m]** 将给出所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
int countWays(int n, int m)
{

    // Initialise dp[][] array
    int dp[m + 1][n + 1];

    // Only 1 way to choose the value
    // with sum K
    for (int i = 0; i <= n; i++) {
        dp[1][i] = 1;
    }

    // Initialise sum
    int sum;

    for (int i = 2; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            sum = 0;

            // Count the ways from previous
            // states
            for (int k = 0; k <= j; k++) {
                sum += dp[i - 1][k];
            }

            // Update the sum
            dp[i][j] = sum;
        }
    }

    // Return the final count of ways
    return dp[m][n];
}

// Driver Code
int main()
{
    int N = 2, K = 3;

    // Function call
    cout << countWays(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
static int countWays(int n, int m)
{

    // Initialise dp[][] array
    int [][]dp = new int[m + 1][n + 1];

    // Only 1 way to choose the value
    // with sum K
    for(int i = 0; i <= n; i++)
    {
       dp[1][i] = 1;
    }

    // Initialise sum
    int sum;

    for(int i = 2; i <= m; i++)
    {
       for(int j = 0; j <= n; j++)
       {
          sum = 0;

          // Count the ways from previous
          // states
          for(int k = 0; k <= j; k++)
          {
             sum += dp[i - 1][k];
          }

          // Update the sum
          dp[i][j] = sum;
       }
    }

    // Return the final count of ways
    return dp[m][n];
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, K = 3;

    // Function call
    System.out.print(countWays(N, K));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of ways
# to write N as sum of k non-negative
# integers
def countWays(n, m):

    # Initialise dp[][] array
    dp = [[ 0 for i in range(n + 1)]
              for i in range(m + 1)]

    # Only 1 way to choose the value
    # with sum K
    for i in range(n + 1):
        dp[1][i] = 1

    # Initialise sum
    sum = 0

    for i in range(2, m + 1):
        for j in range(n + 1):
            sum = 0

            # Count the ways from previous
            # states
            for k in range(j + 1):
                sum += dp[i - 1][k]

            # Update the sum
            dp[i][j] = sum

    # Return the final count of ways
    return dp[m][n]

# Driver Code
if __name__ == '__main__':
    N = 2
    K = 3

    # Function call
    print(countWays(N, K))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
static int countWays(int n, int m)
{

    // Initialise [,]dp array
    int [,]dp = new int[m + 1, n + 1];

    // Only 1 way to choose the value
    // with sum K
    for(int i = 0; i <= n; i++)
    {
       dp[1, i] = 1;
    }

    // Initialise sum
    int sum;

    for(int i = 2; i <= m; i++)
    {
       for(int j = 0; j <= n; j++)
       {
          sum = 0;

          // Count the ways from previous
          // states
          for(int k = 0; k <= j; k++)
          {
             sum += dp[i - 1, k];
          }

          // Update the sum
          dp[i, j] = sum;
       }
    }

    // Return the readonly count of ways
    return dp[m, n];
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, K = 3;

    // Function call
    Console.Write(countWays(N, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
function countWays(n, m)
{

    // Initialise dp[][] array
    var dp = Array.from(Array(m+1), ()=>Array(n+1));

    // Only 1 way to choose the value
    // with sum K
    for (var i = 0; i <= n; i++) {
        dp[1][i] = 1;
    }

    // Initialise sum
    var sum;

    for (var i = 2; i <= m; i++) {
        for (var j = 0; j <= n; j++) {
            sum = 0;

            // Count the ways from previous
            // states
            for (var k = 0; k <= j; k++) {
                sum += dp[i - 1][k];
            }

            // Update the sum
            dp[i][j] = sum;
        }
    }

    // Return the final count of ways
    return dp[m][n];
}

// Driver Code
var N = 2, K = 3;
// Function call
document.write( countWays(N, K));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(K * N<sup>2</sup>)*
***辅助空间复杂度:** O(N*K)*

**优化方法:**计算总和然后存储计数的想法增加了时间复杂度。我们可以通过将总和存储在上面的 [dp[][]表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)中来减少它。
以下是上述办法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
int countWays(int n, int m)
{
    // Initialise dp[][] array
    int dp[m + 1][n + 1];

    // Fill the dp[][] with sum = m
    for (int i = 0; i <= n; i++) {
        dp[1][i] = 1;
        if (i != 0) {
            dp[1][i] += dp[1][i - 1];
        }
    }

    // Iterate the dp[][] to fill the
    // dp[][] array
    for (int i = 2; i <= m; i++) {
        for (int j = 0; j <= n; j++) {

            // Condition for first column
            if (j == 0) {
                dp[i][j] = dp[i - 1][j];
            }

            // Else fill the dp[][] with
            // sum till (i, j)
            else {
                dp[i][j] = dp[i - 1][j];

                // If reach the end, then
                // return the value
                if (i == m && j == n) {
                    return dp[i][j];
                }

                // Update at current index
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 2, K = 3;

    // Function call
    cout << countWays(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
static int countWays(int n, int m)
{
    // Initialise dp[][] array
    int [][]dp = new int[m + 1][n + 1];

    // Fill the dp[][] with sum = m
    for (int i = 0; i <= n; i++)
    {
        dp[1][i] = 1;
        if (i != 0)
        {
            dp[1][i] += dp[1][i - 1];
        }
    }

    // Iterate the dp[][] to fill the
    // dp[][] array
    for (int i = 2; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {

            // Condition for first column
            if (j == 0)
            {
                dp[i][j] = dp[i - 1][j];
            }

            // Else fill the dp[][] with
            // sum till (i, j)
            else
            {
                dp[i][j] = dp[i - 1][j];

                // If reach the end, then
                // return the value
                if (i == m && j == n)
                {
                    return dp[i][j];
                }

                // Update at current index
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
    return Integer.MIN_VALUE;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, K = 3;

    // Function call
    System.out.print(countWays(N, K));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of ways
# to write N as sum of k non-negative
# integers
def countWays(n, m):

    # Initialise dp[][] array
    dp = [[0 for i in range(n + 1)]
             for j in range(m + 1)]

    # Fill the dp[][] with sum = m
    for i in range(n + 1):
        dp[1][i] = 1
        if (i != 0):
            dp[1][i] += dp[1][i - 1]

    # Iterate the dp[][] to fill the
    # dp[][] array
    for i in range(2, m + 1):
        for j in range(n + 1):

            # Condition for first column
            if (j == 0):
                dp[i][j] = dp[i - 1][j]

            # Else fill the dp[][] with
            # sum till (i, j)
            else:
                dp[i][j] = dp[i - 1][j]

                # If reach the end, then
                # return the value
                if (i == m and j == n):
                    return dp[i][j]

                # Update at current index
                dp[i][j] += dp[i][j - 1]

# Driver Code
N = 2
K = 3

# Function call
print(countWays(N, K))

# This code is contributed by ShubhamCoder
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
static int countWays(int n, int m)
{
    // Initialise dp[][] array
    int [,]dp = new int[m + 1, n + 1];

    // Fill the dp[][] with sum = m
    for (int i = 0; i <= n; i++)
    {
        dp[1, i] = 1;
        if (i != 0)
        {
            dp[1, i] += dp[1, i - 1];
        }
    }

    // Iterate the dp[][] to fill the
    // dp[][] array
    for (int i = 2; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {

            // Condition for first column
            if (j == 0)
            {
                dp[i, j] = dp[i - 1, j];
            }

            // Else fill the dp[][] with
            // sum till (i, j)
            else
            {
                dp[i, j] = dp[i - 1, j];

                // If reach the end, then
                // return the value
                if (i == m && j == n)
                {
                    return dp[i, j];
                }

                // Update at current index
                dp[i, j] += dp[i, j - 1];
            }
        }
    }
    return Int32.MinValue;
}

// Driver Code
public static void Main()
{
    int N = 2, K = 3;

    // Function call
    Console.Write(countWays(N, K));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of ways
// to write N as sum of k non-negative
// integers
function countWays(n,m)
{
    // Initialise dp[][] array
    let dp = new Array(m + 1);
    for(let i=0;i<m+1;i++)
    {
        dp[i]=new Array(n+1);
        for(let j=0;j<n+1;j++)
            dp[i][j]=0;
    }

    // Fill the dp[][] with sum = m
    for (let i = 0; i <= n; i++)
    {
        dp[1][i] = 1;
        if (i != 0)
        {
            dp[1][i] += dp[1][i - 1];
        }
    }

    // Iterate the dp[][] to fill the
    // dp[][] array
    for (let i = 2; i <= m; i++)
    {
        for (let j = 0; j <= n; j++)
        {

            // Condition for first column
            if (j == 0)
            {
                dp[i][j] = dp[i - 1][j];
            }

            // Else fill the dp[][] with
            // sum till (i, j)
            else
            {
                dp[i][j] = dp[i - 1][j];

                // If reach the end, then
                // return the value
                if (i == m && j == n)
                {
                    return dp[i][j];
                }

                // Update at current index
                dp[i][j] += dp[i][j - 1];
            }
        }
    }
    return Number.MIN_VALUE;
}

// Driver Code
let N = 2, K = 3;

// Function call
document.write(countWays(N, K));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(K*N)*
***辅助空间复杂度:** O(N*K)*