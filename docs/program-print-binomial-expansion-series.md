# 程序打印二项式展开系列

> 原文:[https://www . geesforgeks . org/program-print-binomial-expansion-series/](https://www.geeksforgeeks.org/program-print-binomial-expansion-series/)

给定三个整数，A，X 和 n，任务是打印下面二项式表达式系列的术语。
(A+X)<sup>n</sup>=<sup>n</sup>C<sub>0</sub>A<sup>n</sup>X<sup>0</sup>+<sup>n</sup>C<sub>1</sub>A<sup>n-1</sup>X<sup>1</sup>+<sup>n</sup>C<sub>2</sub>A<sup>n-2</sup>X+<sup>n</sup>C<sub>n</sub>A<sup>0</sup>X<sup>n</sup>T35】例:

```
Input : A = 1, X = 1, n = 5
Output : 1 5 10 10 5 1

Input : A = 1, B = 2, n = 6
Output : 1 12 60 160 240 192 64 
```

**简单解法:**我们知道，对于 n 的每个值，二项式级数中都会有(n+1)项。所以现在我们使用一个简单的方法，计算系列中每个元素的值并打印出来。

```
nCr = (n!) / ((n-r)! * (r)!)

Below is value of general term. 
Tr+1 = nCn-rAn-rXr
So at each position we have to find the value 
of the general term and print that term .
```

## C++

```
// CPP program to print terms of binomial
// series and also calculate sum of series.
#include <bits/stdc++.h>
using namespace std;

// function to calculate factorial of
// a number
int factorial(int n)
{
    int f = 1;
    for (int i = 2; i <= n; i++)
        f *= i;       
    return f;
}

// function to print the series
void series(int A, int X, int n)
{    
    // calculating the value of n!
    int nFact = factorial(n);

    // loop to display the series
    for (int i = 0; i < n + 1; i++) {

        // For calculating the
        // value of nCr
        int niFact = factorial(n - i);
        int iFact = factorial(i);

        // calculating the value of
        // A to the power k and X to
        // the power k
        int aPow = pow(A, n - i);
        int xPow = pow(X, i);

        // display the series
        cout << (nFact * aPow * xPow) /
                 (niFact * iFact) << " ";
    }
}

// main function started
int main()
{
    int A = 3, X = 4, n = 5;
    series(A, X, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print terms of binomial
// series and also calculate sum of series.

import java.io.*;

class GFG {

    // function to calculate factorial of
    // a number
    static int factorial(int n)
    {
        int f = 1;
        for (int i = 2; i <= n; i++)
            f *= i;

        return f;
    }

    // function to print the series
    static void series(int A, int X, int n)
    {

        // calculating the value of n!
        int nFact = factorial(n);

        // loop to display the series
        for (int i = 0; i < n + 1; i++) {

            // For calculating the
            // value of nCr
            int niFact = factorial(n - i);
            int iFact = factorial(i);

            // calculating the value of
            // A to the power k and X to
            // the power k
            int aPow = (int)Math.pow(A, n - i);
            int xPow = (int)Math.pow(X, i);

            // display the series
            System.out.print((nFact * aPow * xPow)
                         / (niFact * iFact) + " ");
        }
    }

    // main function started
    public static void main(String[] args)
    {
        int A = 3, X = 4, n = 5;

        series(A, X, n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to print terms of binomial
# series and also calculate sum of series.

# function to calculate factorial
# of a number
def factorial(n):

    f = 1
    for i in range(2, n+1):
        f *= i

    return f

# Function to print the series
def series(A, X, n):

    # calculating the value of n!
    nFact = factorial(n)

    # loop to display the series
    for i in range(0, n + 1):

        # For calculating the
        # value of nCr
        niFact = factorial(n - i)
        iFact = factorial(i)

        # calculating the value of
        # A to the power k and X to
        # the power k
        aPow = pow(A, n - i)
        xPow = pow(X, i)

        # display the series
        print (int((nFact * aPow * xPow) /
                   (niFact * iFact)), end = " ")

# Driver Code
A = 3; X = 4; n = 5
series(A, X, n)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to print terms of binomial
// series and also calculate sum of series.
using System;

class GFG {

    // function to calculate factorial of
    // a number
    static int factorial(int n)
    {
        int f = 1;
        for (int i = 2; i <= n; i++)
            f *= i;

        return f;
    }

    // function to print the series
    static void series(int A, int X, int n)
    {

        // calculating the value of n!
        int nFact = factorial(n);

        // loop to display the series
        for (int i = 0; i < n + 1; i++) {

            // For calculating the
            // value of nCr
            int niFact = factorial(n - i);
            int iFact = factorial(i);

            // calculating the value of
            // A to the power k and X to
            // the power k
            int aPow = (int)Math.Pow(A, n - i);
            int xPow = (int)Math.Pow(X, i);

            // display the series
            Console.Write((nFact * aPow * xPow)
                     / (niFact * iFact) + " ");
        }
    }

    // main function started
    public static void Main()
    {
        int A = 3, X = 4, n = 5;

        series(A, X, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// terms of binomial
// series and also
// calculate sum of series.

// function to calculate
// factorial of a number
function factorial($n)
{
    $f = 1;
    for ($i = 2; $i <= $n; $i++)
        $f *= $i;
    return $f;
}

// function to print the series
function series($A, $X, $n)
{

    // calculating the
    // value of n!
    $nFact = factorial($n);

    // loop to display
    // the series
    for ($i = 0; $i < $n + 1; $i++)
    {

        // For calculating the
        // value of nCr
        $niFact = factorial($n - $i);
        $iFact = factorial($i);

        // calculating the value of
        // A to the power k and X to
        // the power k
        $aPow = pow($A, $n - $i);
        $xPow = pow($X, $i);

        // display the series
        echo ($nFact * $aPow * $xPow) /
             ($niFact * $iFact) , " ";
    }
}

    // Driver Code
    $A = 3;
    $X = 4;
    $n = 5;
    series($A, $X, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print terms of binomial
// series and also calculate sum of series.

    // function to calculate factorial of
    // a number
    function factorial(n)
    {
        let f = 1;
        for (let i = 2; i <= n; i++)
            f *= i;

        return f;
    }

    // function to print the series
    function series(A, X, n)
    {

        // calculating the value of n!
        let nFact = factorial(n);

        // loop to display the series
        for (let i = 0; i < n + 1; i++) {

            // For calculating the
            // value of nCr
            let niFact = factorial(n - i);
            let iFact = factorial(i);

            // calculating the value of
            // A to the power k and X to
            // the power k
            let aPow = Math.pow(A, n - i);
            let xPow = Math.pow(X, i);

            // display the series
            document.write((nFact * aPow * xPow)
                         / (niFact * iFact) + " ");
        }
    }

// Driver Code
        let A = 3, X = 4, n = 5;
        series(A, X, n);

          // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
243 1620 4320 5760 3840 1024 
```

**有效解:**
想法是用上一个项计算下一个项。我们可以用 O(1)时间计算下一项。我们使用[二项式系数](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)的以下性质。
<sup>n</sup>C<sub>I+1</sub>=<sup>n</sup>C<sub>I</sub>*(n-I)/(I+1)

## C++

```
// CPP program to print terms of binomial
// series and also calculate sum of series.
#include <bits/stdc++.h>
using namespace std;

// function to print the series
void series(int A, int X, int n)
{
    // Calculating and printing first term
    int term = pow(A, n);
    cout << term << " ";

    // Computing and printing remaining terms
    for (int i = 1; i <= n; i++) {

        // Find current term using previous terms
        // We increment power of X by 1, decrement
        // power of A by 1 and compute nCi using
        // previous term by multiplying previous
        // term with (n - i + 1)/i
        term = term * X * (n - i + 1)/(i * A);

        cout << term << " ";
    }
}

// main function started
int main()
{
    int A = 3, X = 4, n = 5;
    series(A, X, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print terms of binomial
// series and also calculate sum of series.

import java.io.*;

class GFG {

    // function to print the series
    static void series(int A, int X, int n)
    {

        // Calculating and printing first
        // term
        int term = (int)Math.pow(A, n);
        System.out.print(term + " ");

        // Computing and printing
        // remaining terms
        for (int i = 1; i <= n; i++) {

            // Find current term using
            // previous terms We increment
            // power of X by 1, decrement
            // power of A by 1 and compute
            // nCi using previous term by
            // multiplying previous term
            // with (n - i + 1)/i
            term = term * X * (n - i + 1)
                                / (i * A);

            System.out.print(term + " ");
        }
    }

    // main function started
    public static void main(String[] args)
    {
        int A = 3, X = 4, n = 5;

        series(A, X, n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to print terms of binomial
# series and also calculate sum of series.

# Function to print the series
def series(A, X, n):

    # Calculating and printing first term
    term = pow(A, n)
    print(term, end = " ")

    # Computing and printing remaining terms
    for i in range(1, n+1):

        # Find current term using previous terms
        # We increment power of X by 1, decrement
        # power of A by 1 and compute nCi using
        # previous term by multiplying previous
        # term with (n - i + 1)/i
        term = int(term * X * (n - i + 1)/(i * A))

        print(term, end = " ")

# Driver Code
A = 3; X = 4; n = 5
series(A, X, n)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to print terms of binomial
// series and also calculate sum of series.

using System;

public class GFG {

    // function to print the series
    static void series(int A, int X, int n)
    {

        // Calculating and printing first
        // term
        int term = (int)Math.Pow(A, n);
        Console.Write(term + " ");

        // Computing and printing
        // remaining terms
        for (int i = 1; i <= n; i++) {

            // Find current term using
            // previous terms We increment
            // power of X by 1, decrement
            // power of A by 1 and compute
            // nCi using previous term by
            // multiplying previous term
            // with (n - i + 1)/i
            term = term * X * (n - i + 1)
                                / (i * A);

          Console.Write(term + " ");
        }
    }

    // main function started
    public static void Main()
    {
        int A = 3, X = 4, n = 5;

        series(A, X, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// terms of binomial
// series and also
// calculate sum of
// series.

// function to print
// the series
function series($A, $X, $n)
{

    // Calculating and printing
    // first term
    $term = pow($A, $n);
    echo $term , " ";

    // Computing and printing
    // remaining terms
    for ($i = 1; $i <= $n; $i++)
    {

        // Find current term
        // using previous terms
        // We increment power
        // of X by 1, decrement
        // power of A by 1 and
        // compute nCi using
        // previous term by
        // multiplying previous
        // term with (n - i + 1)/i
        $term = $term * $X * ($n - $i + 1) /
                                 ($i * $A);

        echo $term , " ";
    }
}

    // Driver Code
    $A = 3;
    $X = 4;
    $n = 5;
    series($A, $X, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print terms of binomial
// series and also calculate sum of series.

// function to print the series
function series(A, X, n)
{
    // Calculating and printing first term
    let term = Math.pow(A, n);
    document.write(term + " ");

    // Computing and printing remaining terms
    for (let i = 1; i <= n; i++) {

        // Find current term using previous terms
        // We increment power of X by 1, decrement
        // power of A by 1 and compute nCi using
        // previous term by multiplying previous
        // term with (n - i + 1)/i
        term = term * X * (n - i + 1)/(i * A);

        document.write(term + " ");
    }
}

// main function started

    let A = 3, X = 4, n = 5;
    series(A, X, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
243 1620 4320 5760 3840 1024 
```