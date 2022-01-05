# 系列 1 + x/1 + x^2/2 + x^3/3 +的和..+ x^n/n

> 原文:[https://www.geeksforgeeks.org/sum-series-1-x1-x22-x33-xnn/](https://www.geeksforgeeks.org/sum-series-1-x1-x22-x33-xnn/)

这是一个数学级数程序，用户必须输入级数求和的项数。接下来，我们还需要 x 的值，它构成了级数的基础。
**例:**

```
Input : base = 2, range = 5
Output : 18.07

Input : base = 1, range = 10
Output : 3.93
```

**方法 1(简单)**我们只需要按照级数，把基数的值放在 x，取值范围放在 n，就可以得到和。

## C++

```
// C++ program to find sum of series
// 1 + x/1 + x^2/2 + x^3/3 + ....+ x^n/n
#include <math.h>
#include <iostream>
#include <boost/format.hpp>
class gfg
{
public :
double sum(int x, int n)
{
    double i, total = 1.0;
    for (i = 1; i <= n; i++)
        total = total +
                (pow(x, i) / i);
    return total;
}
};
// Driver code
int main()
{
    gfg g;
    int x = 2;
    int n = 5;
    //std::cout<<g.sum(x,n);
    std::cout << boost::format("%.2f") % g.sum(x,n);
    return 0;
}
```

## C

```
// C program to find sum of series
// 1 + x/1 + x^2/2 + x^3/3 + ....+ x^n/n
#include <math.h>
#include <stdio.h>

double sum(int x, int n)
{
    double i, total = 1.0;
    for (i = 1; i <= n; i++)
        total = total +
                (pow(x, i) / i);
    return total;
}

// Driver code
int main()
{
    int x = 2;
    int n = 5;
    printf("%.2f", sum(x, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of series
// 1 + 1/x + x^2/2 + x^3/3 + ....+ x^n/n
import static java.lang.Math.pow;

class GFG
{

// Java code to print the
// sum of the series
static double sum(int x, int n)
{
    double i, total = 1.0;
    for (i = 1; i <= n; i++)
        total = total +
                (Math.pow(x, i) / i);

    return total;
}

// Driver code
public static void main(String[] args)
{
    int x = 2;
    int n = 5;
    System.out.printf("%.2f", sum(x, n));
}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 code to find sum of series
# 1 + x/1 + x^2/2 + x^3/3 + .. .+ x^n/n

def SUM(x, n):
    total = 1
    for i in range(1, n + 1):
        total = total + ((x**i)/i)
    return total

# Driver Code
x = 2
n = 5
s = SUM(x, n)
print(round(s, 2))
```

## C#

```
// C# program to find sum of series
// 1 + 1/x + x^2/2 + x^3/3 + ....+ x^n/n
using System;

class GFG
{

    // Java code to print the
    // sum of the series
    static float sum(int x, int n)
    {
        double i, total = 1.0;
        for (i = 1; i <= n; i++)
            total = total +
                    (Math.Pow(x, i) / i);

        return (float)total;
    }

    // Driver code
    public static void Main()
    {
        int x = 2;
        int n = 5;
        Console.WriteLine(sum(x, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of series
// 1 + x/1 + x^2/2 + x^3/3 + ....+ x^n/n

// Code to print the sum
// of the series
function sum($x, $n)
{
    $i; $total = 1.0;
    for ($i = 1; $i <= $n; $i++)
        $total = $total +
                 (pow($x, $i) / $i);
    return $total;
}

// Driver code
$x = 2;
$n = 5;
echo(sum($x, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find sum of series
// 1 + x/1 + x^2/2 + x^3/3 + ....+ x^n/n
function sum(x, n)
{
    let i, total = 1.0;
    for (i = 1; i <= n; i++)
        total = total +
                (Math.pow(x, i) / i);
    return total;
}

// Driver code
    let g;
    let x = 2;
    let n = 5;
    document.write(sum(x, n).toFixed(2));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
18.07
```

**方法 2(优化)**我们可以避免使用 pow()函数，重新使用之前计算的功率。

## C++

```
// C++ program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n
#include <bits/stdc++.h>
using namespace std;

// C++ code to print the sum
// of the series
double sum(int x, int n)
{
    double i, total = 1.0, multi = x;
    for (i = 1; i <= n; i++)
    {
        total = total + multi / i;
        multi = multi * x;
    }
    return total;
}

// Driver code
int main()
{
    int x = 2;
    int n = 5;
    cout << fixed << setprecision(2) << sum(x, n);
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n
#include <math.h>
#include <stdio.h>

// C code to print the sum
// of the series
double sum(int x, int n)
{
    double i, total = 1.0, multi = x;
    for (i = 1; i <= n; i++) {
        total = total + multi / i;
        multi = multi * x;
    }
    return total;
}

// Driver code
int main()
{
    int x = 2;
    int n = 5;
    printf("%.2f", sum(x, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n

class GFG
{

// Java code to print the sum
// of the given series
static double sum(int x, int n)
{
    double i, total = 1.0, multi = x;
    for (i = 1; i <= n; i++)
    {
        total = total + multi / i;
        multi = multi * x;
    }
    return total;
}

// Driver code
public static void main(String[] args)
{
    int x = 2;
    int n = 5;
    System.out.printf("%.2f", sum(x, n));
}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to find sum of series
# 1 + x^2/2 + x^3/3 + ....+ x^n/n

# Python 3 code to print the
# sum of the series
def sum(x, n):

    total = 1.0
    multi = x
    for i in range(1, n+1):
        total = total + multi / i
        multi = multi * x

    return total

# Driver code
x = 2
n = 5
print(round(sum(x, n), 2))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n
using System;

class GFG
{

    // Java code to print the sum
    // of the given series
    static float sum(int x, int n)
    {
        double i, total = 1.0, multi = x;
        for (i = 1; i <= n; i++)
        {
            total = total + multi / i;
            multi = multi * x;
        }
        return (float)total;
    }

    // Driver code
    public static void Main()
    {
        int x = 2;
        int n = 5;
        Console.WriteLine(sum(x, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n

// code to print the sum
// of the series
function sum($x, $n)
{
    $i; $total = 1.0; $multi = $x;
    for ($i = 1; $i <= $n; $i++)
    {
        $total = $total + $multi / $i;
        $multi = $multi * $x;
    }
    return $total;
}

// Driver code
$x = 2;
$n = 5;
echo(sum($x, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript  program to find sum of series
// 1 + x^2/2 + x^3/3 + ....+ x^n/n

// JavaScript code to print the sum
// of the series
function sum(x, n)
{

    let total = 1.0;
    let multi = x;
    for (let i = 1; i <= n; i++)
    {
        total = total + multi / i;
        multi = multi * x;
    }
    return total;
}

// Driver code
let x = 2;
let n = 5;
document.write(sum(x, n).toFixed(2));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
18.07
```