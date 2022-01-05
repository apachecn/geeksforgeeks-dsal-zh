# 用等分法求一个数的第 n 个根

> 原文:[https://www . geeksforgeeks . org/find-n-number-root-use-divisioning-method/](https://www.geeksforgeeks.org/find-nth-root-of-a-number-using-bisection-method/)

给定两个正整数 **N** 和 **P** 。任务是找到 **P** 的 **N** 根。

**示例:**

> **输入:** P = 1234321，N = 2
> **输出:** 1111
> **说明:**1234321 的平方根是 1111。
> 
> **输入:** P = 123456785，N = 20
> T3】输出: 2.53849

**方法:**有多种方法可以解决给定的问题。下面的算法基于数学概念[求根二等分法](https://www.geeksforgeeks.org/program-for-bisection-method/)。为了求出给定数 P 的第 N 次幂根 **N** ，我们将在 **x** 中形成一个方程作为(**x<sup>P</sup>–P = 0**)，目标是用二等分法求出这个方程的正根。

**等分法是如何工作的？**
取一个区间 **(a，b)** 这样就已经知道根是存在于那个区间的。之后，找到区间的**中间**，检查函数值及其在 **x =中间的导数。**

*   如果函数值为 0，则表示找到了根
*   如果函数值为正，其导数为负，这意味着根位于**的右半部分。**
*   如果函数值为正，其导数为正，这意味着根位于**的左半部分。**

下面是上述方法的实现:

## C++14

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the value
// of the function at a given value of x
double f(double x, int p, double num)
{
    return pow(x, p) - num;
}
// calculating the value
// of the differential of the function
double f_prime(double x, int p)
{
    return p * pow(x, p - 1);
}

// The function that returns
// the root of given number
double root(double num, int p)
{

    // Defining range
    // on which answer can be found
    double left = -num;
    double right = num;

    double x;
    while (true) {

        // finding mid value
        x = (left + right) / 2.0;
        double value = f(x, p, num);
        double prime = f_prime(x, p);
        if (value * prime <= 0)
            left = x;
        else
            right = x;
        if (value < 0.000001 && value >= 0) {
            return x;
        }
    }
}

// Driver code
int main()
{

    double P = 1234321;
    int N = 2;

    double ans = root(P, N);
    cout << ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function that returns the value
  // of the function at a given value of x
  static double f(double x, int p, double num)
  {
      return Math.pow(x, p) - num;
  }

  // calculating the value
  // of the differential of the function
  static double f_prime(double x, int p)
  {
      return p * Math.pow(x, p - 1);
  }

  // The function that returns
  // the root of given number
  static double root(double num, int p)
  {

      // Defining range
      // on which answer can be found
      double left = -num;
      double right = num;

      double x;
      while (true) {

          // finding mid value
          x = (left + right) / 2.0;
          double value = f(x, p, num);
          double prime = f_prime(x, p);
          if (value * prime <= 0)
              left = x;
          else
              right = x;
          if (value < 0.000001 && value >= 0) {
              return x;
          }
      }
  }

  // Driver code
  public static void main(String args[])
  {

      double P = 1234321;
      int N = 2;

      double ans = root(P, N);
      System.out.print(ans);
  }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# python program for above approach

# Function that returns the value
# of the function at a given value of x
def f(x, p, num):

    return pow(x, p) - num

# calculating the value
# of the differential of the function
def f_prime(x, p):

    return p * pow(x, p - 1)

# The function that returns
# the root of given number
def root(num, p):

    # Defining range
    # on which answer can be found
    left = -num
    right = num

    x = 0
    while (True):

        # finding mid value
        x = (left + right) / 2.0
        value = f(x, p, num)
        prime = f_prime(x, p)
        if (value * prime <= 0):
            left = x
        else:
            right = x
        if (value < 0.000001 and value >= 0):
            return x

# Driver code
if __name__ == "__main__":

    P = 1234321
    N = 2

    ans = root(P, N)
    print(ans)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

  // Function that returns the value
  // of the function at a given value of x
  static double f(double x, int p, double num)
  {
      return Math.Pow(x, p) - num;
  }

  // calculating the value
  // of the differential of the function
  static double f_prime(double x, int p)
  {
      return p * Math.Pow(x, p - 1);
  }

  // The function that returns
  // the root of given number
  static double root(double num, int p)
  {

      // Defining range
      // on which answer can be found
      double left = -num;
      double right = num;

      double x;
      while (true) {

          // finding mid value
          x = (left + right) / 2.0;
          double value = f(x, p, num);
          double prime = f_prime(x, p);
          if (value * prime <= 0)
              left = x;
          else
              right = x;
          if (value < 0.000001 && value >= 0) {
              return x;
          }
      }
  }

  // Driver code
  public static void Main(string []args)
  {

      double P = 1234321;
      int N = 2;

      double ans = root(P, N);
      Console.Write(ans);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function that returns the value
        // of the function at a given value of x
        function f(x, p, num) {
            return Math.pow(x, p) - num;
        }

        // calculating the value
        // of the differential of the function
        function f_prime(x, p) {
            return p * Math.pow(x, p - 1);
        }

        // The function that returns
        // the root of given number
        function root(num, p) {

            // Defining range
            // on which answer can be found
            let left = -num;
            let right = num;

            let x;
            while (true) {

                // finding mid value
                x = (left + right) / 2.0;
                let value = f(x, p, num);
                let prime = f_prime(x, p);
                if (value * prime <= 0)
                    left = x;
                else
                    right = x;
                if (value < 0.000001 && value >= 0) {
                    return x;
                }
            }
        }

        // Driver code
        let P = 1234321;
        let N = 2;

        let ans = Math.floor(root(P, N));
        document.write(ans);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
1111
```

**时间复杂度:** O(对数 P)。
**辅助空间:** O(1)。