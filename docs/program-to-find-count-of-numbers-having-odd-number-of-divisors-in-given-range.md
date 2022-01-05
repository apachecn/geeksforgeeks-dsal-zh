# 计算给定范围内奇数除数的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-count-count-of-numbers-count-with-单数-给定范围内的除数/](https://www.geeksforgeeks.org/program-to-find-count-of-numbers-having-odd-number-of-divisors-in-given-range/)

给定两个整数 A 和 B，任务是计算区间[ A，B ]中有多少数有奇数个除数。

**示例:**

```
Input : A = 1, B = 10
Output : 3

Input : A = 5, B = 15
Output : 1
```

**天真方法:**
简单的方法是遍历范围[A，B]之间的所有数字，检查它们的除数是否为奇数。

以下是上述思路的实现:

## C++

```
// C++ program to find count of numbers having
// odd number of divisors in given range

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers having odd
// number of divisors in range [A, B]
int OddDivCount(int a, int b)
{
    // variable to odd divisor count
    int res = 0;
    // iterate from a to b and count their
    // number of divisors
    for (int i = a; i <= b; ++i) {

        // variable to divisor count
        int divCount = 0;
        for (int j = 1; j <= i; ++j) {
            if (i % j == 0) {
                ++divCount;
            }
        }

        // if count of divisor is odd
        // then increase res by 1
        if (divCount % 2) {
            ++res;
        }
    }
    return res;
}

// Driver code
int main()
{
    int a = 1, b = 10;
    cout << OddDivCount(a, b) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of numbers having
// odd number of divisors in given range

import java.io.*;

class GFG {
    // Function to count numbers having odd
    // number of divisors in range [A, B]
    static int OddDivCount(int a, int b)
    {
        // variable to odd divisor count
        int res = 0;
        // iterate from a to b and count their
        // number of divisors
        for (int i = a; i <= b; ++i) {

            // variable to divisor count
            int divCount = 0;
            for (int j = 1; j <= i; ++j) {
                if (i % j == 0) {
                    ++divCount;
                }
            }

            // if count of divisor is odd
            // then increase res by 1
            if ((divCount % 2) != 0) {
                ++res;
            }
        }
        return res;
    }

    // Driver code

    public static void main(String[] args)
    {

        int a = 1, b = 10;
        System.out.println(OddDivCount(a, b));
    }
    // This code is contributed by ajit.
}
```

## 蟒蛇 3

