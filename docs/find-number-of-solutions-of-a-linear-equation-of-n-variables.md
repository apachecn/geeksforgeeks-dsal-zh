# 求一个 n 变量线性方程的解的个数

> 原文:[https://www . geesforgeks . org/find-n 元线性方程的解的个数/](https://www.geeksforgeeks.org/find-number-of-solutions-of-a-linear-equation-of-n-variables/)

给定 n 个变量的线性方程，求其非负整数解的个数。例如，假设给定的方程是“x + 2y = 5”，这个方程的解是“x = 1，y = 2”，“x = 5，y = 0”和“x = 1”。可以假设给定方程中的所有系数都是正整数。
**例:**

```
Input:  coeff[] = {1, 2}, rhs = 5
Output: 3
The equation "x + 2y = 5" has 3 solutions.
(x=3,y=1), (x=1,y=2), (x=5,y=0)

Input:  coeff[] = {2, 2, 3}, rhs = 4
Output: 3
The equation "2x + 2y + 3z = 4"  has 3 solutions.
(x=0,y=2,z=0), (x=2,y=0,z=0), (x=1,y=1,z=0)
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
我们可以递归地解决这个问题。其思想是从 rhs 中减去第一个系数，然后对 rhs 的剩余值进行递归。

```
If rhs = 0
  countSol(coeff, 0, rhs, n-1) = 1
Else
  countSol(coeff, 0, rhs, n-1) = ∑countSol(coeff, i, rhs-coeff[i], m-1) 
                                 where coeff[i]<=rhs and 
                                 i varies from 0 to n-1                             
```

下面是上述解决方案的递归实现。

## C++

```
// A naive recursive C++ program to
// find number of non-negative solutions
// for a given linear equation
#include<bits/stdc++.h>
using namespace std;

// Recursive function that returns
// count of solutions for given rhs
// value and coefficients coeff[start..end]
int countSol(int coeff[], int start,
             int end, int rhs)
{
    // Base case
    if (rhs == 0)
    return 1;

    // Initialize count
    // of solutions
    int result = 0;

    // One by subtract all smaller or
    // equal coefficiants and recur
    for (int i = start; i <= end; i++)
    if (coeff[i] <= rhs)
        result += countSol(coeff, i, end,
                           rhs - coeff[i]);

    return result;
}

// Driver Code
int main()
{
    int coeff[] = {2, 2, 5};
    int rhs = 4;
    int n = sizeof(coeff) / sizeof(coeff[0]);
    cout << countSol(coeff, 0, n - 1, rhs);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive recursive Java program
// to find number of non-negative
// solutions for a given linear equation
import java.io.*;

class GFG
{

    // Recursive function that returns
    // count of solutions for given
    // rhs value and coefficients coeff[start..end]
    static int countSol(int coeff[], int start,
                        int end, int rhs)
    {
        // Base case
        if (rhs == 0)
        return 1;

        // Initialize count of solutions
        int result = 0;

        // One by subtract all smaller or
        // equal coefficiants and recur
        for (int i = start; i <= end; i++)
        if (coeff[i] <= rhs)
            result += countSol(coeff, i, end,
                               rhs - coeff[i]);

        return result;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int coeff[] = {2, 2, 5};
        int rhs = 4;
        int n = coeff.length;
        System.out.println (countSol(coeff, 0,
                                     n - 1, rhs));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# A naive recursive Python program
# to find number of non-negative
# solutions for a given linear equation

# Recursive function that returns
# count of solutions for given rhs
# value and coefficients coeff[stat...end]
def countSol(coeff, start, end, rhs):

    # Base case
    if (rhs == 0):
        return 1

    # Initialize count of solutions
    result = 0

    # One by one subtract all smaller or
    # equal coefficients and recur
    for i in range(start, end+1):
        if (coeff[i] <= rhs):
            result += countSol(coeff, i, end,
                               rhs - coeff[i])

    return result

# Driver Code
coeff = [2, 2, 5]
rhs = 4
n = len(coeff)
print(countSol(coeff, 0, n - 1, rhs))

# This code is contributed
# by Soumen Ghosh
```

## C#

```
// A naive recursive C# program
// to find number of non-negative
// solutions for a given linear equation
using System;

class GFG
{

    // Recursive function that
    // returns count of solutions
    // for given RHS value and
    // coefficients coeff[start..end]
    static int countSol(int []coeff, int start,
                        int end, int rhs)
    {
        // Base case
        if (rhs == 0)
        return 1;

        // Initialize count of solutions
        int result = 0;

        // One by subtract all smaller or
        // equal coefficiants and recur
        for (int i = start; i <= end; i++)
        if (coeff[i] <= rhs)
            result += countSol(coeff, i, end,
                               rhs - coeff[i]);

        return result;
    }

    // Driver Code
    public static void Main ()
    {
        int []coeff = {2, 2, 5};
        int rhs = 4;
        int n = coeff.Length;
        Console.Write (countSol(coeff, 0,
                                n - 1, rhs));

    }
}

// This Code is contributed
// by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive recursive PHP program to
// find number of non-negative solutions
// for a given linear equation

// Recursive function that returns count
// of solutions for given rhs value and
// coefficients coeff[start..end]

function countSol($coeff, $start, $end, $rhs)
{
    // Base case
    if ($rhs == 0)
    return 1;

    // Initialize count of solutions
    $result = 0;

    // One by subtract all smaller or
    // equal coefficiants and recur
    for ($i = $start; $i <= $end; $i++)
    if ($coeff[$i] <= $rhs)
        $result += countSol($coeff, $i, $end,
                            $rhs - $coeff[$i]);

    return $result;
}

// Driver Code
$coeff = array (2, 2, 5);
$rhs = 4;
$n = sizeof($coeff);
echo countSol($coeff, 0, $n - 1, $rhs);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // A naive recursive Javascript program
    // to find number of non-negative
    // solutions for a given linear equation

    // Recursive function that
    // returns count of solutions
    // for given RHS value and
    // coefficients coeff[start..end]
    function countSol(coeff, start, end, rhs)
    {
        // Base case
        if (rhs == 0)
            return 1;

        // Initialize count of solutions
        let result = 0;

        // One by subtract all smaller or
        // equal coefficiants and recur
        for (let i = start; i <= end; i++)
          if (coeff[i] <= rhs)
              result += countSol(coeff, i, end, rhs - coeff[i]);

        return result;
    }

    let coeff = [2, 2, 5];
    let rhs = 4;
    let n = coeff.length;
    document.write(countSol(coeff, 0, n - 1, rhs));

</script>
```

**输出:**

```
3
```

上述解的时间复杂度是指数的。我们可以使用动态规划在[伪多项式时间](https://en.wikipedia.org/wiki/Pseudo-polynomial_time)中解决这个问题(时间复杂度取决于输入的数值)。思路类似于[动态规划解子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)。下面是基于动态编程的实现。

## C++

```
// A Dynamic programming based C++
// program to find number of non-negative
// solutions for a given linear equation
#include<bits/stdc++.h>
using namespace std;

// Returns count of solutions for
// given rhs and coefficients coeff[0..n-1]
int countSol(int coeff[], int n, int rhs)
{
    // Create and initialize a table
    // to store results of subproblems
    int dp[rhs + 1];
    memset(dp, 0, sizeof(dp));
    dp[0] = 1;

    // Fill table in bottom up manner
    for (int i = 0; i < n; i++)
    for (int j = coeff[i]; j <= rhs; j++)
        dp[j] += dp[j - coeff[i]];

    return dp[rhs];
}

// Driver Code
int main()
{
    int coeff[] = {2, 2, 5};
    int rhs = 4;
    int n = sizeof(coeff) / sizeof(coeff[0]);
    cout << countSol(coeff, n, rhs);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic programming based Java program
// to find number of non-negative solutions
// for a given linear equation
import java.util.Arrays;

class GFG
{
    // Returns counr of solutions for given
    // rhs and coefficients coeff[0..n-1]
    static int countSol(int coeff[],
                        int n, int rhs)
    {

        // Create and initialize a table to
        // store results of subproblems
        int dp[] = new int[rhs + 1];
        Arrays.fill(dp, 0);
        dp[0] = 1;

        // Fill table in bottom up manner
        for (int i = 0; i < n; i++)
        for (int j = coeff[i]; j <= rhs; j++)
            dp[j] += dp[j - coeff[i]];

        return dp[rhs];
    }

    // Driver code
    public static void main (String[] args)
    {
        int coeff[] = {2, 2, 5};
        int rhs = 4;
        int n = coeff.length;
        System.out.print(countSol(coeff, n, rhs));
    }
}

// This code is contributed by Anant Agarwal
```

## 蟒蛇 3

```
# A Dynamic Programming based
# Python program to find number
# of non-negative solutions for
# a given linear equation

# Returns count of solutions for given
# rhs and coefficients coeff[0...n-1]
def countSol(coeff, n, rhs):

    # Create and initialize a table
    # to store results of subproblems
    dp = [0 for i in range(rhs + 1)]
    dp[0] = 1

    # Fill table in bottom up manner
    for i in range(n):
        for j in range(coeff[i], rhs + 1):
            dp[j] += dp[j - coeff[i]]

    return dp[rhs]

# Driver Code
coeff = [2, 2, 5]
rhs = 4
n = len(coeff)
print(countSol(coeff, n, rhs))

# This code is contributed
# by Soumen Ghosh
```

## C#

```
// A Dynamic programming based
// C# program to find number of
// non-negative solutions for a
// given linear equation
using System;

class GFG
{
    // Returns counr of solutions
    // for given rhs and coefficients
    // coeff[0..n-1]
    static int countSol(int []coeff,
                        int n, int rhs)
    {

        // Create and initialize a
        // table to store results
        // of subproblems
        int []dp = new int[rhs + 1];

        // Arrays.fill(dp, 0);
        dp[0] = 1;

        // Fill table in
        // bottom up manner
        for (int i = 0; i < n; i++)
        for (int j = coeff[i]; j <= rhs; j++)
            dp[j] += dp[j - coeff[i]];

        return dp[rhs];
    }

    // Driver code
    public static void Main ()
    {
        int []coeff = {2, 2, 5};
        int rhs = 4;
        int n = coeff.Length;
        Console.Write(countSol(coeff,
                               n, rhs));
    }
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// non-negative solutions for a
// given linear equation

// Returns count of solutions
// for given rhs and coefficients
// coeff[0..n-1]
function countSol($coeff, $n, $rhs)
{
    // Create and initialize a table
    // to store results of subproblems
    $dp = str_repeat ("\0", 256);
    $dp[0] = 1;

    // Fill table in
    // bottom up manner
    for ($i = 0; $i < $n; $i++)
    for ($j = $coeff[$i];
         $j <= $rhs; $j++)
        $dp[$j] = $dp[$j] + ($dp[$j -
                             $coeff[$i]]);

    return $dp[$rhs];
}

// Driver Code
$coeff = array(2, 2, 5);
$rhs = 4;

// $n = count($coeff);
$n = sizeof($coeff) / sizeof($coeff[0]);
echo countSol($coeff, $n, $rhs);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

    // A Dynamic programming based
    // Javascript program to find number of
    // non-negative solutions for a
    // given linear equation

    // Returns counr of solutions
    // for given rhs and coefficients
    // coeff[0..n-1]
    function countSol(coeff, n, rhs)
    {

        // Create and initialize a
        // table to store results
        // of subproblems
        let dp = new Array(rhs + 1);
        dp.fill(0);

        // Arrays.fill(dp, 0);
        dp[0] = 1;

        // Fill table in
        // bottom up manner
        for (let i = 0; i < n; i++)
        for (let j = coeff[i]; j <= rhs; j++)
            dp[j] += dp[j - coeff[i]];

        return dp[rhs];
    }

    let coeff = [2, 2, 5];
    let rhs = 4;
    let n = coeff.length;
    document.write(countSol(coeff, n, rhs));

</script>
```

**输出:**

```
3
```

以上解的时间复杂度为 O(n * rhs)
本文由**阿希什·古普塔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息