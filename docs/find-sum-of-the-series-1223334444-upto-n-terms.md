# 求系列 1+22+333+4444+……到 n 项的和

> 原文:[https://www . geesforgeks . org/find-sum-the-series-1223334444-upto-n-terms/](https://www.geeksforgeeks.org/find-sum-of-the-series-1223334444-upto-n-terms/)

给定一个数字 N，任务是找到下面系列的和直到第 N 项:

> **1+22+333+4444**+…最多 n 项

**示例** :

```
Input: N = 3
Output: 356

Input: N = 10 
Output: 12208504795
```

**进场:**

![Let $A_n = 1 + 22 + 333 + 4444 +......+ n( \overbrace{11...1} )$ Then\\ $A_n = \frac{10^{n+1}(9n-1)}{9^3}+\frac{10}{9^3}-\frac{n(n+1)}{18}$ we define $S_n(x)=x+2x^2++3x^2+...+nx^n$\\\\ $9A_n$ $=9+2.99+3.999+....+n(99...99)$\\ $9A_n$ $=(10-1)+2(10^2-1)+3(10^3-1)+...+n(10^n-1)$\\ $9A_n$ $=10+2.10^2+3.10^3+...+n.10^n-(1+2+3+...+n)$\\ $9A_n$ $=S_n(10)-\frac{n(n+1)}{2}$\\\\ Now, \\ $\frac{S_n(x)}{x}= 1+ 2x+3x^2+...+nx^{n}$\\ $\frac{S_n(x)}{x}= \frac{d}{dx}(1+x+x^2+x^3+...+x^n) $\\ $\frac{S_n(x)}{x}= \frac{d}{dx}\left (\frac{x^{n+1}-1}{x-1}\right )$\\ $\frac{S_n(x)}{x}= \frac{nx^{n+1}-(n+1)x^n+1}{(x-1)^2}$\\\\ Finally, $A_n=\frac{1}{9} \left (10 \left ( \frac{n10^{n+1}-(n+1)10^n+1}{9^2}\right )-\frac{n(n+1)}{2}\right )}$ $A_n=\frac{10n^{n+1}(9n-1)}{9^3}+\frac{10}{9^3}-\frac{n(n+1)}{18}$ $   ](img/ead919b1c36af4f7756bd79184a6d4d6.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// CPP program to find the sum
// of given series

#include <iostream>
#include <math.h>

using namespace std;

// Function to calculate sum
int findSum(int n)
{
    // Return sum
    return (pow(10, n + 1) * (9 * n - 1) + 10) /
                    pow(9, 3) - n * (n + 1) / 18;
}

// Driver code
int main()
{
    int n = 3;

    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// Sum of first n terms
import java.util.*;

class solution
{
static int calculateSum(int n)
{

// Returning the final sum
return ((int)Math.pow(10, n + 1) * (9 * n - 1) + 10) /
                (int)Math.pow(9, 3) - n * (n + 1) / 18;
}

// Driver code
public static void main(String ar[])
{
// no. of terms to find the sum
int n=3;
System.out.println("Sum= "+ calculateSum(n));

}
}

//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python program to find the sum of given series.

# Function to calculate sum
def solve_sum(n):
    # Return sum
    return (pow(10, n + 1)*(9 * n - 1)+10)/pow(9, 3)-n*(n + 1)/18

# driver code
n = 3

print(int(solve_sum(n)))
```

## C#

```
// C# Program to find
// Sum of first n terms
using System;
class solution
{
static int calculateSum(int n)
{

// Returning the final sum
return ((int)Math.Pow(10, n + 1) * (9 * n - 1) + 10) /
                (int)Math.Pow(9, 3) - n * (n + 1) / 18;
}

// Driver code
public static void  Main()
{
// no. of terms to find the sum
int n=3;
Console.WriteLine("Sum= "+ calculateSum(n));

}
}

//This code is contributed by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum
// of given series

// Function to calculate sum
function findSum($n)
{
    // Return sum
    return (pow(10, $n + 1) *
               (9 * $n - 1) + 10) /
            pow(9, 3) - $n * ($n + 1) / 18;
}

// Driver code

$n = 3;

echo findSum($n);

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>
// Javascript Program to find
// Sum of first n terms

    function calculateSum( n)
    {

        // Returning the const sum
        return (parseInt(Math.pow(10, n + 1)) * (9 * n - 1) + 10) /
                parseInt(Math.pow(9, 3)) - n * (n + 1) / 18;
     }

    // Driver code

    // no. of terms to find the sum
    let n = 3;
    document.write("Sum= " + calculateSum(n));

// This code is contributed by 29AjayKumar 
</script>
```

**Output:** 

```
356
```