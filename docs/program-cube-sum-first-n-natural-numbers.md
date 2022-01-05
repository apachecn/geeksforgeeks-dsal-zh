# 前 n 个自然数的立方和程序

> 原文:[https://www . geesforgeks . org/program-cube-sum-first-n-natural-numbers/](https://www.geeksforgeeks.org/program-cube-sum-first-n-natural-numbers/)

打印系列 1<sup>3</sup>+2<sup>3</sup>+3<sup>3</sup>+4<sup>3</sup>+……。+ n <sup>3</sup> 直到第 n 个学期。
**举例:**

```
Input : n = 5
Output : 225
13 + 23 + 33 + 43 + 53 = 225

Input : n = 7
Output : 784
13 + 23 + 33 + 43 + 53 + 
63 + 73 = 784
```

一个**简单的解决方法**就是一个个添加条款。

## C++

```
// Simple C++ program to find sum of series
// with cubes of first n natural numbers
#include <iostream>
using namespace std;

/* Returns the sum of series */
int sumOfSeries(int n)
{
    int sum = 0;
    for (int x = 1; x <= n; x++)
        sum += x * x * x;
    return sum;
}

// Driver Function
int main()
{
    int n = 5;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find sum of series
// with cubes of first n natural numbers

import java.util.*;
import java.lang.*;
class GFG {

    /* Returns the sum of series */
    public static int sumOfSeries(int n)
    {
        int sum = 0;
        for (int x = 1; x <= n; x++)
            sum += x * x * x;
        return sum;
    }

    // Driver Function
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(sumOfSeries(n));
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Simple Python program to find sum of series
# with cubes of first n natural numbers

# Returns the sum of series
def sumOfSeries(n):
    sum = 0
    for i in range(1, n + 1):
        sum += i * i*i

    return sum

# Driver Function
n = 5
print(sumOfSeries(n))

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// Simple C# program to find sum of series
// with cubes of first n natural numbers
using System;

class GFG {
    /* Returns the sum of series */
    static int sumOfSeries(int n)
    {
        int sum = 0;
        for (int x = 1; x <= n; x++)
            sum += x * x * x;
        return sum;
    }

    // Driver Function
    public static void Main()
    {
        int n = 5;
        Console.Write(sumOfSeries(n));
    }
}
// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to find sum of series
// with cubes of first n natural numbers

// Returns the sum of series
function sumOfSeries( $n)
{
    $sum = 0;
    for ($x = 1; $x <= $n; $x++)
        $sum += $x * $x * $x;
    return $sum;
}

// Driver code
$n = 5;
echo sumOfSeries($n);

// This Code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

//  Simple javascript program to find sum of series
// with cubes of first n natural numbers

/* Returns the sum of series */
function sumOfSeries( n)
{
    let sum = 0;
    for (let x = 1; x <= n; x++)
        sum += x * x * x;
    return sum;
}

// Driven Program

    let n = 5;
     document.write(sumOfSeries(n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
225
```

时间复杂度:O(n)
一个**有效的解决方案**是使用直接的数学公式 **(n ( n + 1 ) / 2) ^ 2**

```
For n = 5 sum by formula is
       (5*(5 + 1 ) / 2)) ^ 2
          = (5*6/2) ^ 2
          = (15) ^ 2
          = 225

For n = 7, sum by formula is
       (7*(7 + 1 ) / 2)) ^ 2
          = (7*8/2) ^ 2
          = (28) ^ 2
          = 784
```

## C++

```
// A formula based C++ program to find sum
// of series with cubes of first n natural
// numbers
#include <iostream>
using namespace std;

int sumOfSeries(int n)
{
    int x = (n * (n + 1) / 2);
    return x * x;
}

// Driver Function
int main()
{
    int n = 5;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A formula based Java program to find sum
// of series with cubes of first n natural
// numbers

import java.util.*;
import java.lang.*;
class GFG {
    /* Returns the sum of series */
    public static int sumOfSeries(int n)
    {
        int x = (n * (n + 1) / 2);

        return x * x;
    }

    // Driver Function
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(sumOfSeries(n));
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# A formula based Python program to find sum
# of series with cubes of first n natural
# numbers

# Returns the sum of series
def sumOfSeries(n):
    x = (n * (n + 1)  / 2)
    return (int)(x * x)

# Driver Function
n = 5
print(sumOfSeries(n))

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// A formula based C# program to
// find sum of series with cubes
// of first n natural numbers
using System;

class GFG {

    // Returns the sum of series
    public static int sumOfSeries(int n)
    {
        int x = (n * (n + 1) / 2);

        return x * x;
    }

    // Driver Function
    public static void Main()
    {
        int n = 5;

        Console.Write(sumOfSeries(n));
    }
}

// Code Contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A formula based PHP program to find sum
// of series with cubes of first n natural
// numbers

function sumOfSeries($n)
{
    $x = ($n * ($n + 1) / 2);
    return $x * $x;
}

// Driver Function
$n = 5;
echo sumOfSeries($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Simple javascript program to find sum of series
// with cubes of first n natural numbers

/* Returns the sum of series */
function sumOfSeries( n)
{
    x = (n * (n + 1) / 2)
    return (x * x)
}

// Driven Program

    let n = 5;
    document.write(sumOfSeries(n));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
225
```

时间复杂度:O(1)
**这个公式是如何工作的？**
我们可以用数学归纳法证明这个公式。我们可以很容易地看到，这个公式适用于 n = 1 和 n = 2。假设 n = k-1 是真的。

```
Let the formula be true for n = k-1.
Sum of first (k-1) natural numbers = 
            [((k - 1) * k)/2]2

Sum of first k natural numbers = 
          = Sum of (k-1) numbers + k3
          = [((k - 1) * k)/2]2 + k3
          = [k2(k2 - 2k + 1) + 4k3]/4
          = [k4 + 2k3 + k2]/4
          = k2(k2 + 2k + 1)/4
          = [k*(k+1)/2]2
```

**以上程序导致溢出，即使结果没有超出整数限制。**像[之前的帖子](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)一样，我们可以通过先做除法在一定程度上避免溢出。

## C++

```
// Efficient CPP program to find sum of cubes
// of first n natural numbers that avoids
// overflow if result is going to be withing
// limits.
#include <iostream>
using namespace std;

// Returns sum of first n natural
// numbers
int sumOfSeries(int n)
{
    int x;
    if (n % 2 == 0)
        x = (n / 2) * (n + 1);
    else
        x = ((n + 1) / 2) * n;
    return x * x;
}

// Driver code
int main()
{
    int n = 5;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find sum of cubes
// of first n natural numbers that avoids
// overflow if result is going to be withing
// limits.
import java.util.*;
import java.lang.*;
class GFG {
    /* Returns the sum of series */
    public static int sumOfSeries(int n)
    {
        int x;
        if (n % 2 == 0)
            x = (n / 2) * (n + 1);
        else
            x = ((n + 1) / 2) * n;
        return x * x;
    }

    // Driver Function
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(sumOfSeries(n));
    }
}
// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Efficient Python program to find sum of cubes
# of first n natural numbers that avoids
# overflow if result is going to be withing
# limits.

# Returns the sum of series
def sumOfSeries(n):
    x = 0
    if n % 2 == 0 :
        x = (n / 2) * (n + 1)
    else:
        x = ((n + 1) / 2) * n

    return (int)(x * x)

# Driver Function
n = 5
print(sumOfSeries(n))

# Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// Efficient C# program to find sum of
// cubes of first n natural numbers
// that avoids overflow if result is
// going to be withing limits.
using System;

class GFG {

    /* Returns the sum of series */
    public static int sumOfSeries(int n)
    {
        int x;
        if (n % 2 == 0)
            x = (n / 2) * (n + 1);
        else
            x = ((n + 1) / 2) * n;
        return x * x;
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;
        Console.WriteLine(sumOfSeries(n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to
// find sum of cubes of first 
// n natural numbers that avoids
// overflow if result is going
// to be with in limits.

// Returns sum of first n
// natural numbers
function sumOfSeries($n)
{
    $x;
    if ($n % 2 == 0)
        $x = ($n / 2) * ($n + 1);
    else
        $x = (($n + 1) / 2) * $n;
    return $x * $x;
}

// Driver code
$n = 5;
echo sumOfSeries($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Simple javascript program to find sum of series
// with cubes of first n natural numbers

/* Returns the sum of series */
function sumOfSeries( n)
{
  x=0
    if (n % 2 == 0)
        x = (n / 2) * (n + 1)
    else
        x = ((n + 1) / 2) * n

    return (x * x)
}

// Driven Program

    let n = 5;
    document.write(sumOfSeries(n));

// This code contributed by sravan

</script>
```

**输出:**

```
225
```

本文由 **R_Raj** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。