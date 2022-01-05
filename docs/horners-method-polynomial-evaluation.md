# 霍纳多项式评估法

> 原文:[https://www . geesforgeks . org/horners-method-多项式-求值/](https://www.geeksforgeeks.org/horners-method-polynomial-evaluation/)

给定一个 c<sub>n</sub>x<sup>n</sup>+c<sub>n-1</sub>x<sup>n-1</sup>+c<sub>n-2</sub>x<sup>n-2</sup>+…+c<sub>1</sub>x+c<sub>0</sub>和一个 x 值的多项式，求给定值 x 的多项式值。这里 c <sub>n</sub> ，c..是整数(可以是负数), n 是正整数。
输入是数组的形式，比如 *poly[]* ，其中 poly[0]代表 x <sup>n</sup> 的系数，poly[1]代表 x <sup>n-1</sup> 的系数，以此类推。
**举例:**

```
// Evaluate value of 2x3 - 6x2 + 2x - 1 for x = 3
Input: poly[] = {2, -6, 2, -1}, x = 3
Output: 5

// Evaluate value of 2x3 + 3x + 1 for x = 2
Input: poly[] = {2, 0, 3, 1}, x = 2
Output: 23
```

计算多项式的一种简单方法是逐个计算所有项。首先计算 x <sup>n</sup> ，将该值乘以 c <sub>n</sub> ，对其他项重复相同的步骤并返回总和。如果我们使用一个简单的循环来评估 x <sup>n</sup> ，这种方法的时间复杂度为 0(n<sup>2</sup>)。如果我们使用 [O(Logn)方法来评估 x <sup>n</sup>](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/) ，时间复杂度可以提高到 O(nLogn)。
[**霍纳法**](http://en.wikipedia.org/wiki/Horner%27s_method) 可用于求 O(n)时间内的多项式。为了理解方法，让我们考虑 2x<sup>3</sup>–6x<sup>2</sup>+2x–1 的例子。多项式可以计算为((2x–6)x+2)x–1。其思想是将结果初始化为 x <sup>n</sup> 的系数，在这种情况下是 2，将结果与 x 重复相乘，并将下一个系数添加到结果中。最后返回结果。
下面是霍纳方法的实现。

## C++

```
#include <iostream>
using namespace std;

// returns value of poly[0]x(n-1) + poly[1]x(n-2) + .. + poly[n-1]
int horner(int poly[], int n, int x)
{
    int result = poly[0]; // Initialize result

    // Evaluate value of polynomial using Horner's method
    for (int i=1; i<n; i++)
        result = result*x + poly[i];

    return result;
}

// Driver program to test above function.
int main()
{
    // Let us evaluate value of 2x3 - 6x2 + 2x - 1 for x = 3
    int poly[] = {2, -6, 2, -1};
    int x = 3;
    int n = sizeof(poly)/sizeof(poly[0]);
    cout << "Value of polynomial is " << horner(poly, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of Horner Method
// for Polynomial Evaluation
import java.io.*;

class HornerPolynomial
{
    // Function that returns value of poly[0]x(n-1) +
    // poly[1]x(n-2) + .. + poly[n-1]
    static int horner(int poly[], int n, int x)
    {
        // Initialize result
        int result = poly[0]; 

        // Evaluate value of polynomial using Horner's method
        for (int i=1; i<n; i++)
            result = result*x + poly[i];

        return result;
    }

    // Driver program
    public static void main (String[] args)
    {
        // Let us evaluate value of 2x3 - 6x2 + 2x - 1 for x = 3
        int[] poly = {2, -6, 2, -1};
        int x = 3;
        int n = poly.length;
        System.out.println("Value of polynomial is "
                                        + horner(poly,n,x));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python program for
# implementation of Horner Method
# for Polynomial Evaluation

# returns value of poly[0]x(n-1)
# + poly[1]x(n-2) + .. + poly[n-1]
def horner(poly, n, x):

    # Initialize result
    result = poly[0] 

    # Evaluate value of polynomial
    # using Horner's method
    for i in range(1, n):

        result = result*x + poly[i]

    return result

# Driver program to
# test above function.

# Let us evaluate value of
# 2x3 - 6x2 + 2x - 1 for x = 3
poly = [2, -6, 2, -1]
x = 3
n = len(poly)

print("Value of polynomial is " , horner(poly, n, x))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program for implementation of
// Horner Method  for Polynomial Evaluation.
using System;

class GFG
{
    // Function that returns value of poly[0]x(n-1) +
    // poly[1]x(n-2) + .. + poly[n-1]
    static int horner(int []poly, int n, int x)
    {
        // Initialize result
        int result = poly[0];

        // Evaluate value of polynomial
        // using Horner's method
        for (int i = 1; i < n; i++)
            result = result * x + poly[i];

        return result;
    }

    // Driver Code
    public static void Main()
    {
        // Let us evaluate value of
        // 2x3 - 6x2 + 2x - 1 for x = 3
        int []poly = {2, -6, 2, -1};
        int x = 3;
        int n = poly.Length;
        Console.Write("Value of polynomial is "
                            + horner(poly,n,x));
    }
}

// This code Contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for implementation
// of Horner Method for Polynomial
// Evaluation.

// returns value of poly[0]x(n-1) +
// poly[1]x(n-2) + .. + poly[n-1]
function horner($poly, $n, $x)
{
    // Initialize result
    $result = $poly[0];

    // Evaluate value of polynomial
    // using Horner's method
    for ($i = 1; $i < $n; $i++)
        $result = $result *
                  $x + $poly[$i];

    return $result;
}

// Driver Code

// Let us evaluate value of
// 2x3 - 6x2 + 2x - 1 for x = 3
$poly = array(2, -6, 2, -1);
$x = 3;
$n = sizeof($poly) / sizeof($poly[0]);

echo "Value of polynomial is ".
         horner($poly, $n, $x);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// Javascript program for implementation
// of Horner Method for Polynomial
// Evaluation.

// returns value of poly[0]x(n-1) +
// poly[1]x(n-2) + .. + poly[n-1]
function horner(poly, n, x)
{

    // Initialize result
    let result = poly[0];

    // Evaluate value of polynomial
    // using Horner's method
    for (let i = 1; i < n; i++)
        result = result *
                  x + poly[i];

    return result;
}

// Driver Code

// Let us evaluate value of
// 2x3 - 6x2 + 2x - 1 for x = 3
let poly = new Array(2, -6, 2, -1);
let x = 3;
let n = poly.length

document.write("Value of polynomial is " +
         horner(poly, n, x));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
Value of polynomial is 5
```

**时间复杂度** : O(n)

**辅助空间:** O(1)
如发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息