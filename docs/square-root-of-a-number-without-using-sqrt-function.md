# 不使用 sqrt()函数的数的平方根

> 原文:[https://www . geeksforgeeks . org/不使用-sqrt-function 的数字平方根/](https://www.geeksforgeeks.org/square-root-of-a-number-without-using-sqrt-function/)

给定一个数字 **N** ，任务是在不使用 [sqrt()](https://www.geeksforgeeks.org/sqrt-sqrtl-sqrtf-cpp/) 函数的情况下求 **N** 的平方根。

**示例:**

> **输入:**N = 25
> T3】输出: 5
> 
> **输入:**N = 3
> T3】输出: 1.73205
> 
> **输入:**N = 2.5
> T3】输出: 1.58114

**进场:**

*   从 i = 1 开始迭代。如果 **i * i = n** ，则将 **i** 打印为 **n** 是一个平方根为 **i** 的完美正方形。
*   否则找到最小的 **i** ，对于它 **i * i** 严格大于 **n** 。
*   现在我们知道 **n** 的平方根在区间**I–1**和 **i** 内，可以用二分搜索法算法求平方根。
*   找到**I–1**和 **i** 的中间，并将**中间*中间**与 **n** 进行比较，精度可达小数点后 5 位。
    1.  如果**中间*中间= n** 则返回**中间**。
    2.  如果**中*中< n** 然后在下半场重现。
    3.  如果**中间*中间> n** 那么上半年重现。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function that returns square root
// of a number with precision upto 5 decimal places
double Square(double n, double i, double j)
{
    double mid = (i + j) / 2;
    double mul = mid * mid;

    // If mid itself is the square root,
    // return mid
    if ((mul == n) || (abs(mul - n) < 0.00001))
        return mid;

    // If mul is less than n, recur second half
    else if (mul < n)
        return Square(n, mid, j);

    // Else recur first half
    else
        return Square(n, i, mid);
}

// Function to find the square root of n
void findSqrt(double n)
{
    double i = 1;

    // While the square root is not found
    bool found = false;
    while (!found) {

        // If n is a perfect square
        if (i * i == n) {
            cout << fixed << setprecision(0) << i;
            found = true;
        }
        else if (i * i > n) {

            // Square root will lie in the
            // interval i-1 and i
            double res = Square(n, i - 1, i);
            cout << fixed << setprecision(5) << res;
            found = true;
        }
        i++;
    }
}

// Driver code
int main()
{
    double n = 3;

    findSqrt(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Recursive function that returns
// square root of a number with
// precision upto 5 decimal places
static double Square(double n,
                     double i, double j)
{
    double mid = (i + j) / 2;
    double mul = mid * mid;

    // If mid itself is the square root,
    // return mid
    if ((mul == n) ||  
        (Math.abs(mul - n) < 0.00001))
        return mid;

    // If mul is less than n,
    // recur second half
    else if (mul < n)
        return Square(n, mid, j);

    // Else recur first half
    else
        return Square(n, i, mid);
}

// Function to find the square root of n
static void findSqrt(double n)
{
    double i = 1;

    // While the square root is not found
    boolean found = false;
    while (!found)
    {

        // If n is a perfect square
        if (i * i == n)
        {
            System.out.println(i);
            found = true;
        }

        else if (i * i > n)
        {

            // Square root will lie in the
            // interval i-1 and i
            double res = Square(n, i - 1, i);
            System.out.printf("%.5f", res);
            found = true;
        }
        i++;
    }
}

// Driver code
public static void main(String[] args)
{
    double n = 3;

    findSqrt(n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Recursive function that returns square root
# of a number with precision upto 5 decimal places
def Square(n, i, j):

    mid = (i + j) / 2;
    mul = mid * mid;

    # If mid itself is the square root,
    # return mid
    if ((mul == n) or (abs(mul - n) < 0.00001)):
        return mid;

    # If mul is less than n, recur second half
    elif (mul < n):
        return Square(n, mid, j);

    # Else recur first half
    else:
        return Square(n, i, mid);

# Function to find the square root of n
def findSqrt(n):
    i = 1;

    # While the square root is not found
    found = False;
    while (found == False):

        # If n is a perfect square
        if (i * i == n):
            print(i);
            found = True;

        elif (i * i > n):

            # Square root will lie in the
            # interval i-1 and i
            res = Square(n, i - 1, i);
            print ("{0:.5f}".format(res))
            found = True
        i += 1;

# Driver code
if __name__ == '__main__':
    n = 3;

    findSqrt(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Recursive function that returns
// square root of a number with
// precision upto 5 decimal places
static double Square(double n,
                     double i, double j)
{
    double mid = (i + j) / 2;
    double mul = mid * mid;

    // If mid itself is the square root,
    // return mid
    if ((mul == n) ||
        (Math.Abs(mul - n) < 0.00001))
        return mid;

    // If mul is less than n,
    // recur second half
    else if (mul < n)
        return Square(n, mid, j);

    // Else recur first half
    else
        return Square(n, i, mid);
}

// Function to find the square root of n
static void findSqrt(double n)
{
    double i = 1;

    // While the square root is not found
    Boolean found = false;
    while (!found)
    {

        // If n is a perfect square
        if (i * i == n)
        {
            Console.WriteLine(i);
            found = true;
        }

        else if (i * i > n)
        {

            // Square root will lie in the
            // interval i-1 and i
            double res = Square(n, i - 1, i);
            Console.Write("{0:F5}", res);
            found = true;
        }
        i++;
    }
}

// Driver code
public static void Main(String[] args)
{
    double n = 3;

    findSqrt(n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Recursive function that returns
// square root of a number with
// precision upto 5 decimal places
function Square(n, i, j)
{
    var mid = ((i + j) / 2);
    var mul = mid * mid;

    // If mid itself is the square root,
    // return mid
    if ((mul == n) || (Math.abs(mul - n) < 0.00001))
        return mid;

    // If mul is less than n,
    // recur second half
    else if (mul < n)
        return Square(n, mid, j);

    // Else recur first half
    else
        return Square(n, i, mid);
}

// Function to find the square root of n
function findSqrt(n)
{
    var i = 1;

    // While the square root is not found
    var found = false;
    while (!found)
    {

        // If n is a perfect square
        if (i * i == n)
        {
            document.write(i);
            found = true;
        }

        else if (i * i > n)
        {

            // Square root will lie in the
            // interval i-1 and i
            var res = Square(n, i - 1, i);
            document.write(res.toFixed(5));
            found = true;
        }
        i++;
    }
}

// Driver code
var n = 3;

findSqrt(n);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
1.73205
```