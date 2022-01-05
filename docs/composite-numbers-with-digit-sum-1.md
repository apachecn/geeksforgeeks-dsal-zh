# 数字和为 1 的复合数字

> 原文:[https://www . geesforgeks . org/composite-numbers-with-digital-sum-1/](https://www.geeksforgeeks.org/composite-numbers-with-digit-sum-1/)

给定一个范围**【L，R】**，任务是从该范围中找出所有复合的数字，并且它们的数字的最终总和是 **1** 。
**例:**

> **输入:** L = 10，R = 100
> **输出:**10 28 46 55 64 82 91 100
> 10 = 1+0 = 1
> 28 = 2+8 = 10 = 1+0 = 1
> …
> 91 = 9+1 = 10 = 1+0 = 1
> 100 = 1+0+0 = 1
> **输入:** L

**方法:**对于范围内的每个数字，检查该数字是否为[复合](https://www.geeksforgeeks.org/composite-number/)，即它的除数不是 1，而是数字本身。如果当前数字是一个复合数字，那么继续计算它的数字总和，直到数字减少到一个数字，如果这个数字是 1，那么选择的数字是一个有效的数字。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function that returns true if number n
// is a composite number
bool isComposite(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function that returns true if the eventual
// digit sum of number nm is 1
bool isDigitSumOne(int nm)
{

    // Loop till the sum is not single digit number
    while (nm > 9) {

        // Initialize the sum as zero
        int sum_digit = 0;

        // Find the sum of digits
        while (nm > 0) {
            int digit = nm % 10;
            sum_digit = sum_digit + digit;
            nm = nm / 10;
        }
        nm = sum_digit;
    }

    // If sum is eventually 1
    if (nm == 1)
        return true;
    else
        return false;
}

// Function to print the required numbers
// from the given range
void printValidNums(int l, int r)
{
    for (int i = l; i <= r; i++) {

        // If i is one of the required numbers
        if (isComposite(i) && isDigitSumOne(i))
            cout << i << " ";
    }
}

// Driver code
int main(void)
{
    int l = 10, r = 100;

    printValidNums(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
public class GFG {

    // Function that returns true if number n
    // is a composite number
    static boolean isComposite(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return false;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return true;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return true;

        return false;
    }

    // Function that returns true if the eventual
    // digit sum of number nm is 1
    static boolean isDigitSumOne(int nm)
    {

        // Loop till the sum is not single
        // digit number
        while (nm > 9) {

            // Initialize the sum as zero
            int sum_digit = 0;

            // Find the sum of digits
            while (nm > 0) {
                int digit = nm % 10;
                sum_digit = sum_digit + digit;
                nm = nm / 10;
            }
            nm = sum_digit;
        }

        // If sum is eventually 1
        if (nm == 1)
            return true;
        else
            return false;
    }

    // Function to print the required numbers
    // from the given range
    static void printValidNums(int l, int r)
    {
        for (int i = l; i <= r; i++) {

            // If i is one of the required numbers
            if (isComposite(i) && isDigitSumOne(i))
                System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main(String arg[])
    {
        int l = 10, r = 100;
        printValidNums(l, r);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if number n
# is a composite number
def isComposite(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return False

    # This is checked so that we can skip 
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return True
    i = 5
    while(i * i <= n):

        if (n % i == 0 or n % (i + 2) == 0):
            return True
        i = i + 6

    return False

# Function that returns true if the eventual
# digit sum of number nm is 1
def isDigitSumOne(nm) :

    # Loop till the sum is not single
    # digit number
    while(nm>9) :

        # Initialize the sum as zero
        sum_digit = 0

        # Find the sum of digits
        while(nm != 0) :
            digit = nm % 10
            sum_digit = sum_digit + digit
            nm = nm // 10
        nm = sum_digit

    # If sum is eventually 1
    if(nm == 1):
        return True
    else:
        return False

# Function to print the required numbers
# from the given range
def printValidNums(m, n ):
    for i in range(m, n + 1):

        # If i is one of the required numbers
        if(isComposite(i) and isDigitSumOne(i)) :
            print(i, end =" ")

# Driver code
l = 10
r = 100
printValidNums(m, n)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function that returns true if number n
    // is a composite number
    static bool isComposite(int n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return false;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return true;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return true;

        return false;
    }

    // Function that returns true if the
    // eventual digit sum of number nm is 1
    static bool isDigitSumOne(int nm)
    {

        // Loop till the sum is not single
        // digit number
        while (nm > 9)
        {

            // Initialize the sum as zero
            int sum_digit = 0;

            // Find the sum of digits
            while (nm > 0)
            {
                int digit = nm % 10;
                sum_digit = sum_digit + digit;
                nm = nm / 10;
            }
            nm = sum_digit;
        }

        // If sum is eventually 1
        if (nm == 1)
            return true;
        else
            return false;
    }

    // Function to print the required numbers
    // from the given range
    static void printValidNums(int l, int r)
    {
        for (int i = l; i <= r; i++)
        {

            // If i is one of the required numbers
            if (isComposite(i) && isDigitSumOne(i))
                Console.Write(i + " ");
        }
    }

    // Driver code
    static public void Main ()
    {
        int l = 10, r = 100;
        printValidNums(l, r);
    }
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function that returns true if number n
// is a composite number
function isComposite($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return true;

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
            return true;

    return false;
}

// Function that returns true if the eventual
// digit sum of number nm is 1
function isDigitSumOne($nm)
{

    // Loop till the sum is not single
    // digit number
    while ($nm > 9)
    {

        // Initialize the sum as zero
        $sum_digit = 0;

        // Find the sum of digits
        while ($nm > 0)
        {
            $digit = $nm % 10;
            $sum_digit = $sum_digit + $digit;
            $nm = floor($nm / 10);
        }
        $nm = $sum_digit;
    }

    // If sum is eventually 1
    if ($nm == 1)
        return true;
    else
        return false;
}

// Function to print the required numbers
// from the given range
function printValidNums($l, $r)
{
    for ($i = $l; $i <= $r; $i++)
    {

        // If i is one of the required numbers
        if (isComposite($i) && isDigitSumOne($i))
            echo $i, " ";
    }
}

// Driver code
$l = 10; $r = 100;

printValidNums($l, $r);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function that returns true if number n
// is a composite number
function isComposite(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return false;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return true;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return true;

    return false;
}

// Function that returns true if the eventual
// digit sum of number nm is 1
function isDigitSumOne(nm)
{

    // Loop till the sum is not single digit number
    while (nm > 9) {

        // Initialize the sum as zero
        let sum_digit = 0;

        // Find the sum of digits
        while (nm > 0) {
            let digit = nm % 10;
            sum_digit = sum_digit + digit;
            nm = Math.floor(nm / 10);
        }
        nm = sum_digit;
    }

    // If sum is eventually 1
    if (nm == 1)
        return true;
    else
        return false;
}

// Function to print the required numbers
// from the given range
function printValidNums(l, r)
{
    for (let i = l; i <= r; i++) {

        // If i is one of the required numbers
        if (isComposite(i) && isDigitSumOne(i))
            document.write(i + " ");
    }
}

// Driver code

    let l = 10, r = 100;

    printValidNums(l, r);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
10 28 46 55 64 82 91 100
```

**优化:**我们可以使用[筛选算法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)预计算复合数。