```
# Python3 program to find count
# of numbers having odd number
# of divisors in given range

# Function to count numbers
# having odd number of divisors
# in range [A, B]
def OddDivCount(a, b):

    # variable to odd divisor count
    res = 0

    # iterate from a to b and count
    # their number of divisors
    for i in range(a, b + 1) :

        # variable to divisor count
        divCount = 0
        for j in range(1, i + 1) :
            if (i % j == 0) :
                divCount += 1

        # if count of divisor is odd
        # then increase res by 1
        if (divCount % 2) :
            res += 1
    return res

# Driver code
if __name__ == "__main__":
    a = 1
    b = 10
    print(OddDivCount(a, b))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find count of numbers having
// odd number of divisors in given range
using System;

class Geeks {

    // Function to count numbers having odd
    // number of divisors in range [A, B]
    static int OddDivCount(int a, int b)
    {
        // variable to odd divisor count
        int res = 0;
        // iterate from a to b and count their
        // number of divisors
        for (int i = a; i <= b; ++i) {

            // variable to divisor count
            int divCount = 0;
            for (int j = 1; j <= i; ++j) {
                if (i % j == 0) {
                    ++divCount;
                }
            }

            // if count of divisor is odd
            // then increase res by 1
            if ((divCount % 2) != 0) {
                ++res;
            }
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int a = 1, b = 10;
        Console.WriteLine(OddDivCount(a, b));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of
// numbers having odd number of
// divisors in given range

// Function to count numbers having odd
// number of divisors in range [A, B]
function OddDivCount($a, $b)
{
    // variable to odd divisor count
    $res = 0;

    // iterate from a to b and count
    // their number of divisors
    for ($i = $a; $i <= $b; ++$i)
    {

        // variable to divisor count
        $divCount = 0;
        for ($j = 1; $j <= $i; ++$j)
        {
            if ($i % $j == 0)
            {
                ++$divCount;
            }
        }

        // if count of divisor is odd
        // then increase res by 1
        if ($divCount % 2)
        {
            ++$res;
        }
    }
    return $res;
}

// Driver code
$a = 1;
$b = 10;
echo OddDivCount($a, $b) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find count of
// numbers having odd number of divisors
// in given range

// Function to count numbers having odd
// number of divisors in range [A, B]
function OddDivCount(a, b)
{

    // Variable to odd divisor count
    let res = 0;

    // Iterate from a to b and count their
    // number of divisors
    for(let i = a; i <= b; ++i)
    {

        // Variable to divisor count
        let divCount = 0;
        for(let j = 1; j <= i; ++j)
        {
            if (i % j == 0)
            {
                ++divCount;
            }
        }

        // If count of divisor is odd
        // then increase res by 1
        if ((divCount % 2) != 0)
        {
            ++res;
        }
    }
    return res;
}

// Driver code
let a = 1, b = 10;
document.write(OddDivCount(a, b));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n <sup>2</sup>

**更好的方法:**
一个数可以用它的素因子的乘积，加上适当的幂来表示。这些幂可以用来得到一个整数的因子数。如果数字是 **num** ，可以表示为(a<sup>P1</sup>)*(b<sup>p2</sup>)*(c<sup>P3</sup>)
，那么 num 的因子个数是(p1 + 1) * (p2 + 1) * (p3 + 1)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of divisors of a number
int divisor(int a)
{
    int div = 1, count = 0;
    for (int i = 2; i <= sqrt(a); i++) {

        // Count the powers of the current
        // prime i which divides a
        while (a % i == 0) {
            count++;
            a = a / i;
        }

        // Update the count of divisors
        div = div * (count + 1);

        // Reset the count
        count = 0;
    }

    // If the remaining a is prime then a^1
    // will be one of its prime factors
    if (a > 1) {
        div = div * (2);
    }
    return div;
}

// Function to count numbers having odd
// number of divisors in range [A, B]
int OddDivCount(int a, int b)
{
    // To store the count of elements
    // having odd number of divisors
    int res = 0;

    // Iterate from a to b and find the
    // count of their divisors
    for (int i = a; i <= b; ++i) {

        // To store the count of divisors of i
        int divCount = divisor(i);

        // If the divisor count of i is odd
        if (divCount % 2) {
            ++res;
        }
    }
    return res;
}

// Driver code
int main()
{
    int a = 1, b = 10;
    cout << OddDivCount(a, b);

    return 0;
}
// This code is contributed by jrolofmeister
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count
// of divisors of a number
static int divisor(int a)
{
    int div = 1, count = 0;
    for (int i = 2; i <= Math.sqrt(a); i++)
    {

        // Count the powers of the current
        // prime i which divides a
        while (a % i == 0)
        {
            count++;
            a = a / i;
        }

        // Update the count of divisors
        div = div * (count + 1);

        // Reset the count
        count = 0;
    }

    // If the remaining a is prime then a^1
    // will be one of its prime factors
    if (a > 1)
    {
        div = div * (2);
    }
    return div;
}

// Function to count numbers having odd
// number of divisors in range [A, B]
static int OddDivCount(int a, int b)
{
    // To store the count of elements
    // having odd number of divisors
    int res = 0;

    // Iterate from a to b and find the
    // count of their divisors
    for (int i = a; i <= b; ++i)
    {

        // To store the count of divisors of i
        int divCount = divisor(i);

        // If the divisor count of i is odd
        if (divCount % 2 == 1)
        {
            ++res;
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int a = 1, b = 10;
    System.out.println(OddDivCount(a, b));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of divisors of a number
def divisor(a):

    div = 1;
    count = 0;
    for i in range(2, int(pow(a, 1 / 2)) + 1):

        # Count the powers of the current
        # prime i which divides a
        while (a % i == 0):
            count += 1;
            a = a / i;

        # Update the count of divisors
        div = div * (count + 1);

        # Reset the count
        count = 0;

    # If the remaining a is prime then a^1
    # will be one of its prime factors
    if (a > 1):
        div = div * (2);

    return div;

# Function to count numbers having odd
# number of divisors in range [A, B]
def OddDivCount(a, b):

    # To store the count of elements
    # having odd number of divisors
    res = 0;

    # Iterate from a to b and find the
    # count of their divisors
    for i in range(a, b + 1):

        # To store the count of divisors of i
        divCount = divisor(i);

        # If the divisor count of i is odd
        if (divCount % 2):
            res += 1;

    return res;

# Driver code
if __name__ == '__main__':
    a, b = 1, 10;
    print(OddDivCount(a, b));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count
// of divisors of a number
static int divisor(int a)
{
    int div = 1, count = 0;
    for (int i = 2;
             i <= Math.Sqrt(a); i++)
    {

        // Count the powers of the current
        // prime i which divides a
        while (a % i == 0)
        {
            count++;
            a = a / i;
        }

        // Update the count of divisors
        div = div * (count + 1);

        // Reset the count
        count = 0;
    }

    // If the remaining a is prime then a^1
    // will be one of its prime factors
    if (a > 1)
    {
        div = div * (2);
    }
    return div;
}

// Function to count numbers having odd
// number of divisors in range [A, B]
static int OddDivCount(int a, int b)
{
    // To store the count of elements
    // having odd number of divisors
    int res = 0;

    // Iterate from a to b and find the
    // count of their divisors
    for (int i = a; i <= b; ++i)
    {

        // To store the count of divisors of i
        int divCount = divisor(i);

        // If the divisor count of i is odd
        if (divCount % 2 == 1)
        {
            ++res;
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int a = 1, b = 10;
    Console.WriteLine(OddDivCount(a, b));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>   
    // Javascript implementation of the approach

    // Function to return the count
    // of divisors of a number
    function divisor(a)
    {
        let div = 1, count = 0;
        for (let i = 2; i <= Math.sqrt(a); i++)
        {

            // Count the powers of the current
            // prime i which divides a
            while (a % i == 0)
            {
                count++;
                a = parseInt(a / i, 10);
            }

            // Update the count of divisors
            div = div * (count + 1);

            // Reset the count
            count = 0;
        }

        // If the remaining a is prime then a^1
        // will be one of its prime factors
        if (a > 1)
        {
            div = div * (2);
        }
        return div;
    }

    // Function to count numbers having odd
    // number of divisors in range [A, B]
    function OddDivCount(a, b)
    {
        // To store the count of elements
        // having odd number of divisors
        let res = 0;

        // Iterate from a to b and find the
        // count of their divisors
        for (let i = a; i <= b; ++i)
        {

            // To store the count of divisors of i
            let divCount = divisor(i);

            // If the divisor count of i is odd
            if (divCount % 2 == 1)
            {
                ++res;
            }
        }
        return res;
    }

    let a = 1, b = 10;
    document.write(OddDivCount(a, b));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n * logn)
请参考[这篇](https://www.geeksforgeeks.org/number-elements-odd-factors-given-range/)文章了解 O(1)方法。