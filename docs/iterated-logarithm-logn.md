# 重对数对数*(n)

> 原文:[https://www.geeksforgeeks.org/iterated-logarithm-logn/](https://www.geeksforgeeks.org/iterated-logarithm-logn/)

[重对数或 Log*(n)](https://en.wikipedia.org/wiki/Iterated_logarithm) 是在结果小于或等于 1 之前，对数函数必须迭代应用的次数。

![\log ^{*}n:=\begin{cases}0n\leq 1;\\1+\log ^{*}(\log n)n>1\end{cases}       ](img/5eec7fb2e1f5589a998e47fb66cb7309.png "Rendered by QuickLaTeX.com")

**应用:**用于算法分析(详见[维基](https://en.wikipedia.org/wiki/Iterated_logarithm#Analysis_of_algorithms)

## C++

```
// Recursive CPP program to find value of
// Iterated Logarithm
#include <bits/stdc++.h>
using namespace std;

int _log(double x, double base)
{
    return (int)(log(x) / log(base));
}

double recursiveLogStar(double n, double b)
{
    if (n > 1.0)
        return 1.0 + recursiveLogStar(_log(n, b), b);
    else
        return 0;
}

// Driver code
int main()
{
    int n = 100, base = 5;
    cout << "Log*(" << n << ") = "
         << recursiveLogStar(n, base) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// find value of Iterated Logarithm
import java.io.*;

class GFG
{
static int _log(double x,
                double base)
{
    return (int)(Math.log(x) /
                 Math.log(base));
}

static double recursiveLogStar(double n,
                               double b)
{
    if (n > 1.0)
        return 1.0 +
               recursiveLogStar(_log(n,
                                 b), b);
    else
        return 0;
}

// Driver code
public static void main (String[] args)
{
    int n = 100, base = 5;
    System.out.println("Log*(" + n + ") = " +
                  recursiveLogStar(n, base));
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Recursive Python3 program to find value of
# Iterated Logarithm
import math

def _log(x, base):

    return (int)(math.log(x) / math.log(base))

def recursiveLogStar(n, b):

    if(n > 1.0):
        return 1.0 + recursiveLogStar(_log(n, b), b)
    else:
        return 0

# Driver code
if __name__=='__main__':
    n = 100
    base = 5
    print("Log*(", n, ") = ", recursiveLogStar(n, base))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// Recursive C# program to
// find value of Iterated Logarithm

using System;

public class GFG{
static int _log(double x, double baset)
{
    return (int)(Math.Log(x) /
                Math.Log(baset));
}

static double recursiveLogStar(double n,
                            double b)
{
    if (n > 1.0)
        return 1.0 +
            recursiveLogStar(_log(n,
                                b), b);
    else
        return 0;
}

// Driver code
    static public void Main (){

    int n = 100, baset = 5;
    Console.WriteLine("Log*(" + n + ") = " +
                recursiveLogStar(n, baset));
}
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PhP program to find
// value of Iterated Logarithm

function _log($x, $base)
{
    return (int)(log($x) / log($base));
}

function recursiveLogStar($n, $b)
{
    if ($n > 1.0)
        return 1.0 +
               recursiveLogStar(_log($n,
                               $b), $b);
    else
        return 0;
}

// Driver code
$n = 100; $base = 5;
echo "Log*(" , $n , ")"," = ",
recursiveLogStar($n, $base), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to
// find value of Iterated Logarithm

    function _log( x, base)
{
    return (Math.log(x) /
                 Math.log(base));
}

function recursiveLogStar(n, b)
{
    if (n > 1.0)
        return 1.0 +
               recursiveLogStar(_log(n,
                                 b), b);
    else
        return 0;
}

// Driver code

    let n = 100, base = 5;
    document.write("Log*(" + n + ") = " +
                  recursiveLogStar(n, base));

    // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
Log*(100) = 2
```

**迭代实现:**

## C++

```
// Iterative CPP function to find value of
// Iterated Logarithm
int iterativeLogStar(double n, double b)
{
    int count = 0;
    while (n >= 1) {
        n = _log(n, b);
        count++;
    }
    return count;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java function to find value of
// Iterated Logarithm
public static int iterativeLogStar(double n, double b)
{
    int count = 0;
    while (n >= 1) {
        n = _log(n, b);
        count++;
    }
    return count;
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Iterative Python function to find value of
# Iterated Logarithm

def iterativeLogStar(n, b):

    count = 0
    while(n >= 1):
        n = _log(n, b)
        count = count + 1

    return count

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// Iterative C# function to find value of
// Iterated Logarithm
static int iterativeLogStar(double n, double b)
{
    int count = 0;
    while (n >= 1)
    {
        n = _log(n, b);
        count++;
    }
    return count;
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Iterative javascript function to find
// value of Iterated Logarithm
function iterativeLogStar(n, b)
{
    var count = 0;
    while (n >= 1)
    {
        n = _log(n, b);
        count++;
    }
    return count;
}

// This code is contributed by 29AjayKumar

</script>
```

本文由 [**阿布舍克·拉杰普特**](https://auth.geeksforgeeks.org/profile.php?user=Abhishek rajput) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。