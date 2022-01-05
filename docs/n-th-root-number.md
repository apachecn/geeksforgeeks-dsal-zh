# 一个数的第 N 个根

> 原文:[https://www.geeksforgeeks.org/n-th-root-number/](https://www.geeksforgeeks.org/n-th-root-number/)

给定两个数 N 和 A，求 A 的第 N 个根，在数学中，数 A 的第 N 个根是给出 A 的实数，当我们把它提升到整数的 N 次方时，这些根用于数论和数学的其他高级分支。
更多信息请参考[维基](https://en.wikipedia.org/wiki/Nth_root)页面。
**示例:**

```
Input : A = 81
        N = 4
Output : 3 
3^4 = 81
```

由于这个问题涉及实值函数 A^(1/N)，我们可以使用[牛顿法](https://www.geeksforgeeks.org/program-for-newton-raphson-method/)来解决这个问题，该方法从最初的猜测开始，并向结果迭代移动。
我们可以使用牛顿法推导出两个连续迭代值之间的关系如下:

```
according to newton’s method
x(K+1) = x(K) – f(x) / f’(x)        
here    f(x)  = x^(N) – A
so    f’(x) = N*x^(N - 1)
and     x(K) denoted the value of x at Kth iteration
putting the values and simplifying we get,
x(K + 1) = (1 / N) * ((N - 1) * x(K) + A / x(K) ^ (N - 1))
```

利用上述关系，我们可以解决给定的问题。在下面的代码中，我们迭代 x 的值，直到 x 的两个连续值之间的差变得低于期望的精度。
以下是上述方法的实施:

## C++

```
// C++ program to calculate Nth root of a number
#include <bits/stdc++.h>
using namespace std;

//  method returns Nth power of A
double nthRoot(int A, int N)
{
    // initially guessing a random number between
    // 0 and 9
    double xPre = rand() % 10;

    //  smaller eps, denotes more accuracy
    double eps = 1e-3;

    // initializing difference between two
    // roots by INT_MAX
    double delX = INT_MAX;

    //  xK denotes current value of x
    double xK;

    //  loop until we reach desired accuracy
    while (delX > eps)
    {
        //  calculating current value from previous
        // value by newton's method
        xK = ((N - 1.0) * xPre +
              (double)A/pow(xPre, N-1)) / (double)N;
        delX = abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

//    Driver code to test above methods
int main()
{
    int N = 4;
    int A = 81;

    double nthRootValue = nthRoot(A, N);
    cout << "Nth root is " << nthRootValue << endl;

    /*
        double Acalc = pow(nthRootValue, N);
        cout << "Error in difference of powers "
             << abs(A - Acalc) << endl;
    */

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate Nth root of a number
class GFG
{

    // method returns Nth power of A
    static double nthRoot(int A, int N)
    {

        // initially guessing a random number between
        // 0 and 9
        double xPre = Math.random() % 10;

        // smaller eps, denotes more accuracy
        double eps = 0.001;

        // initializing difference between two
        // roots by INT_MAX
        double delX = 2147483647;

        // xK denotes current value of x
        double xK = 0.0;

        // loop until we reach desired accuracy
        while (delX > eps)
        {
            // calculating current value from previous
            // value by newton's method
            xK = ((N - 1.0) * xPre +
            (double)A / Math.pow(xPre, N - 1)) / (double)N;
            delX = Math.abs(xK - xPre);
            xPre = xK;
        }

        return xK;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 4;
        int A = 81;

        double nthRootValue = nthRoot(A, N);
        System.out.println("Nth root is "
        + Math.round(nthRootValue*1000.0)/1000.0);

        /*
            double Acalc = pow(nthRootValue, N);
            cout << "Error in difference of powers "
                << abs(A - Acalc) << endl;
        */
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to calculate
# Nth root of a number
import math
import random

# method returns Nth power of A
def nthRoot(A,N):

    # initially guessing a random number between
    # 0 and 9
    xPre = random.randint(1,101) % 10

    #  smaller eps, denotes more accuracy
    eps = 0.001

    # initializing difference between two
    # roots by INT_MAX
    delX = 2147483647

    #  xK denotes current value of x
    xK=0.0

    #  loop until we reach desired accuracy
    while (delX > eps):

        # calculating current value from previous
        # value by newton's method
        xK = ((N - 1.0) * xPre +
              A/pow(xPre, N-1)) /N
        delX = abs(xK - xPre)
        xPre = xK;

    return xK

# Driver code
N = 4
A = 81
nthRootValue = nthRoot(A, N)

print("Nth root is ", nthRootValue)

## Acalc = pow(nthRootValue, N);
## print("Error in difference of powers ",
##             abs(A - Acalc))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to calculate Nth root of a number
using System;
class GFG
{

    // method returns Nth power of A
    static double nthRoot(int A, int N)
    {
        Random rand = new Random();
        // initially guessing a random number between
        // 0 and 9
        double xPre = rand.Next(10);;

        // smaller eps, denotes more accuracy
        double eps = 0.001;

        // initializing difference between two
        // roots by INT_MAX
        double delX = 2147483647;

        // xK denotes current value of x
        double xK = 0.0;

        // loop until we reach desired accuracy
        while (delX > eps)
        {
            // calculating current value from previous
            // value by newton's method
            xK = ((N - 1.0) * xPre +
            (double)A / Math.Pow(xPre, N - 1)) / (double)N;
            delX = Math.Abs(xK - xPre);
            xPre = xK;
        }

        return xK;
    }

    // Driver code
    static void Main()
    {
        int N = 4;
        int A = 81;

        double nthRootValue = nthRoot(A, N);
        Console.WriteLine("Nth root is "+Math.Round(nthRootValue*1000.0)/1000.0);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// Nth root of a number

// method returns
// Nth power of A
function nthRoot($A, $N)
{
    // initially guessing a
    // random number between
    // 0 and 9
    $xPre = rand() % 10;

    // smaller eps, denotes
    // more accuracy
    $eps = 0.001;

    // initializing difference
    // between two roots by INT_MAX
    $delX = PHP_INT_MAX;

    // xK denotes current
    // value of x
    $xK;

    // loop until we reach
    // desired accuracy
    while ($delX > $eps)
    {
        // calculating current
        // value from previous
        // value by newton's method
        $xK = ((int)($N - 1.0) *
                     $xPre + $A /
                     (int)pow($xPre,
                              $N - 1)) / $N;
        $delX = abs($xK - $xPre);
        $xPre = $xK;
    }

    return floor($xK);
}

// Driver code
$N = 4;
$A = 81;

$nthRootValue = nthRoot($A, $N);
echo "Nth root is " ,
      $nthRootValue ,"\n";

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // method returns Nth power of A
    function nthRoot(A, N)
    {

        // initially guessing a random number between
        // 0 and 9
        let xPre = Math.random() % 10;

        // smaller eps, denotes more accuracy
        let eps = 0.001;

        // initializing difference between two
        // roots by INT_MAX
        let delX = 2147483647;

        // xK denotes current value of x
        let xK = 0.0;

        // loop until we reach desired accuracy
        while (delX > eps)
        {
            // calculating current value from previous
            // value by newton's method
            xK = ((N - 1.0) * xPre +
            A / Math.pow(xPre, N - 1)) / N;
            delX = Math.abs(xK - xPre);
            xPre = xK;
        }

        return xK;
    }

// Driver Code

        let N = 4;
        let A = 81;

        let nthRootValue = nthRoot(A, N);
        document.write("Nth root is "+Math.round(nthRootValue*1000.0)/1000.0);

</script>
```

**输出:**

```
Nth root is 3
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。