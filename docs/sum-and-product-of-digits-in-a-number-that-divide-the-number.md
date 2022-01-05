# 一个数中数字的和与积除以该数

> 原文:[https://www . geeksforgeeks . org/除以数字的数字和积/](https://www.geeksforgeeks.org/sum-and-product-of-digits-in-a-number-that-divide-the-number/)

给定正整数 **N** 。任务是找出数的位数的和与积，将数 n 等分
**例:**

```
Input: N = 12
Output: Sum = 3, product = 2
1 and 2 divide 12\. So, their sum is 3 and product is 2.

Input: N = 1012
Output: Sum = 4, product = 2
1, 1 and 2 divide 1012.
```

**逼近:**思路是用模 10 求数 n 的每个数字，然后检查它是否除 n。相应地，把它加到和上，然后乘以乘积。请注意，数字可以是 0，所以请注意这种情况。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Print the sum and product of digits
//  that divides the number.
void countDigit(int n)
{
    int temp = n, sum = 0, product = 1;
    while (temp != 0) {

        // Fetching each digit of the number
        int d = temp % 10;
        temp /= 10;

        // Checking if digit is greater than 0
        // and can divides n.
        if (d > 0 && n % d == 0) {
            sum += d;
            product *= d;
        }
    }

    cout << "Sum = " << sum;
    cout << "\nProduct = " << product;
}

// Driver code
int main()
{
    int n = 1012;

    countDigit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.lang.*;
import java.util.*;

class GFG
{
// Print the sum and product of
// digits that divides the number.
static void countDigit(int n)
{
    int temp = n, sum = 0, product = 1;
    while (temp != 0)
    {

        // Fetching each digit of
        // the number
        int d = temp % 10;
        temp /= 10;

        // Checking if digit is greater
        // than 0 and can divides n.
        if (d > 0 && n % d == 0)
        {
            sum += d;
            product *= d;
        }
    }

    System.out.print("Sum = " + sum);
    System.out.print("\nProduct = " + product);
}

// Driver code
public static void main(String args[])
{
    int n = 1012;

    countDigit(n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Print the sum and product of digits
# that divides the number.
def countDigit(n):
    temp = n
    sum = 0
    product = 1
    while(temp != 0):

        # Fetching each digit of the number
        d = temp % 10
        temp //= 10

        # Checking if digit is greater
        # than 0 and can divides n.
        if(d > 0 and n % d == 0):
            sum += d
            product *= d

    print("Sum =", sum)
    print("Product =", product)

# Driver code
if __name__=='__main__':

    n = 1012
    countDigit(n)

# This code is contributed
# by Kirti_Mangal

```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
// Print the sum and product of
// digits that divides the number.
static void countDigit(int n)
{
    int temp = n, sum = 0, product = 1;
    while (temp != 0)
    {

        // Fetching each digit of
        // the number
        int d = temp % 10;
        temp /= 10;

        // Checking if digit is greater
        // than 0 and can divides n.
        if (d > 0 && n % d == 0)
        {
            sum += d;
            product *= d;
        }
    }

    Console.Write("Sum = " + sum);
    Console.Write("\nProduct = " + product);
}

// Driver code
public static void Main()
{
    int n = 1012;

    countDigit(n);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Print the sum and product of digits
// that divides the number.
function countDigit($n)
{
    $temp = $n;
    $sum = 0;
    $product = 1;
    while ($temp != 0) {

        // Fetching each digit of the number
        $d = $temp % 10;
        $temp =(int)($temp/10);

        // Checking if digit is greater than 0
        // and can divides n.
        if ($d > 0 && $n % $d == 0) {
            $sum += $d;
            $product *= $d;
        }
    }

    echo "Sum = ".$sum;
    echo "\nProduct = ".$product;
}

// Driver code

    $n = 1012;

    countDigit($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// java script  implementation of the above approach

// Print the sum and product of digits
// that divides the number.
function countDigit(n)
{
    let temp = n;
    let sum = 0;
    let product = 1;
    while (temp != 0) {

        // Fetching each digit of the number
        let d = temp % 10;
        temp =parseInt(temp/10);

        // Checking if digit is greater than 0
        // and can divides n.
        if (d > 0 && n % d == 0) {
            sum += d;
            product *= d;
        }
    }

    document.write( "Sum = "+sum);
    document.write( "<br>Product = "+product);
}

// Driver code

    let n = 1012;

    countDigit(n);

// This code is contributed by Gottumukkala Bobby
</script>
```

**Output:** 

```
Sum = 4
Product = 2
```