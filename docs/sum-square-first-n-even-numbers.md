# 前 n 个偶数的平方和

> 原文:[https://www . geesforgeks . org/sum-square-first-n-偶数/](https://www.geeksforgeeks.org/sum-square-first-n-even-numbers/)

给定一个数 n，求前 n 个偶数自然数的平方和。

**例:**

```
Input : 3
Output : 56 
22 + 42 + 62 = 56

Input : 8
Output : 816
22 + 42 + 62 + 82 + 102 + 122 + 142 + 162 
```

一个**简单的解法**就是遍历 n 个偶数，求平方和。

## c++

```
// Simple C++ method to find sum
// of square of first n even numbers.
#include <iostream>
using namespace std;

int squareSum(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += (2 * i) * (2 * i);
    return sum;
}

// Driver Code
int main()
{
    cout << squareSum(8);
    return 0;
}
```

## Java

```
// Simple Java method to find sum of
// square of first n even numbers.
import java.io.*;

class GFG
{
    static int squareSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (2 * i) * (2 * i);
        return sum;
    }

    // Driver Code
    public static void main(String args[])
                  throws IOException
    {
        System.out.println(squareSum(8));
    }
}

// This code is contributed by Nikita Tiwari
```

## python 3

```
# Simple Python3 code to
# find sum of square of
# first n even numbers

def squareSum( n ):
    sum = 0
    for i in range (0, n + 1):
        sum += (2 * i) * (2 * i)

    return sum

# driver code
ans = squareSum(8)
print (ans)

# This code is contributed by Saloni Gupta
```

## c#

```
// Simple C# method to find sum of
// square of first n even numbers.
using System;

class GFG
{
    static int squareSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (2 * i) * (2 * i);

        return sum;
    }

    // Driver code
    public static void Main()
    {
        Console.Write(squareSum(8));
    }
}

// This code is contributed by vt_m.
```

## PHP

```
<?php
// Simple PHP method to find sum of
// square of first n even numbers.

function squareSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += (2 * $i) * (2 * $i);
    return $sum;
}

    echo squareSum(8);

// This code is contributed by vt_m.
?>
```

## Javascript

T33】

**输出:**

```
816
```

一个**有效的解决方案**是应用下面的公式。

```
***sum = 2 * n * (n + 1) * (2 * n + 1)/3***

How does it work? 
We know that sum of square of first 
n natural numbers is = n(n+1)/2

Sum of square of first n even natural numbers = 
        22 + 42 + .... + (2n)2
      = 4 * (12 + 22 + .... + n2)
      = 4 * n(n+1)(2n+1) / 6
      = 2 * n(n+1)(2n+1)/3 
```

## c++

```
// Efficient C++ method to find sum
// of square of first n even numbers.
#include <iostream>
using namespace std;

int squareSum(int n)
{
    return 2 * n * (n + 1) *
            (2 * n + 1) / 3;
}

// Driver code
int main()
{
    cout << squareSum(8);
    return 0;
}
```

## Java

```
// Efficient Java method to find sum
// of square of first n even numbers.
import java.io.*;

class GFG
{
    static int squareSum(int n)
    {
        return 2 * n * (n + 1) *
                (2 * n + 1) / 3;
    }

    // Driver Code
    public static void main(String args[])
                    throws IOException
    {
        System.out.println(squareSum(8));
    }
}

// This code is contributed by Nikita Tiwari
```

## python 3

```
# Efficient Python3 code to
# find sum of square of
# first n even numbers

def squareSum( n ):

    return int(2 * n * (n + 1) * (2 * n + 1) / 3)

# driver code
ans = squareSum(8)
print (ans)

# This code is contributed by Saloni Gupta
```

## c#

```
// Efficient C# method to find sum
// of square of first n even numbers.
using System;

class GFG
{

    static int squareSum(int n)
    {
        return 2 * n * (n + 1) * (2 * n + 1) / 3;
    }

    // driver code
    public static void Main()
    {
        Console.Write(squareSum(8));
    }
}

// This code is contributed by vt_m.
```

## PHP

```
<?php
// Efficient PHP method to find sum of
// square of first n even numbers.

function squareSum( $n)
{
    return 2 * $n * ($n + 1) *
             (2 * $n + 1) / 3;
}

echo squareSum(8);

// This code is contributed by vt_m.
?>
```

T30】Javascript

**输出** :

```
816
```