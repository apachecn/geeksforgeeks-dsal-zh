# 前 n 个奇数的平方和

> 原文:[https://www . geesforgeks . org/sum-square-first-n-奇数/](https://www.geeksforgeeks.org/sum-square-first-n-odd-numbers/)

给定一个数 n，求前 n 个奇数自然数的平方和。

**例:**

```
Input : 3
Output : 35 
12 + 32 + 52 = 35

Input : 8
Output : 680
12 + 32 + 52 + 72 + 92 + 112 + 132 + 152 
```

一个**简单的解法**就是遍历 n 个奇数，求平方和。

下面是该方法的实现。

## C++

```
// Simple C++ method to find sum of square of
// first n odd numbers.
#include <iostream>
using namespace std;

int squareSum(int n)
{
    int sum = 0;
    for (int i = 1; i <=  n; i++)
        sum += (2*i - 1) * (2*i - 1);
    return sum;
}

int main()
{
    cout << squareSum(8);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java method to
// find sum of square of
// first n odd numbers.

import java.io.*;

class GFG {

    static int squareSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <=  n; i++)
            sum += (2*i - 1) * (2*i - 1);
        return sum;
    }

    //Driver Code
    public static void main(String args[])
    {  
        System.out.println(squareSum(8));
    }
}

// This code is contributed by
// Nikita tiwari.
```

## 蟒蛇 3

```
# Simple Python method
# to find sum of square
# of first n odd numbers.
def squareSum(n):

    sm = 0
    for i in range(1, n + 1):
        sm += (2 * i - 1) * (2 * i - 1)

    return sm

# Driver Code
n=8
print(squareSum(n))

# This code is contributed by Ansu Kumari
```

## C#

```
// Simple C# method to find
// sum of square of first
// n odd numbers.
using System;

class GFG {

    static int squareSum(int n)
    {
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += (2*i - 1) * (2*i - 1);
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        Console.Write(squareSum(8));
    }
}

// This code is contributed by
// vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP method to find sum
// of square of first n odd numbers.

function squareSum( $n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += (2*$i - 1) * (2*$i - 1);
    return $sum;
}

    echo squareSum(8);

// This code is contributed by Vt_m.
?>
```

## java 描述语言

```
<script>

// Simple Javascript method to find
// sum of square of first n odd numbers.
function squareSum(n)
{
    let sum = 0;
    for(let i = 1; i <=  n; i++)
        sum += (2 * i - 1) * (2 * i - 1);

    return sum;
}

// Driver code
document.write(squareSum(8));

// This code is contributed by souravmahato348

</script>
```

**输出:**

```
680
```

一个**有效的解决方案**是应用下面的公式。

```
sum = n * (4n2 - 1) / 3

How does it work? 
Please refer sum of squares of even and odd
numbers for proof.
```

## c++

```
// Efficient C++ method to find sum of
// square of first n odd numbers.
#include <iostream>
using namespace std;

int squareSum(int n)
{
    return n*(4*n*n - 1)/3;
}

int main()
{
    cout << squareSum(8);
    return 0;
}
```

## Java

```
// Efficient Java method
// to find sum of
// square of first n odd numbers.

import java.io.*;

class GFG {

    static int squareSum(int n)
    {
        return n*(4*n*n - 1)/3;
    }

    public static void main(String args[])
    {
        System.out.println(squareSum(8));
    }
}

// This code is contributed by
// Nikita tiwari.
```

## python 3

```
# Python3 code to find sum
# of square of first n odd numbers

def squareSum( n ):

    return int(n * ( 4 * n * n - 1) / 3)

# driver code
ans = squareSum(8)
print (ans)

# This code is contributed by Saloni Gupta
```

## c#

```
// Efficient C# method to
// find sum of square of
// first n odd numbers.
using System;

class GFG {

    static int squareSum(int n)
    {
        return n * (4 * n * n - 1)/3;
    }

    // driver code   
    public static void Main()
    {
        Console.Write(squareSum(8));
    }
}

// This code is contributed by
// Vt_m.
```

## PHP

```
<?php
// Efficient PHP method to find sum of
// square of first n odd numbers.

function squareSum($n)
{
    return $n * (4 * $n * $n - 1) / 3;
}

    echo squareSum(8);

// This code is contributed by Vt_m.
?>
```

T30】Javascript

**输出:**

```
680
```