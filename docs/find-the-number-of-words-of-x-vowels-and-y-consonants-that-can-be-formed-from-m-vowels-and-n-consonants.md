# 找出 M 个元音和 N 个辅音可以组成的 X 个元音和 Y 个辅音的字数

> 原文:[https://www . geesforgeks . org/find-由 m 元音和 n 辅音组成的 x 元音和 y 辅音的字数/](https://www.geeksforgeeks.org/find-the-number-of-words-of-x-vowels-and-y-consonants-that-can-be-formed-from-m-vowels-and-n-consonants/)

给定四个整数 **X** 、 **Y** 、 **M** 和 **N** 。任务是从 **M** 元音和 **N** 辅音的总数中选择 **X** 元音数和 **Y** 辅音数，找出构成一个单词的方法数。
**举例:**

> **输入:** X = 2，Y = 2，M = 3，N = 3
> **输出:** 216
> 从总共 3 个元音中选择 2 个元音的方式总数为![3\choose2  ](img/515281fe2fc0c51da623dad5db4013b2.png "Rendered by QuickLaTeX.com")即 3
> 从总共 3 个辅音中选择 2 个辅音的方式总数为![3\choose2  ](img/515281fe2fc0c51da623dad5db4013b2.png "Rendered by QuickLaTeX.com")即 3。
> 从 3 中选择 2 个辅音，从 3 中选择 2 个元音的方式总数为![3\choose2  ](img/515281fe2fc0c51da623dad5db4013b2.png "Rendered by QuickLaTeX.com") * ![3\choose2  ](img/515281fe2fc0c51da623dad5db4013b2.png "Rendered by QuickLaTeX.com") = 9
> 它们之间排列 4 个字母的方式总数= 4！= 24
> 因此，所需的路数= 24 * 9 = 216
> **输入:** X = 1，Y = 2，M = 2，N = 3
> **输出:** 36

[推荐:请先在{IDE}上尝试您的方法，然后再继续解决方案。](https://ide.geeksforgeeks.org/)
**进场:**

*   从 M 个元音总数中选择 X 个元音的方法总数为![M\choose X](img/426e8a838a1756feaa87941d1118119c.png "Rendered by QuickLaTeX.com")
*   从 N 个辅音的总数中选择 Y 个辅音的方法总数为![N\choose Y](img/465859574a115dcc6ecce469bbb83e57.png "Rendered by QuickLaTeX.com")
*   从 N 中选择 Y 辅音，从 M 中选择 X 元音的方式总数为![N\choose Y  ](img/02e133fec55fe7d08e9e1846c51be582.png "Rendered by QuickLaTeX.com") * ![M\choose X](img/426e8a838a1756feaa87941d1118119c.png "Rendered by QuickLaTeX.com")
*   字母之间排列(X+Y)的方式总数= (X+Y)！
*   因此，所需的路数= (X+Y)！* ![N\choose Y  ](img/02e133fec55fe7d08e9e1846c51be582.png "Rendered by QuickLaTeX.com") * ![M\choose X](img/426e8a838a1756feaa87941d1118119c.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// CPP program to find the number of words
// of X vowels  and Y consonants can be
// formed from M vowels and N consonants
#include <bits/stdc++.h>
using namespace std;

// Function to returns factorial of n
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Function to find nCr
int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of words
// of X vowels  and Y consonants can be
// formed from M vowels and N consonants
int NumberOfWays(int X, int Y, int M, int N)
{
    return fact(X + Y) * nCr(M, X) * nCr(N, Y);
}

// Driver code
int main()
{
    int X = 2, Y = 2, M = 3, N = 3;

    // Function call
    cout << NumberOfWays(X, Y, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of words
// of X vowels and Y consonants can be
// formed from M vowels and N consonants
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

    // Function to returns factorial of n
    static int fact(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to find nCr
    static int nCr(int n, int r)
    {
        return fact(n) / (fact(r) *
                          fact(n - r));
    }

    // Function to find the number of words
    // of X vowels and Y consonants can be
    // formed from M vowels and N consonants
    static int NumberOfWays(int X, int Y,
                            int M, int N)
    {
        return fact(X + Y) * nCr(M, X) *
                             nCr(N, Y);
    }

    // Driver code
    public static void main (String[] args)
                  throws java.lang.Exception
    {
        int X = 2, Y = 2, M = 3, N = 3;

        // Function call
        System.out.println(NumberOfWays(X, Y, M, N));        
    }
}

// This code is contributed by Nidhiva
```

## 蟒蛇 3

```
# Python 3 program to find the number of words
# of X vowels and Y consonants can be
# formed from M vowels and N consonants

# Function to returns factorial of n
def fact(n):
    res = 1
    for i in range(2, n + 1, 1):
        res = res * i
    return res

# Function to find nCr
def nCr(n, r):
    return fact(n) // (fact(r) * fact(n - r))

# Function to find the number of words
# of X vowels and Y consonants can be
# formed from M vowels and N consonants
def NumberOfWays(X, Y, M, N):
    return fact(X + Y) * nCr(M, X) * nCr(N, Y)

# Driver code
if __name__ == '__main__':
    X = 2
    Y = 2
    M = 3
    N = 3

    # Function call
    print(NumberOfWays(X, Y, M, N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number of words
// of X vowels and Y consonants can be
// formed from M vowels and N consonants
using System;

class GFG
{

    // Function to returns factorial of n
    static int fact(int n)
    {
        int res = 1;
        for (int i = 2; i <= n; i++)
            res = res * i;
        return res;
    }

    // Function to find nCr
    static int nCr(int n, int r)
    {
        return fact(n) / (fact(r) *
                          fact(n - r));
    }

    // Function to find the number of words
    // of X vowels and Y consonants can be
    // formed from M vowels and N consonants
    static int NumberOfWays(int X, int Y,
                            int M, int N)
    {
        return fact(X + Y) * nCr(M, X) *
                             nCr(N, Y);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int X = 2, Y = 2, M = 3, N = 3;

        // Function call
        Console.WriteLine(NumberOfWays(X, Y, M, N));        
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to find the number of words
      // of X vowels and Y consonants can be
      // formed from M vowels and N consonants

      // Function to returns factorial of n
      function fact(n) {
        var res = 1;
        for (var i = 2; i <= n; i++)
            res = res * i;
        return res;
      }

      // Function to find nCr
      function nCr(n, r) {
        return fact(n) / (fact(r) * fact(n - r));
      }

      // Function to find the number of words
      // of X vowels and Y consonants can be
      // formed from M vowels and N consonants
      function NumberOfWays(X, Y, M, N) {
        return fact(X + Y) * nCr(M, X) * nCr(N, Y);
      }

      // Driver code
      var X = 2,
        Y = 2,
        M = 3,
        N = 3;

      // Function call
      document.write(NumberOfWays(X, Y, M, N));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
216
```