# 检查两个数的除数之和是否相同

> 原文:[https://www . geesforgeks . org/check-如果两个数的除数之和相同/](https://www.geeksforgeeks.org/check-if-sum-of-divisors-of-two-numbers-are-same/)

给定两个数字 n1 和 n2，我们需要检查这些数字是否是等价的数字。
**等价数**是这样的数，它们的定数之和是相同的。
例如，159、559 和 703 是等价数。这是因为所有三个数字都有 57 作为它们的除数之和。

**示例:**

> 输入:n1 = 559，n2 = 703
> 输出:是。
> 说明:两个数都有 57 作为它们的定数之和。
> 
> 输入:n1 = 36，n2 = 57
> 输出:No.
> 说明:36 有和 55，而 57 有它们的定数的和 23。

对于给定的数，求[完全数](https://www.geeksforgeeks.org/perfect-number/)的适当除数之和，然后检查两个和是否相等。

## C++

```
// C++ program to find if two numbers are
// equivalent or not
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of all proper divisors
// num --> given natural number
int divSum(int n)
{
    // To store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i = 2; i * i <= n; i++)
        if (n % i == 0)
            sum = sum + i + n / i;

    return sum;
}

// Function to check if both numbers
// are equivalent or not
bool areEquivalent(int num1, int num2)
{
    return divSum(num1) == divSum(num2);
}

// Drivers code
int main()
{
    int num1 = 559, num2 = 703;

    areEquivalent(num1, num2) ?
                  cout << "Equivalent" :
                  cout << "Not Equivalent";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if two numbers are
// equivalent or not
import java.math.*;

class GFG {

    // Function to calculate sum of all proper
    // divisors num --> given natural number
    static int divSum(int n)
    {
        // To store sum of divisors
        int sum = 1;

        // Find all divisors and add them
        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                sum = sum + i + n / i;

        return sum;
    }

    // Function to check if both numbers
    // are equivalent or not
    static boolean areEquivalent(int num1, int num2)
    {

        return divSum(num1) == divSum(num2);
    }

    // Drivers code
    public static void main(String[] args)
    {
        int num1 = 559;
        int num2 = 703;

        if (areEquivalent(num1, num2))
            System.out.println("Equivalent");
        else
            System.out.println("Not Equivalent");
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# if two numbers are
# equivalent or not
import math

# Function to calculate sum
# of all proper divisors
# num --> given natural number
def divSum(n):

    # To store sum of divisors
    sum = 1;

    # Find all divisors
    # and add them
    i = 2;
    while(i * i <= n):
        if (n % i == 0):
            sum = (sum + i +
                   math.floor(n / i));
        i += 1;

    return sum;

# Function to check
# if both numbers
# are equivalent or not
def areEquivalent(num1, num2):
    return divSum(num1) == divSum(num2);

# Driver code
num1 = 559;
num2 = 703;

if (areEquivalent(num1, num2) == True):
    print("Equivalent");
else:
    print("Not Equivalent");

# This code is contributed by mits
```

## C#

```
// C# program to find if two
// numbers are equivalent or not
using System;

class GFG
{

    // Function to calculate sum
    // of all proper divisors
    // num --> given natural number
    static int divSum(int n)
    {
        // To store sum of divisors
        int sum = 1;

        // Find all divisors
        // and add them
        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                sum = sum + i + n / i;

        return sum;
    }

    // Function to check if
    // both numbers are
    // equivalent or not
    static bool areEquivalent(int num1,
                              int num2)
    {
        return divSum(num1) == divSum(num2);
    }

    // Driver code
    static public void Main ()
    {
        int num1 = 559;
        int num2 = 703;

        if (areEquivalent(num1, num2))
            Console.WriteLine("Equivalent");
        else
            Console.WriteLine("Not Equivalent");
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// if two numbers are
// equivalent or not

// Function to calculate sum
// of all proper divisors
// num --> given natural number
function divSum($n)
{
    // To store sum of divisors
    $sum = 1;

    // Find all divisors
    // and add them
    for ($i = 2; $i * $i <= $n; $i++)
        if ($n % $i == 0)
            $sum = $sum + $i +
                   floor($n / $i);

    return $sum;
}

// Function to check
// if both numbers
// are equivalent or not
function areEquivalent($num1, $num2)
{
    return divSum($num1) == divSum($num2);
}

// Driver code
$num1 = 559; $num2 = 703;

if (areEquivalent($num1, $num2) == true)
    echo "Equivalent" ;

else
    echo "Not Equivalent";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find if two
    // numbers are equivalent or not

    // Function to calculate sum
    // of all proper divisors
    // num --> given natural number
    function divSum(n)
    {
        // To store sum of divisors
        let sum = 1;

        // Find all divisors
        // and add them
        for (let i = 2; i * i <= n; i++)
            if (n % i == 0)
                sum = sum + i + parseInt(n / i, 10);

        return sum;
    }

    // Function to check if
    // both numbers are
    // equivalent or not
    function areEquivalent(num1, num2)
    {
        return divSum(num1) == divSum(num2);
    }

    let num1 = 559;
    let num2 = 703;

    if (areEquivalent(num1, num2))
      document.write("Equivalent");
    else
      document.write("Not Equivalent");

</script>
```

**Output:** 

```
Equivalent
```