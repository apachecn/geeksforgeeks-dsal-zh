# 求前 N 个整数，使其位数之和等于 10

> 原文:[https://www . geesforgeks . org/find-first-n-integer-so-它们的数字总和等于-10/](https://www.geeksforgeeks.org/find-the-first-n-integers-such-that-the-sum-of-their-digits-is-equal-to-10/)

给定一个整数 **N** ，任务是先打印数字之和为 **10** 的 **N** 个整数。
**举例:**

> **输入:** N = 4
> **输出:** 19 28 37 46
> **输入:** N = 6
> **输出:** 19 28 37 46 55 64

**方法:**初始化 **num = 19** 得到该系列的第一个号码，现在将 **9** 加到前面的号码上，检查新号码的位数之和是否为 **10** 。如果是，则这是该系列的下一个编号，这是因为所需系列的任意两个连续编号之间的差值至少为**9**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// sum of digits of n
int sum(int n)
{
    int sum = 0;
    while (n) {

        // Add the last digit to the sum
        sum = sum + n % 10;

        // Remove last digit
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to print the first n numbers
// whose sum of digits is 10
void firstN(int n)
{

    // First number of the series is 19
    int num = 19, cnt = 1;
    while (cnt != n) {

        // If the sum of digits of the
        // current number is equal to 10
        if (sum(num) == 10) {

            // Print the number
            cout << num << " ";
            cnt++;
        }

        // Add 9 to the previous number
        num += 9;
    }
}

// Driver code
int main()
{
    int n = 10;
    firstN(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the
// sum of digits of n
static int sum(int n)
{
    int sum = 0;
    while (n > 0)
    {

        // Add the last digit to the sum
        sum = sum + n % 10;

        // Remove last digit
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to print the first n numbers
// whose sum of digits is 10
static void firstN(int n)
{

    // First number of the series is 19
    int num = 19, cnt = 1;
    while (cnt != n)
    {

        // If the sum of digits of the
        // current number is equal to 10
        if (sum(num) == 10)
        {

            // Print the number
            System.out.print(num + " ");
            cnt++;
        }

        // Add 9 to the previous number
        num += 9;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    firstN(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# sum of digits of n
def sum(n) :

    sum = 0;
    while (n) :

        # Add the last digit to the sum
        sum = sum + n % 10;

        # Remove last digit
        n = n // 10;

    # Return the sum of digits
    return sum;

# Function to print the first n numbers
# whose sum of digits is 10
def firstN(n) :

    # First number of the series is 19
    num = 19; cnt = 1;

    while (cnt != n) :

        # If the sum of digits of the
        # current number is equal to 10
        if (sum(num) == 10) :

            # Print the number
            print(num,end= " ");
            cnt += 1;

        # Add 9 to the previous number
        num += 9;

# Driver code
if __name__ == "__main__" :

    n = 10;
    firstN(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// sum of digits of n
static int sum(int n)
{
    int sum = 0;
    while (n > 0)
    {

        // Add the last digit to the sum
        sum = sum + n % 10;

        // Remove last digit
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to print the first n numbers
// whose sum of digits is 10
static void firstN(int n)
{

    // First number of the series is 19
    int num = 19, cnt = 1;
    while (cnt != n)
    {

        // If the sum of digits of the
        // current number is equal to 10
        if (sum(num) == 10)
        {

            // Print the number
            Console.Write(num + " ");
            cnt++;
        }

        // Add 9 to the previous number
        num += 9;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;
    firstN(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the
    // sum of digits of n
    function sum(n) {
        var sum = 0;
        while (n > 0) {

            // Add the last digit to the sum
            sum = sum + n % 10;

            // Remove last digit
            n = parseInt(n / 10);
        }

        // Return the sum of digits
        return sum;
    }

    // Function to print the first n numbers
    // whose sum of digits is 10
    function firstN(n) {

        // First number of the series is 19
        var num = 19, cnt = 1;
        while (cnt != n) {

            // If the sum of digits of the
            // current number is equal to 10
            if (sum(num) == 10) {

                // Print the number
                document.write(num + " ");
                cnt++;
            }

            // Add 9 to the previous number
            num += 9;
        }
    }

    // Driver code

        var n = 10;
        firstN(n);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
19 28 37 46 55 64 73 82 91
```