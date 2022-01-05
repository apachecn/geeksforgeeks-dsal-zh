# 斯特拉八角琴号

> 原文:[https://www.geeksforgeeks.org/stella-octangula-number/](https://www.geeksforgeeks.org/stella-octangula-number/)

给定一个数字 n，检查它是 [**还是**号。形式为![n(2n^{2} - 1)    ](img/8e32b8988925458df411559267ae8e12.png "Rendered by QuickLaTeX.com")的数，其中 n 是一个整数(0，1，2，3，4，…)叫做 Stella Octangula。前几个 Stella Octangula 数字是 0、1、14、51、124、245、426、679、1016、1449、1990、…
Stella octangula 数字是完美的正方形是 **1** 和 **9653449** 。
给定一个数字 x，检查是否是 Stella octangula。](https://en.wikipedia.org/wiki/Stella_octangula_number)

**示例:**

```
Input: x = 51
Output: Yes
For n = 3, the value of expression
n(2n2 - 1) is 51

Input: n = 53
Output: No
```

一个**简单的解决方案**是从 n = 0 开始运行一个循环。每 n，检查 n(2n<sup>2</sup>–1)是否等于 x。当 n(2n<sup>2</sup>–1)的值小于或等于 x 时，我们运行循环

一个有效的解决方案是使用[无界二分搜索法](https://www.geeksforgeeks.org/find-the-point-where-a-function-becomes-negative/)。我们首先找到一个 n 的值，使得 n(2n<sup>2</sup>–1)大于 x。然后我们应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。

## C++

```
// Program to check if a number is Stella
// Octangula Number
#include <bits/stdc++.h>
using namespace std;

// Returns value of n*(2*n*n - 1)
int f(int n) {
   return n*(2*n*n - 1);
}

// Finds if a value of f(n) is equal to x
// where n is in interval [low..high]
bool binarySearch(int low, int high, int x)
{
    while (low <= high) {
        long long mid = (low + high) / 2;

        if (f(mid) < x)
            low = mid + 1;
        else if (f(mid) > x)
            high = mid - 1;
        else
            return true;
    }
    return false;
}

// Returns true if x isStella Octangula Number.
// Else returns false.
bool isStellaOctangula(int x)
{
    if (x == 0)
      return true;

    // Find 'high' for binary search by
    // repeated doubling
    int i = 1;
    while (f(i) < x)
        i = i*2;

    // If condition is satisfied for a
    // power of 2.
    if (f(i) == x)
        return true;

    //  Call binary search
    return binarySearch(i/2, i, x);
}

// driver code
int main()
{
    int n = 51;
    if (isStellaOctangula(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to check if
// a number is Stella
// Octangula Number
import java.io.*;

class GFG
{

// Returns value of
// n*(2*n*n - 1)
static int f(int n)
{
    return n * (2 * n *
                n - 1);
}

// Finds if a value of
// f(n) is equal to x
// where n is in
// interval [low..high]
static boolean binarySearch(int low,
                            int high,
                            int x)
{
    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (f(mid) < x)
            low = mid + 1;
        else if (f(mid) > x)
            high = mid - 1;
        else
            return true;
    }
    return false;
}

// Returns true if x
// is Stella Octangula
// Number.Else returns
// false.
static boolean isStellaOctangula(int x)
{
    if (x == 0)
    return true;

    // Find 'high' for
    // binary search by
    // repeated doubling
    int i = 1;
    while (f(i) < x)
        i = i * 2;

    // If condition is
    // satisfied for a
    // power of 2.
    if (f(i) == x)
        return true;

    // Call binary search
    return binarySearch(i / 2,
                        i, x);
}

// Driver code
public static void main (String[] args)
{
    int n = 51;
    if (isStellaOctangula(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to check if a number
# is Stella octangula number

# Returns value of n*(2*n*n - 1)
def f(n):

    return n * (2 * n * n - 1);

# Finds if a value of f(n) is equal to x
# where n is in interval [low..high]
def binarySearch(low, high, x):

    while (low <= high):
        mid = int((low + high) // 2);

        if (f(mid) < x):
            low = mid + 1;
        elif (f(mid) > x):
            high = mid - 1;
        else:
            return True;

    return False;

# Returns true if x isStella octangula
#  number. Else returns false.
def isStellaOctangula(x):

    if (x == 0):
        return True;

    # Find 'high' for binary search
    # by repeated doubling
    i = 1;
    while (f(i) < x):
        i = i * 2;

    # If condition is satisfied for a
    # power of 2.
    if (f(i) == x):
        return True;

    # Call binary search
    return binarySearch(i / 2, i, x);

# Driver code
n = 51;

if (isStellaOctangula(n) == True):
    print("Yes");
else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// Program to check if
// a number is Stella
// Octangula Number
using System;

class GFG
{

// Returns value of
// n*(2*n*n - 1)
static int f(int n)
{
    return n * (2 * n *
                n - 1);
}

// Finds if a value of
// f(n) is equal to x
// where n is in
// interval [low..high]
static bool binarySearch(int low,
                         int high,
                         int x)
{
    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (f(mid) < x)
            low = mid + 1;
        else if (f(mid) > x)
            high = mid - 1;
        else
            return true;
    }
    return false;
}

// Returns true if x
// is Stella Octangula
// Number.Else returns
// false.
static bool isStellaOctangula(int x)
{
    if (x == 0)
    return true;

    // Find 'high' for
    // binary search by
    // repeated doubling
    int i = 1;
    while (f(i) < x)
        i = i * 2;

    // If condition is
    // satisfied for a
    // power of 2.
    if (f(i) == x)
        return true;

    // Call binary search
    return binarySearch(i / 2,
                        i, x);
}

// Driver code
public static void Main ()
{
    int n = 51;
    if (isStellaOctangula(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed
// by anuj_67.
```

## java 描述语言

```
<script>

// JavaScript program to check if
// a number is Stella
// Octangula Number

// Returns value of
// n*(2*n*n - 1)
function f(n)
{
    return n * (2 * n *
                n - 1);
}

// Finds if a value of
// f(n) is equal to x
// where n is in
// interval [low..high]
function binarySearch(low, high, x)
{
    while (low <= high)
    {
        let mid = (low + high) / 2;

        if (f(mid) < x)
            low = mid + 1;
        else if (f(mid) > x)
            high = mid - 1;
        else
            return true;
    }
    return false;
}

// Returns true if x
// is Stella Octangula
// Number.Else returns
// false.
function isStellaOctangula(x)
{
    if (x == 0)
    return true;

    // Find 'high' for
    // binary search by
    // repeated doubling
    let i = 1;
    while (f(i) < x)
        i = i * 2;

    // If condition is
    // satisfied for a
    // power of 2.
    if (f(i) == x)
        return true;

    // Call binary search
    return binarySearch(i / 2,
                        i, x);
}

// Driver code

    let n = 51;
    if (isStellaOctangula(n))
        document.write("Yes");
    else
        document.write("No");

          // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
Yes
```