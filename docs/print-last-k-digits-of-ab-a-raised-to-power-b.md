# 打印 a^b 的最后 k 位数字(a 升到 b 的幂)

> 原文:[https://www . geeksforgeeks . org/print-最后 k 位数-a B- a-升幂-b/](https://www.geeksforgeeks.org/print-last-k-digits-of-ab-a-raised-to-power-b/)

给定正整数 k，a 和 b，我们需要打印 a^b ie 的最后 k 位数字..功率(a，b)。

```
Input Constraint:
k <= 9, a <= 10^6, b<= 10^6
```

**示例:**

```
Input : a = 11, b = 3, k = 2
Output : 31
Explanation : a^b = 11^3 = 1331, hence 
last two digits are 31

Input : a = 10, b = 10000, k = 5
Output : 00000
Explanation : a^b = 1000..........0 (total 
zeros = 10000), hence last 5 digits are 00000
```

## 天真的解决方案

首先计算 a^b，然后通过与 10^k.取模取最后 k 位。当 a^b 太大时，上述解决方案失败，因为我们在 C/C++中最多只能容纳 2^64 -1。

## 有效解

有效的方法是每次乘法后只保留 k 个数字。这个想法与[模幂运算](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)中讨论的非常相似，在这里我们讨论了一种寻找的一般方法(a^b)%c，这里的 c 是 10^k.

下面是实现。

## C++

```
// C++ code to find last k digits of a^b
#include <iostream>
using namespace std;

/* Iterative Function to calculate (x^y)%p in O(log y) */
int power(long long int x, long long int y, long long int p)
{
    long long int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// C++ function to calculate
// number of digits in x
int numberOfDigits(int x)
{
    int i = 0;
    while (x) {
        x /= 10;
        i++;
    }
    return i;
}

// C++ function to print last k digits of a^b
void printLastKDigits(int a, int b, int k)
{
    cout << "Last " << k;
    cout << " digits of " << a;
    cout << "^" << b << " = ";

    // Generating 10^k
    int temp = 1;
    for (int i = 1; i <= k; i++)
        temp *= 10;

    // Calling modular exponentiation
    temp = power(a, b, temp);

    // Printing leftmost zeros. Since (a^b)%k
    // can have digits less then k. In that
    // case we need to print zeros
    for (int i = 0; i < k - numberOfDigits(temp); i++)
        cout << 0;

    // If temp is not zero then print temp
    // If temp is zero then already printed
    if (temp)
        cout << temp;
}

// Driver program to test above functions
int main()
{
    int a = 11;
    int b = 3;
    int k = 2;
    printLastKDigits(a, b, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find last k digits of a^b

public class GFG
{
    /* Iterative Function to calculate (x^y)%p in O(log y) */
    static int power(long x, long y, long p)
    {
        long res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0) {

            // If y is odd, multiply x with result
            if ((y & 1) != 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return (int) res;
    }

    // Method  to print last k digits of a^b
    static void printLastKDigits(int a, int b, int k)
    {
        System.out.print("Last " + k + " digits of " + a +
                            "^"  +  b + " = ");

        // Generating 10^k
        int temp = 1;
        for (int i = 1; i <= k; i++)
            temp *= 10;

        // Calling modular exponentiation
        temp = power(a, b, temp);

        // Printing leftmost zeros. Since (a^b)%k
        // can have digits less then k. In that
        // case we need to print zeros
        for (int i = 0; i < k - Integer.toString(temp).length() ; i++)
            System.out.print(0);

        // If temp is not zero then print temp
        // If temp is zero then already printed
        if (temp != 0)
            System.out.print(temp);
    }

    // Driver Method
    public static void main(String[] args)
    {
        int a = 11;
        int b = 3;
        int k = 2;
        printLastKDigits(a, b, k);
    }
}
```

## 蟒蛇 3

```
# Python 3 code to find last
# k digits of a^b

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0) :

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# function to calculate
# number of digits in x
def numberOfDigits(x):

    i = 0
    while (x) :
        x //= 10
        i += 1

    return i

# function to print last k digits of a^b
def printLastKDigits( a, b, k):

    print("Last " + str( k)+" digits of " +
                    str(a) + "^" + str(b), end = " = ")

    # Generating 10^k
    temp = 1
    for i in range(1, k + 1):
        temp *= 10

    # Calling modular exponentiation
    temp = power(a, b, temp)

    # Printing leftmost zeros. Since (a^b)%k
    # can have digits less then k. In that
    # case we need to print zeros
    for i in range( k - numberOfDigits(temp)):
        print("0")

    # If temp is not zero then print temp
    # If temp is zero then already printed
    if (temp):
        print(temp)

# Driver Code
if __name__ == "__main__":
    a = 11
    b = 3
    k = 2
    printLastKDigits(a, b, k)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find last k digits of a^b
using System;

class GFG
{

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(long x, long y, long p)
{
    long res = 1; // Initialize result

    x = x % p; // Update x if it is more
               // than or equal to p

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return (int) res;
}

// Method to print last k digits of a^b
static void printLastKDigits(int a, int b, int k)
{
    Console.Write("Last " + k + " digits of " +
                            a + "^" + b + " = ");

    // Generating 10^k
    int temp = 1;
    for (int i = 1; i <= k; i++)
        temp *= 10;

    // Calling modular exponentiation
    temp = power(a, b, temp);

    // Printing leftmost zeros. Since (a^b)%k
    // can have digits less then k. In that
    // case we need to print zeros
    for (int i = 0;    
             i < k - temp.ToString().Length; i++)
        Console.WriteLine(0);

    // If temp is not zero then print temp
    // If temp is zero then already printed
    if (temp != 0)
        Console.Write(temp);
}

// Driver Code
public static void Main()
{
    int a = 11;
    int b = 3;
    int k = 2;
    printLastKDigits(a, b, k);
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find last k digits of a^b

/* Iterative Function to calculate
   (x^y)%p in O(log y) */

function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it is more
                  // than or equal to p

    while ($y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// function to calculate
// number of digits in x
function numberOfDigits($x)
{
    $i = 0;
    while ($x)
    {
        $x = (int)$x / 10;
        $i++;
    }
    return $i;
}

// function to print last k digits of a^b
function printLastKDigits( $a, $b, $k)
{
    echo "Last ",$k;
    echo " digits of " ,$a;
    echo "^" , $b , " = ";

    // Generating 10^k
    $temp = 1;
    for ($i = 1; $i <= $k; $i++)
        $temp *= 10;

    // Calling modular exponentiation
    $temp = power($a, $b, $temp);

    // Printing leftmost zeros. Since
    // (a^b)%k can have digits less
    // then k. In that case we need
    // to print zeros
    for ($i = 0;
         $i < $k - numberOfDigits($temp); $i++)
        echo 0;

    // If temp is not zero then print temp
    // If temp is zero then already printed
    if ($temp)
        echo $temp;
}

// Driver Code
$a = 11;
$b = 3;
$k = 2;
printLastKDigits($a, $b, $k);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript code to find last k digits of a^b

    /* Iterative Function to calculate (x^y)%p in O(log y) */
    function power(x , y , p) {
        var res = 1; // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0) {

            // If y is odd, multiply x with result
            if ((y & 1) != 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return parseInt( res);
    }

    // Method to print last k digits of a^b
    function printLastKDigits(a , b , k) {
        document.write("Last " + k + " digits of " + a + "^" + b + " = ");

        // Generating 10^k
        var temp = 1;
        for (i = 1; i <= k; i++)
            temp *= 10;

        // Calling modular exponentiation
        temp = power(a, b, temp);

        // Printing leftmost zeros. Since (a^b)%k
        // can have digits less then k. In that
        // case we need to print zeros
        for (i = 0; i < k - temp.toString().length; i++)
            document.write(0);

        // If temp is not zero then print temp
        // If temp is zero then already printed
        if (temp != 0)
            document.write(temp);
    }

    // Driver Method

        var a = 11;
        var b = 3;
        var k = 2;
        printLastKDigits(a, b, k);

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
Last 2 digits of 11^3 = 31
```

**时间复杂度:**O(log b)
T3】空间复杂度: O(1)
本文由 [**Pratik Chhajer**](https://github.com/pratik-chhajer) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。