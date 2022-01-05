# 检查 a 到 b 的整数乘积是正、负还是零

> 原文:[https://www . geesforgeks . org/check-整数乘积从 a 到 b 是正负值还是零/](https://www.geeksforgeeks.org/check-whether-product-of-integers-from-a-to-b-is-positive-negative-or-zero/)

给定两个整数 **a** 和 **b** ，任务是检查来自 rage v【a，b】即**a *(a+1)*(a+2)*……* b**的整数乘积是正、负还是零。
**举例:**

> **输入:** a = -10，b = -2
> **输出:**负
> **输入:** a = -10，b = 2
> **输出:**零

**天真的做法:**我们可以运行一个从 **a** 到 **b** 的循环，将所有从 **a** 到 **b** 的数字相乘，检查产品是正负值还是零。对于 **a** 和 **b** 的较大值，该解决方案将失败，并将导致溢出。
**有效途径:**有三种可能情况:

1.  如果 **a > 0** 和 **b > 0** ，则所得产品为正。
2.  如果 **a < 0** 和 **b > 0** ，那么结果将为零，因为**a *(a+1)*……* 0 *……(b–1)* b = 0**。
3.  如果 **a < 0** 和 **b < 0** ，那么结果将取决于数字的计数(因为所有数字都是负数)
    *   如果负数的计数是偶数，那么结果将是正数。
    *   否则结果将是负面的。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to check whether the product
// of integers of the range [a, b]
// is positive, negative or zero
void solve(long long int a, long long int b)
{

    // If both a and b are positive then
    // the product will be positive
    if (a > 0 && b > 0) {
        cout << "Positive";
    }

    // If a is negative and b is positive then
    // the product will be zero
    else if (a <= 0 && b >= 0) {
        cout << "Zero" << endl;
    }

    // If both a and b are negative then
    // we have to find the count of integers
    // in the range
    else {

        // Total integers in the range
        long long int n = abs(a - b) + 1;

        // If n is even then the resultant
        // product is positive
        if (n % 2 == 0) {
            cout << "Positive" << endl;
        }
        // If n is odd then the resultant
        // product is negative
        else {
            cout << "Negative" << endl;
        }
    }
}

// Driver code
int main()
{
    int a = -10, b = -2;

    solve(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to check whether the product
// of integers of the range [a, b]
// is positive, negative or zero
static void solve(long a, long b)
{

    // If both a and b are positive then
    // the product will be positive
    if (a > 0 && b > 0)
    {
        System.out.println( "Positive");
    }

    // If a is negative and b is positive then
    // the product will be zero
    else if (a <= 0 && b >= 0)
    {
        System.out.println( "Zero" );
    }

    // If both a and b are negative then
    // we have to find the count of integers
    // in the range
    else
    {

        // Total integers in the range
        long n = Math.abs(a - b) + 1;

        // If n is even then the resultant
        // product is positive
        if (n % 2 == 0)
        {
            System.out.println( "Positive");
        }

        // If n is odd then the resultant
        // product is negative
        else
        {
            System.out.println( "Negative");
        }
    }
}

    // Driver code
    public static void main (String[] args)
    {
        int a = -10, b = -2;

        solve(a, b);
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to check whether the product
# of integers of the range [a, b]
# is positive, negative or zero
def solve(a,b):

    # If both a and b are positive then
    # the product will be positive
    if (a > 0 and b > 0):
        print("Positive")

    # If a is negative and b is positive then
    # the product will be zero
    elif (a <= 0 and b >= 0):
        print("Zero")

    # If both a and b are negative then
    # we have to find the count of integers
    # in the range
    else:

        # Total integers in the range
        n = abs(a - b) + 1

        # If n is even then the resultant
        # product is positive
        if (n % 2 == 0):
            print("Positive")

        # If n is odd then the resultant
        # product is negative
        else:
            print("Negative")

# Driver code
if __name__ == '__main__':
    a = -10
    b = -2

    solve(a, b)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to check whether the product
    // of integers of the range [a, b]
    // is positive, negative or zero
    static void solve(long a, long b)
    {

        // If both a and b are positive then
        // the product will be positive
        if (a > 0 && b > 0)
        {
            Console.WriteLine( "Positive");
        }

        // If a is negative and b is positive then
        // the product will be zero
        else if (a <= 0 && b >= 0)
        {
            Console.WriteLine( "Zero" );
        }

        // If both a and b are negative then
        // we have to find the count of integers
        // in the range
        else
        {

            // Total integers in the range
            long n = Math.Abs(a - b) + 1;

            // If n is even then the resultant
            // product is positive
            if (n % 2 == 0)
            {
                Console.WriteLine( "Positive");
            }

            // If n is odd then the resultant
            // product is negative
            else
            {
                Console.WriteLine( "Negative");
            }
        }
    }

    // Driver code
    public static void Main ()
    {
        int a = -10, b = -2;

        solve(a, b);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript  implementation of the approach

// Function to check whether the product
// of integers of the range [a, b]
// is positive, negative or zero
function  solve( a,  b)
{

    // If both a and b are positive then
    // the product will be positive
    if (a > 0 && b > 0)
    {
        document.write( "Positive");
    }

    // If a is negative and b is positive then
    // the product will be zero
    else if (a <= 0 && b >= 0)
    {
        document.write( "Zero" );
    }

    // If both a and b are negative then
    // we have to find the count of integers
    // in the range
    else
    {

        // Total integers in the range
        let  n = Math.abs(a - b) + 1;

        // If n is even then the resultant
        // product is positive
        if (n % 2 == 0)
        {
            document.write( "Positive");
        }

        // If n is odd then the resultant
        // product is negative
        else
        {
            document.write( "Negative");
        }
    }
}

    // Driver code

        let a = -10;
        let b = -2;

        solve(a, b);

// This code is contributed by Bobby

</script>
```

**Output:** 

```
Negative
```