# 给定和最小差的同素对

> 原文:[https://www . geeksforgeeks . org/给定和最小差的同素对/](https://www.geeksforgeeks.org/co-prime-pair-with-given-sum-minimum-difference/)

同素或互素对是那些 GCD 为 1 的数对。给定一个数，n 代表一个同素对(A，B)的和，使得 A–B 最小。

**示例:**

```
Input : 12 
Output : 5 7
Possible co-prime pairs are (5, 7), (1, 11)
but difference between 5 and 7 is minimum

Input : 13
Output : 6 7
Possible co-prime pairs are (6, 7), (5, 8),
(4, 9), (3, 10), (2, 11) and (1, 12) 
but difference between 6 and 7  is minimum 
```

一个**简单的解决方案**是迭代所有从 1 到 n-1 的数字。对于每个数字 x，检查 n–x 和 x 是否为同素。如果是，那么如果这两者之间的差异小于迄今为止的最小差异，则更新结果。
一个**有效的解决方案**是基于这样一个事实，即具有最小差异的数字应该接近 n/2。我们从 n/2 循环到 1。检查每一个可能的对，当发现第一个可能的同素对时，显示它并停止循环。

## C++

```
// CPP program to represent a number 
// as sum of a co-prime pair such that
// difference between them is minimum
#include <bits/stdc++.h>
using namespace std;

// function to check if pair
// is co-prime or not
bool coprime(int a, int b)
{
    return (__gcd(a, b) == 1);
}

// function to find and print
// co-prime pair
void pairSum(int n){

    int mid = n / 2;

    for (int i = mid; i >= 1; i--) {
        if (coprime(i, n - i) == 1) {
            cout << i << " " << n - i;
            break;
        }
    }
}

// driver code
int main()
{
    int n = 11;
    pairSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to represent a
// number as sum of a co-prime
// pair such that difference
// between them is minimum
class GFG
{
    static int __gcd(int a, int b)
    {
        return b == 0 ? a :
           __gcd(b, a % b);
    }

    // function to check if pair
    // is co-prime or not
    static boolean coprime(int a, int b)
    {
        return (__gcd(a, b) == 1);
    }

    // function to find and
    // print co-prime pair
    static void pairSum(int n)
    {
        int mid = n / 2;

        for (int i = mid; i >= 1; i--)
        {
            if (coprime(i, n - i) == true)
            {
                System.out.print( i + " " +
                                  (n - i));
                break;
            }
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 11;
        pairSum(n);

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to represent
# a number as sum of a co-prime
# pair such that difference
# between them is minimum
import math

# function to check if pair
# is co-prime or not
def coprime(a, b):
    return 1 if(math.gcd(a, b) == 1) else 0;

# function to
# find and print
# co-prime pair
def pairSum(n):
    mid = int(n / 2);
    i = mid;
    while(i >= 1):
        if (coprime(i, n - i) == 1):
            print(i, n - i);
            break;
        i = i - 1;

# Driver code
n = 11;
pairSum(n);

# This code is contributed
# by mits
```

## C#

```
// C# program to represent a number
// as sum of a co-prime pair such that
// difference between them is minimum
using System;

class GFG {

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // function to check if pair
    // is co-prime or not
    static bool coprime(int a, int b)
    {
        return (__gcd(a, b) == 1);
    }

    // function to find and print
    // co-prime pair
    static void pairSum(int n)
    {
        int mid = n / 2;

        for (int i = mid; i >= 1; i--)
        {
            if (coprime(i, n - i) == true)
            {
                Console.Write( i + " "
                               + (n - i));
                break;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 11;
        pairSum(n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to represent
// a number as sum of a
// co-prime pair such that
// difference between them
// is minimum

function gcd($num1, $num2)
{

/* finds the greatest common
factor between two numbers */
while ($num2 != 0)
{
    $t = $num1 % $num2;
    $num1 = $num2;
    $num2 = $t;
}
return $num1;
}

// function to check if pair
// is co-prime or not
function coprime($a, $b)
{
    if(gcd($a, $b) == 1)
    return 1;
    else
    return 0;
}

// function to find and
// print co-prime pair
function pairSum($n)
{
    $mid = (int)(($n / 2));

    for ($i = $mid; $i >= 1; $i--)
    {
        if (coprime($i, $n - $i) == 1)
        {
            echo $i . " " . ($n - $i);
            break;
        }
    }
}

// Driver code
$n = 11;
pairSum($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript  program to represent a
// number as sum of a co-prime
// pair such that difference
// between them is minimum

    function __gcd(a, b)
    {
        return b == 0 ? a :
           __gcd(b, a % b);
    }

    // function to check if pair
    // is co-prime or not
    function coprime(a, b)
    {
        return (__gcd(a, b) == 1);
    }

    // function to find and
    // prlet co-prime pair
    function pairSum(n)
    {
        let mid = Math.floor(n / 2);

        for (let i = mid; i >= 1; i--)
        {
            if (coprime(i, n - i) == true)
            {
                document.write( i + " " +
                                  (n - i));
                break;
            }
        }
    }

// Driver code

        let n = 11;
        pairSum(n);

</script>
```

**输出:**

```
5 6
```