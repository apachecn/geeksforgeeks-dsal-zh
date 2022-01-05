# 求二进制表示为回文的第 n 个数

> 原文:[https://www . geesforgeks . org/find-n-th-number-what-binary-表象-回文/](https://www.geeksforgeeks.org/find-n-th-number-whose-binary-representation-palindrome/)

求二进制表示为回文的第 n 个数。考虑二进制表示时，不要考虑前导零。考虑二进制表示为回文的第一个数字为 1，而不是 0

**示例:**

```
Input : 1
Output : 1
1st Number whose binary representation 
is palindrome is 1 (1)

Input : 9
Output : 27
9th Number whose binary representation
is palindrome is 27 (11011)
```

**方法 1:天真**
一种天真的方法是，遍历从 1 到 2^31-1 的所有整数，如果该数是回文，则递增回文计数。当回文计数达到所需的 n 时，中断循环并返回当前整数。

## C++

```
// C++ program to find n-th number whose binary
// representation is palindrome.
#include <bits/stdc++.h>
using namespace std;

// Finds if the kth bit is set in the binary
// representation 
int isKthBitSet(int x, int k)
{
    return (x & (1 << (k - 1))) ? 1 : 0;
}

// Returns the position of leftmost set bit
// in the binary representation 
int leftmostSetBit(int x)
{
    int count = 0;
    while (x) {
        count++;
        x = x >> 1;
    }
    return count;
}

// Finds whether the integer in binary
// representation is palindrome or not
int isBinPalindrome(int x)
{
    int l = leftmostSetBit(x);
    int r = 1;

    // One by one compare bits
    while (l > r) {

        // Compare left and right bits and converge
        if (isKthBitSet(x, l) != isKthBitSet(x, r))
            return 0;
        l--;
        r++;
    }
    return 1;
}

int findNthPalindrome(int n)
{
    int pal_count = 0;

    // Start from 1, traverse through
    // all the integers 
    int i = 0;
    for (i = 1; i <= INT_MAX; i++) {
        if (isBinPalindrome(i)) {
            pal_count++;
        }
        // If we reach n, break the loop
        if (pal_count == n)
            break;
    }

    return i;
}

// Driver code
int main()
{
    int n = 9;

    // Function Call
    cout << findNthPalindrome(n);
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find n-th number whose binary
// representation is palindrome.
#include <stdio.h>
#define INT_MAX 2147483647

// Finds if the kth bit is set in the binary
// representation 
int isKthBitSet(int x, int k)
{
    return (x & (1 << (k - 1))) ? 1 : 0;
}

// Returns the position of leftmost set bit
// in the binary representation
int leftmostSetBit(int x)
{
    int count = 0;
    while (x) {
        count++;
        x = x >> 1;
    }
    return count;
}

// Finds whether the integer in binary
// representation is palindrome or not
int isBinPalindrome(int x)
{
    int l = leftmostSetBit(x);
    int r = 1;

    // One by one compare bits
    while (l > r) {

        // Compare left and right bits and converge
        if (isKthBitSet(x, l) != isKthBitSet(x, r))
            return 0;
        l--;
        r++;
    }
    return 1;
}

int findNthPalindrome(int n)
{
    int pal_count = 0;

    // Start from 1, traverse through
    // all the integers
    int i = 0;
    for (i = 1; i <= INT_MAX; i++) {
        if (isBinPalindrome(i)) {
            pal_count++;
        }
        // If we reach n, break the loop 
        if (pal_count == n)
            break;
    }

    return i;
}

// Driver code
int main()
{
    int n = 9;

    // Function Call
    printf("%d", findNthPalindrome(n));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th
// number whose binary
// representation is palindrome.
import java.io.*;

class GFG {
    static int INT_MAX = 2147483647;

    // Finds if the kth bit
    // is set in the binary
    // representation
    static int isKthBitSet(int x, int k)
    {
        return ((x & (1 << (k - 1))) > 0) ? 1 : 0;
    }

    // Returns the position of
    // leftmost set bit in the
    // binary representation 
    static int leftmostSetBit(int x)
    {
        int count = 0;
        while (x > 0) {
            count++;
            x = x >> 1;
        }
        return count;
    }

    // Finds whether the integer
    // in binary representation is
    // palindrome or not
    static int isBinPalindrome(int x)
    {
        int l = leftmostSetBit(x);
        int r = 1;

        // One by one compare bits
        while (l > r) {

            // Compare left and right
            // bits and converge
            if (isKthBitSet(x, l) != isKthBitSet(x, r))
                return 0;
            l--;
            r++;
        }
        return 1;
    }

    static int findNthPalindrome(int n)
    {
        int pal_count = 0;

        // Start from 1, traverse
        // through all the integers
        int i = 0;
        for (i = 1; i <= INT_MAX; i++) {
            if (isBinPalindrome(i) > 0) {
                pal_count++;
            }

            // If we reach n,
            // break the loop
            if (pal_count == n)
                break;
        }

        return i;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 9;

        // Function Call
        System.out.println(findNthPalindrome(n));
    }
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find n-th number
# whose binary representation is palindrome.
INT_MAX = 2147483647

# Finds if the kth bit is set in
# the binary representation

def isKthBitSet(x, k):

    return 1 if (x & (1 << (k - 1))) else 0

# Returns the position of leftmost
# set bit in the binary representation

def leftmostSetBit(x):

    count = 0
    while (x):
        count += 1
        x = x >> 1

    return count

# Finds whether the integer in binary
# representation is palindrome or not

def isBinPalindrome(x):

    l = leftmostSetBit(x)
    r = 1

    # One by one compare bits
    while (l > r):

        # Compare left and right bits
        # and converge
        if (isKthBitSet(x, l) != isKthBitSet(x, r)):
            return 0
        l -= 1
        r += 1
    return 1

def findNthPalindrome(n):
    pal_count = 0

    # Start from 1, traverse
    # through all the integers
    i = 0
    for i in range(1, INT_MAX + 1):
        if (isBinPalindrome(i)):
            pal_count += 1

        # If we reach n, break the loop
        if (pal_count == n):
            break

    return i

# Driver code
if __name__ == "__main__":
    n = 9

    # Function Call
    print(findNthPalindrome(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find n-th
// number whose binary
// representation is palindrome.
using System;

class GFG {

    static int INT_MAX = 2147483647;

    // Finds if the kth bit
    //  is set in the binary
    // representation
    static int isKthBitSet(int x, int k)
    {
        return ((x & (1 << (k - 1))) > 0) ? 1 : 0;
    }

    // Returns the position of
    // leftmost set bit in the
    // binary representation 
    static int leftmostSetBit(int x)
    {
        int count = 0;
        while (x > 0) {
            count++;
            x = x >> 1;
        }
        return count;
    }

    // Finds whether the integer
    // in binary representation is
    // palindrome or not 
    static int isBinPalindrome(int x)
    {
        int l = leftmostSetBit(x);
        int r = 1;

        // One by one compare bits
        while (l > r) {

            // Compare left and right
            // bits and converge
            if (isKthBitSet(x, l) != isKthBitSet(x, r))
                return 0;
            l--;
            r++;
        }
        return 1;
    }

    static int findNthPalindrome(int n)
    {
        int pal_count = 0;

        // Start from 1, traverse
        // through all the integers
        int i = 0;
        for (i = 1; i <= INT_MAX; i++) {
            if (isBinPalindrome(i) > 0) {
                pal_count++;
            }

            // If we reach n,
            // break the loop
            if (pal_count == n)
                break;
        }

        return i;
    }

    // Driver code
    static public void Main()
    {
        int n = 9;

        // Function Call
        Console.WriteLine(findNthPalindrome(n));
    }
}

// This code is contributed ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th number whose 
// binary representation is palindrome.

// Finds if the kth bit is set in 
// the binary representation 
function isKthBitSet($x, $k)
{
    return ($x & (1 << ($k - 1))) ? 1 : 0;
}

// Returns the position of leftmost set 
// bit in the binary representation
function leftmostSetBit($x)
{
    $count = 0;
    while ($x)
    {
        $count++;
        $x = $x >> 1;
    }
    return $count;
}

// Finds whether the integer in binary 
// representation is palindrome or not
function isBinPalindrome($x)
{
    $l = leftmostSetBit($x);
    $r = 1;

    // One by one compare bits
    while ($l > $r) 
    {

        // Compare left and right bits
        // and converge
        if (isKthBitSet($x, $l) != 
            isKthBitSet($x, $r))
            return 0;
        $l--;
        $r++;
    }
    return 1;
}

function findNthPalindrome($n)
{
    $pal_count = 0;

    // Start from 1, traverse through 
    // all the integers 
    $i = 0;
    for ($i = 1; $i <= PHP_INT_MAX; $i++) 
    {
        if (isBinPalindrome($i)) 
        {
            $pal_count++;
        }

        // If we reach n, break the loop
        if ($pal_count == $n)
            break;
    }
    return $i;
}

// Driver code
$n = 9;

// Function Call
echo (findNthPalindrome($n));

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th
// number whose binary
// representation is palindrome.
let INT_MAX = 2147483647;

// Finds if the kth bit
// is set in the binary
// representation
function isKthBitSet(x, k)
{
    return ((x & (1 << (k - 1))) > 0) ? 1 : 0;
}

// Returns the position of
// leftmost set bit in the
// binary representation
function leftmostSetBit(x)
{
    let count = 0;

    while (x > 0)
    {
        count++;
        x = x >> 1;
    }
    return count;
}

// Finds whether the integer
// in binary representation is
// palindrome or not
function isBinPalindrome(x)
{
    let l = leftmostSetBit(x);
    let r = 1;

    // One by one compare bits
    while (l > r)
    {

        // Compare left and right
        // bits and converge
        if (isKthBitSet(x, l) != 
            isKthBitSet(x, r))
            return 0;

        l--;
        r++;
    }
    return 1;
}

function findNthPalindrome(n)
{
    let pal_count = 0;

    // Start from 1, traverse
    // through all the integers
    let i = 0;
    for(i = 1; i <= INT_MAX; i++) 
    {
        if (isBinPalindrome(i) > 0)
        {
            pal_count++;
        }

        // If we reach n,
        // break the loop
        if (pal_count == n)
            break;
    }
    return i;
}

// Driver code
let n = 9;

// Function Call
document.write(findNthPalindrome(n));

// This code is contributed by suresh07

</script>
```

**Output**

```
27
```