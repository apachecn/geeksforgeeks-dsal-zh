# 找出至少有一个字符重复的 M 个字符单词的个数

> 原文:[https://www . geesforgeks . org/find-m 字符单词的计数-至少有一个字符重复/](https://www.geeksforgeeks.org/find-the-count-of-m-character-words-which-have-at-least-one-character-repeated/)

给定两个整数 **N** 和 **M** ，任务是计算由给定的 **N** 个不同字符形成的 **M** 个字符长度的总字数，使得这些单词至少有一个字符重复一次以上。
**举例:**

> **输入:** N = 3，M = 2
> **输出:** 3
> 假设字符为{'a '，' b '，' c'}
> 所有可以用这些字符构成的 2 个长度字
> 均为“aa”、“ab”、“ac”、“ba”、“bb”、“bc”、“ca”、“cb”和“cc”。
> 在这些单词中，只有“aa”、“bb”和“cc”至少有一个字符重复了一次以上。
> **输入:** N = 10，M = 5
> **输出:** 69760

**方法:**
从 N 个字符中可能的 M 个字符单词的总数，**总数= N <sup>M</sup>** 。
无字符重复出现的 N 个字符中可能出现的 M 个字符单词的总数，**no repeat =<sup>N</sup>P<sub>M</sub>**。
因此，至少单个字符出现一次以上的总单词是**total–no repeat**，即**N<sup>M</sup>–<sup>N</sup>P<sub>M</sub>**。
以下是上述方法的实施:

## C++

```
// C++ implementation for the above approach
#include <math.h>
#include <iostream>
using namespace std;

// Function to return the
// factorial of a number
int fact(int n)
{
    if (n <= 1)
        return 1;
    return n * fact(n - 1);
}

// Function to return the value of nPr
int nPr(int n, int r)
{
    return fact(n) / fact(n - r);
}

// Function to return the total number of
// M length words which have at least a
// single character repeated more than once
int countWords(int N, int M)
{
    return pow(N, M) - nPr(N, M);
}

// Driver code
int main()
{
    int N = 10, M = 5;
    cout << (countWords(N, M));
    return 0;
}

// This code is contributed by jit_t
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the
    // factorial of a number
    static int fact(int n)
    {
        if (n <= 1)
            return 1;
        return n * fact(n - 1);
    }

    // Function to return the value of nPr
    static int nPr(int n, int r)
    {
        return fact(n) / fact(n - r);
    }

    // Function to return the total number of
    // M length words which have at least a
    // single character repeated more than once
    static int countWords(int N, int M)
    {
        return (int)Math.pow(N, M) - nPr(N, M);
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 10, M = 5;
        System.out.print(countWords(N, M));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Function to return the
# factorial of a number
def fact(n):

    if (n <= 1):
        return 1;
    return n * fact(n - 1);

# Function to return the value of nPr
def nPr(n, r):

    return fact(n) // fact(n - r);

# Function to return the total number of
# M length words which have at least a
# single character repeated more than once
def countWords(N, M):

    return pow(N, M) - nPr(N, M);

# Driver code
N = 10; M = 5;
print(countWords(N, M));

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // factorial of a number
    static int fact(int n)
    {
        if (n <= 1)
            return 1;
        return n * fact(n - 1);
    }

    // Function to return the value of nPr
    static int nPr(int n, int r)
    {
        return fact(n) / fact(n - r);
    }

    // Function to return the total number of
    // M length words which have at least a
    // single character repeated more than once
    static int countWords(int N, int M)
    {
        return (int)Math.Pow(N, M) - nPr(N, M);
    }

    // Driver code
    static public void Main ()
    {
        int N = 10, M = 5;
        Console.Write(countWords(N, M));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
// javascript implementation of the approach

    // Function to return the
    // factorial of a number

    function fact(n)
    {
        if (n <= 1)
            return 1;
        return n * fact(n - 1);
    }

    // Function to return the value of nPr

    function nPr( n,  r)
    {
        return fact(n) / fact(n - r);
    }

    // Function to return the total number of
    // M length words which have at least a
    // single character repeated more than once

    function countWords( N,  M)
    {
        return Math.pow(N, M) - nPr(N, M);
    }

    // Driver code
        var N = 10 ;
        var M = 5;
        document.write(countWords(N, M));

  // This code is contributed by bunnyram19.
```

**Output:** 

```
69760
```