# N 与其最大奇数位的乘积

> 原文:[https://www . geeksforgeeks . org/n 产品及其最大奇数位/](https://www.geeksforgeeks.org/product-of-n-with-its-largest-odd-digit/)

给定一个整数 **N** ，任务是找到奇数位最大的 **N** 的乘积。如果 **N** 中没有奇数，则打印 **-1** 作为输出。
**举例:**

> **输入:**12345
> T3】输出:61725
> 12345 中最大的奇数位是 5 和 12345 * 5 = 61725
> **输入:** 24068
> **输出:** -1

**方式:**遍历 **N** 的所有数字，设置 **maxOdd = -1** ，如果当前数字为奇数 **> maxOdd** 则更新 **maxOdd =当前数字**。
如果最后， **maxOdd = -1** 则打印 **-1** 否则打印 **N * maxOdd** 。
以下是上述方法的实施:

## C++

```
// C++ program to find the product of N
// with its largest odd digit
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest odd digit in n
int largestOddDigit(int n)
{
    // If all digits are even then -1 will be returned
    int maxOdd = -1;
    while (n > 0) {

        // Last digit from n
        int digit = n % 10;

        // If current digit is odd and > maxOdd
        if (digit % 2 == 1 && digit > maxOdd)
            maxOdd = digit;

        // Remove last digit
        n = n / 10;
    }

    // Return the maximum odd digit
    return maxOdd;
}

// Function to return the product of n
// with its largest odd digit
int getProduct(int n)
{
    int maxOdd = largestOddDigit(n);

    // If there are no odd digits in n
    if (maxOdd == -1)
        return -1;

    // Product of n with its largest odd digit
    return (n * maxOdd);
}

// Driver code
int main()
{
    int n = 12345;
    cout << getProduct(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of N
// with its largest odd digit

class GFG
{

// Function to return the largest
// odd digit in n
static int largestOddDigit(int n)
{
    // If all digits are even then -1
    // will be returned
    int maxOdd = -1;
    while (n > 0)
    {

        // Last digit from n
        int digit = n % 10;

        // If current digit is odd and > maxOdd
        if (digit % 2 == 1 && digit > maxOdd)
            maxOdd = digit;

        // Remove last digit
        n = n / 10;
    }

    // Return the maximum odd digit
    return maxOdd;
}

// Function to return the product of n
// with its largest odd digit
static int getProduct(int n)
{
    int maxOdd = largestOddDigit(n);

    // If there are no odd digits in n
    if (maxOdd == -1)
        return -1;

    // Product of n with its largest odd digit
    return (n * maxOdd);
}

// Driver code
public static void main(String[] args)
{
    int n = 12345;
    System.out.println(getProduct(n));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find the product
# of N with its largest odd digit

# Function to return the largest
# odd digit in n
def largestOddDigit(n) :

    # If all digits are even then -1
    # will be returned
    maxOdd = -1
    while (n > 0) :

        # Last digit from n
        digit = n % 10

        # If current digit is odd and > maxOdd
        if (digit % 2 == 1 and digit > maxOdd) :
            maxOdd = digit

        # Remove last digit
        n = n // 10

    # Return the maximum odd digit
    return maxOdd

# Function to return the product
# of n with its largest odd digit
def getProduct(n) :

    maxOdd = largestOddDigit(n)

    # If there are no odd digits in n
    if (maxOdd == -1) :
        return -1

    # Product of n with its largest
    # odd digit
    return (n * maxOdd)

# Driver code
if __name__ == "__main__" :

    n = 12345
    print(getProduct(n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the product of N
// with its largest odd digit
using System;

class GFG
{

// Function to return the largest
// odd digit in n
static int largestOddDigit(int n)
{
    // If all digits are even then -1
    // will be returned
    int maxOdd = -1;
    while (n > 0)
    {

        // Last digit from n
        int digit = n % 10;

        // If current digit is odd and > maxOdd
        if (digit % 2 == 1 && digit > maxOdd)
            maxOdd = digit;

        // Remove last digit
        n = n / 10;
    }

    // Return the maximum odd digit
    return maxOdd;
}

// Function to return the product of n
// with its largest odd digit
static int getProduct(int n)
{
    int maxOdd = largestOddDigit(n);

    // If there are no odd digits in n
    if (maxOdd == -1)
        return -1;

    // Product of n with its largest odd digit
    return (n * maxOdd);
}

// Driver code
public static void Main()
{
    int n = 12345;
    Console.Write(getProduct(n));
}
}

// This code is contributed
// by Akanksha_Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the product
// of N with its largest odd digit

// Function to return the largest
// odd digit in n
function largestOddDigit($n)
{
    // If all digits are even then
    // -1 will be returned
    $maxOdd = -1;
    while ($n > 0)
    {

        // Last digit from n
        $digit = $n % 10;

        // If current digit is odd and > maxOdd
        if ($digit % 2 == 1 && $digit > $maxOdd)
            $maxOdd = $digit;

        // Remove last digit
        $n = $n / 10;
    }

    // Return the maximum odd digit
    return $maxOdd;
}

// Function to return the product
// of n with its largest odd digit
function getProduct($n)
{
    $maxOdd = largestOddDigit($n);

    // If there are no odd digits in n
    if ($maxOdd == -1)
        return -1;

    // Product of n with its largest
    // odd digit
    return ($n * $maxOdd);
}

// Driver code
$n = 12345;
echo getProduct($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript program to find the product of N
// with its largest odd digit

    // Function to return the largest
    // odd digit in n
    function largestOddDigit(n)
    {

        // If all digits are even then -1
        // will be returned
        var maxOdd = -1;
        while (n > 0)
        {

            // Last digit from n
            var digit = n % 10;

            // If current digit is odd and > maxOdd
            if (digit % 2 == 1 && digit > maxOdd)
                maxOdd = digit;

            // Remove last digit
            n = n / 10;
        }

        // Return the maximum odd digit
        return maxOdd;
    }

    // Function to return the product of n
    // with its largest odd digit
    function getProduct(n)
    {
        var maxOdd = largestOddDigit(n);

        // If there are no odd digits in n
        if (maxOdd == -1)
            return -1;

        // Product of n with its largest odd digit
        return (n * maxOdd);
    }

    // Driver code
    var n = 12345;
    document.write(getProduct(n));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
61725
```