# 打印给定范围内的所有好号

> 原文:[https://www . geesforgeks . org/print-all-good-numbers-in-给定范围/](https://www.geeksforgeeks.org/print-all-good-numbers-in-given-range/)

给定一个数字“d”和一个范围[L，R]，其中 L < R, print all good numbers in given range that don’t contain digit ‘d’. A number is good if its every digit is larger than the sum of digits which are on the right side of that digit. For example 9620 is good number because 2 > 0，6 > 2+0 和 9 > 6+2+0。

**示例:**

```
Input:  L = 410, R = 520, d = 3
Output: 410 420 421 510 520 
All the numbers in output are good (every digit is more
than sum of digits on right of it) and don't have digit 3.

Input:  L = 410, R = 520, d = 1
Output: 420 430 520 
All the numbers in output are good (every digit is more
than sum of digits on right of it) and don't have digit 1.
```

这个想法是遍历给定范围内的所有数字。对于每个数字，遍历所有数字。遍历时，记录到目前为止的数字和。在任何时候，如果先前的总和大于或等于总和，则返回 false。此外，如果当前数字变为“d”，则返回 false。

下面是这个想法的实现。

## C++

```
// C++ program to print good numbers in a given range [L, R]
#include<bits/stdc++.h>
using namespace std;

// To check whether n is a good number and doesn't contain
// digit 'd'.
bool isValid(int n, int d)
{
    // Get last digit and initialize sum from right side
    int digit = n%10;
    int sum = digit;

    // If last digit is d, return
    if (digit == d)
    return false;

    // Traverse remaining digits
    n /= 10;
    while (n)
    {
        // Current digit
        digit = n%10;

        // If digit is d or digit is less than or
        // equal to sum of digits on right side
        if (digit == d || digit <= sum)
            return false;

        // Update sum and n
        else
        {
            sum += digit;
            n /= 10;
        }
    }
    return 1;
}

// Print Good numbers in range [L, R]
void printGoodNumbers(int L, int R, int d)
{
// Traverse all numbers in given range
for (int i=L; i<=R; i++)
{
    // If current numbers is good, print it.
    if (isValid(i, d))
        cout << i << " ";
}
}

// Driver program
int main()
{
    int L = 410, R = 520, d = 3;

    // Print good numbers in [L, R]
    printGoodNumbers(L, R, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print good numbers in a given range [L, R]
import java.io.*;

class Numbers
{
    // Function to check whether n is a good number and doesn't contain
    // digit 'd'
    static boolean isValid(int n, int d)
    {
        // Get last digit and initialize sum from right side
        int digit = n%10;
        int sum = digit;

        // If last digit is d, return
        if (digit == d)
        return false;

        // Traverse remaining digits
        n /= 10;
        while (n>0)
        {
            // Current digit
            digit = n%10;

            // If digit is d or digit is less than or
            // equal to sum of digits on right side
            if (digit == d || digit <= sum)
                return false;

            // Update sum and n
                else
                {
                    sum += digit;
                    n /= 10;
                }
        }
    return true;
    }

    // Print Good numbers in range [L, R]
    static void printGoodNumber(int L, int R, int d)
    {
        // Traverse all numbers in given range
        for(int i=L;i<=R;i++)
        {
            // If current numbers is good, print it
            if(isValid(i, d))
                System.out.print(i+" ");
        }
    }

    // Driver program
    public static void main (String[] args)
    {
        int L = 410, R = 520, d = 3;

        // Print good numbers in [L, R]
        printGoodNumber(L, R, d);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print good
# numbers in a given range [L, R]

# Function to check whether n is
# a good number and doesn't contain
# digit 'd'
def isValid(n, d):

    # Get last digit and initialize
    # sum from right side
    digit = n % 10;
    sum = digit;

    # If last digit is d, return
    if (digit == d):
        return False;

    # Traverse remaining digits
    n = int(n / 10);
    while (n > 0):

        # Current digit
        digit = n % 10;

        # If digit is d or digit is
        # less than or equal to sum
        # of digits on right side
        if(digit == d or digit <= sum):
            return False;

        # Update sum and n
        else:
            sum += digit;
            n = int(n / 10);
    return True;

# Print Good numbers in range [L, R]
def printGoodNumber(L, R, d):

    # Traverse all numbers
    # in given range
    for i in range(L, R + 1):

        # If current numbers is good,
        # print it
        if(isValid(i, d)):
            print(i, end = " ");

# Driver Code
L = 410;
R = 520;
d = 3;

# Print good numbers in [L, R]
printGoodNumber(L, R, d);

# This code is contributed by mits
```

## C#

```
// C# program to print good numbers in a
// given range [L, R]
using System;

class GFG {

    // Function to check whether n is a good
    // number and doesn't contain digit 'd'
    static bool isValid(int n, int d)
    {

        // Get last digit and initialize
        // sum from right side
        int digit = n % 10;
        int sum = digit;

        // If last digit is d, return
        if (digit == d)
            return false;

        // Traverse remaining digits
        n /= 10;
        while (n > 0)
        {

            // Current digit
            digit = n % 10;

            // If digit is d or digit is
            // less than or equal to sum of
            // digits on right side
            if (digit == d || digit <= sum)
                return false;

            // Update sum and n
            else
            {
                sum += digit;
                n /= 10;
            }
        }

    return true;
    }

    // Print Good numbers in range [L, R]
    static void printGoodNumber(int L,
                               int R, int d)
    {

        // Traverse all numbers in given range
        for(int i = L; i <= R; i++)
        {

            // If current numbers is good,
            // print it
            if(isValid(i, d))
                Console.Write(i+" ");
        }
    }

    // Driver program
    public static void Main ()
    {
        int L = 410, R = 520, d = 3;

        // Print good numbers in [L, R]
        printGoodNumber(L, R, d);
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print good
// numbers in a given range [L, R]

// To check whether n is a good
// number and doesn't contain digit 'd'.
function isValid($n, $d)
{
    // Get last digit and initialize
    // sum from right side
    $digit = $n % 10;
    $sum = $digit;

    // If last digit is d, return
    if ($digit == $d)
    return false;

    // Traverse remaining digits
    $n = (int)($n / 10);
    while ($n)
    {
        // Current digit
        $digit = $n % 10;

        // If digit is d or digit is less
        // than or equal to sum of digits
        // on right side
        if ($digit == $d || $digit <= $sum)
            return false;

        // Update sum and n
        else
        {
            $sum += $digit;
            $n = (int)($n / 10);
        }
    }
    return 1;
}

// Print Good numbers in range [L, R]
function printGoodNumbers($L, $R, $d)
{
// Traverse all numbers in given range
for ($i = $L; $i <= $R; $i++)
{
    // If current numbers is good,
    // print it.
    if (isValid($i, $d))
        echo $i . " ";
}
}

// Driver Code
$L = 410;
$R = 520;
$d = 3;

// Print good numbers in [L, R]
printGoodNumbers($L, $R, $d);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print good numbers
// in a given range [L, R]class Numbers

// Function to check whether n is a good
// number and doesn't contain digit 'd'
function isValid(n, d)
{

    // Get last digit and initialize
    // sum from right side
    var digit = n % 10;
    var sum = digit;

    // If last digit is d, return
    if (digit == d)
        return false;

    // Traverse remaining digits
    n = parseInt(n / 10);
    while (n > 0)
    {

        // Current digit
        digit = n%10;

        // If digit is d or digit is less than or
        // equal to sum of digits on right side
        if (digit == d || digit <= sum)
            return false;

        // Update sum and n
        else
        {
            sum += digit;
            n = parseInt(n / 10);
        }
    }
    return true;
}

// Print Good numbers in range [L, R]
function printGoodNumber(L, R, d)
{

    // Traverse all numbers in given range
    for(i = L; i <= R; i++)
    {

        // If current numbers is good, print it
        if (isValid(i, d))
            document.write(i + " ");
    }
}

// Driver code
var L = 410, R = 520, d = 3;

// Print good numbers in [L, R]
printGoodNumber(L, R, d);

// This code is contributed by shikhasingrajput

</script>
```

**输出:**

```
 410 420 421 510 520 
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息