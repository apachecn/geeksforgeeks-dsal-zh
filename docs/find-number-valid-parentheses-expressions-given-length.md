# 求给定长度的有效括号表达式的个数

> 原文:[https://www . geesforgeks . org/find-number-valid-括号-表达式-给定长度/](https://www.geeksforgeeks.org/find-number-valid-parentheses-expressions-given-length/)

给定一个数字 n，求该长度的有效括号表达式的数目。
**例:**

```
Input: 2
Output: 1 
There is only possible valid expression of length 2, "()"

Input: 4
Output: 2 
Possible valid expression of length 4 are "(())" and "()()" 

Input: 6
Output: 5
Possible valid expressions are ((())), ()(()), ()()(), (())() and (()())
```

这主要是[加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)的一个应用。如果 n 是偶数，则输入 n 的全部可能有效表达式为第 n/2 个加泰罗尼亚数字，如果 n 是奇数，则为 0。

下面给出的是实现:

## C++

```
// C++ program to find valid paranthesisations of length n
// The majority of code is taken from method 3 of
// https://www.geeksforgeeks.org/program-nth-catalan-number/
#include <bits/stdc++.h>
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
unsigned long int binomialCoeff(unsigned int n,
                                unsigned int k)
{
    unsigned long int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient based function to
// find nth catalan number in O(n) time
unsigned long int catalan(unsigned int n)
{
    // Calculate value of 2nCn
    unsigned long int c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Function to find possible ways to put balanced
// parenthesis in an expression of length n
unsigned long int findWays(unsigned n)
{
    // If n is odd, not possible to
    // create any valid parentheses
    if (n & 1)
        return 0;

    // Otherwise return n/2'th Catalan Number
    return catalan(n / 2);
}

// Driver program to test above functions
int main()
{
    int n = 6;
    cout << "Total possible expressions of length "
         << n << " is " << findWays(6);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find valid paranthesisations of length n
// The majority of code is taken from method 3 of
// https://www.geeksforgeeks.org/program-nth-catalan-number/

class GFG {

    // Returns value of Binomial Coefficient C(n, k)
    static long binomialCoeff(int n, int k)
    {
        long res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
        for (int i = 0; i < k; ++i) {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    // A Binomial coefficient based function to
    // find nth catalan number in O(n) time
    static long catalan(int n)
    {
        // Calculate value of 2nCn
        long c = binomialCoeff(2 * n, n);

        // return 2nCn/(n+1)
        return c / (n + 1);
    }

    // Function to find possible ways to put balanced
    // parenthesis in an expression of length n
    static long findWays(int n)
    {
        // If n is odd, not possible to
        // create any valid parentheses
        if ((n & 1) != 0)
            return 0;

        // Otherwise return n/2'th Catalan Number
        return catalan(n / 2);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        int n = 6;
        System.out.println("Total possible expressions of length " +
                                          n + " is " + findWays(6));
    }
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to find valid
# paranthesisations of length n
# The majority of code is taken
# from method 3 of
# https:#www.geeksforgeeks.org/program-nth-catalan-number/

# Returns value of Binomial
# Coefficient C(n, k)
def binomialCoeff(n, k):
    res = 1;

    # Since C(n, k) = C(n, n-k)
    if (k > n - k):
        k = n - k;

    # Calculate value of [n*(n-1)*---
    # *(n-k+1)] / [k*(k-1)*---*1]
    for i in range(k):
        res *= (n - i);
        res /= (i + 1);

    return int(res);

# A Binomial coefficient based
# function to find nth catalan 
# number in O(n) time
def catalan(n):

    # Calculate value of 2nCn
    c = binomialCoeff(2 * n, n);

    # return 2nCn/(n+1)
    return int(c / (n + 1));

# Function to find possible
# ways to put balanced parenthesis
# in an expression of length n
def findWays(n):

    # If n is odd, not possible to
    # create any valid parentheses
    if(n & 1):
        return 0;

    # Otherwise return n/2'th
    # Catalan Number
    return catalan(int(n / 2));

# Driver Code
n = 6;
print("Total possible expressions of length",
                       n, "is", findWays(6));

# This code is contributed by mits
```

## C#

```
// C# program to find valid paranthesisations
// of length n The majority of code is taken
// from method 3 of
// https://www.geeksforgeeks.org/program-nth-catalan-number/
using System;

class GFG {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static long binomialCoeff(int n, int k)
    {
        long res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of [n*(n-1)*---*
        // (n-k+1)] / [k*(k-1)*---*1]
        for (int i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    // A Binomial coefficient based function to
    // find nth catalan number in O(n) time
    static long catalan(int n)
    {

        // Calculate value of 2nCn
        long c = binomialCoeff(2 * n, n);

        // return 2nCn/(n+1)
        return c / (n + 1);
    }

    // Function to find possible ways to put
    // balanced parenthesis in an expression
    // of length n
    static long findWays(int n)
    {
        // If n is odd, not possible to
        // create any valid parentheses
        if ((n & 1) != 0)
            return 0;

        // Otherwise return n/2'th
        // Catalan Number
        return catalan(n / 2);
    }

    // Driver program to test
    // above functions
    public static void Main()
    {
        int n = 6;
        Console.Write("Total possible expressions"
                       + "of length " + n + " is "
                                   + findWays(6));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find valid
// paranthesisations of length n
// The majority of code is taken
// from method 3 of
// https://www.geeksforgeeks.org/program-nth-catalan-number/

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff($n, $k)
{
    $res = 1;

    // Since C(n, k) = C(n, n-k)
    if ($k > $n - $k)
        $k = $n - $k;

    // Calculate value of [n*(n-1)*---
    // *(n-k+1)] / [k*(k-1)*---*1]
    for ($i = 0; $i < $k; ++$i)
    {
        $res *= ($n - $i);
        $res /= ($i + 1);
    }

    return $res;
}

// A Binomial coefficient
// based function to find
// nth catalan number in
// O(n) time
function catalan($n)
{

    // Calculate value of 2nCn
    $c = binomialCoeff(2 * $n, $n);

    // return 2nCn/(n+1)
    return $c / ($n + 1);
}

// Function to find possible
// ways to put balanced
// parenthesis in an expression
// of length n
function findWays($n)
{

    // If n is odd, not possible to
    // create any valid parentheses
    if ($n & 1)
        return 0;

    // Otherwise return n/2'th
    // Catalan Number
    return catalan($n / 2);
}

    // Driver Code
    $n = 6;
    echo "Total possible expressions of length "
                    , $n , " is " , findWays(6);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript program to find valid
// paranthesisations of length n
// The majority of code is taken
// from method 3 of
// https://www.geeksforgeeks.org/program-nth-catalan-number/

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff(n, k)
{
    let res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of [n*(n-1)*---
    // *(n-k+1)] / [k*(k-1)*---*1]
    for (let i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// A Binomial coefficient
// based function to find
// nth catalan number in
// O(n) time
function catalan(n)
{

    // Calculate value of 2nCn
    let c = binomialCoeff(2 * n, n);

    // return 2nCn/(n+1)
    return c / (n + 1);
}

// Function to find possible
// ways to put balanced
// parenthesis in an expression
// of length n
function findWays(n)
{

    // If n is odd, not possible to
    // create any valid parentheses
    if (n & 1)
        return 0;

    // Otherwise return n/2'th
    // Catalan Number
    return catalan(n / 2);
}

    // Driver Code
    let n = 6;
    document.write("Total possible expressions of length " +
                   n + " is " + findWays(6));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
Total possible expressions of length 6 is 5
```

**时间复杂度:** O(n)

**辅助空间:** O(1)
本文由**萨钦**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息