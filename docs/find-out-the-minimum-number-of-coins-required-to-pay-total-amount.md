# 找出需要支付总金额的最小硬币数

> 原文:[https://www . geeksforgeeks . org/find-需要支付的最低硬币总数/](https://www.geeksforgeeks.org/find-out-the-minimum-number-of-coins-required-to-pay-total-amount/)

给定总金额 N 和无限数量的价值 **1** 、 **10** 和 **25** 币的硬币。找出准确支付金额所需的最小硬币数量 **N** 。
**举例:**

```
Input : N = 14
Output : 5
You will use *one* coin of value 10 and 
*four* coins of value 1.

Input :  N = 88
Output : 7
```

**进场:**T2【有三种不同情况:

1.  如果**N**T2【10】的值，那么价值为 1 的硬币只能用于支付。
2.  当 **N** > 9 和< 25 时，那么价值为 1 和 10 的硬币将用于支付。在这里，为了尽量减少硬币的使用数量，价值 10 的硬币将是首选。

3.  时**N**T2【24】。那么所有价值 1、10 和 25 的硬币都将用于支付。为了最大限度地减少硬币数量，首要目标是尽可能多地首先使用价值 25 的硬币，然后使用价值 10 的硬币，然后使用价值 1 的硬币。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// of coins required

#include <iostream>
using namespace std;

// Function to find the minimum number
// of coins required
int countCoins(int n)
{
    int c = 0;

    if (n < 10) {
        // counts coins which have value 1
        // we will need n coins of value 1
        return n;
    }
    if (n > 9 && n < 25) {
        // counts coins which have value 1 and 10
        c = n / 10 + n % 10;
        return c;
    }
    if (n > 24) {
        // counts coins which have value 25
        c = n / 25;

        if (n % 25 < 10) {

            // counts coins which have value 1 and 25
            c = c + n % 25;
            return c;
        }

        if (n % 25 > 9) {
            // counts coins which have value 1, 10 and 25
            c = c + (n % 25) / 10 + (n % 25) % 10;
            return c;
        }
    }
}

// Driver Code
int main()
{
    int n = 14;

    cout << countCoins(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of coins required

class GFG {

    // Function to find the minimum number
    // of coins required
    static int countCoins(int n)
    {
        int c = 0;
        if (n < 10) {
            // counts coins which have value 1
            // we will need n coins of value 1
            return n;
        }
        if (n > 9 && n < 25) {

            // counts coins which have value 1 and 10
            c = n / 10 + n % 10;

            return c;
        }
        if (n > 24) {
            // counts coins which have value 25
            c = n / 25;

            if (n % 25 < 10) {
                // counts coins which have value 1 and 25
                c = c + n % 25;

                return c;
            }
            if (n % 25 > 9) {
                // counts coins which have value 1, 10 and 25
                c = c + (n % 25) / 10 + (n % 25) % 10;

                return c;
            }
        }

        return c;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 14;
        System.out.println(countCoins(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of coins required

# Function to find the minimum number
# of coins required
def countCoins(n):

    c = 0

    if (n < 10):

        # counts coins which have value 1
        # we will need n coins of value 1
        return n

    if (n > 9 and n < 25):

        # counts coins which have value 1 and 10
        c = n // 10 + n % 10
        return c

    if (n > 24):

        # counts coins which have value 25
        c = n // 25

        if (n % 25 < 10):

            # counts coins which have value
            # 1 and 25
            c = c + n % 25
            return c

        if (n % 25 > 9):

            # counts coins which have value
            # 1, 10 and 25
            c = (c + (n % 25) // 10 +
                     (n % 25) % 10)
            return c

# Driver Code
n = 14

print(countCoins(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find the minimum number 
// of coins required 
using System;

class GFG
{ 

    // Function to find the minimum number 
    // of coins required 
    static int countCoins(int n) 
    { 
        int c = 0; 
        if (n < 10) 
        { 
            // counts coins which have value 1 
            // we will need n coins of value 1 
            return n; 
        } 
        if (n > 9 && n < 25)
        { 

            // counts coins which have value 1 and 10 
            c = n / 10 + n % 10; 

            return c; 
        } 
        if (n > 24)
        { 
            // counts coins which have value 25 
            c = n / 25; 

            if (n % 25 < 10) 
            { 
                // counts coins which have value 1 and 25 
                c = c + n % 25; 

                return c; 
            } 
            if (n % 25 > 9)
            { 
                // counts coins which have value 1, 10 and 25 
                c = c + (n % 25) / 10 + (n % 25) % 10; 

                return c; 
            } 
        } 

        return c; 
    } 

    // Driver Code 
    public static void Main() 
    { 
        int n = 14; 
        Console.WriteLine(countCoins(n)); 
    }
} 

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum number
// of coins required

// Function to find the minimum number
// of coins required
function countCoins($n)
{
    $c = 0;
    if ($n < 10)
    {
        // counts coins which have value 1
        // we will need n coins of value 1
        return $n;
    }

    if ($n > 9 && $n < 25) 
    {

        // counts coins which have value 1 and 10
        $c = (int)($n / 10 + $n % 10);

        return $c;
    }

    if ($n > 24) 
    {
        // counts coins which have value 25
        $c = (int)($n / 25);

        if ($n % 25 < 10) 
        {

            // counts coins which have value 1 and 25
            $c = $c + $n % 25;

            return $c;
        }
        if ($n % 25 > 9)
        {
            // counts coins which have value 1, 10 and 25
            $c = $c + ($n % 25) / 10 + ($n % 25) % 10;

            return $c;
        }
    }

    return $c;
}

// Driver Code
$n = 14;
echo(countCoins($n));

// This code is contributed Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to find the minimum number
// of coins required

// Function to find the minimum number
// of coins required
function countCoins( n)
{
    var c = 0;

    if (n < 10)
    {

        // counts coins which have value 1
        // we will need n coins of value 1
        return n;
    }
    if (n > 9 && n < 25)
    {

        // counts coins which have value 1 and 10
        c = n / 10 + n % 10;
        return Math.trunc(c);
    }
    if (n > 24) 
    {

        // counts coins which have value 25
        c = n / 25;
        if (n % 25 < 10)
        {

            // counts coins which have value 1 and 25
            c = c + n % 25;
            return Math.trunc(c);
        }

        if (n % 25 > 9)
        {

            // counts coins which have value 1, 10 and 25
            c = c + (n % 25) / 10 + (n % 25) % 10;
            return Math.trunc(c);
        }
    }
}

var n = 14;
document.write(countCoins(n));

// This code is contributed by akshitsaxenaa09.
</script>
```

**Output:** 

```
5
```