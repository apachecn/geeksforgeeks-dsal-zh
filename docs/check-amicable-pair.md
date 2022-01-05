# 检查友好配对

> 原文:[https://www.geeksforgeeks.org/check-amicable-pair/](https://www.geeksforgeeks.org/check-amicable-pair/)

[友好数](https://www.geeksforgeeks.org/pairs-amicable-numbers/)是两个不同的相关数，因此每个数的适当因子的[和等于另一个数。(一个数的适当除数是该数的正因子，而不是该数本身。
**例:**](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/) 

```
Input : x = 220, y = 284
Output : Yes 
Proper divisors of 220 are 1, 2, 4, 5,
10, 11, 20, 22, 44, 55 and 110\. Sum of 
these is 284\. Proper divisors of 284 
are 1, 2, 4, 71 and 142 with sum 220.

Input : 1 2
Output :No
```

逻辑很简单。我们比较两个数的适当除数的和，并将一个数的和与另一个数的和进行比较。

## C++

```
// CPP program to check if two numbers are
// Amicable or not.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of all 
// proper divisors of a given number
int divSum(int n)
{
    // Sum of divisors
    int result = 0;

    // find all divisors which divides 'num'
    for (int i = 2; i <= sqrt(n); i++)
    {
        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {
            // if both divisors are same
            // then add it once else add
            // both
            if (i == (n / i))
                result += i;
            else
                result += (i + n/i);
        }
    }

    // Add 1 and n to result as above loop
    // considers proper divisors greater 
    // than 1.
    return (result + 1);
}

// Returns true if x and y are Amicable
// else false.
bool areAmicable(int x, int y)
{
    if (divSum(x) != y)
       return false;

    return (divSum(y) == x);
}

int main() {
    int x = 220, y = 284;
    if (areAmicable(x, y))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if two numbers are
// Amicable or not.
import java.io.*;

class GFG 
{
    // Function to calculate sum of all 
    // proper divisors of a given number
    static int divSum(int n)
    {
        // Sum of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i = 2; i <= Math.sqrt(n); i++)
        {
            // if 'i' is divisor of 'n'
            if (n % i == 0)
            {
                // if both divisors are same
                // then add it once else add
                // both
                if (i == (n / i))
                    result += i;
                else
                    result += (i + n / i);
            }
        }

        // Add 1 and n to result as above loop
        // considers proper divisors greater 
        // than 1.
        return (result + 1);
    }

    // Returns true if x and y are Amicable
    // else false.
    static boolean areAmicable(int x, int y)
    {
        if (divSum(x) != y)
        return false;

        return (divSum(y) == x);
    }

    public static void main (String[] args) 
    {
        int x = 220, y = 284;
        if (areAmicable(x, y))
        System.out.println( "Yes");
        else
        System.out.println("No");

    }
} 

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to check 
# if two numbers are
# Amicable or not.
import math

# def to calculate sum 
# of all proper divisors
# of a given number
def divSum(n) :

    # Sum of divisors
    result = 0

    # find all divisors 
    # which divides 'num'
    for i in range(2, int(math.sqrt(n)) + 1) :

        # if 'i' is 
        # divisor of 'n'
        if (n % i == 0) :

            # if both divisors are same
            # then add it once else add
            # both
            if (i == int(n / i)) :
                result = result + i
            else :
                result = result + 
                         (i + int(n / i))

    # Add 1 and n to result 
    # as above loop considers
    # proper divisors greater 
    # than 1.
    return (result + 1)

# Returns true if x and y 
# are Amicable else false.
def areAmicable(x, y) :

    if (divSum(x) != y) :
        return False

    return (divSum(y) == x) 

# Driver Code
x = 220
y = 284
if (areAmicable(x, y)) :
    print ("Yes")
else :
    print ("No")

# This code is contributed by 
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to check if two numbers are
// Amicable or not.
using System;

class GFG 
{
    // Function to calculate sum of all 
    // proper divisors of a given number
    static int divSum(int n)
    {
        // Sum of divisors
        int result = 0;

        // find all divisors which divides 'num'
        for (int i = 2; i <= Math.Sqrt(n); i++)
        {
            // if 'i' is divisor of 'n'
            if (n % i == 0)
            {
                // if both divisors are same
                // then add it once else add
                // both
                if (i == (n / i))
                    result += i;
                else
                    result += (i + n / i);
            }
        }

        // Add 1 and n to result as above loop
        // considers proper divisors greater 
        // than 1.
        return (result + 1);
    }

    // Returns true if x and y are Amicable
    // else false.
    static bool areAmicable(int x, int y)
    {
        if (divSum(x) != y)
        return false;

        return (divSum(y) == x);
    }

    public static void Main () 
    {
        int x = 220, y = 284;

        if (areAmicable(x, y))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine("No");

    }
} 

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if two
// numbers are Amicable or not.

// Function to calculate sum of all 
// proper divisors of a given number
function divSum( $n)
{

    // Sum of divisors
    $result = 0;

    // find all divisors 
    // which divides 'num'
    for ($i = 2; $i <= sqrt($n); $i++)
    {

        // if 'i' is divisor of 'n'
        if ($n % $i == 0)
        {

            // if both divisors are same
            // then add it once else add
            // both
            if ($i == ($n / $i))
                $result += $i;
            else
                $result += ($i + $n / $i);
        }
    }

    // Add 1 and n to result 
    // as above loop considers
    // proper divisors greater 
    // than 1.
    return ($result + 1);
}

// Returns true if x and y 
// are Amicable else false.
function areAmicable($x, $y)
{
    if (divSum($x) != $y)
        return false;

    return (divSum($y) == $x);
}

    // Driver Code
    $x = 220;
    $y = 284;
    if (areAmicable($x, $y))
        echo "Yes";
    else
        echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if two 
// numbers are Amicable or not. 

// Function to calculate sum of all 
// proper divisors of a given number 
function divSum(n) 
{ 

    // Sum of divisors 
    let result = 0; 

    // find all divisors 
    // which divides 'num' 
    for (let i = 2; i <= Math.sqrt(n); i++) 
    { 

        // if 'i' is divisor of 'n' 
        if (n % i == 0) 
        { 

            // if both divisors are same 
            // then add it once else add 
            // both 
            if (i == (n / i)) 
                result += i; 
            else
                result += (i + n / i); 
        } 
    } 

    // Add 1 and n to result 
    // as above loop considers 
    // proper divisors greater 
    // than 1. 
    return (result + 1); 
} 

// Returns true if x and y 
// are Amicable else false. 
function areAmicable(x, y) 
{ 
    if (divSum(x) != y) 
        return false; 

    return (divSum(y) == x); 
} 

    // Driver Code 
    let x = 220; 
    let y = 284; 
    if (areAmicable(x, y)) 
        document.write("Yes"); 
    else
        document.write("No"); 

// This code is contributed by _saurabh_jaiswal. 

</script>
```

**输出:**

```
Yes
```