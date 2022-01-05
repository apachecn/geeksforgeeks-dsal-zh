# 排列球的方式，使得相邻球的类型不同

> 原文:[https://www . geesforgeks . org/排列球的方法-这样相邻的球是不同类型的/](https://www.geeksforgeeks.org/ways-to-arrange-balls-such-that-adjacent-balls-are-of-different-types/)

有 P 型的“P”球、Q 型的“Q”球和 r 型的“r”球。使用这些球，我们希望创建一条直线，使得没有两个相同类型的球相邻。
**例:**

```
Input  : p = 1, q = 1, r = 0
Output : 2
There are only two arrangements PQ and QP

Input  : p = 1, q = 1, r = 1
Output : 6
There are only six arrangements PQR, QPR,
QRP, RQP, PRQ and RPQ

Input  : p = 2, q = 1, r = 1
Output : 6
There are only six arrangements PQRP, QPRP,
PRQP, RPQP, PRPQ and PQPR
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/arrange-balls0052/1)

**天真解:**
这个问题的天真解是递归解。我们递归调用三种情况
1)最后一个放置的球是 P 型
2)最后一个放置的球是 Q 型
3)最后一个放置的球是 R 型
以下是上述思路的实现。

## C++

```
// C++ program to count number of ways to arrange three
// types of balls such that no two balls of same color
// are adjacent to each other
#include<bits/stdc++.h>
using namespace std;

// Returns count of arrangements where last placed ball is
// 'last'.  'last' is 0 for 'p', 1 for 'q' and 2 for 'r'
int countWays(int p, int q, int r, int last)
{
    // if number of balls of any color becomes less
    // than 0 the number of ways arrangements is 0.
    if (p<0 || q<0 || r<0)
        return 0;

    // If last ball required is of type P and the number
    // of balls of P type is 1 while number of balls of
    // other color is 0 the number of ways is 1.
    if (p==1 && q==0 && r==0 && last==0)
        return 1;

    // Same case as above for 'q' and 'r'
    if (p==0 && q==1 && r==0 && last==1)
        return 1;
    if (p==0 && q==0 && r==1 && last==2)
        return 1;

    // if last ball required is P and the number of ways is
    // the sum of number of ways to form sequence with 'p-1' P
    // balls, q Q Balls and r R balls ending with Q and R.
    if (last==0)
        return countWays(p-1,q,r,1) + countWays(p-1,q,r,2);

    // Same as above case for 'q' and 'r'
    if (last==1)
        return countWays(p,q-1,r,0) + countWays(p,q-1,r,2);
    if (last==2)
        return countWays(p,q,r-1,0) + countWays(p,q,r-1,1);
}

// Returns count of required arrangements
int countUtil(int p, int q, int r)
{
   // Three cases arise:
   return countWays(p, q, r, 0) +  // Last required balls is type P
          countWays(p, q, r, 1) +  // Last required balls is type Q
          countWays(p, q, r, 2); // Last required balls is type R
}

// Driver code to test above
int main()
{
    int p = 1, q = 1, r = 1;
    printf("%d", countUtil(p, q, r));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of ways to arrange three types of
// balls such that no two balls of
// same color are adjacent to each other
class GFG {

    // Returns count of arrangements
    // where last placed ball is
    // 'last'. 'last' is 0 for 'p',
    // 1 for 'q' and 2 for 'r'
    static int countWays(int p, int q, int r, int last)
    {
        // if number of balls of any
        // color becomes less than 0
        // the number of ways arrangements is 0.
        if (p < 0 || q < 0 || r < 0)
        return 0;

        // If last ball required is
        // of type P and the number
        // of balls of P type is 1
        // while number of balls of
        // other color is 0 the number
        // of ways is 1.
        if (p == 1 && q == 0 && r == 0 && last == 0)
            return 1;

        // Same case as above for 'q' and 'r'
        if (p == 0 && q == 1 && r == 0 && last == 1)
            return 1;
        if (p == 0 && q == 0 && r == 1 && last == 2)
            return 1;

        // if last ball required is P
        // and the number of ways is
        // the sum of number of ways
        // to form sequence with 'p-1' P
        // balls, q Q Balls and r R balls
        // ending with Q and R.
        if (last == 0)
        return countWays(p - 1, q, r, 1) +
               countWays(p - 1, q, r, 2);

        // Same as above case for 'q' and 'r'
        if (last == 1)
            return countWays(p, q - 1, r, 0) +
                   countWays(p, q - 1, r, 2);

        if (last == 2)
        return countWays(p, q, r - 1, 0) +
               countWays(p, q, r - 1, 1);

        return 0;
    }

    // Returns count of required arrangements
    static int countUtil(int p, int q, int r) {
        // Three cases arise:
        return countWays(p, q, r, 0) + // Last required balls is type P
               countWays(p, q, r, 1) + // Last required balls is type Q
               countWays(p, q, r, 2);  // Last required balls is type R
    }

    // Driver code
    public static void main(String[] args)
    {
        int p = 1, q = 1, r = 1;
        System.out.print(countUtil(p, q, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count
# number of ways to arrange
# three types of balls such 
# that no two balls of same
# color are adjacent to each
# other

# Returns count of arrangements
# where last placed ball is
# 'last'. 'last' is 0 for 'p',
# 1 for 'q' and 2 for 'r'
def countWays(p, q, r, last):

    # if number of balls of
    # any color becomes less
    # than 0 the number of
    # ways arrangements is 0.
    if (p < 0 or q < 0 or r < 0):
        return 0;

    # If last ball required is
    # of type P and the number
    # of balls of P type is 1
    # while number of balls of
    # other color is 0 the number
    # of ways is 1.
    if (p == 1 and q == 0 and
        r == 0 and last == 0):
        return 1;

    # Same case as above
    # for 'q' and 'r'
    if (p == 0 and q == 1 and
        r == 0 and last == 1):
        return 1;

    if (p == 0 and q == 0 and
        r == 1 and last == 2):
        return 1;

    # if last ball required is P
    # and the number of ways is
    # the sum of number of ways
    # to form sequence with 'p-1' P
    # balls, q Q Balls and r R
    # balls ending with Q and R.
    if (last == 0):
        return (countWays(p - 1, q, r, 1) +
                countWays(p - 1, q, r, 2));

    # Same as above case
    # for 'q' and 'r'
    if (last == 1):
        return (countWays(p, q - 1, r, 0) +
                countWays(p, q - 1, r, 2));
    if (last == 2):
        return (countWays(p, q, r - 1, 0) +
                countWays(p, q, r - 1, 1));

# Returns count of
# required arrangements
def countUtil(p, q, r):

    # Three cases arise:
    # Last required balls is type P
    # Last required balls is type Q
    # Last required balls is type R
    return (countWays(p, q, r, 0) +
            countWays(p, q, r, 1) +
            countWays(p, q, r, 2));

# Driver Code
p = 1;
q = 1;
r = 1;
print(countUtil(p, q, r));

# This code is contributed by mits
```

## C#

```
// C# program to count number
// of ways to arrange three types of
// balls such that no two balls of
// same color are adjacent to each other
using System;

class GFG {

    // Returns count of arrangements
    // where last placed ball is
    // 'last'. 'last' is 0 for 'p',
    // 1 for 'q' and 2 for 'r'
    static int countWays(int p, int q,
                            int r, int last)
    {

        // if number of balls of any
        // color becomes less than 0
        // the number of ways
        // arrangements is 0.
        if (p < 0 || q < 0 || r < 0)
            return 0;

        // If last ball required is
        // of type P and the number
        // of balls of P type is 1
        // while number of balls of
        // other color is 0 the number
        // of ways is 1.
        if (p == 1 && q == 0 && r == 0
                              && last == 0)
            return 1;

        // Same case as above for 'q' and 'r'
        if (p == 0 && q == 1 && r == 0
                               && last == 1)
            return 1;
        if (p == 0 && q == 0 && r == 1
                               && last == 2)
            return 1;

        // if last ball required is P
        // and the number of ways is
        // the sum of number of ways
        // to form sequence with 'p-1' P
        // balls, q Q Balls and r R balls
        // ending with Q and R.
        if (last == 0)
            return countWays(p - 1, q, r, 1) +
                    countWays(p - 1, q, r, 2);

        // Same as above case for 'q' and 'r'
        if (last == 1)
            return countWays(p, q - 1, r, 0) +
                countWays(p, q - 1, r, 2);

        if (last == 2)
            return countWays(p, q, r - 1, 0) +
                    countWays(p, q, r - 1, 1);

        return 0;
    }

    // Returns count of required arrangements
    static int countUtil(int p, int q, int r)
    {

        // Three cases arise:
        // 1\. Last required balls is type P
        // 2\. Last required balls is type Q
        // 3\. Last required balls is type R
        return countWays(p, q, r, 0) +
               countWays(p, q, r, 1) +
               countWays(p, q, r, 2);
    }

    // Driver code
    public static void Main()
    {
        int p = 1, q = 1, r = 1;

        Console.Write(countUtil(p, q, r));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to arrange three
// types of balls such that
// no two balls of same color
// are adjacent to each other

// Returns count of arrangements
// where last placed ball is
// 'last'. 'last' is 0 for 'p',
// 1 for 'q' and 2 for 'r'
function countWays($p, $q,
                   $r, $last)
{

    // if number of balls of
    // any color becomes less
    // than 0 the number of
    // ways arrangements is 0.
    if ($p < 0 || $q
           < 0 || $r < 0)
        return 0;

    // If last ball required is
    // of type P and the number
    // of balls of P type is 1
    // while number of balls of
    // other color is 0 the number
    // of ways is 1.
    if ($p == 1 && $q == 0 &&
        $r == 0 && $last == 0)
        return 1;

    // Same case as above
    // for 'q' and 'r'
    if ($p == 0 && $q == 1 &&
        $r == 0 && $last == 1)
        return 1;

    if ($p == 0 && $q == 0 &&
        $r == 1 && $last == 2)
        return 1;

    // if last ball required is P
    // and the number of ways is
    // the sum of number of ways
    // to form sequence with 'p-1' P
    // balls, q Q Balls and r R
    // balls ending with Q and R.
    if ($last == 0)
        return countWays($p - 1, $q, $r, 1) +
               countWays($p - 1, $q, $r, 2);

    // Same as above case
    // for 'q' and 'r'
    if ($last == 1)
        return countWays($p, $q - 1, $r, 0) +
               countWays($p, $q - 1, $r, 2);
    if ($last == 2)
        return countWays($p, $q, $r - 1, 0) +
               countWays($p, $q, $r - 1, 1);
}

// Returns count of
// required arrangements
function countUtil($p, $q, $r)
{

    // Three cases arise:
    // Last required balls is type P
    // Last required balls is type Q
    // Last required balls is type R
    return countWays($p, $q, $r, 0) +
           countWays($p, $q, $r, 1) +
           countWays($p, $q, $r, 2);
}

    // Driver Code
    $p = 1;
    $q = 1;
    $r = 1;
    echo(countUtil($p, $q, $r));

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count number
// of ways to arrange three
// types of balls such that no
// two balls of same color
// are adjacent to each other

    // Returns count of arrangements
    // where last placed ball is
    // 'last'. 'last' is 0 for 'p',
    // 1 for 'q' and 2 for 'r'
    function countWays(p, q, r, last)
    {

        // if number of balls of any
        // color becomes less than 0
        // the number of ways arrangements is 0.
        if (p < 0 || q < 0 || r < 0)
        return 0;

        // If last ball required is
        // of type P and the number
        // of balls of P type is 1
        // while number of balls of
        // other color is 0 the number
        // of ways is 1.
        if (p == 1 && q == 0 && r == 0 && last == 0)
            return 1;

        // Same case as above for 'q' and 'r'
        if (p == 0 && q == 1 && r == 0 && last == 1)
            return 1;
        if (p == 0 && q == 0 && r == 1 && last == 2)
            return 1;

        // if last ball required is P
        // and the number of ways is
        // the sum of number of ways
        // to form sequence with 'p-1' P
        // balls, q Q Balls and r R balls
        // ending with Q and R.
        if (last == 0)
        return countWays(p - 1, q, r, 1) +
               countWays(p - 1, q, r, 2);

        // Same as above case for 'q' and 'r'
        if (last == 1)
            return countWays(p, q - 1, r, 0) +
                   countWays(p, q - 1, r, 2);

        if (last == 2)
        return countWays(p, q, r - 1, 0) +
               countWays(p, q, r - 1, 1);

        return 0;
    }

    // Returns count of required arrangements
    function countUtil(p, q, r)
    {

        // Three cases arise:
        return countWays(p, q, r, 0) + // Last required balls is type P
               countWays(p, q, r, 1) + // Last required balls is type Q
               countWays(p, q, r, 2);  // Last required balls is type R
    }

// Driver Code

        let p = 1, q = 1, r = 1;
        document.write(countUtil(p, q, r));

    // This code is contributed by target_2.
</script>
```

**输出:**

```
6
```

该解决方案的时间复杂度是指数级的。
我们可以观察到有很多子问题被一次又一次地解决，所以这个问题可以用动态规划(DP)来解决。我们可以很容易地解决这个问题。

## C++

```
// C++ program to count number of ways to arrange three
// types of balls such that no two balls of same color
// are adjacent to each other
#include<bits/stdc++.h>
using namespace std;
#define MAX 100

// table to store to store results of subproblems
int dp[MAX][MAX][MAX][3];

// Returns count of arrangements where last placed ball is
// 'last'.  'last' is 0 for 'p', 1 for 'q' and 2 for 'r'
int countWays(int p, int q, int r, int last)
{
    // if number of balls of any color becomes less
    // than 0 the number of ways arrangements is 0.
    if (p<0 || q<0 || r<0)
        return 0;

    // If last ball required is of type P and the number
    // of balls of P type is 1 while number of balls of
    // other color is 0 the number of ways is 1.
    if (p==1 && q==0 && r==0 && last==0)
        return 1;

    // Same case as above for 'q' and 'r'
    if (p==0 && q==1 && r==0 && last==1)
        return 1;
    if (p==0 && q==0 && r==1 && last==2)
        return 1;

    // If this subproblem is already evaluated
    if (dp[p][q][r][last] != -1)
        return dp[p][q][r][last];

    // if last ball required is P and the number of ways is
    // the sum of number of ways to form sequence with 'p-1' P
    // balls, q Q Balls and r R balls ending with Q and R.
    if (last==0)
       dp[p][q][r][last] = countWays(p-1,q,r,1) + countWays(p-1,q,r,2);

    // Same as above case for 'q' and 'r'
    else if (last==1)
       dp[p][q][r][last] = countWays(p,q-1,r,0) + countWays(p,q-1,r,2);
    else //(last==2)
       dp[p][q][r][last] =  countWays(p,q,r-1,0) + countWays(p,q,r-1,1);

    return dp[p][q][r][last];
}

// Returns count of required arrangements
int countUtil(int p, int q, int r)
{
   // Initialize 'dp' array
   memset(dp, -1, sizeof(dp));

   // Three cases arise:
   return countWays(p, q, r, 0) +  // Last required balls is type P
          countWays(p, q, r, 1) +  // Last required balls is type Q
          countWays(p, q, r, 2); // Last required balls is type R
}

// Driver code to test above
int main()
{
    int p = 1, q = 1, r = 1;
    printf("%d", countUtil(p, q, r));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of ways to arrange three
// types of balls such that no
// two balls of same color
// are adjacent to each other
import java.util.Arrays;

class GFG
{

    static final int MAX = 100;

    // table to store to store results of subproblems
    static int dp[][][][] = new int[MAX][MAX][MAX][3];

    // Returns count of arrangements
    // where last placed ball is
    // 'last'. 'last' is 0 for 'p',
    // 1 for 'q' and 2 for 'r'
    static int countWays(int p, int q, int r, int last)
    {
        // if number of balls of any
        // color becomes less than 0
        // the number of ways arrangements is 0.
        if (p < 0 || q < 0 || r < 0)
        return 0;

        // If last ball required is
        // of type P and the number
        // of balls of P type is 1
        // while number of balls of
        // other color is 0 the number
        // of ways is 1.
        if (p == 1 && q == 0 && r == 0 && last == 0)
            return 1;

        // Same case as above for 'q' and 'r'
        if (p == 0 && q == 1 && r == 0 && last == 1)
            return 1;

        if (p == 0 && q == 0 && r == 1 && last == 2)
            return 1;

        // If this subproblem is already evaluated
        if (dp[p][q][r][last] != -1)
            return dp[p][q][r][last];

        // if last ball required is P and
        // the number of ways is the sum
        // of number of ways to form sequence
        // with 'p-1' P balls, q Q balss and
        // r R balls ending with Q and R.
        if (last == 0)
        dp[p][q][r][last] = countWays(p - 1, q, r, 1) +
                            countWays(p - 1, q, r, 2);

        // Same as above case for 'q' and 'r'
        else if (last == 1)
        dp[p][q][r][last] = countWays(p, q - 1, r, 0) +
                            countWays(p, q - 1, r, 2);
        //(last==2)
        else
        dp[p][q][r][last] = countWays(p, q, r - 1, 0) +
                            countWays(p, q, r - 1, 1);

        return dp[p][q][r][last];
    }

    // Returns count of required arrangements
    static int countUtil(int p, int q, int r)
    {
        // Initialize 'dp' array
        for (int[][][] row : dp)
        {
            for (int[][] innerRow : row)
            {
                for (int[] innerInnerRow : innerRow)
                {
                    Arrays.fill(innerInnerRow, -1);
                }
            }
        };

        // Three cases arise:
        return countWays(p, q, r, 0) + // Last required balls is type P
            countWays(p, q, r, 1) +    // Last required balls is type Q
            countWays(p, q, r, 2);       // Last required balls is type R
    }

    // Driver code
    public static void main(String[] args)
    {
        int p = 1, q = 1, r = 1;
        System.out.print(countUtil(p, q, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count number
// of ways to arrange three
// types of balls such that no
// two balls of same color
// are adjacent to each other
using System;

class GFG
{

    static int MAX = 101;

    // table to store to store results of subproblems
    static int[,,,] dp = new int[MAX, MAX, MAX, 4];

    // Returns count of arrangements
    // where last placed ball is
    // 'last'. 'last' is 0 for 'p',
    // 1 for 'q' and 2 for 'r'
    static int countWays(int p, int q, int r, int last)
    {
        // if number of balls of any
        // color becomes less than 0
        // the number of ways arrangements is 0.
        if (p < 0 || q < 0 || r < 0)
        return 0;

        // If last ball required is
        // of type P and the number
        // of balls of P type is 1
        // while number of balls of
        // other color is 0 the number
        // of ways is 1.
        if (p == 1 && q == 0 && r == 0 && last == 0)
            return 1;

        // Same case as above for 'q' and 'r'
        if (p == 0 && q == 1 && r == 0 && last == 1)
            return 1;

        if (p == 0 && q == 0 && r == 1 && last == 2)
            return 1;

        // If this subproblem is already evaluated
        if (dp[p, q, r, last] != -1)
            return dp[p, q, r, last];

        // if last ball required is P and
        // the number of ways is the sum
        // of number of ways to form sequence
        // with 'p-1' P balls, q Q balss and
        // r R balls ending with Q and R.
        if (last == 0)
        dp[p, q, r, last] = countWays(p - 1, q, r, 1) +
                            countWays(p - 1, q, r, 2);

        // Same as above case for 'q' and 'r'
        else if (last == 1)
        dp[p, q, r, last] = countWays(p, q - 1, r, 0) +
                            countWays(p, q - 1, r, 2);
        //(last==2)
        else
        dp[p, q, r, last] = countWays(p, q, r - 1, 0) +
                            countWays(p, q, r - 1, 1);

        return dp[p, q, r, last];
    }

    // Returns count of required arrangements
    static int countUtil(int p, int q, int r)
    {
        // Initialize 'dp' array
        for(int i = 0; i < MAX; i++)
        for(int j = 0; j < MAX; j++)
        for(int k = 0; k < MAX; k++)
        for(int l = 0; l < 4; l++)
        dp[i, j, k, l] = -1;

        // Three cases arise:
        return countWays(p, q, r, 0) + // Last required balls is type P
            countWays(p, q, r, 1) + // Last required balls is type Q
            countWays(p, q, r, 2); // Last required balls is type R
    }

    // Driver code
    static void Main()
    {
        int p = 1, q = 1, r = 1;
        Console.WriteLine(countUtil(p, q, r));
    }
}

// This code is contributed by mits.
```

## 蟒蛇 3

```
# Python3 program to count number of ways to
# arrange three types of balls such that no
# two balls of same color are adjacent to each other
MAX = 100;

# table to store to store results of subproblems
dp = [[[[-1] * 4 for i in range(MAX)]
                 for j in range(MAX)]
                 for k in range(MAX)];

# Returns count of arrangements where last
# placed ball is 'last'. 'last' is 0 for 'p',
# 1 for 'q' and 2 for 'r'
def countWays(p, q, r, last):

    # if number of balls of any color becomes less
    # than 0 the number of ways arrangements is 0.
    if (p < 0 or q < 0 or r < 0):
        return 0;

    # If last ball required is of type P and the
    # number of balls of P type is 1 while number
    # of balls of other color is 0 the number of
    # ways is 1.
    if (p == 1 and q == 0 and
        r == 0 and last == 0):
        return 1;

    # Same case as above for 'q' and 'r'
    if (p == 0 and q == 1 and
        r == 0 and last == 1):
        return 1;
    if (p == 0 and q == 0 and
        r == 1 and last == 2):
        return 1;

    # If this subproblem is already evaluated
    if (dp[p][q][r][last] != -1):
        return dp[p][q][r][last];

    # if last ball required is P and the number
    # of ways is the sum of number of ways to 
    # form sequence with 'p-1' P balls, q Q Balls
    # and r R balls ending with Q and R.
    if (last == 0):
        dp[p][q][r][last] = (countWays(p - 1, q, r, 1) +
                             countWays(p - 1, q, r, 2));

    # Same as above case for 'q' and 'r'
    elif (last == 1):
        dp[p][q][r][last] = (countWays(p, q - 1, r, 0) +
                             countWays(p, q - 1, r, 2));
    else:

        #(last==2)
        dp[p][q][r][last] = (countWays(p, q, r - 1, 0) +
                             countWays(p, q, r - 1, 1));

    return dp[p][q][r][last];

# Returns count of required arrangements
def countUtil(p, q, r):

    # Three cases arise:
    # Last required balls is type P
    # Last required balls is type Q
    # Last required balls is type R
    return (countWays(p, q, r, 0) +
            countWays(p, q, r, 1) +
            countWays(p, q, r, 2));

# Driver Code
p, q, r = 1, 1, 1;
print(countUtil(p, q, r));

# This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of ways to
// arrange three types of balls such that
// no two balls of same color are adjacent
// to each other
$MAX = 100;

// table to store to store results of subproblems
$dp = array_fill(0, $MAX, array_fill(0, $MAX,
      array_fill(0, $MAX, array_fill(0, 3, -1))));

// Returns count of arrangements where last
// placed ball is 'last'. 'last' is 0 for 'p',
// 1 for 'q' and 2 for 'r'
function countWays($p, $q, $r, $last)
{
    global $dp;

    // if number of balls of any color becomes less
    // than 0 the number of ways arrangements is 0.
    if ($p < 0 || $q < 0 || $r < 0)
        return 0;

    // If last ball required is of type P and the
    // number of balls of P type is 1 while number
    // of balls of other color is 0 the number of
    // ways is 1.
    if ($p == 1 && $q == 0 && $r == 0 && $last == 0)
        return 1;

    // Same case as above for 'q' and 'r'
    if ($p == 0 && $q == 1 && $r == 0 && $last == 1)
        return 1;
    if ($p == 0 && $q == 0 && $r == 1 && $last == 2)
        return 1;

    // If this subproblem is already evaluated
    if ($dp[$p][$q][$r][$last] != -1)
        return $dp[$p][$q][$r][$last];

    // if last ball required is P and the number of
    // ways is the sum of number of ways to form
    // sequence with 'p-1' P balls, q Q Balls and r
    // R balls ending with Q and R.
    if ($last == 0)
    $dp[$p][$q][$r][$last] = countWays($p - 1, $q, $r, 1) +
                             countWays($p - 1, $q, $r, 2);

    // Same as above case for 'q' and 'r'
    else if ($last == 1)
    $dp[$p][$q][$r][$last] = countWays($p, $q - 1, $r, 0) +
                             countWays($p, $q - 1, $r, 2);
    else //(last==2)
    $dp[$p][$q][$r][$last] = countWays($p, $q, $r - 1, 0) +
                             countWays($p, $q, $r - 1, 1);

    return $dp[$p][$q][$r][$last];
}

// Returns count of required arrangements
function countUtil($p, $q, $r)
{

// Three cases arise:
return countWays($p, $q, $r, 0) + // Last required balls is type P
       countWays($p, $q, $r, 1) + // Last required balls is type Q
       countWays($p, $q, $r, 2); // Last required balls is type R
}

// Driver code
$p = 1;
$q = 1;
$r = 1;
print(countUtil($p, $q, $r));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to count number
// of ways to arrange three
// types of balls such that no
// two balls of same color
// are adjacent to each other

var MAX = 100;

// table to store to store results of subproblems
var dp = Array(MAX).fill(-1).map(x =>
Array(MAX).fill(-1).map(x =>
Array(MAX).fill(-1).map(x => Array(3).fill(-1))));

// Returns count of arrangements
// where last placed ball is
// 'last'. 'last' is 0 for 'p',
// 1 for 'q' and 2 for 'r'
function countWays( p , q , r , last)
{
    // if number of balls of any
    // color becomes less than 0
    // the number of ways arrangements is 0.
    if (p < 0 || q < 0 || r < 0)
    return 0;

    // If last ball required is
    // of type P and the number
    // of balls of P type is 1
    // while number of balls of
    // other color is 0 the number
    // of ways is 1.
    if (p == 1 && q == 0 && r == 0 && last == 0)
        return 1;

    // Same case as above for 'q' and 'r'
    if (p == 0 && q == 1 && r == 0 && last == 1)
        return 1;

    if (p == 0 && q == 0 && r == 1 && last == 2)
        return 1;

    // If this subproblem is already evaluated
    if (dp[p][q][r][last] != -1)
        return dp[p][q][r][last];

    // if last ball required is P and
    // the number of ways is the sum
    // of number of ways to form sequence
    // with 'p-1' P balls, q Q balss and
    // r R balls ending with Q and R.
    if (last == 0)
    dp[p][q][r][last] = countWays(p - 1, q, r, 1) +
                        countWays(p - 1, q, r, 2);

    // Same as above case for 'q' and 'r'
    else if (last == 1)
    dp[p][q][r][last] = countWays(p, q - 1, r, 0) +
                        countWays(p, q - 1, r, 2);
    //(last==2)
    else
    dp[p][q][r][last] = countWays(p, q, r - 1, 0) +
                        countWays(p, q, r - 1, 1);

    return dp[p][q][r][last];
}

// Returns count of required arrangements
function countUtil(p , q , r)
{

    // Three cases arise:
    return countWays(p, q, r, 0) + // Last required balls is type P
        countWays(p, q, r, 1) +    // Last required balls is type Q
        countWays(p, q, r, 2);       // Last required balls is type R
}

// Driver code
var p = 1, q = 1, r = 1;
document.write(countUtil(p, q, r));

// This code contributed by Princi Singh
</script>
```

**输出:**

```
6
```

**时间复杂度:**O(p * q * r)
T3】辅助空间: O(p*q*r*3)
本文由 **Bhavuk Chawla** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。