# 一个范围内斐波那契数的和

> 原文:[https://www . geesforgeks . org/斐波那契数列之和/区间数/](https://www.geeksforgeeks.org/sum-of-fibonacci-numbers-in-a-range/)

给定一个范围**【l，r】**，任务是求 **fib(l) + fib(l + 1) + fib(l + 2) +的和…..+ fib(r)** 其中 **fib(n)** 是 **n <sup>第</sup>** 个斐波那契数。

**示例:**

> **输入:** l = 2，r = 5
> **输出:**11
> fib(2)+fib(3)+fib(4)+fib(5)= 1+2+3+5 = 11
> 
> **输入:** l = 4，r = 8
> T3】输出: 50

**天真方法:**简单计算 **fib(l) + fib(l + 1) + fib(l + 2) + …..+ fib(r)** 在**O(r–l)**时间复杂度。
为了在 **O(1)** 中找到 **fib(n)** ，我们将借助黄金比例。

**使用比奈公式的斐波那契计算**

> fib(n)=φ<sup>n</sup>–psi<sup>n</sup>)/？5
> 其中，
> φ=(1+sqrt(5))/2 大致等于 1.61803398875
> psi = 1–φ=(1–sqrt(5))/2 大致等于 0.61803398875

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the nth Fibonacci number
int fib(int n)
{
    double phi = (1 + sqrt(5)) / 2;
    return round(pow(phi, n) / sqrt(5));
}

// Function to return the required sum
ll calculateSum(int l, int r)
{

    // To store the sum
    ll sum = 0;

    // Calculate the sum
    for (int i = l; i <= r; i++)
        sum += fib(i);

    return sum;
}

// Driver code
int main()
{
    int l = 4, r = 8;
    cout << calculateSum(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;
class GFG
{

// Function to return the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.sqrt(5)) / 2;
    return (int)Math.round(Math.pow(phi, n) / Math.sqrt(5));
}

// Function to return the required sum
static int calculateSum(int l, int r)
{

    // To store the sum
    int sum = 0;

    // Calculate the sum
    for (int i = l; i <= r; i++)
        sum += fib(i);

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int l = 4, r = 8;
    System.out.println(calculateSum(l, r));

}
}

//This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the nth
# Fibonacci number
def fib(n):
    phi = ((1 + (5 ** (1 / 2))) / 2);
    return round((phi ** n) / (5 ** (1 / 2)));

# Function to return the required sum
def calculateSum(l, r):

    # To store the sum
    sum = 0;

    # Calculate the sum
    for i in range(l, r + 1):
        sum += fib(i);

    return sum;

# Driver Code
if __name__ == '__main__':
    l, r = 4, 8;
    print(calculateSum(l, r));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.Sqrt(5)) / 2;
    return (int)Math.Round(Math.Pow(phi, n) / Math.Sqrt(5));
}

// Function to return the required sum
static int calculateSum(int l, int r)
{

    // To store the sum
    int sum = 0;

    // Calculate the sum
    for (int i = l; i <= r; i++)
        sum += fib(i);

    return sum;
}

