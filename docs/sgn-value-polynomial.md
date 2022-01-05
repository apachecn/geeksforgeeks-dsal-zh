# 多项式的 Sgn 值

> 原文:[https://www.geeksforgeeks.org/sgn-value-polynomial/](https://www.geeksforgeeks.org/sgn-value-polynomial/)

给定多项式函数 f(x) = 1+ a1*x + a2*(x^2) + … an(x^n).当给定 x 和所有系数时，求这些函数的 [Sgn](https://en.wikipedia.org/wiki/Sign_function) 值。

```
If value of polynomial greater than 0
   Sign = 1
Else If value of polynomial less than 0
   Sign = -1
Else if value of polynomial is 0
   Sign = 0
```

**例:**

```
Input: poly[] = [1, 2, 3] 
       x = 1 
Output:  1 
Explanation: f(1) = 6 which is > 0 
hence 1.

Input: poly[] = [1, -1, 2, 3] 
       x = -2 
Output: -1 
Explanation: f(-2)=-11 which is less 
then 0, hence -1.
```

一种**天真的**方法是计算 x 的每一次幂，然后通过乘以它的系数将其添加到答案中。计算 x 的幂需要 O(n)个时间，对于 n 个系数。因此，将总复杂性归结为 O(n * n)
一种**高效的**方法是使用[霍纳方法](https://www.geeksforgeeks.org/horners-method-polynomial-evaluation/)。我们使用霍纳方法评估多项式的值。然后我们根据值的符号返回值。
以下是上述方法的实施

## C++

```
// CPP program to find sign value of a
// polynomial
#include <iostream>
using namespace std;

// returns value of poly[0]x(n-1) + poly[1]x(n-2)
// + .. + poly[n-1]
int horner(int poly[], int n, int x)
{
    int result = poly[0];  // Initialize result

    // Evaluate value of polynomial
    // using Horner's method
    for (int i=1; i<n; i++)
        result = result*x + poly[i];

    return result;
}

// Returns sign value of polynomial
int findSign(int poly[], int n, int x)
{
   int result = horner(poly, n, x);
   if (result > 0)
      return 1;
   else if (result < 0)
      return -1;
   return 0;
}

// Driver program to test above function.
int main()
{
    // Let us evaluate value of 2x3 - 6x2
    // + 2x - 1 for x = 3
    int poly[] = {2, -6, 2, -1};
    int x = 3;
    int n = sizeof(poly)/sizeof(poly[0]);
    cout << "Sign of polynomial is "
         << findSign(poly, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sign value of a
// polynomial

class GFG
{
    // returns value of poly[0]x(n-1) + poly[1]x(n-2)
    // + .. + poly[n-1]
    static int horner(int poly[], int n, int x)
    {
        // Initialize result
        int result = poly[0];

        // Evaluate value of polynomial
        // using Horner's method
        for (int i = 1; i < n; i++)
            result = result * x + poly[i];

        return result;
    }

    // Returns sign value of polynomial
    static int findSign(int poly[], int n, int x)
    {
        int result = horner(poly, n, x);
        if (result > 0)
            return 1;
        else if (result < 0)
            return -1;
        return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        // Let us evaluate value of 2x3 - 6x2
        // + 2x - 1 for x = 3
        int poly[] = {2, -6, 2, -1};
        int x = 3;
        int n = poly.length;
        System.out.print("Sign of polynomial is "+
                              findSign(poly, n, x));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# sign value of a
# polynomial

# returns value of poly[0]x(n-1) +
# poly[1]x(n-2) + .. + poly[n-1]
def horner( poly, n, x):

    # Initialize result
    result = poly[0];

    # Evaluate value of
    # polynomial using
    # Horner's method
    for i in range(1,n):
        result = (result * x +
                     poly[i]);
    return result;

# Returns sign value
# of polynomial
def findSign(poly, n, x):
    result = horner(poly, n, x);
    if (result > 0):
        return 1;
    elif (result < 0):
        return -1;
    return 0;

# Driver Code

# Let us evaluate value
# of 2x3 - 6x2
# + 2x - 1 for x = 3
poly = [2, -6, 2, -1];
x = 3;
n = len(poly);

print("Sign of polynomial is ",
         findSign(poly, n, x));

# This code is contributed by mits
```

## C#

```
// C# program to find sign value of a
// polynomial
using System;

class GFG {

    // returns value of poly[0]x(n-1)
    // + poly[1]x(n-2) + .. + poly[n-1]
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

    // Returns sign value of polynomial
    static int findSign(int []poly, int n, int x)
    {

        int result = horner(poly, n, x);

        if (result > 0)
            return 1;
        else if (result < 0)
            return -1;

        return 0;
    }

    // Driver code
    public static void Main ()
    {

        // Let us evaluate value of 2x3 - 6x2
        // + 2x - 1 for x = 3
        int []poly = {2, -6, 2, -1};
        int x = 3;
        int n = poly.Length;

        Console.Write("Sign of polynomial is "
                      + findSign(poly, n, x));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sign value of a
// polynomial

// returns value of poly[0]x(n-1) +
// poly[1]x(n-2) + .. + poly[n-1]
function horner( $poly, $n, $x)
{

    // Initialize result
    $result = $poly[0];

    // Evaluate value of polynomial
    // using Horner's method
    for ($i = 1; $i < $n; $i++)
        $result = $result * $x + $poly[$i];

    return $result;
}

// Returns sign value
// of polynomial
function findSign($poly, $n, $x)
{
    $result = horner($poly, $n, $x);
    if ($result > 0)
        return 1;
    else if ($result < 0)
        return -1;
    return 0;
}

    // Driver Code
    // Let us evaluate value
    // of 2x3 - 6x2
    // + 2x - 1 for x = 3
    $poly = array(2, -6, 2, -1);
    $x = 3;
    $n = count($poly);
    echo "Sign of polynomial is "
        , findSign($poly, $n, $x);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sign value of a
// polynomial

// Returns value of poly[0]x(n-1) + poly[1]x(n-2)
// + .. + poly[n-1]
function horner(poly, n, x)
{

    // Initialize result
    var result = poly[0];

    // Evaluate value of polynomial
    // using Horner's method
    for(var i = 1; i < n; i++)
        result = result * x + poly[i];

    return result;
}

// Returns sign value of polynomial
function findSign(poly, n, x)
{
    var result = horner(poly, n, x);
    if (result > 0)
        return 1;
    else if (result < 0)
        return -1;

    return 0;
}

// Driver Code

// Let us evaluate value of 2x3 - 6x2
// + 2x - 1 for x = 3
var poly = [ 2, -6, 2, -1 ];
var x = 3;
var n = poly.length;

document.write("Sign of polynomial is "+
               findSign(poly, n, x));

// This code is contributed by kirti

</script>
```

**输出:**

```
Sign of polynomial is 1
```

**时间复杂度** : O(n)
本文由[**Raja vikramatitya**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。