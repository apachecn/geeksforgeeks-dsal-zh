# 小于 N 的最大数字，数字和大于 N 的数字和

> 原文:[https://www . geesforgeks . org/最大数字小于 n，数字和大于 n 的数字和/](https://www.geeksforgeeks.org/largest-number-less-than-n-with-digit-sum-greater-than-the-digit-sum-of-n/)

给定一个整数 **N** ，任务是找到小于 **N** 的最大数字，使其位数之和大于 **N** 的位数之和。如果任何数字都不满足条件，则打印 **-1** 。
**举例:**

> **输入:** N = 100
> **输出:** 99
> 99 是小于 100 的最大数字，其位数之和大于 100 的位数之和
> **输入:** N = 49
> **输出:** -1

**进场:**从 **N-1** 到 **1** 开始一个[循环](https://www.geeksforgeeks.org/loops-in-c/)，检查任意数字的位数之和是否大于 **N** 的位数之和。满足条件的第一个数字是所需的数字。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the sum of the digits of n
int sumOfDigits(int n)
{
    int res = 0;

    // Loop for each digit of the number
    while (n > 0) {
        res += n % 10;
        n /= 10;
    }

    return res;
}

// Function to return the greatest
// number less than n such that
// the sum of its digits is greater
// than the sum of the digits of n
int findNumber(int n)
{

    // Starting from n-1
    int i = n - 1;

    // Check until 1
    while (i > 0) {

        // If i satisfies the given condition
        if (sumOfDigits(i) > sumOfDigits(n))
            return i;
        i--;
    }

    // If the condition is not satisfied
    return -1;
}

// Driver code
int main()
{
    int n = 824;
    cout << findNumber(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

import java.io.*;

class GFG {
    // Function to return the sum of the digits of n
static int sumOfDigits(int n)
{
    int res = 0;

    // Loop for each digit of the number
    while (n > 0) {
        res += n % 10;
        n /= 10;
    }

    return res;
}

// Function to return the greatest
// number less than n such that
// the sum of its digits is greater
// than the sum of the digits of n
static int findNumber(int n)
{

    // Starting from n-1
    int i = n - 1;

    // Check until 1
    while (i > 0) {

        // If i satisfies the given condition
        if (sumOfDigits(i) > sumOfDigits(n))
            return i;
        i--;
    }

    // If the condition is not satisfied
    return -1;
}

// Driver code
    public static void main (String[] args) {

    int n = 824;
    System.out.println (findNumber(n));
    }
//This code is contributed by akt_mit   
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum
# of the digits of n
def sumOfDigits(n) :

    res = 0;

    # Loop for each digit of the number
    while (n > 0) :
        res += n % 10
        n /= 10

    return res;

# Function to return the greatest
# number less than n such that
# the sum of its digits is greater
# than the sum of the digits of n
def findNumber(n) :

    # Starting from n-1
    i = n - 1;

    # Check until 1
    while (i > 0) :

        # If i satisfies the given condition
        if (sumOfDigits(i) > sumOfDigits(n)) :
            return i

        i -= 1

    # If the condition is not satisfied
    return -1;

# Driver code
if __name__ == "__main__" :

    n = 824;
    print(findNumber(n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to return the sum
// of the digits of n
static int sumOfDigits(int n)
{
    int res = 0;

    // Loop for each digit of
    // the number
    while (n > 0)
    {
        res += n % 10;
        n /= 10;
    }

    return res;
}

// Function to return the greatest
// number less than n such that
// the sum of its digits is greater
// than the sum of the digits of n
static int findNumber(int n)
{

    // Starting from n-1
    int i = n - 1;

    // Check until 1
    while (i > 0)
    {

        // If i satisfies the given condition
        if (sumOfDigits(i) > sumOfDigits(n))
            return i;
        i--;
    }

    // If the condition is
    // not satisfied
    return -1;
}

// Driver code
static public void Main ()
{
    int n = 824;
    Console.WriteLine (findNumber(n));
}
}

// This code is contributed by @Tushil
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach

// Function to return the sum of
// the digits of n
function sumOfDigits($n)
{
    $res = 0;

    // Loop for each digit of the number
    while ($n > 0)
    {
        $res += $n % 10;
        $n /= 10;
    }

    return $res;
}

// Function to return the greatest
// number less than n such that
// the sum of its digits is greater
// than the sum of the digits of n
function findNumber($n)
{

    // Starting from n-1
    $i = $n - 1;

    // Check until 1
    while ($i > 0)
    {

        // If i satisfies the given condition
        if (sumOfDigits($i) > sumOfDigits($n))
            return $i;
        $i--;
    }

    // If the condition is not satisfied
    return -1;
}

// Driver code
$n = 824;

echo findNumber($n);

// This code is contributed by Mukul singh
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the sum of the digits of n
    function sumOfDigits(n)
    {
        var res = 0;

        // Loop for each digit of the number
        while (n > 0)
        {
            res += n % 10;
            n = parseInt(n/10);
        }

        return res;
    }

    // Function to return the greatest
    // number less than n such that
    // the sum of its digits is greater
    // than the sum of the digits of n
    function findNumber(n)
    {

        // Starting from n-1
        var i = n - 1;

        // Check until 1
        while (i > 0)
        {

            // If i satisfies the given condition
            if (sumOfDigits(i) > sumOfDigits(n))
                return i;
            i--;
        }

        // If the condition is not satisfied
        return -1;
    }

    // Driver code
    var n = 824;
    document.write(findNumber(n));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
819
```

**时间复杂度:** O(N)

**辅助空间:** O(1)