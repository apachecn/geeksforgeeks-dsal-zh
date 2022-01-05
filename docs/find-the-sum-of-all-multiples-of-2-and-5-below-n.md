# 求 N 以下所有 2 和 5 的倍数之和

> 原文:[https://www . geesforgeks . org/find-n 下 2 和 5 的所有倍数之和/](https://www.geeksforgeeks.org/find-the-sum-of-all-multiples-of-2-and-5-below-n/)

给定一个数 n，任务是找出 n 以下所有 2 和 5 的倍数之和(n 可能等于 10^10).

**示例**:

```
Input : N = 10
Output : 25
Explanation : 2 + 4 + 6 + 8 + 5

Input : N = 20
Output : 110
```

**方法:**
我们知道 2 的倍数构成一个 AP，如下所示:

> **2、4、6、8、10、12、14** …。(1)

同样，5 的倍数构成 AP，如下所示:

> **5、10、15** ……(2)

现在， **Sum(1) + Sum(2)** = 2，4，5，6，8，10，10，12，14，15…
这里，重复 10。事实上，所有 10 或 2*5 的倍数都是重复的，因为它被计数两次，一次在 2 的系列中，另一次在 5 的系列中。因此，我们将从和(1) +和(2)中减去 10 的和。

A.P .和的公式是:

> **n * ( a + l ) / 2**
> 其中![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")为项数，![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")为起始项，![l  ](img/ae53c539214f6954fa235fcc60aaab38.png "Rendered by QuickLaTeX.com")为末项。

所以，最终答案是:

> S<sub>2</sub>+S<sub>5</sub>–S<sub>10</sub>

下面是上述方法的实现:

## C++

```
// CPP program to find the sum of all
// multiples of 2 and 5 below N

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
// multiples of 2 and 5 below N
long long sumMultiples(long long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 2) + sumAP(n, 5) - sumAP(n, 10);
}

// Driver code
int main()
{
    long long n = 20;

    cout << sumMultiples(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// multiples of 2 and 5 below N

class GFG{
// Function to find sum of AP series
static long sumAP(long n, long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of 2 and 5 below N
static long sumMultiples(long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 2) + sumAP(n, 5) - sumAP(n, 10);
}

// Driver code
public static void main(String[] args)
{
    long n = 20;

    System.out.println(sumMultiples(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# all multiples of 2 and 5 below N

# Function to find sum of AP series
def sumAP(n, d):

    # Number of terms
    n = int(n / d);

    return (n) * (1 + n) * (d / 2);

# Function to find the sum of all
# multiples of 2 and 5 below N
def sumMultiples(n):

    # Since, we need the sum of
    # multiples less than N
    n -= 1;

    return (int(sumAP(n, 2) + sumAP(n, 5) -
                              sumAP(n, 10)));

# Driver code
n = 20;

print(sumMultiples(n));

# This code is contributed by mits
```

## C#

```
// C# program to find the sum of all
// multiples of 2 and 5 below N

using System;

public class GFG{

    // Function to find sum of AP series
static long sumAP(long n, long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of 2 and 5 below N
static long sumMultiples(long n)
{
    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 2) + sumAP(n, 5) - sumAP(n, 10);
}

// Driver code

    static public void Main (){
            long n = 20;

        Console.WriteLine(sumMultiples(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// multiples of 2 and 5 below N
// Function to find sum of AP series
function sumAP($n, $d)
{
    // Number of terms
    $n = (int)($n /$d);

    return ($n) * ((1 + $n) *
                   (int)$d / 2);
}

// Function to find the sum of all
// multiples of 2 and 5 below N
function sumMultiples($n)
{
    // Since, we need the sum of
    // multiples less than N
    $n--;

    return sumAP($n, 2) + sumAP($n, 5) -
                          sumAP($n, 10);
}

// Driver code
$n = 20;

echo sumMultiples($n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Java script program to find the sum of all
// multiples of 2 and 5 below N

// Function to find sum of AP series
function sumAP(n, d)
{

    // Number of terms
    n = parseInt(n / d);

    return (n) * ((1 + n) *
         parseInt(d) / 2);
}

// Function to find the sum of all
// multiples of 2 and 5 below N
function sumMultiples(n)
{

    // Since, we need the sum of
    // multiples less than N
    n--;

    return sumAP(n, 2) + sumAP(n, 5) -
           sumAP(n, 10);
}

// Driver code
n = 20;

document.write( sumMultiples(n));

// This code is contributed by bobby

</script>
```

**Output:** 

```
110
```