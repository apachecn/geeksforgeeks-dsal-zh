# 递归计算 e^x 的程序(使用泰勒级数)

> 原文:[https://www . geesforgeks . org/program-to-compute-ex-by-recursive/](https://www.geeksforgeeks.org/program-to-calculate-ex-by-recursion/)

指数函数的值可以用泰勒级数计算。

```
 = 1 + x/1! + /2! + /3! + ...... + until n terms
```

随着项数的增加，得到更精确的 e <sup>x</sup> 值。

要使用递归函数找到 e^x，我们需要使用静态变量。一个函数只能返回一个值，当我们需要在递归函数中包含多个值时，我们使用静态变量。泰勒级数是多个值的组合，如和、幂和阶乘项，因此我们将使用静态变量。

对于 x 的幂，我们将使用 p，对于阶乘，我们将使用 f 作为静态变量。

下面显示的函数用于增加 x 的幂。

```
p = p*x 
```

下面的函数用于寻找阶乘。

```
f = f*n
```

下面的函数用于计算级数的和。

```
r+p/f
```

其中 r 是对函数的递归调用。

以下是上述想法的实现。

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Recursive Function with static
// variables p and f
double e(int x, int n)
{
    static double p = 1, f = 1;
    double r;

    // Termination condition
    if (n == 0)
        return 1;

    // Recursive call
    r = e(x, n - 1);

    // Update the power of x
    p = p * x;

    // Factorial
    f = f * n;

    return (r + p / f);
}

// Driver code
int main()
{
    int x = 4, n = 15;
    cout<<"\n"<< e(x, n);

    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// C implementation of the approach
#include <stdio.h>

// Recursive Function with static
// variables p and f
double e(int x, int n)
{
    static double p = 1, f = 1;
    double r;

    // Termination condition
    if (n == 0)
        return 1;

    // Recursive call
    r = e(x, n - 1);

    // Update the power of x
    p = p * x;

    // Factorial
    f = f * n;

    return (r + p / f);
}

// Driver code
int main()
{
    int x = 4, n = 15;
    printf("%lf \n", e(x, n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.text.*;

class GFG {

    // Recursive Function with static
    // variables p and f
    static double p = 1, f = 1;
    static double e(int x, int n)
    {
        double r;

        // Termination condition
        if (n == 0)
            return 1;

        // Recursive call
        r = e(x, n - 1);

        // Update the power of x
        p = p * x;

        // Factorial
        f = f * n;

        return (r + p / f);
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 4, n = 15;
        DecimalFormat df = new DecimalFormat("0.######");
        System.out.println(df.format(e(x, n)));
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python implementation of the approach

# Recursive Function
# global variables p and f
p = 1.0
f = 1.0

def e(x, n):

    global p, f

    # Termination condition
    if (n == 0):
        return 1

    # Recursive call
    r = e(x, n - 1)

    # Update the power of x
    p = p * x

    # Factorial
    f = f * n

    return (r + p / f)

# Driver code

x = 4
n = 15
print(e(x, n))

# This contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Recursive Function with static
    // variables p and f
    static double p = 1, f = 1;
    static double e(int x, int n)
    {
        double r;

        // Termination condition
        if (n == 0)
            return 1;

        // Recursive call
        r = e(x, n - 1);

        // Update the power of x
        p = p * x;

        // Factorial
        f = f * n;

        return (r + p / f);
    }

    // Driver code
    static void Main()
    {
        int x = 4, n = 15;
        Console.WriteLine(Math.Round(e(x, n), 6));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Recursive Function with static
// variables p and f
p = 1, f = 1;
function e(x, n)
{
    var r;

    // Termination condition
    if (n == 0)
        return 1;

    // Recursive call
    r = e(x, n - 1);

    // Update the power of x
    p = p * x;

    // Factorial
    f = f * n;

    return (r + p / f);
}

// Driver Code
var x = 4, n = 15;
var res = e(x, n);

document.write(res.toFixed(6));

// This code is contributed by kirti

</script>
```

**Output:** 

```
54.597883
```

**时间复杂度:**

为了找到这一点，我们将确定执行的总乘法。

e^x = 1 + x/1！+ x^2/2！+ x^3/3！++直到 n 个术语

= 1+x/1+x * x/1 * 2+x * x * x/1 * 2 * 3+x * x * x * x/1 * 2 * 3 * 4……+直到 n 个术语

0 0 2 4 8 上述项的乘法次数

因此，对于 n 项，所执行的总乘法相当于 n 个自然数的和(因为形成了偶数的并行序列)。

我们知道 n 个自然数的和= n*(n+1)/2，其阶为 n <sup>2</sup>

因此，如果该方法为 0(n<sup>2</sup>，则时间复杂度为 0)

**辅助空间:**

递归调用将发生 n + 1 次，因此最多将创建 n+1 个激活记录。这说明空间复杂度是 O(n)。