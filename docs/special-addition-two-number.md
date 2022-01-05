# 两个数字的无进位相加

> 原文:[https://www.geeksforgeeks.org/special-addition-two-number/](https://www.geeksforgeeks.org/special-addition-two-number/)

给你两个正数 n 和 m，你必须简单地找到这两个数的加法，但是给定一个条件，在这个加法中没有任何进位系统。也就是说，在较高的 msb 时不添加进位。
**例:**

```
Input : m = 456, n = 854
Output : 200

Input : m = 456, n = 4
Output : 450
```

**算法:**

```
Input n, m while(n||m)
    {
        // Add each bits 
        bit_sum = (n%10) + (m%10);

        // Neglect carry
        bit_sum %= 10;

        // Update result
        // multiplier to maintain place value
        res = (bit_sum * multiplier) + res;
        n /= 10;
        m /= 10;

        // Update multiplier
        multiplier *=10;
    } print res
```

**方法:**
为了解决这个问题，我们需要一点一点地增加数字，从最右边的一位(LSB)开始增加两个数字，并从两个位置相同的数字增加整数。此外，我们将忽略每个位置进位，以便进位不会影响更高的位位置。
开始一位一位地将两个数相加，对于每一位取整数的和，然后忽略它们的进位，取 bit_sum 的模 10，通过将 bit_sum 与指定位置值的乘数相乘，进一步将 bit_sum 与 res 相加。(每次迭代乘数增加 10 倍。)
以下是上述办法的执行情况:

## C++

```
// CPP program for special
// addition of two number
#include <bits/stdc++.h>
using namespace std;

int xSum(int n, int m)
{
    // variable to store result  
    int res = 0;

    // variable to maintain
    // place value
    int multiplier = 1;

    // variable to maintain
    // each digit sum
    int bit_sum;

    // Add numbers till each
    // number become zero
    while (n || m) {

        // Add each bits
        bit_sum = (n % 10) + (m % 10);

        // Neglect carry
        bit_sum %= 10;

        // Update result
        res = (bit_sum * multiplier) + res;
        n /= 10;
        m /= 10;

        // Update multiplier
        multiplier *= 10;
    }
    return res;
}

// Driver program
int main()
{
    int n = 8458;
    int m = 8732;
    cout << xSum(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for special
// addition of two number
import java.util.*;
import java.lang.*;

public class GfG {

    public static int xSum(int n, int m)
    {
        int res = 0;
        int multiplier = 1;
        int bit_sum;

        // Add numbers till each
        // number become zero
        while (true) {

            if(n==0 && m==0)
            break;

            // Add each bits
            bit_sum = (n % 10) + (m % 10);

            // Neglect carry
            bit_sum %= 10;

            // Update result
            res = (bit_sum * multiplier) + res;
            n /= 10;
            m /= 10;

            // Update multiplier
            multiplier *= 10;

        }
        return res;
    }

    // Driver function
    public static void main(String args[])
    {
        int n = 8458;
        int m = 8732;
        System.out.println(xSum(n, m));
    }
}
/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 program for special
# addition of two number
import math

def xSum(n, m) :

    # variable to
    # store result
    res = 0

    # variable to maintain
    # place value
    multiplier = 1

    # variable to maintain
    # each digit sum
    bit_sum = 0

    # Add numbers till each
    # number become zero
    while (n or m) :

        # Add each bits
        bit_sum = ((n % 10) +
                   (m % 10))

        # Neglect carry
        bit_sum = bit_sum % 10

        # Update result
        res = (bit_sum *
               multiplier) + res
        n = math.floor(n / 10)
        m = math.floor(m / 10)

        # Update multiplier
        multiplier = multiplier * 10

    return res

# Driver code
n = 8458
m = 8732
print (xSum(n, m))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program for special
// addition of two number
using System;

public class GfG {

    public static int xSum(int n, int m)
    {
        int res = 0;
        int multiplier = 1;
        int bit_sum;

        // Add numbers till each
        // number become zero
        while (true) {

            // Add each bits
            bit_sum = (n % 10) + (m % 10);

            // Neglect carry
            bit_sum %= 10;

            // Update result
            res = (bit_sum * multiplier) + res;
            n /= 10;
            m /= 10;

            // Update multiplier
            multiplier *= 10;
            if (n == 0)
                break;
            if (m == 0)
                break;
        }
        return res;
    }

    // Driver function
    public static void Main()
    {
        int n = 8458;
        int m = 8732;
        Console.WriteLine(xSum(n, m));
    }
}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program for special
// addition of two number

function xSum($n, $m)
{

    // variable to store result
    $res = 0;

    // variable to maintain
    // place value
    $multiplier = 1;

    // variable to maintain
    // each digit sum
    $bit_sum;

    // Add numbers till each
    // number become zero
    while ($n || $m) {

        // Add each bits
        $bit_sum = ($n % 10) +
                   ($m % 10);

        // Neglect carry
        $bit_sum %= 10;

        // Update result
        $res = ($bit_sum * $multiplier) + $res;
        $n =floor($n / 10);
        $m =floor($m / 10);

        // Update multiplier
        $multiplier *= 10;
    }
    return $res;
}

    // Driver code
    $n = 8458;
    $m = 8732;
    echo xSum($n, $m);

//This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for special
// addition of two number
function xSum(n, m)
{
    // variable to store result
    var res = 0;

    // variable to maintain
    // place value
    var multiplier = 1;

    // variable to maintain
    // each digit sum
    var bit_sum;

    // Add numbers till each
    // number become zero
    while (n || m) {

        // Add each bits
        bit_sum = (n % 10) + (m % 10);

        // Neglect carry
        bit_sum %= 10;

        // Update result
        res = (bit_sum * multiplier) + res;
        n = parseInt(n / 10);
        m = parseInt(m / 10);

        // Update multiplier
        multiplier *= 10;
    }
    return res;
}

// Driver program
var n = 8458;
var m = 8732;
document.write(xSum(n, m));

    // This code is contributed by noob2000.
</script>
```

**输出:**

```
6180
```