# 给定一个以十进制为基数的数 N，求任意基数 B 的位数之和

> 原文:[https://www . geesforgeks . org/给定一个十进制数 n-base-find-任何基数中的数字总和-b/](https://www.geeksforgeeks.org/given-a-number-n-in-decimal-base-find-the-sum-of-digits-in-any-base-b/)

给定一个以十进制为基数的数 **N** ，任务是求任意基数的数的位数之和 **B** 。
**例:**

> **输入:** N = 100，B = 8
> **输出:** 9
> **解释:**
> (100) <sub>8</sub> = 144
> 和(144) = 1 + 4 + 4 = 9
> **输入:** N = 50，B = 2
> **输出:** 3
> **解释:**T21

**方法:**用基数 B 对数字 N 进行模运算，再用 **N = N / B** 更新数字，找到单位数字，每一步加单位数字更新和。
以下是上述办法的实施情况

## C++

```
// C++ Implementation to Compute Sum of
// Digits of Number N in Base B

#include <iostream>
using namespace std;

// Function to compute sum of
// Digits of Number N in base B
int sumOfDigit(int n, int b)
{

    // Initialize sum with 0
    int unitDigit, sum = 0;
    while (n > 0) {

        // Compute unit digit of the number
        unitDigit = n % b;

        // Add unit digit in sum
        sum += unitDigit;

        // Update value of Number
        n = n / b;
    }
    return sum;
}

// Driver function
int main()
{
    int n = 50;
    int b = 2;
    cout << sumOfDigit(n, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to Compute Sum of
// Digits of Number N in Base B
class GFG
{

// Function to compute sum of
// Digits of Number N in base B
static int sumOfDigit(int n, int b)
{

    // Initialize sum with 0
    int unitDigit, sum = 0;
    while (n > 0)
    {

        // Compute unit digit of the number
        unitDigit = n % b;

        // Add unit digit in sum
        sum += unitDigit;

        // Update value of Number
        n = n / b;
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 50;
    int b = 2;
    System.out.print(sumOfDigit(n, b));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Implementation to Compute Sum of
# Digits of Number N in Base B

# Function to compute sum of
# Digits of Number N in base B
def sumOfDigit(n, b):

    # Initialize sum with 0
    unitDigit = 0
    sum = 0
    while (n > 0):

        # Compute unit digit of the number
        unitDigit = n % b

        # Add unit digit in sum
        sum += unitDigit

        # Update value of Number
        n = n // b

    return sum

# Driver code
n = 50
b = 2
print(sumOfDigit(n, b))

# This code is contributed by ApurvaRaj
```

## C#

```
// C# Implementation to Compute Sum of
// Digits of Number N in Base B
using System;

class GFG
{

// Function to compute sum of
// Digits of Number N in base B
static int sumOfDigit(int n, int b)
{

    // Initialize sum with 0
    int unitDigit, sum = 0;
    while (n > 0)
    {

        // Compute unit digit of the number
        unitDigit = n % b;

        // Add unit digit in sum
        sum += unitDigit;

        // Update value of Number
        n = n / b;
    }
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int n = 50;
    int b = 2;
    Console.Write(sumOfDigit(n, b));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript Implementation to Compute Sum of
// Digits of Number N in Base B

// Function to compute sum of
// Digits of Number N in base B
function sumOfDigit(n, b)
{

    // Initialize sum with 0
    var unitDigit, sum = 0;
    while (n > 0)
    {

        // Compute unit digit of the number
        unitDigit = n % b;

        // Add unit digit in sum
        sum += unitDigit;

        // Update value of Number
        n = parseInt(n / b);
    }
    return sum;
}

// Driver function
var n = 50;
var b = 2;
document.write(sumOfDigit(n, b));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)，N =位数

**辅助空间:** O(1)