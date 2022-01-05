# 大于或等于 X 的最小数，其位数之和可被 Y 整除

> 原文:[https://www . geesforgeks . org/最小数字大于或等于 x，其数字总和可被 y 整除/](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-x-whose-sum-of-digits-is-divisible-by-y/)

给定两个整数 **X** 和 **Y** ，任务是找出大于或等于 **X** 的最小数，其位数之和可被 **Y** 整除。
**注:***1*<=**X**<=*1000*，1<=**Y**<=*50*。
**例:**

> **输入:** X = 10，Y = 5
> **输出:** 14
> **说明:**
> 14 是大于 10 的最小数，其位数之和(1+4 = 5)可被 5 整除。
> **输入:** X = 5923，Y = 13
> **输出:** 5939

**方法:**这个问题的思路是从 **X** 开始运行一个循环，检查每个整数的位数之和是否能被 **Y** 整除。返回第一个数字，其数字总和可被 **Y** 整除。给定 **X** 和 **Y** 的约束，答案总是存在的。
以下是上述方法的实施:

## C++

```
// C++ program to find the smallest number
// greater than or equal to X and divisible by Y

#include <bits/stdc++.h>
using namespace std;

#define MAXN 10000000

// Function that returns the sum
// of digits of a number
int sumOfDigits(int n)
{
    // Initialize variable to
    // store the sum
    int sum = 0;

    while (n > 0) {

        // Add the last digit
        // of the number
        sum += n % 10;

        // Remove the last digit
        // from the number
        n /= 10;
    }
    return sum;
}

// Function that returns the smallest number
// greater than or equal to X and divisible by Y
int smallestNum(int X, int Y)
{
    // Initialize result variable
    int res = -1;

    // Loop through numbers greater
    // than  equal to X
    for (int i = X; i < MAXN; i++) {

        // Calculate sum of digits
        int sum_of_digit = sumOfDigits(i);

        // Check if sum of digits
        // is divisible by Y
        if (sum_of_digit % Y == 0) {
            res = i;
            break;
        }
    }

    return res;
}

// Driver code
int main()
{
    int X = 5923, Y = 13;

    cout << smallestNum(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number
// greater than or equal to X and divisible by Y

class GFG{

static final int MAXN = 10000000;

// Function that returns the sum
// of digits of a number
static int sumOfDigits(int n)
{

    // Initialize variable to
    // store the sum
    int sum = 0;
    while (n > 0)
    {

         // Add the last digit
         // of the number
         sum += n % 10;

         // Remove the last digit
         // from the number
         n /= 10;
    }
    return sum;
}

// Function that returns the smallest number
// greater than or equal to X and divisible by Y
static int smallestNum(int X, int Y)
{

    // Initialize result variable
    int res = -1;

    // Loop through numbers greater
    // than equal to X
    for (int i = X; i < MAXN; i++)
    {

        // Calculate sum of digits
        int sum_of_digit = sumOfDigits(i);

        // Check if sum of digits
        // is divisible by Y
        if (sum_of_digit % Y == 0)
        {
            res = i;
            break;
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int X = 5923, Y = 13;
    System.out.print(smallestNum(X, Y));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to find the smallest number
# greater than or equal to X and divisible by Y

MAXN = 10000000

# Function that returns the 
# sum of digits of a number
def sumOfDigits(n):

    # Initialize variable 
    # to store the sum
    sum = 0

    while(n > 0):

        # Add the last digit
        # of the number
        sum += n % 10

        # Remove the last digit
        # from the number
        n //= 10

    return sum

# Function that returns the smallest number
# greater than or equal to X and divisible by Y
def smallestNum(X, Y):

    # Initialize result variable
    res = -1;

    # Loop through numbers greater
    # than equal to X
    for i in range(X, MAXN):

        # Calculate sum of digits
        sum_of_digit = sumOfDigits(i)

        # Check if sum of digits
        # is divisible by Y
        if sum_of_digit % Y == 0:
            res = i
            break

    return res    

# Driver code
if __name__=='__main__':

    (X, Y) = (5923, 13)

    print(smallestNum(X, Y))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the smallest number
// greater than or equal to X and divisible by Y
using System;

class GFG{

static readonly int MAXN = 10000000;

// Function that returns the sum
// of digits of a number
static int sumOfDigits(int n)
{

    // Initialize variable to
    // store the sum
    int sum = 0;
    while(n > 0)
    {

         // Add the last digit
         // of the number
         sum += n % 10;

         // Remove the last digit
         // from the number
         n /= 10;
    }
    return sum;
}

// Function that returns the smallest number
// greater than or equal to X and divisible by Y
static int smallestNum(int X, int Y)
{

    // Initialize result variable
    int res = -1;

    // Loop through numbers greater
    // than equal to X
    for(int i = X; i < MAXN; i++)
    {

        // Calculate sum of digits
        int sum_of_digit = sumOfDigits(i);

        // Check if sum of digits
        // is divisible by Y
        if(sum_of_digit % Y == 0)
        {
           res = i;
           break;
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int X = 5923, Y = 13;
    Console.Write(smallestNum(X, Y));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// javascript program to find the smallest number
// greater than or equal to X and divisible by Y
var MAXN = 10000000;

// Function that returns the sum
// of digits of a number
function sumOfDigits(n)
{

    // Initialize variable to
    // store the sum
    var sum = 0;
    while (n > 0)
    {

         // Add the last digit
         // of the number
         sum += n % 10;

         // Remove the last digit
         // from the number
         n  = parseInt(n/10);
    }
    return sum;
}

// Function that returns the smallest number
// greater than or equal to X and divisible by Y
function smallestNum(X , Y)
{

    // Initialize result variable
    var res = -1;

    // Loop through numbers greater
    // than equal to X
    for (i = X; i < MAXN; i++)
    {

        // Calculate sum of digits
        var sum_of_digit = sumOfDigits(i);

        // Check if sum of digits
        // is divisible by Y
        if (sum_of_digit % Y == 0)
        {
            res = i;
            break;
        }
    }
    return res;
}

// Driver code
var X = 5923, Y = 13;
document.write(smallestNum(X, Y));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
5939
```

时间复杂度:0(最大值)

辅助空间:0(1)