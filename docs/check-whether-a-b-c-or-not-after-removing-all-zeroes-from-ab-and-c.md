# 将 a、b、c 全部清零后检查 a + b 是否= c

> 原文:[https://www . geeksforgeeks . org/check-a-b-c-or-not-在从 a B-和-c 中移除所有零之后/](https://www.geeksforgeeks.org/check-whether-a-b-c-or-not-after-removing-all-zeroes-from-ab-and-c/)

给定两个整数 **a** 和 **b** ，任务是将它们相加得到 **c** 。之后，从 **a** 、 **b** 和 **c** 中删除零，如果**a**+**b**=**c**则返回**“是”**否则返回**“否”**。
**举例:**

> **输入:** a = 101，b = 102
> **输出:**是
> 101 + 102 = 203。
> 去掉 a、b、c 的所有零后，a = 11，b = 12，c = 23
> 现在检查 **a + b = c** 是否为 11 + 12 = 23。所以打印“是”。
> **输入:** a = 105，b = 108
> **输出:**否
> 去掉所有零后 **a** + **b** ！= **c** ，因此输出号为

**进场:**

*   创建一个从数字 **n** 中删除零的函数。
*   检查(删除零(a)+删除零(b)=删除零(a+b))然后打印**是**否则打印**否**

下面是上述方法的实现。

## C++

```
// C++ program to check the sum after
// Removing all zeroes is true or not
#include <bits/stdc++.h>
using namespace std;

// Function to remove zeroes
int removeZero(int n)
{
    // Initialize result to zero holds the
    // Result after removing zeroes from no
    int res = 0;

    // Initialize variable d to 1 that holds
    // digits of no
    int d = 1;

    // Loop while n is greater then zero
    while (n > 0) {

        // Check if n mod 10 is not equal to
        // zero
        if (n % 10 != 0) {

            // store the result by removing zeroes
            // And increment d by 10
            res += (n % 10) * d;
            d *= 10;
        }

        // Go to the next digit
        n /= 10;
    }

    // Return the result
    return res;
}

// Function to check if sum is true after
// Removing all zeroes.
bool isEqual(int a, int b)
{
    // Call removeZero() for both sides
    // and check whether they are equal
    // After removing zeroes.

    if (removeZero(a) + removeZero(b) == removeZero(a + b))
        return true;

    return false;
}

// Driver code
int main()
{
    int a = 105, b = 106;
    isEqual(a, b) ? cout << "Yes"
                  : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check the sum after
// Removing all zeroes is true or not
public class GfG {

    // Function to remove zeroes
    public static int removeZero(int n)
    {
        // Initialize result to zero holds the
        // Result after removing zeroes from no
        int res = 0;

        // Initialize variable d to 1 that holds
        // digits of no
        int d = 1;

        // Loop while n is greater then zero
        while (n > 0) {

            // Check if n mod 10 is not equal to
            // zero
            if (n % 10 != 0) {

                // store the result by removing zeroes
                // And increment d by 10
                res += (n % 10) * d;
                d *= 10;
            }

            // Go to the next digit
            n /= 10;
        }

        // Return the result
        return res;
    }

    // Function to check if sum is true after
    // Removing all zeroes.
    public static boolean isEqual(int a, int b)
    {
        // Call removeZero() for both sides
        // and check whether they are equal
        // After removing zeroes.

        if (removeZero(a) + removeZero(b) == removeZero(a + b))
            return true;

        return false;
    }

     public static void main(String []args){

        int a = 105, b = 106;

        if (isEqual(a, b) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
     }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 program to check the sum after
# Removing all zeroes is true or not

# Function to remove zeroes
def removeZero(n):

    # Initialize result to zero holds the
    # Result after removing zeroes from no
    res = 0

    # Initialize variable d to 1 that
    # holds digits of no
    d = 1

    # Loop while n is greater then zero
    while (n > 0):

        # Check if n mod 10 is not equal
        # to zero
        if (n % 10 != 0):

            # store the result by removing
            # zeroes And increment d by 10
            res += (n % 10) * d
            d *= 10

        # Go to the next digit
        n //= 10

    # Return the result
    return res

# Function to check if sum is true
# after Removing all zeroes.
def isEqual(a, b):

    # Call removeZero() for both sides
    # and check whether they are equal
    # After removing zeroes.
    if (removeZero(a) +
        removeZero(b) == removeZero(a + b)):
        return True

    return False

# Driver code
a = 105
b = 106
if(isEqual(a, b)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by sahishelangia
```

## C#

```
// C# program to check the sum after
// Removing all zeroes is true or not
using System;
class GFG
{

// Function to remove zeroes
public static int removeZero(int n)
{
    // Initialize result to zero holds the
    // Result after removing zeroes from no
    int res = 0;

    // Initialize variable d to 1 that holds
    // digits of no
    int d = 1;

    // Loop while n is greater then zero
    while (n > 0)
    {

        // Check if n mod 10 is not equal to
        // zero
        if (n % 10 != 0)
        {

            // store the result by removing zeroes
            // And increment d by 10
            res += (n % 10) * d;
            d *= 10;
        }

        // Go to the next digit
        n /= 10;
    }

    // Return the result
    return res;
}

// Function to check if sum is true after
// Removing all zeroes.
public static bool isEqual(int a, int b)
{
    // Call removeZero() for both sides
    // and check whether they are equal
    // After removing zeroes.

    if (removeZero(a) +
        removeZero(b) == removeZero(a + b))
        return true;

    return false;
}

// Driver Code
public static void Main()
{
    int a = 105, b = 106;

    if (isEqual(a, b) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check the sum after
// Removing all zeroes is true or not.

// Function to remove zeroes
function removeZero($n)
{
    // Initialize result to zero holds the
    // Result after removing zeroes from no
    $res = 0;

    // Initialize variable d to 1 that
    // holds digits of no
    $d = 1;

    // Loop while n is greater then zero
    while ($n > 0)
    {

        // Check if n mod 10 is not equal
        // to zero
        if ($n % 10 != 0)
        {

            // store the result by removing
            // zeroes and increment d by 10
            $res += ($n % 10) * $d;
            $d *= 10;
        }

        // Go to the next digit
        $n = floor($n / 10);
    }

    // Return the result
    return $res;
}

// Function to check if sum is true
// after Removing all zeroes.
function isEqual($a, $b)
{
    // Call removeZero() for both sides
    // and check whether they are equal
    // After removing zeroes.
    if (removeZero($a) +
        removeZero($b) == removeZero($a + $b))
        return true;

    return false;
}

// Driver code
$a = 105 ;
$b = 106 ;

if (isEqual($a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to check the sum after
// Removing all zeroes is true or not

// Function to remove zeroes
function removeZero( n)
{
    // Initialize result to zero holds the
    // Result after removing zeroes from no
    let res = 0;

    // Initialize variable d to 1 that holds
    // digits of no
    let d = 1;

    // Loop while n is greater then zero
    while (n > 0) {

        // Check if n mod 10 is not equal to
        // zero
        if (n % 10 != 0) {

            // store the result by removing zeroes
            // And increment d by 10
            res += (n % 10) * d;
            d *= 10;
        }

        // Go to the next digit
        n = Math.floor(n/10);
    }

    // Return the result
    return res;
}

// Function to check if sum is true after
// Removing all zeroes.
function isEqual( a, b)
{
    // Call removeZero() for both sides
    // and check whether they are equal
    // After removing zeroes.

    if (removeZero(a) + removeZero(b) == removeZero(a + b))
        return true;

    return false;
}

    // Driver Code

    let a = 105, b = 106;
    if (isEqual(a, b) == true)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```