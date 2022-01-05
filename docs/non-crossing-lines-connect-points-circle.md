# 连接圆内各点的非交叉线

> 原文:[https://www . geesforgeks . org/非交叉线-连接点-圆圈/](https://www.geeksforgeeks.org/non-crossing-lines-connect-points-circle/)

考虑一个圆周上有 **n 个**点的圆，其中 **n 为偶数**。计算我们可以连接这些点的方法的数量，这样就不会有两条连接线相互交叉，并且每个点都恰好与另一个点相连。任何一点都可以与其他任何一点相连。

```
Consider a circle with 4 points.
    1
2        3
    4
In above diagram, there are two 
non-crossing ways to connect
{{1, 2}, {3, 4}} and {{1, 3}, {2, 4}}.

Note that {{2, 3}, {1, 4}} is invalid
as it would cause a cross
```

**例:**

```
Input : n = 2
Output : 1

Input : n = 4
Output : 2

Input : n = 6
Output : 5

Input : n = 3
Output : Invalid
n must be even.
```

我们需要画 n/2 条线来连接 n 个点。当我们画一条线时，我们把需要连接的点分成两组。每一组都需要在自身内部进行连接。下面是相同的递归关系。

```
Let m = n/2

// For each line we draw, we divide points
// into two sets such that one set is going
// to be connected with i lines and other
// with m-i-1 lines.
Count(m) = ∑ Count(i) * Count(m-i-1) 
           where 0 <= i < m
Count(0) = 1

Total number of ways with n points 
               = Count(m) = Count(n/2)
```

如果仔细看上面的复发，其实是[加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)的复发。所以任务简化为寻找第 n/2 个加泰罗尼亚数字。
以下是基于上述思路的实施。

## C++

```
// C++ program to count number of ways to connect n (where n
// is even) points on a circle such that no two connecting
// lines cross each other and every point is connected with
// one other point.
#include<iostream>
using namespace std;

// A dynamic programming based function to find nth
// Catalan number
unsigned long int catalanDP(unsigned int n)
{
    // Table to store results of subproblems
    unsigned long int catalan[n+1];

    // Initialize first two values in table
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[] using recursive formula
    for (int i=2; i<=n; i++)
    {
        catalan[i] = 0;
        for (int j=0; j<i; j++)
            catalan[i] += catalan[j] * catalan[i-j-1];
    }

    // Return last entry
    return catalan[n];
}

// Returns count of ways to connect n points on a circle
// such that no two connecting lines cross each other and
// every point is connected with one other point.
unsigned long int countWays(unsigned long int n)
{
   // Throw error if n is odd
   if (n & 1)
   {
      cout << "Invalid";
      return 0;
   }

   // Else return n/2'th Catalan number
   return catalanDP(n/2);
}

// Driver program to test above function
int main()
{
    cout << countWays(6) << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of ways to connect n (where
// n is even) points on a circle
// such that no two connecting
// lines cross each other and
// every point is connected with
// one other point.
import java.io.*;

class GFG
{

// A dynamic programming
// based function to find
// nth Catalan number
static int catalanDP(int n)
{
    // Table to store
    // results of subproblems
    int []catalan = new int [n + 1];

    // Initialize first
    // two values in table
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[]
    // using recursive formula
    for (int i = 2; i <= n; i++)
    {
        catalan[i] = 0;
        for (int j = 0; j < i; j++)
            catalan[i] += catalan[j] *
                          catalan[i - j - 1];
    }

    // Return last entry
    return catalan[n];
}

// Returns count of ways to
// connect n points on a circle
// such that no two connecting
// lines cross each other and
// every point is connected
// with one other point.
static int countWays(int n)
{
    // Throw error if n is odd
    if (n < 1)
    {
        System.out.println("Invalid");
        return 0;
    }

    // Else return n/2'th
    // Catalan number
    return catalanDP(n / 2);
}

// Driver Code
public static void main (String[] args)
{
    System.out.println(countWays(6) + " ");
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to count number
# of ways to connect n (where n
# is even) points on a circle such
# that no two connecting lines
# cross each other and every point
# is connected with one other point.

# A dynamic programming based
# function to find nth Catalan number
def catalanDP(n):

    # Table to store results
    # of subproblems
    catalan = [1 for i in range(n + 1)]

    # Fill entries in catalan[]
    # using recursive formula
    for i in range(2, n + 1):
        catalan[i] = 0
        for j in range(i):
            catalan[i] += (catalan[j] *
                           catalan[i - j - 1])
    # Return last entry
    return catalan[n]

# Returns count of ways to connect
# n points on a circle such that
# no two connecting lines cross
# each other and every point is
# connected with one other point.
def countWays(n):

    # Throw error if n is odd
    if (n & 1):
        print("Invalid")
        return 0

    # Else return n/2'th Catalan number
    return catalanDP(n // 2)

# Driver Code
print(countWays(6))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to count number
// of ways to connect n (where
// n is even) points on a circle
// such that no two connecting
// lines cross each other and
// every point is connected with
// one other point.
using System;

class GFG
{

// A dynamic programming
// based function to find
// nth Catalan number
static int catalanDP(int n)
{
    // Table to store
    // results of subproblems
    int []catalan = new int [n + 1];

    // Initialize first
    // two values in table
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[]
    // using recursive formula
    for (int i = 2; i <= n; i++)
    {
        catalan[i] = 0;
        for (int j = 0; j < i; j++)
            catalan[i] += catalan[j] *
                          catalan[i - j - 1];
    }

    // Return last entry
    return catalan[n];
}

// Returns count of ways to
// connect n points on a circle
// such that no two connecting
// lines cross each other and
// every point is connected
// with one other point.
static int countWays(int n)
{
    // Throw error if n is odd
    if (n < 1)
    {
        Console.WriteLine("Invalid");
        return 0;
    }

    // Else return n/2'th
    // Catalan number
    return catalanDP(n / 2);
}

// Driver Code
static public void Main ()
{
    Console.WriteLine(countWays(6) + " ");
}
}

// This code is contributed
// by M_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// ways to connect n (where n is
// even) points on a circle such
// that no two connecting lines
// cross each other and every
// point is connected with one
// other point.

// A dynamic programming based
// function to find nth Catalan number
function catalanDP($n)
{
    // Table to store results
    // of subproblems Initialize
    // first two values in table
    $catalan[0] = $catalan[1] = 1;

    // Fill entries in catalan[]
    // using recursive formula
    for ($i = 2; $i <= $n; $i++)
    {
        $catalan[$i] = 0;
        for ($j = 0; $j < $i; $j++)
            $catalan[$i] += $catalan[$j] *
                            $catalan[$i - $j - 1];
    }

    // Return last entry
    return $catalan[$n];
}

// Returns count of ways to connect
// n points on a circle such that
// no two connecting lines cross
// each other and every point is
// connected with one other point.
function countWays($n)
{
// Throw error if n is odd
if ($n & 1)
{
    echo "Invalid";
    return 0;
}

// Else return n/2'th
// Catalan number
return catalanDP($n / 2);
}

// Driver Code
echo countWays(6) , " ";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// javascript program to count number of
// ways to connect n (where n is
// even) points on a circle such
// that no two connecting lines
// cross each other and every
// point is connected with one
// other point.

// A dynamic programming based
// function to find nth Catalan number
function catalanDP(n)
{
    // Table to store results
    // of subproblems Initialize
    // first two values in table
    let catalan = []
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[]
    // using recursive formula
    for (let i = 2; i <= n; i++)
    {
        catalan[i] = 0;
        for (let j = 0; j < i; j++)
            catalan[i] += catalan[j] *
                            catalan[i - j - 1];
    }

    // Return last entry
    return catalan[n];
}

// Returns count of ways to connect
// n points on a circle such that
// no two connecting lines cross
// each other and every point is
// connected with one other point.
function countWays(n)
{
// Throw error if n is odd
if (n & 1)
{
    document.write("Invalid");
    return 0;
}

// Else return n/2'th
// Catalan number
return catalanDP(n / 2);
}

// Driver Code
document.write(countWays(6) + " ");

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
5
```

**时间复杂度:**O(n)<sup>2</sup>)
T5】辅助空间: O(n)
本文由 **Shivam Agrawal** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息