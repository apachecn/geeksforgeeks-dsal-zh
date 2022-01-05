# 求两个数乘积的最大位数之和

> 原文:[https://www . geesforgeks . org/find-两位数乘积的最大位数总和/](https://www.geeksforgeeks.org/find-the-maximum-sum-of-digits-of-the-product-of-two-numbers/)

给定一个大小为 **N** ( > 2)的数组 **arr[]** 。任务是找出给定数组中任意两个数乘积的最大位数和。
**例:**

> **输入:** arr[] = {8，7}
> **输出:**11
> **8**与 **7** 的乘积为 **56** 。56 位数之和等于 **11** 。
> **输入:** arr[] = {4，3，5}
> **输出:**6
> 4&3 的乘积= 12。数字之和= 3。
> 3 的乘积& 5 = 15。数字总和= 6。
> 4 的乘积& 5 = 20。数字之和= 2。

**方法:**运行嵌套循环，选择数组的两个数，得到乘积。对于每个产品，检查[数字总和](https://www.geeksforgeeks.org/program-for-sum-the-digits-of-a-given-number/)并找出最大数字总和。
以下是上述方法的实施:

## C++

```
// C++ program find the maximum sum of
// digits of the product of two numbers
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the digits
int sumDigits(int n)
{
    int digit_sum = 0;
    while (n) {
        digit_sum += n % 10;
        n /= 10;
    }
    return digit_sum;
}

// Function to find the maximum sum of digits of product
int productOfNumbers(int arr[], int n)
{
    int sum = INT_MIN;

    // Run nested loops
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            int product = arr[i] * arr[j];

            // Find the maximum sum
            sum = max(sum, sumDigits(product));
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << productOfNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find the maximum sum of
// digits of the product of two numbers
import java.io.*;

class GFG
{

// Function to find the sum of the digits
static int sumDigits(int n)
{
    int digit_sum = 0;
    while (n > 0)
    {
        digit_sum += n % 10;
        n /= 10;
    }
    return digit_sum;
}

// Function to find the maximum sum
// of digits of product
static int productOfNumbers(int []arr, int n)
{
    int sum = Integer.MIN_VALUE;

    // Run nested loops
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            int product = arr[i] * arr[j];

            // Find the maximum sum
            sum = Math.max(sum, sumDigits(product));
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 4, 3, 5 };

    int n = arr.length;

    System.out.print( productOfNumbers(arr, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program find the maximum sum of
# digits of the product of two numbers
import sys

# Function to find the sum of the digits
def sumDigits(n):

    digit_sum = 0;
    while (n > 0):
        digit_sum += n % 10;
        n /= 10;

    return digit_sum;

# Function to find the maximum sum
# of digits of product
def productOfNumbers(arr, n):

    sum = -sys.maxsize - 1;

    # Run nested loops
    for i in range(n - 1):
        for j in range(i + 1, n):
            product = arr[i] * arr[j];

            # Find the maximum sum
            sum = max(sum, sumDigits(product));

    # Return the required answer
    return sum;

# Driver code
if __name__ == '__main__':

    arr =[ 4, 3, 5 ];

    n = len(arr);

    print(int(productOfNumbers(arr, n)));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program find the maximum sum of
// digits of the product of two numbers
using System;

class GFG
{

// Function to find the sum of the digits
static int sumDigits(int n)
{
    int digit_sum = 0;
    while (n > 0)
    {
        digit_sum += n % 10;
        n /= 10;
    }
    return digit_sum;
}

// Function to find the maximum sum
// of digits of product
static int productOfNumbers(int []arr, int n)
{
    int sum = int.MinValue;

    // Run nested loops
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            int product = arr[i] * arr[j];

            // Find the maximum sum
            sum = Math.Max(sum, sumDigits(product));
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 4, 3, 5 };

    int n = arr.Length;

    Console.Write(productOfNumbers(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program find the maximum sum of
    // digits of the product of two numbers

    // Function to find the sum of the digits
    function sumDigits(n)
    {
        let digit_sum = 0;
        while (n > 0) {
            digit_sum += n % 10;
            n = parseInt(n / 10, 10);
        }
        return digit_sum;
    }

    // Function to find the maximum sum of digits of product
    function productOfNumbers(arr, n)
    {
        let sum = Number.MIN_VALUE;

        // Run nested loops
        for (let i = 0; i < n - 1; i++) {
            for (let j = i + 1; j < n; j++) {
                let product = arr[i] * arr[j];

                // Find the maximum sum
                sum = Math.max(sum, sumDigits(product));
            }
        }

        // Return the required answer
        return sum;
    }

    let arr = [ 4, 3, 5 ];

    let n = arr.length;

    document.write(productOfNumbers(arr, n));

</script>
```

**输出:**

```
6
```