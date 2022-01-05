# 长度为 N 的二进制串的数量，具有 K 个相邻的设置位

> 原文:[https://www . geeksforgeeks . org/长度为 n 的二进制字符串的数量与 k 个相邻集位/](https://www.geeksforgeeks.org/number-of-binary-strings-of-length-n-with-k-adjacent-set-bits/)

给定![n        ](img/ef54a958fbcc183986eba32074828428.png "Rendered by QuickLaTeX.com")和![k        ](img/51813d50bcfc61c0a6e8719c007c734d.png "Rendered by QuickLaTeX.com")。任务是从 2 个 <sup>n 个</sup>中找出长度为 **n 个**的二进制串的数量，使得它们满足 f(位串)= k。
其中，

```
f(x) = Number of times a set bit is adjacent to 
       another set bit in a binary string x.

For Example:
f(011101101) = 3
f(010100000) = 0
f(111111111) = 8
```

**示例** :

```
Input : n = 5, k = 2
Output : 6
Explanation
There are 6 ways to form bit strings of length 5 
such that f(bit string s) = 2,
These possible strings are:-
00111, 01110, 10111, 11011, 11100, 11101
```

**方法 1(蛮力):**最简单的方法是递归地解决问题，通过传递当前索引，f(位串)的值形成直到当前索引，我们放置在二进制串中的最后一位形成直到(当前索引–1)。如果我们达到的指数是**当前指数= n** 和 **f(位串)= k** 的值，那么我们以这种方式计数，否则我们不会。
下面是蛮力方法的实现:

## C++

```
// C++ program to find the number of Bit Strings
// of length N with K adjacent set bits

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
int waysToKAdjacentSetBits(int n, int k, int currentIndex,
                           int adjacentSetBits, int lastBit)
{

    /* Base Case when we form bit string of length n */
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    int noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                              adjacentSetBits + 1, 1);
        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k,currentIndex + 1,
                                                 adjacentSetBits, 0);
    }
    else if (!lastBit) {
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 1);
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                 adjacentSetBits, 0);
    }

    return noOfWays;
}

// Driver Code
int main()
{
    int n = 5, k = 2;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(n, k, 1, 0, 0);

    cout << "Number of ways = " << totalWays << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of Bit Strings
// of length N with K adjacent set bits

import java.util.*;

class solution
{

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
static int waysToKAdjacentSetBits(int n, int k, int currentIndex,
                        int adjacentSetBits, int lastBit)
{

    // Base Case when we form bit string of length n
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    int noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                            adjacentSetBits + 1, 1);
        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k,currentIndex + 1,
                                                adjacentSetBits, 0);
    }
    else if (lastBit == 0) {
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 1);
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 0);
    }

    return noOfWays;
}

// Driver Code
public static void main(String args[])
{
    int n = 5, k = 2;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(n, k, 1, 0, 0);

    System.out.println("Number of ways = "+totalWays);

}
}

//This code is contributed by
// Surendra _Gangwar
```

## 蟒蛇 3

```
# Python 3 program to find the number of Bit
# Strings of length N with K adjacent set bits

# Function to find the number of Bit Strings
# of length N with K adjacent set bits
def waysToKAdjacentSetBits(n, k, currentIndex,
                           adjacentSetBits, lastBit):

    # Base Case when we form bit string of length n
    if (currentIndex == n):

        # if f(bit string) = k, count this way
        if (adjacentSetBits == k):
            return 1;
        return 0

    noOfWays = 0

    # Check if the last bit was set, if it was set
    # then call for next index by incrementing the
    # adjacent bit count else just call the next
    # index with same value of adjacent bit count
    # and either set the bit at current index or
    # let it remain unset
    if (lastBit == 1):

        # set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                           adjacentSetBits + 1, 1);
        # unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k,currentIndex + 1,
                                           adjacentSetBits, 0);

    elif (lastBit != 1):
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                               adjacentSetBits, 1);
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                               adjacentSetBits, 0);

    return noOfWays;

# Driver Code
n = 5; k = 2;

# total ways = (ways by placing 1st bit as 1 +
#                ways by placing 1st bit as 0)
totalWays = (waysToKAdjacentSetBits(n, k, 1, 0, 1) +
             waysToKAdjacentSetBits(n, k, 1, 0, 0));

print("Number of ways =", totalWays);

# This code is contributed by Akanksha Rai
```

## C#

```
// C# program to find the number of Bit Strings
// of length N with K adjacent set bits
using System;

class GFG
{
// Function to find the number of Bit Strings
// of length N with K adjacent set bits
static int waysToKAdjacentSetBits(int n, int k, int currentIndex,
                                  int adjacentSetBits, int lastBit)
{

    /* Base Case when we form bit
    string of length n */
    if (currentIndex == n)
    {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    int noOfWays = 0;

    /* Check if the last bit was set, if it was
    set then call for next index by incrementing
    the adjacent bit count else just call the next
    index with same value of adjacent bit count and
    either set the bit at current index or let it
    remain unset */
    if (lastBit == 1)
    {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                            adjacentSetBits + 1, 1);
        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k,currentIndex + 1,
                                                adjacentSetBits, 0);
    }
    else if (lastBit != 1)
    {
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 1);
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 0);
    }

    return noOfWays;
}

// Driver Code
public static void Main()
{
    int n = 5, k = 2;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(n, k, 1, 0, 1) +
                    waysToKAdjacentSetBits(n, k, 1, 0, 0);

    Console.WriteLine("Number of ways = " + totalWays);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the number of
// Bit Strings of length N with K
// adjacent set bits

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
function waysToKAdjacentSetBits($n, $k, $currentIndex,
                           $adjacentSetBits, $lastBit)
{

    /* Base Case when we form bit
       string of length n */
    if ($currentIndex == $n)
    {

        // if f(bit string) = k, count this way
        if ($adjacentSetBits == $k)
            return 1;
        return 0;
    }

    $noOfWays = 0;

    /* Check if the last bit was set, if it
    was set then call for next index by
    incrementing the adjacent bit count else
    just call the next index with same value
    of adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if ($lastBit == 1)
    {
        // set the bit at currentIndex
        $noOfWays += waysToKAdjacentSetBits($n, $k, $currentIndex + 1,
                                            $adjacentSetBits + 1, 1);
        // unset the bit at currentIndex
        $noOfWays += waysToKAdjacentSetBits($n, $k,$currentIndex + 1,
                                                $adjacentSetBits, 0);
    }
    else if (!$lastBit)
    {
        $noOfWays += waysToKAdjacentSetBits($n, $k, $currentIndex + 1,
                                                $adjacentSetBits, 1);
        $noOfWays += waysToKAdjacentSetBits($n, $k, $currentIndex + 1,
                                                $adjacentSetBits, 0);
    }

    return $noOfWays;
}

// Driver Code
$n = 5;
$k = 2;

/* total ways = (ways by placing 1st bit as 1 +
                ways by placing 1st bit as 0) */
$totalWays = waysToKAdjacentSetBits($n, $k, 1, 0, 1) +
             waysToKAdjacentSetBits($n, $k, 1, 0, 0);

echo "Number of ways = ", $totalWays, "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find the number of Bit Strings
// of length N with K adjacent set bits

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
function waysToKAdjacentSetBits(n, k, currentIndex,
                           adjacentSetBits, lastBit)
{

    /* Base Case when we form bit string of length n */
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    let noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                              adjacentSetBits + 1, 1);
        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(n, k,currentIndex + 1,
                                                 adjacentSetBits, 0);
    }
    else if (!lastBit) {
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                adjacentSetBits, 1);
        noOfWays += waysToKAdjacentSetBits(n, k, currentIndex + 1,
                                                 adjacentSetBits, 0);
    }

    return noOfWays;
}

// Driver Code
    let n = 5, k = 2;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    let totalWays = waysToKAdjacentSetBits(n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(n, k, 1, 0, 0);

    document.write("Number of ways = " + totalWays);

</script>
```

**Output:** 

```
Number of ways = 6
```

**方法 2(高效):**在方法 1 中，有重叠的子问题需要移除，对此我们可以应用动态规划(memoicing)。
为了优化方法 1，我们可以将记忆应用于上述递归解，例如，

```
DP[i][j][k] = Number of  ways to form bit string of length i with 
              f(bit string till i) = j where the last bit is k,
              which can be 0 or 1 depending on whether the
              last bit was set or not
```

下面是高效方法的实现:

## C++

```
// C++ program to find the number of Bit Strings
// of length N with K adjacent set bits

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
int waysToKAdjacentSetBits(int dp[][MAX][2], int n, int k,
                           int currentIndex, int adjacentSetBits, int lastBit)
{
    /* Base Case when we form bit
       string of length n */
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    if (dp[currentIndex][adjacentSetBits][lastBit] != -1) {

        return dp[currentIndex][adjacentSetBits][lastBit];
    }

    int noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                 adjacentSetBits + 1, 1);

        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                    adjacentSetBits, 0);
    }

    else if (!lastBit) {
        noOfWays += waysToKAdjacentSetBits(dp, n, k,  currentIndex + 1,
                                                     adjacentSetBits, 1);

        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                   adjacentSetBits, 0);
    }

    dp[currentIndex][adjacentSetBits][lastBit] = noOfWays;

    return noOfWays;
}

// Driver Code
int main()
{
    int n = 5, k = 2;

    /* dp[i][j][k] represents bit strings of length i
    with f(bit string) = j and last bit as k */
    int dp[MAX][MAX][2];
    memset(dp, -1, sizeof(dp));

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(dp, n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(dp, n, k, 1, 0, 0);

    cout << "Number of ways = " << totalWays << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of Bit Strings
// of length N with K adjacent set bits
class solution
{

static final int  MAX=1000;

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
static int waysToKAdjacentSetBits(int dp[][][], int n, int k,
                           int currentIndex, int adjacentSetBits, int lastBit)
{
    /* Base Case when we form bit
       string of length n */
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    if (dp[currentIndex][adjacentSetBits][lastBit] != -1) {

        return dp[currentIndex][adjacentSetBits][lastBit];
    }

    int noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                 adjacentSetBits + 1, 1);

        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                    adjacentSetBits, 0);
    }

    else if (lastBit==0) {
        noOfWays += waysToKAdjacentSetBits(dp, n, k,  currentIndex + 1,
                                                     adjacentSetBits, 1);

        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1,
                                                   adjacentSetBits, 0);
    }

    dp[currentIndex][adjacentSetBits][lastBit] = noOfWays;

    return noOfWays;
}

// Driver Code
public static void main(String args[])
{
    int n = 5, k = 2;

    /* dp[i][j][k] represents bit strings of length i
    with f(bit string) = j and last bit as k */
    int dp[][][]= new int[MAX][MAX][2];

    //initialize the dp
    for(int i=0;i<MAX;i++)
        for(int j=0;j<MAX;j++)
            for(int k1=0;k1<2;k1++)
            dp[i][j][k1]=-1;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(dp, n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(dp, n, k, 1, 0, 0);

    System.out.print( "Number of ways = " + totalWays + "\n");
}
}
```

## 蟒蛇 3

```
# Python3 program to find the number of Bit Strings
# of length N with K adjacent set bits

MAX = 1000

# Function to find the number of Bit Strings
# of length N with K adjacent set bits
def waysToKAdjacentSetBits(dp, n, k, currentIndex, adjacentSetBits, lastBit):
    """ Base Case when we form bit
       string of length n """
    if currentIndex == n:
        # if f(bit string) = k, count this way
        if adjacentSetBits == k:
            return 1
        return 0

    if dp[currentIndex][adjacentSetBits][lastBit] != -1:
        return dp[currentIndex][adjacentSetBits][lastBit]

    noOfWays = 0

    """ Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset """

    if lastBit == 1:
        # set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1, adjacentSetBits + 1, 1)

        # unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1, adjacentSetBits, 0)

    elif not lastBit:
        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1, adjacentSetBits, 1)

        noOfWays += waysToKAdjacentSetBits(dp, n, k, currentIndex + 1, adjacentSetBits, 0)

    dp[currentIndex][adjacentSetBits][lastBit] = noOfWays

    return noOfWays

n, k = 5, 2

""" dp[i][j][k] represents bit strings of length i
with f(bit string) = j and last bit as k """
dp = [[[-1 for i in range(2)] for i in range(MAX)] for j in range(MAX)]
""" total ways = (ways by placing 1st bit as 1 +
                ways by placing 1st bit as 0) """
totalWays = waysToKAdjacentSetBits(dp, n, k, 1, 0, 1) + waysToKAdjacentSetBits(dp, n, k, 1, 0, 0)
print( "Number of ways =", totalWays)

# This code is contributed by decode2207.
```

## C#

```
using System;

// C# program to find the number
// of Bit Strings of length N
// with K adjacent set bits
class GFG
{

static readonly int MAX=1000;

// Function to find the number
// of Bit Strings of length N
// with K adjacent set bits
static int waysToKAdjacentSetBits(int [,,]dp,
                            int n, int k,
                            int currentIndex,
                            int adjacentSetBits,
                            int lastBit)
{
    /* Base Case when we form bit
    string of length n */
    if (currentIndex == n)
    {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    if (dp[currentIndex, adjacentSetBits,
                            lastBit] != -1)
    {

        return dp[currentIndex,
        adjacentSetBits, lastBit];
    }

    int noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1)
    {

        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n,
                                k, currentIndex + 1,
                                adjacentSetBits + 1, 1);

        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n,
                                k, currentIndex + 1,
                                adjacentSetBits, 0);
    }

    else if (lastBit==0)
    {
        noOfWays += waysToKAdjacentSetBits(dp,
                                n, k, currentIndex + 1,
                                adjacentSetBits, 1);

        noOfWays += waysToKAdjacentSetBits(dp,
                                n, k, currentIndex + 1,
                                adjacentSetBits, 0);
    }

    dp[currentIndex,adjacentSetBits,lastBit] = noOfWays;

    return noOfWays;
}

// Driver Code
public static void Main(String []args)
{
    int n = 5, k = 2;

    /* dp[i,j,k] represents bit strings
    of length i with f(bit string) = j
    and last bit as k */
    int [,,]dp = new int[MAX, MAX, 2];

    // initialize the dp
    for(int i = 0; i < MAX; i++)
        for(int j = 0; j < MAX; j++)
            for(int k1 = 0; k1 < 2; k1++)
                dp[i, j, k1]=-1;

    /* total ways = (ways by placing 1st bit as 1 +
                    ways by placing 1st bit as 0) */
    int totalWays = waysToKAdjacentSetBits(dp, n, k, 1, 0, 1)
                    + waysToKAdjacentSetBits(dp, n, k, 1, 0, 0);

    Console.Write( "Number of ways = " + totalWays + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the number of Bit Strings
// of length N with K adjacent set bits

var MAX = 1000;

// Function to find the number of Bit Strings
// of length N with K adjacent set bits
function waysToKAdjacentSetBits(dp, n, k,
currentIndex, adjacentSetBits, lastBit)
{
    /* Base Case when we form bit
       string of length n */
    if (currentIndex == n) {

        // if f(bit string) = k, count this way
        if (adjacentSetBits == k)
            return 1;
        return 0;
    }

    if (dp[currentIndex][adjacentSetBits][lastBit] != -1) {

        return dp[currentIndex][adjacentSetBits][lastBit];
    }

    var noOfWays = 0;

    /* Check if the last bit was set,
    if it was set then call for
    next index by incrementing the
    adjacent bit count else just call
    the next index with same value of
    adjacent bit count and either set the
    bit at current index or let it remain
    unset */

    if (lastBit == 1) {
        // set the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k,
        currentIndex + 1, adjacentSetBits + 1, 1);

        // unset the bit at currentIndex
        noOfWays += waysToKAdjacentSetBits(dp, n, k,
        currentIndex + 1, adjacentSetBits, 0);
    }

    else if (!lastBit) {
        noOfWays += waysToKAdjacentSetBits(dp, n, k, 
        currentIndex + 1, adjacentSetBits, 1);

        noOfWays += waysToKAdjacentSetBits(dp, n, k,
        currentIndex + 1, adjacentSetBits, 0);
    }

    dp[currentIndex][adjacentSetBits][lastBit] = noOfWays;

    return noOfWays;
}

// Driver Code

var n = 5, k = 2;

/* dp[i][j][k] represents bit strings of length i
with f(bit string) = j and last bit as k */
var dp = Array.from(Array(MAX), ()=>Array(MAX));
for(var i =0; i<MAX; i++)
        for(var j =0; j<MAX; j++)
            dp[i][j] = new Array(2).fill(-1);
/* total ways = (ways by placing 1st bit as 1 +
                ways by placing 1st bit as 0) */
var totalWays = waysToKAdjacentSetBits(dp, n, k, 1, 0, 1)
                + waysToKAdjacentSetBits(dp, n, k, 1, 0, 0);
document.write( "Number of ways = " + totalWays + "<br>");

</script>
```

**Output:** 

```
Number of ways = 6
```