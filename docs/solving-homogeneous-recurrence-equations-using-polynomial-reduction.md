# 利用多项式约简求解齐次递推方程

> 原文:[https://www . geesforgeks . org/求解-齐次-递推-方程-使用-多项式-约简/](https://www.geeksforgeeks.org/solving-homogeneous-recurrence-equations-using-polynomial-reduction/)

一个**递归关系**是一个[方程](https://en.wikipedia.org/wiki/Equation)，一旦给出一个或多个初始项，[递归地](https://en.wikipedia.org/wiki/Recursion)定义一个[序列](https://en.wikipedia.org/wiki/Sequence)或多维数组的值；序列或数组的每个进一步的项被定义为前述项的[函数](https://en.wikipedia.org/wiki/Function_(mathematics))。以下是使用多项式归约方法求解递归方程所需的步骤:

1.  对于给定的递推方程，形成一个特征方程。
2.  求解特征方程，求特征方程的根。
3.  用未知系数简化解。
4.  根据初始条件求解方程，得到具体的解。

**例:**
考虑以下二阶递推方程:

```
*T(n) = a<sub>1</sub>T(n-1) + a<sub>2</sub>T(n-2)*
```

为了求解这个方程，把它写成一个特征方程。
让我们重新排列等式如下:

```
*T(n) - a<sub>1</sub>T(n-1) - a<sub>2</sub>T(n-2) = 0*
```

设， *T(n) = x <sup>n</sup>*
现在我们可以说*T(n-1)= x<sup>n-1</sup>T8】和*T(n-2)= x<sup>n-2</sup>*T13】现在等式将为:*

```
*x<sup>n</sup> + a<sub>1</sub>x<sup>n-1</sup> + a<sub>2</sub>x<sup>n-2</sup>  = 0*
```

将整个方程除以 *x <sup>n-2</sup>* 【由于 *x* 不等于 *0* ，我们得到:

```
*x<sup>2</sup> + a<sub>1</sub>x + a<sub>2</sub> = 0*
```

我们得到的特征方程为*x<sup>2</sup>+a<sub>1</sub>x+a<sub>2</sub>= 0*
现在，求这个方程的根。
在求特征方程的根时，可能存在三种情况，它们是:

**情况 1:特征方程的根是真实且不同的**
如果特征方程有 *r* 个不同的根，那么可以说 *r* 个基本解是可能的。人们可以用任意线性组合的根来得到线性递归方程的通解。

如果 *r <sub>1</sub> ，r <sub>2</sub> ，r <sub>3</sub> ……，r <sub>k</sub>* 是特征方程的根，则递推方程的通解为:

```
*t<sub>n</sub> = c<sub>1</sub>r<sub>1</sub><sup>n</sup> + c<sub>2</sub>r<sub>2</sub><sup>n</sup> + c<sub>3</sub>r<sub>3</sub><sup>n</sup> +...........+ c<sub>k</sub>r<sub>k</sub><sup>n</sup>*
```

**情况 2:特征方程的根是实的但不分明**
我们考虑特征方程的根不分明，根 r 在 m 的重数内，这种情况下，特征方程的解将是:

```
*r<sub>1</sub> = r<sup>n</sup>*
*r<sub>2</sub> = nr<sup>n</sup>*
*r<sub>3</sub> = n<sup>2</sup>r<sup>n</sup>*
*.........*
*r<sub>m</sub> = n<sup>m-1</sup>r<sup>n</sup>*
```

因此，包括所有的解，以得到给定递归方程的一般解。

**情况 3:特征方程的根是不同的但不是真实的**
如果特征方程的根是复数，那么求根的共轭对。
如果 *r <sub>1</sub>* 和 *r <sub>2</sub>* 是特征方程的两个根，并且它们彼此共轭，则可以表示为:

```
*r<sub>1</sub> = re<sup>ix</sup>*
*r<sub>2</sub> = re<sup>-ix</sup>*
```

一般解决方案是:

```
*t<sub>n</sub> =* rn*(c<sub>1</sub>cos nx + c<sub>2</sub>sin nx)*
```

**示例:**

让我们求解给定的递归关系:

```
*T(n) = 7*T(n-1) - 12*T(n-2)*
```

让 T(n) = x <sup>n</sup>
现在我们可以说 T(n-1) = x <sup>n-1</sup> 和 T(n-2)=x <sup>n-2</sup>
并将整个方程除以 x <sup>n-2</sup> ，我们得到:

```
*x<sup>2</sup> - 7*x + 12 = 0*
```

下面是求解给定二次方程的实现:

## C++

```
// C++ program to find roots
// of a quadratic equation
#include<bits/stdc++.h>
using namespace std;

class Quadratic{

public:

// Prints roots of quadratic
// equation ax * 2 + bx + x
void findRoots(int a, int b, int c)
{

    // If a is 0, then equation is not
    // quadratic, but linear
    if (a == 0)
    {
        cout << "Invalid";
        return;
    }

    int d = b * b - 4 * a * c;
    float sqrt_val = sqrt(abs(d));

    // Real Roots
    if (d > 0)
    {
       cout << "Roots are real and different" << endl;
       cout << fixed << std::setprecision(1)
            << float((-b + sqrt_val) / (2 * a)) << endl;
       cout << fixed << std::setprecision(1)
            << float((-b - sqrt_val) / (2 * a)) << endl;
    }

    // Imaginary Roots
    else
    {
        cout << "Roots are complex" << endl;
        cout << fixed << std::setprecision(1)
             << float(b / (2.0 * a)) << " + i"
             << sqrt_val << endl;
        cout << fixed << std::setprecision(1)
             << float(b / (2.0 * a)) << " - i"
             << sqrt_val << endl;
    }
}
};

// Driver code
int main()
{
    Quadratic obj;

    // Given value of coefficients
    int a = 1, b = -7, c = 12;

    obj.findRoots(a, b, c);
}

// This code is contributed by SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find roots
// of a quadratic equation
import java.io.*;
import static java.lang.Math.*;
class Quadratic {

    // Prints roots of quadratic
    // equation ax * 2 + bx + x
    void findRoots(int a, int b, int c)
    {
        // If a is 0, then equation is not
        // quadratic, but linear
        if (a == 0) {
            System.out.println("Invalid");
            return;
        }

        int d = b * b - 4 * a * c;
        double sqrt_val = sqrt(abs(d));

        // Real Roots
        if (d > 0) {
            System.out.println(
                "Roots are real"
                + " and different \n");

            System.out.println(
                (double)(-b + sqrt_val)
                    / (2 * a)
                + "\n"

                + (double)(-b - sqrt_val)
                      / (2 * a));
        }

        // Imaginary Roots
        else {
            System.out.println(
                "Roots are complex \n");

            System.out.println(
                -(double)b / (2 * a)
                + " + i"
                + sqrt_val + "\n"
                + -(double)b / (2 * a)
                + " - i" + sqrt_val);
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Quadratic obj = new Quadratic();

        // Given value of coefficients
        int a = 1, b = -7, c = 12;
        obj.findRoots(a, b, c);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find roots
# of a quadratic equation
from math import sqrt

# Prints roots of quadratic
# equation ax * 2 + bx + x
def findRoots(a, b, c):

    # If a is 0, then equation is not
    # quadratic, but linear
    if (a == 0):
        print("Invalid")
        return

    d = b * b - 4 * a * c
    sqrt_val = sqrt(abs(d))

    # Real Roots
    if (d > 0):
        print("Roots are real and different")

        print((-b + sqrt_val) / (2 * a))
        print((-b - sqrt_val) / (2 * a))

    # Imaginary Roots
    else:
        print("Roots are complex \n")

        print(-b / (2 * a), " +  i",
              sqrt_val, "\n",
              -b / (2 * a), " - i",
              sqrt_val)

# Driver code
if __name__ == '__main__':

    # Given value of coefficients
    a = 1
    b = -7
    c = 12

    findRoots(a, b, c)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find roots
// of a quadratic equation
using System;
class Quadratic{

// Prints roots of quadratic
// equation ax * 2 + bx + x
void findRoots(int a,
               int b, int c)
{
  // If a is 0, then equation
  // is not quadratic, but linear
  if (a == 0)
  {
    Console.WriteLine("Invalid");
    return;
  }

  int d = b * b - 4 *
          a * c;
  double sqrt_val =
         Math.Sqrt(Math.Abs(d));

  // Real Roots
  if (d > 0)
  {
    Console.WriteLine("Roots are real" +
                      " and different \n");

    Console.WriteLine((double)
                      (-b + sqrt_val) /
                      (2 * a) + "\n" +
                      (double)
                      (-b - sqrt_val) /
                      (2 * a));
  }

  // Imaginary Roots
  else
  {
    Console.WriteLine("Roots are complex \n");

    Console.WriteLine(-(double)b / (2 * a) +
                      " + i" + sqrt_val +
                      "\n" + -(double)b /
                      (2 * a) + " - i" +
                      sqrt_val);
  }
}

// Driver code
public static void Main(String []args)
{
  Quadratic obj = new Quadratic();

  // Given value of coefficients
  int a = 1, b = -7, c = 12;
  obj.findRoots(a, b, c);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to find roots
// of a quadratic equation

// Prints roots of quadratic
// equation ax * 2 + bx + x
function findRoots(a, b, c)
{

    // If a is 0, then equation is not
        // quadratic, but linear
        if (a == 0) {
            document.write("Invalid");
            return;
        }

        let d = b * b - 4 * a * c;
        let sqrt_val = Math.sqrt(Math.abs(d));

        // Real Roots
        if (d > 0) {
            document.write(
                "Roots are real"
                + " and different <br>");

            document.write(
                (-b + sqrt_val)
                    / (2 * a)
                + "<br>"

                + (-b - sqrt_val)
                      / (2 * a));
        }

        // Imaginary Roots
        else {
            document.write(
                "Roots are complex <bR>");

            document.write(
                -b / (2 * a)
                + " + i"
                + sqrt_val + "<br>"
                + -b / (2 * a)
                + " - i" + sqrt_val);
        }
}

// Driver code
// Given value of coefficients
let a = 1, b = -7, c = 12;
findRoots(a, b, c);

// This code is contributed by unknown2108
</script>
```

**Output**

```
Roots are real and different
4.0
3.0
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*