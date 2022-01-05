# N 以下 3 和 7 的所有倍数之和

> 原文:[https://www . geesforgeks . org/n 以下 3 和 7 的所有倍数之和/](https://www.geeksforgeeks.org/sum-of-all-the-multiples-of-3-and-7-below-n/)

给定一个数 *N* ，任务是求 *3* 和 *7* 在 *N* 下面的所有倍数的和。
**注:**一个数在和中不能重复。

**示例:**

> **输入:**N = 10
> T3】输出: 25
> 3 + 6 + 7 + 9 = 25
> 
> **输入:**N = 24
> T3】输出:105
> 3+6+7+9+12+14+15+18+21 = 105

**进场:**

*   我们知道 *3* 的倍数组成 [AP](https://www.geeksforgeeks.org/progressions-ap-gp-hp-and-practice-problems/) 为*S<sub>3</sub>= 3+6+9+12+15+18+21+…*
*   而 *7* 的倍数组成一个 AP 为 *S <sub>7</sub> = 7 + 14 + 21 + 28 + …*
*   现在，*Sum = S<sub>3</sub>+S<sub>7</sub>T5【即*3+6+7+9+12+14+15+18+21+21+……**
*   从上一步开始， *21* 重复两次。事实上， *21* (或 3*7)的所有倍数将重复计算两次，一次在系列*S<sub>3</sub>T7】中，另一次在系列*S<sub>7</sub>T11】中。所以 *21* 的倍数需要从结果中剔除。**
*   所以，最终结果将是*S<sub>3</sub>+S<sub>7</sub>–S<sub>21</sub>*

> 一个 AP 级数和的公式为:
> *n * ( a + l ) / 2*
> 其中 n 为项数，a 为起始项，l 为末项。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of all
// multiples of 3 and 7 below N

#include <bits/stdc++.h>
using namespace std;

// Function to find sum of AP series
long long sumAP(long long n, long long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of 3 and 7 below N
long long sumMultiples(long long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 3) + sumAP(n, 7) - sumAP(n, 21);
}

// Driver code
int main()
{
    long long n = 24;

    cout << sumMultiples(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// multiples of 3 and 7 below N
import java.util.*;

class solution
{

// Function to find sum of AP series
static long sumAP(long n, long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of 3 and 7 below N
static long sumMultiples(long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 3) + sumAP(n, 7) - sumAP(n, 21);
}

// Driver code
public static void main(String args[])
{
    long n = 24;

    System.out.println(sumMultiples(n));

 }
}

//This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# all multiples of 3 and 7 below N

# Function to find sum of AP series
def sumAP(n, d):

    # Number of terms
    n = int(n / d);

    return (n) * (1 + n) * (d / 2);

# Function to find the sum of all
# multiples of 3 and 7 below N
def sumMultiples(n):

    # Since, we need the sum of
    # multiples less than N
    n -= 1;

    return int(sumAP(n, 3) +
               sumAP(n, 7) -
               sumAP(n, 21));

# Driver code
n = 24;

print(sumMultiples(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to find the sum of all
// multiples of 3 and 7 below N
using System;

class GFG
{

// Function to find sum of AP series
static long sumAP(long n, long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of 3 and 7 below N
static long sumMultiples(long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 3) + sumAP(n, 7) -
                         sumAP(n, 21);
}

// Driver code
static public void Main(String []args)
{
    long n = 24;

    Console.WriteLine(sumMultiples(n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// multiples of 3 and 7 below N

// Function to find sum of AP series
function sumAP($n, $d)
{
    // Number of terms
    $n = (int)($n / $d);

    return ($n) * (1 + $n) * ($d / 2);
}

// Function to find the sum of all
// multiples of 3 and 7 below N
function sumMultiples($n)
{
    // Since, we need the sum of
    // multiples less than N
    $n--;

    return sumAP($n, 3) +
           sumAP($n, 7) - sumAP($n, 21);
}

// Driver code
$n = 24;

echo sumMultiples($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the sum of all
// multiples of 3 and 7 below N

// Function to find sum of AP series
function sumAP(n, d)
{

    // Number of terms
    n = parseInt(n / d);

    return (n) * (1 + n) * (d / 2);
}

// Function to find the sum of all
// multiples of 3 and 7 below N
function sumMultiples(n)
{

    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 3) +
           sumAP(n, 7) -
           sumAP(n, 21);
}

// Driver code
let n = 24;

document.write(sumMultiples(n));

// This code is contributed by mohan1240760

</script>
```

**Output:** 

```
105
```