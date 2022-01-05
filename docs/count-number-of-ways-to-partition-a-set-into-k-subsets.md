# 统计将一个集合划分为 k 个子集的方法数量

> 原文:[https://www . geeksforgeeks . org/count-将集合划分为 k 个子集的方式数/](https://www.geeksforgeeks.org/count-number-of-ways-to-partition-a-set-into-k-subsets/)

给定两个数字 n 和 k，其中 n 代表一个集合中的元素数量，找到一些方法将集合划分为 k 个子集。
**例:**

```
Input: n = 3, k = 2
Output: 3
Explanation: Let the set be {1, 2, 3}, we can partition
             it into 2 subsets in following ways
             {{1,2}, {3}},  {{1}, {2,3}},  {{1,3}, {2}}  

Input: n = 3, k = 1
Output: 1
Explanation: There is only one way {{1, 2, 3}}
```

**<u>递归求解</u>**

*   **方法:**首先，我们定义一个递归解来寻找第 n 个元素的解。有两种情况。
    1.  以前的*n–1*元素分为 k 个分区，即 *S(n-1，k)* 方式。将第 n 个元素放入前 k 个分区之一。所以，*计数= k * S(n-1，k)*
    2.  之前的*n–1*元素被划分为 k–1 个分区，即 *S(n-1，k-1)* 方式。将第 n 个元素放入一个新分区(单元素分区)。所以，*计数= S(n-1，k-1)*
    3.  总计数= k * S(n-1，k) + S(n-1，k-1)。
*   **算法:**
    1.  创建一个递归函数，该函数接受两个参数，n 和 k。该函数返回 n 个元素划分成 k 个集合的总数。
    2.  处理基本案件。如果 n = 0 或 k = 0 或 k > n，则返回 0，因为不能有任何子集。如果 n 等于 k 或 k 等于 1，返回 1。
    3.  否则计算值如下: *S(n，k) = k*S(n-1，k) + S(n-1，k-1)* ，即用递归参数调用递归函数，计算 S(n，k)的值。
    4.  返回总和。
*   **实施:**

## C++

```
// A C++ program to count number of partitions
// of a set with n elements into k subsets
#include<iostream>
using namespace std;

// Returns count of different partitions of n
// elements in k subsets
int countP(int n, int k)
{
  // Base cases
  if (n == 0 || k == 0 || k > n)
     return 0;
  if (k == 1 || k == n)
      return 1;

  // S(n+1, k) = k*S(n, k) + S(n, k-1)
  return  k*countP(n-1, k) + countP(n-1, k-1);
}

// Driver program
int main()
{
   cout <<  countP(3, 2);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to count number
// of partitions of a set with
// n elements into k subsets
import java.io.*;

class GFG
{
    // Returns count of different
    // partitions of n elements in
    // k subsets
    public static int countP(int n, int k)
    {
       // Base cases
       if (n == 0 || k == 0 || k > n)
          return 0;
       if (k == 1 || k == n)
          return 1;

       // S(n+1, k) = k*S(n, k) + S(n, k-1)
       return (k * countP(n - 1, k)
              + countP(n - 1, k - 1));
    }

    // Driver program
    public static void main(String args[])
    {
       System.out.println(countP(3, 2));

    }
}

//This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# A Python3 program to count number
# of partitions of a set with n
# elements into k subsets

# Returns count of different partitions
# of n elements in k subsets
def countP(n, k):

    # Base cases
    if (n == 0 or k == 0 or k > n):
        return 0
    if (k == 1 or k == n):
        return 1

    # S(n+1, k) = k*S(n, k) + S(n, k-1)
    return (k * countP(n - 1, k) +
                countP(n - 1, k - 1))

# Driver Code
if __name__ == "__main__":
    print(countP(3, 2))

# This code is contributed
# by Akanksha Rai(Abby_akku)
```

## C#

```
// C# program to count number
// of partitions of a set with
// n elements into k subsets
using System;

class GFG {

    // Returns count of different
    // partitions of n elements in
    // k subsets
    public static int countP(int n, int k)
    {

        // Base cases
        if (n == 0 || k == 0 || k > n)
            return 0;
        if (k == 1 || k == n)
            return 1;

        // S(n+1, k) = k*S(n, k) + S(n, k-1)
        return (k * countP(n - 1, k)
                + countP(n - 1, k - 1));
    }

    // Driver program
    public static void Main()
    {
        Console.WriteLine(countP(3, 2));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to count
// number of partitions of
// a set with n elements
// into k subsets

// Returns count of different
// partitions of n elements
// in k subsets
function countP($n, $k)
{
    // Base cases
    if ($n == 0 || $k == 0 || $k > $n)
        return 0;
    if ($k == 1 || $k == $n)
        return 1;

    // S(n+1, k) = k*S(n, k)
    // + S(n, k-1)
    return $k * countP($n - 1, $k) +
            countP($n - 1, $k - 1);
}

    // Driver Code
    echo countP(3, 2);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Javascript  program to count number
// of partitions of a set with
// n elements into k subsets

    // Returns count of different
    // partitions of n elements in
    // k subsets
    function countP(n, k)
    {

        // Base cases
       if (n == 0 || k == 0 || k > n)
          return 0;
       if (k == 1 || k == n)
          return 1;

       // S(n + 1, k) = k*S(n, k) + S(n, k - 1)
       return (k * countP(n - 1, k)
              + countP(n - 1, k - 1));
    }

    // Driver program
    document.write(countP(3, 2));

    // This code is contributed by avanitrachhadiya2155   
</script>
```

*   **输出:**

```
3
```

*   **复杂度分析:**
    *   **时间复杂度:** O(2^n).
        对于 n 的每个值，调用两个递归函数。更具体地说，时间复杂度是指数级的。
    *   **空间复杂度:** O(n)(由于调用栈)。

**<u>高效解决方案</u>**

*   **方法:**上述递归解的时间复杂度为指数。可以通过减少重叠子问题来优化解决方案。下面是 *countP(10，7)* 的递归树。子问题 *countP(8，6)* 或 *CP(8，6)* 被多次调用。

![](img/1114d4a781a09f914283943ba7b71d18.png)

*   所以这个问题同时具有动态规划问题的两个性质(参见[类型 1](https://www.geeksforgeeks.org/dynamic-programming-set-1/) 和[类型 2](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/) )。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，通过使用所示的递归公式以自下而上的方式构建临时数组 **dp[][]** ，可以避免相同子问题的重新计算。
    接下来是减少子问题，以优化问题的复杂性。这可以通过两种方式实现:
    1.  *自下而上的方式:*这将保持递归结构完整，并将值存储在 hashmap 或 2D 数组中。然后只计算一次该值，下次调用该函数时返回该值。
    2.  *自上而下的方式:*这保持了大小为 n*k 的 2D 数组，其中 dp[i][j]表示 I 个元素划分为 j 个集合的总数。填写 dp[i][0]和 dp[0][i]的基本情况。对于值(I，j)，需要 dp[i-1][j]和 dp[i-1][j-1]的值。所以从第 0 行到第 n 行，从第 0 列到第 k 列填充 DP。
*   **算法:**
    1.  创建大小为(n + 1 )* ( k + 1)的 Dp 数组 dp[n+1][k+1]。
    2.  填充基本案例的值。对于 I 从 0 到 n 的所有值，填充 *dp[i][0] = 0* ，对于 I 从 0 到 k 的所有值，填充 *dp[0][k] = 0*
    3.  运行嵌套循环，外环从 1 到 n，内环从 1 到 k。
    4.  对于索引 I 和 j(分别为外环和内环)，计算*DP[I][j]= j * DP[I–1][j]+DP[I–1][j–1]*，如果 j == 1 或 i == j，计算 dp[i][j] = 1。
    5.  打印数值 dp[n][k]
*   **实施:**

## C++

```
// A Dynamic Programming based C++ program to count
// number of partitions of a set with n elements
// into k subsets
#include<iostream>
using namespace std;

// Returns count of different partitions of n
// elements in k subsets
int countP(int n, int k)
{
  // Table to store results of subproblems
  int dp[n+1][k+1];

  // Base cases
  for (int i = 0; i <= n; i++)
     dp[i][0] = 0;
  for (int i = 0; i <= k; i++)
     dp[0][k] = 0;

  // Fill rest of the entries in dp[][]
  // in bottom up manner
  for (int i = 1; i <= n; i++)
     for (int j = 1; j <= i; j++)
       if (j == 1 || i == j)
          dp[i][j] = 1;
       else
          dp[i][j] = j * dp[i - 1][j] + dp[i - 1][j - 1];

  return dp[n][k];
}

// Driver program
int main()
{
   cout <<  countP(5, 2);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java program to count
// number of partitions of a set with n elements
// into k subsets
class GFG{

// Returns count of different partitions of n
// elements in k subsets
static int countP(int n, int k)
{
    // Table to store results of subproblems
    int[][] dp = new int[n+1][k+1];

    // Base cases
    for (int i = 0; i <= n; i++)
    dp[i][0] = 0;
    for (int i = 0; i <= k; i++)
    dp[0][k] = 0;

    // Fill rest of the entries in dp[][]
    // in bottom up manner
    for (int i = 1; i <= n; i++)
    for (int j = 1; j <= k; j++)
    if (j == 1 || i == j)
        dp[i][j] = 1;
    else
        dp[i][j] = j * dp[i - 1][j] + dp[i - 1][j - 1];

        return dp[n][k];

}

// Driver program
public static void main(String[] args )
{
    System.out.println(countP(5, 2));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# A Dynamic Programming based Python3 program
# to count number of partitions of a set with
# n elements into k subsets

# Returns count of different partitions
# of n elements in k subsets
def countP(n, k):

    # Table to store results of subproblems
    dp = [[0 for i in range(k + 1)]
             for j in range(n + 1)]

    # Base cases
    for i in range(n + 1):
        dp[i][0] = 0

    for i in range(k + 1):
        dp[0][k] = 0

    # Fill rest of the entries in
    # dp[][] in bottom up manner
    for i in range(1, n + 1):
        for j in range(1, k + 1):
            if (j == 1 or i == j):
                dp[i][j] = 1
            else:
                dp[i][j] = (j * dp[i - 1][j] +
                                dp[i - 1][j - 1])

    return dp[n][k]

# Driver Code
if __name__ == '__main__':
    print(countP(5, 2))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// A Dynamic Programming based C# program 
// to count number of partitions of a 
// set with n elements into k subsets
using System;

class GFG
{

// Returns count of different partitions of n
// elements in k subsets
static int countP(int n, int k)
{
    // Table to store results of subproblems
    int[,] dp = new int[n + 1, k + 1];

    // Base cases
    for (int i = 0; i <= n; i++)
        dp[i, 0] = 0;
    for (int i = 0; i <= k; i++)
        dp[0, k] = 0;

    // Fill rest of the entries in dp[][]
    // in bottom up manner
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= k; j++)
            if (j == 1 || i == j)
                dp[i, j] = 1;
            else
                dp[i, j] = j * dp[i - 1, j] + dp[i - 1, j - 1];

        return dp[n, k];

}

// Driver code
public static void Main( )
{
    Console.Write(countP(5, 2));
}
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based PHP
// program to count number of
// partitions of a set with n 
// elements into k subsets

// Returns count of different
// partitions of n elements in
// k subsets
function countP($n, $k)
{

// Table to store results
// of subproblems
$dp[$n + 1][$k + 1] = array(array());

// Base cases
for ($i = 0; $i <= $n; $i++)
    $dp[$i][0] = 0;
for ($i = 0; $i <= $k; $i++)
    $dp[0][$k] = 0;

// Fill rest of the entries in
// dp[][] in bottom up manner
for ($i = 1; $i <= $n; $i++)
    for ($j = 1; $j <= $i; $j++)
    if ($j == 1 || $i == $j)
        $dp[$i][$j] = 1;
    else
        $dp[$i][$j] = $j * $dp[$i - 1][$j] +
                           $dp[$i - 1][$j - 1];

return $dp[$n][$k];
}

// Driver Code
echo countP(5, 2);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
// A Dynamic Programming based Javascript program to count
// number of partitions of a set with n elements
// into k subsets

    // Returns count of different partitions of n
    // elements in k subsets
    function countP(n,k)
    {
        // Table to store results of subproblems
        let dp = new Array(n+1);
        for(let i = 0; i < n + 1; i++)
        {
            dp[i] = new Array(k+1);
            for(let j = 0; j < k + 1; j++)
            {
                dp[i][j] = -1;
            }
        }

        // Base cases
        for (let i = 0; i <= n; i++)
            dp[i][0] = 0;
        for (let i = 0; i <= k; i++)
            dp[0][k] = 0;

        // Fill rest of the entries in dp[][]
        // in bottom up manner
        for (let i = 1; i <= n; i++)
            for (let j = 1; j <= k; j++)
            if (j == 1 || i == j)
                dp[i][j] = 1;
            else
                dp[i][j] = j * dp[i - 1][j] + dp[i - 1][j - 1];

        return dp[n][k];
    }

    // Driver program
    document.write(countP(5, 2))

    // This code is contributed by rag2127
</script>
```

*   **输出:**

```
15
```

*   **复杂度分析:**
    *   **时间复杂度:** O(n*k)。
        填充了大小为 n*k 的 2D dp 数组，因此时间复杂度为 O(n*k)。
    *   **空间复杂度:** O(n*k)。
        需要额外的 2D 动力定位阵列。

**类似文章:** [铃号](https://www.geeksforgeeks.org/bell-numbers-number-of-ways-to-partition-a-set/)
本文由**拉杰夫·阿格沃尔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。