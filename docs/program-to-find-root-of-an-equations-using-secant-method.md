# 用割线法求方程根的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-of-an-equations-in-secant-method/](https://www.geeksforgeeks.org/program-to-find-root-of-an-equations-using-secant-method/)

割线法用于求方程 f(x) = 0 的根。它是从根的两个不同估计 x1 和 x2 开始的。这是一个迭代过程，包括对根的线性插值。如果两个中间值之间的差值小于收敛因子，则迭代停止。

**示例:**

```
Input : equation = x3 + x - 1 
        x1 = 0, x2 = 1, E = 0.0001
Output : Root of the given equation = 0.682326
         No. of iteration=5
```

**算法**

```
Initialize: x1, x2, E, n         // E = convergence indicator
calculate f(x1),f(x2)

if(f(x1) * f(x2) = E); //repeat the loop until the convergence
    print 'x0' //value of the root
    print 'n' //number of iteration
}
else
    print "can not found a root in the given interval"
```

## C++

```
// C++ Program to find root of an
// equations using secant method
#include <bits/stdc++.h>
using namespace std;
// function takes value of x and returns f(x)
float f(float x)
{
    // we are taking equation as x^3+x-1
    float f = pow(x, 3) + x - 1;
    return f;
}

void secant(float x1, float x2, float E)
{
    float n = 0, xm, x0, c;
    if (f(x1) * f(x2) < 0) {
        do {
            // calculate the intermediate value
            x0 = (x1 * f(x2) - x2 * f(x1)) / (f(x2) - f(x1));

            // check if x0 is root of equation or not
            c = f(x1) * f(x0);

            // update the value of interval
            x1 = x2;
            x2 = x0;

            // update number of iteration
            n++;

            // if x0 is the root of equation then break the loop
            if (c == 0)
                break;
            xm = (x1 * f(x2) - x2 * f(x1)) / (f(x2) - f(x1));
        } while (fabs(xm - x0) >= E); // repeat the loop
                                // until the convergence

        cout << "Root of the given equation=" << x0 << endl;
        cout << "No. of iterations = " << n << endl;
    } else
        cout << "Can not find a root in the given interval";
}

// Driver code
int main()
{
    // initializing the values
    float x1 = 0, x2 = 1, E = 0.0001;
    secant(x1, x2, E);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find root of an
// equations using secant method
class GFG {

    // function takes value of x and
    // returns f(x)
    static float f(float x) {

        // we are taking equation
        // as x^3+x-1
        float f = (float)Math.pow(x, 3)
                               + x - 1;

        return f;
    }

    static void secant(float x1, float x2,
                                float E) {

        float n = 0, xm, x0, c;
        if (f(x1) * f(x2) < 0)
        {
            do {

                // calculate the intermediate
                // value
                x0 = (x1 * f(x2) - x2 * f(x1))
                            / (f(x2) - f(x1));

                // check if x0 is root of
                // equation or not
                c = f(x1) * f(x0);

                // update the value of interval
                x1 = x2;
                x2 = x0;

                // update number of iteration
                n++;

                // if x0 is the root of equation
                // then break the loop
                if (c == 0)
                    break;
                xm = (x1 * f(x2) - x2 * f(x1))
                            / (f(x2) - f(x1));

                // repeat the loop until the
                // convergence
            } while (Math.abs(xm - x0) >= E);

            System.out.println("Root of the" +
                    " given equation=" + x0);

            System.out.println("No. of "
                      + "iterations = " + n);
        }

        else
            System.out.print("Can not find a"
              + " root in the given interval");
    }

    // Driver code
    public static void main(String[] args) {

        // initializing the values
        float x1 = 0, x2 = 1, E = 0.0001f;
        secant(x1, x2, E);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Program to find root of an
# equations using secant method

# function takes value of x
# and returns f(x)
def f(x):

    # we are taking equation
    # as x^3+x-1
    f = pow(x, 3) + x - 1;
    return f;

def secant(x1, x2, E):
    n = 0; xm = 0; x0 = 0; c = 0;
    if (f(x1) * f(x2) < 0):
        while True:

            # calculate the intermediate value
            x0 = ((x1 * f(x2) - x2 * f(x1)) /
                            (f(x2) - f(x1)));

            # check if x0 is root of
            # equation or not
            c = f(x1) * f(x0);

            # update the value of interval
            x1 = x2;
            x2 = x0;

            # update number of iteration
            n += 1;

            # if x0 is the root of equation
            # then break the loop
            if (c == 0):
                break;
            xm = ((x1 * f(x2) - x2 * f(x1)) /
                            (f(x2) - f(x1)));

            if(abs(xm - x0) < E):
                break;

        print("Root of the given equation =",
                               round(x0, 6));
        print("No. of iterations = ", n);

    else:
        print("Can not find a root in ",
                   "the given interval");

# Driver code

# initializing the values
x1 = 0;
x2 = 1;
E = 0.0001;
secant(x1, x2, E);

# This code is contributed by mits
```