// Driver code
public static void Main()
{
    int l = 4, r = 8;
    Console.WriteLine(calculateSum(l, r));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the nth
// Fibonacci number
function fib($n)
{
    $phi = (1 + sqrt(5)) / 2;
    return (int)round(pow($phi, $n) / sqrt(5));
}

// Function to return the required sum
function calculateSum($l, $r)
{

    // To store the sum
    $sum = 0;

    // Calculate the sum
    for ($i = $l; $i <= $r; $i++)
        $sum += fib($i);

    return $sum;
}

// Driver code
$l = 4;
$r = 8;
echo calculateSum($l, $r);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the nth Fibonacci number
    function fib(n) {
        var phi = (1 + Math.sqrt(5)) / 2;
        return parseInt( Math.round
        (Math.pow(phi, n)/ Math.sqrt(5))
        );
    }

    // Function to return the required sum
    function calculateSum(l , r) {

        // To store the sum
        var sum = 0;

        // Calculate the sum
        for (i = l; i <= r; i++)
            sum += fib(i);

        return sum;
    }

    // Driver code

        var l = 4, r = 8;
        document.write(calculateSum(l, r));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
50
```

**高效方法:**思路是找到斐波那契数之和与第 n <sup>个</sup>个斐波那契数的关系，用**比奈公式**计算其值。

**关系演绎**

1.  F(i)指第 i <sup>个</sup>斐波那契数。
2.  S(i)指的是直到 F(i)的斐波那契数之和。

> 我们可以将关系式 F(n+1)= F(n)+F(n–1)改写如下:
> F(n–1)= F(n+1)–F(n)
> 类似地，
> F(n–2)= F(n)–F(n–1)
> ……
> ……
> ……
> F(0)= F(2)–F(1)
> 将所有方程相加，在左侧，我们有
> F(0) + F(1)

因此，
S(n–1)= F(n+1)–F(1)
S(n–1)= F(n+1)–1
T3】S(n)= F(n+2)–1

为了找到 **S(n)** ，只需计算 **(n + 2) <sup>th</sup>** 斐波那契数，从结果中减去 **1** 。
因此，
S(l，r)= S(r)–S(l–1)
S(l，r)= F(r+2)–1 –( F(l+1)–1)
**S(l，r)= F(r+2)–F(l+1)**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth Fibonacci number
int fib(int n)
{
    double phi = (1 + sqrt(5)) / 2;
    return round(pow(phi, n) / sqrt(5));
}

// Function to return the required sum
int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);
    return sum;
}

// Driver code
int main()
{
    int l = 4, r = 8;
    cout << calculateSum(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.sqrt(5)) / 2;
    return (int) Math.round(Math.pow(phi, n) / Math.sqrt(5));
}

// Function to return the required sum
static int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int l = 4, r = 8;
    System.out.println(calculateSum(l, r));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the nth
# Fibonacci number
def fib(n):

    phi = (1 + math.sqrt(5)) / 2;
    return int(round(pow(phi, n) /
                         math.sqrt(5)));

# Function to return the required sum
def calculateSum(l, r):

    # Using our deduced result
    sum = fib(r + 2) - fib(l + 1);
    return sum;

# Driver code
l = 4;
r = 8;
print(calculateSum(l, r));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the nth Fibonacci number
static int fib(int n)
{
    double phi = (1 + Math.Sqrt(5)) / 2;
    return (int) Math.Round(Math.Pow(phi, n) /
                            Math.Sqrt(5));
}

// Function to return the required sum
static int calculateSum(int l, int r)
{

    // Using our deduced result
    int sum = fib(r + 2) - fib(l + 1);
    return sum;
}

// Driver code
public static void Main()
{
    int l = 4, r = 8;
    Console.WriteLine(calculateSum(l, r));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the nth Fibonacci number
function fib($n)
{
    $phi = (1 + sqrt(5)) / 2;
    return (int) round(pow($phi, $n) / sqrt(5));
}

// Function to return the required sum
function calculateSum($l, $r)
{

    // Using our deduced result
    $sum = fib($r + 2) - fib($l + 1);
    return $sum;
}

// Driver code
$l = 4; $r = 8;
echo(calculateSum($l, $r));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the nth Fibonacci number
    function fib(n) {
        var phi = (1 + Math.sqrt(5)) / 2;
        return parseInt( Math.round(Math.pow(phi, n) / Math.sqrt(5)));
    }

    // Function to return the required sum
    function calculateSum(l , r) {

        // Using our deduced result
        var sum = fib(r + 2) - fib(l + 1);
        return sum;
    }

    // Driver code

        var l = 4, r = 8;
        document.write(calculateSum(l, r));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
50
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)