## C#

```
// C# Program to find root of an
// equations using secant method
using System;

class GFG {

    // function takes value of
    // x and returns f(x)
    static float f(float x)
    {

        // we are taking equation
        // as x^3+x-1
        float f = (float)Math.Pow(x, 3)
                                + x - 1;
        return f;
    }

    static void secant(float x1, float x2,
                    float E)                

    {

        float n = 0, xm, x0, c;
        if (f(x1) * f(x2) < 0)
        {
            do {

                // calculate the intermediate
                // value
                x0 = (x1 * f(x2) - x2 * f(x1))
                    / (f(x2) - f(x1));

                // check if x0 is root of
                // equation or not
                c = f(x1) * f(x0);

                // update the value of interval
                x1 = x2;
                x2 = x0;

                // update number of iteration
                n++;

                // if x0 is the root of equation
                // then break the loop
                if (c == 0)
                    break;
                xm = (x1 * f(x2) - x2 * f(x1))
                    / (f(x2) - f(x1));

                // repeat the loop until
                // the convergence
            } while (Math.Abs(xm - x0) >= E);

            Console.WriteLine("Root of the" +
                    " given equation=" + x0);

            Console.WriteLine("No. of " +
                              "iterations = " + n);
        }

        else
            Console.WriteLine("Can not find a" +
                              " root in the given interval");
    }

    // Driver code
    public static void Main(String []args)
    {

        // initializing the values
        float x1 = 0, x2 = 1, E = 0.0001f;
        secant(x1, x2, E);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find root of an
// equations using secant method

// function takes value of x
// and returns f(x)
function f( $x)
{

    // we are taking equation
    // as x^3+x-1
    $f = pow($x, 3) + $x - 1;
    return $f;
}

function secant($x1, $x2, $E)
{
    $n = 0; $xm;
    $x0; $c;
    if (f($x1) * f($x2) < 0)
    {
        do {

            // calculate the intermediate value
            $x0 = ($x1 * f($x2) - $x2 *
                  f($x1)) / (f($x2) - f($x1));

            // check if x0 is root
            // of equation or not
            $c = f($x1) * f($x0);

            // update the value of interval
            $x1 = $x2;
            $x2 = $x0;

            // update number of iteration
            $n++;

            // if x0 is the root of equation
            // then break the loop
            if ($c == 0)
                break;
            $xm = ($x1 * f($x2) - $x2 * f($x1)) /
                              (f($x2) - f($x1));

        // repeat the loop
        // until the convergence
        } while (abs($xm - $x0) >= $E);

        echo "Root of the given equation=". $x0."\n" ;
        echo "No. of iterations = ". $n ;

    } else
        echo "Can not find a root in the given interval";
}

// Driver code
{

    // initializing the values
    $x1 = 0; $x2 = 1;
    $E = 0.0001;
    secant($x1, $x2, $E);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript Program to find root of an
// equations using secant method

// function takes value of x and returns f(x)
function f(x)
{
    // we are taking equation as x^3+x-1
    let f = Math.pow(x, 3) + x - 1;
    return f;
}

function secant(x1, x2, E)
{
    let n = 0, xm, x0, c;
    if (f(x1) * f(x2) < 0) {
        do {
            // calculate the intermediate value
            x0 = (x1 * f(x2) - x2 * f(x1)) / (f(x2) - f(x1));

            // check if x0 is root of equation or not
            c = f(x1) * f(x0);

            // update the value of interval
            x1 = x2;
            x2 = x0;

            // update number of iteration
            n++;

            // if x0 is the root of equation then break the loop
            if (c == 0)
                break;
            xm = (x1 * f(x2) - x2 * f(x1)) / (f(x2) - f(x1));
        } while (Math.abs(xm - x0) >= E); // repeat the loop
                                // until the convergence

        document.write("Root of the given equation=" + x0.toFixed(6) + "<br>");
        document.write("No. of iterations = " + n + "<br>");
    } else
        document.write("Can not find a root in the given interval");
}

// Driver code
    // initializing the values
    let x1 = 0, x2 = 1, E = 0.0001;
    secant(x1, x2, E);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
Root of the given equation = 0.682326
No. of iterations = 5
```

时间复杂度= 0(1)

**参考**
[https://en.wikipedia.org/wiki/Secant_method](https://en.wikipedia.org/wiki/Secant_method)
本文由**尼提斯·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。