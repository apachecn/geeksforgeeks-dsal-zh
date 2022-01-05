# 可以加到 N 上的 X 的最小值，使位数之和最小化到≤ K

> 原文:[https://www . geeksforgeeks . org/x 的最小可加值为 n，以最小化小于或等于 k 的位数总和/](https://www.geeksforgeeks.org/minimum-value-of-x-that-can-be-added-to-n-to-minimize-sum-of-the-digits-to-less-than-or-equal-to-k/)

给定两个整数 **N** 和 **K** ，任务是找到可以加到 **N** 上的最小整数 **X** ，这样新形成的数字的位数之和就不会超过 **K** 。

**示例:**

> **输入:** N = 1，K = 1
> **输出:** 0
> **说明:**
> 给定数字的位数之和为 1，已经等于 K(=1)。
> 
> **输入:** N = 11，K = 1
> **输出:** 89
> **解释:**
> 将数字 89 加到给定的数字 11 上，结果为 100。
> 形成的新号码位数之和为 1，不超过 K(=1)。
> 因此，可以添加的最小数量是 89。

**方法:**按照以下步骤解决问题:

1.  检查给定数字 **N** 的数字之和[是否不超过 **K** 。如果发现为真，则添加的最少数字为 0。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)
2.  现在，从单位所在地开始计算位数总和，一直持续到位数总和超过 **K** 。
3.  现在，找到数字之和大于或等于 **K** 的部分 **N** 。因此，删除该部分的最后一个数字，使数字之和小于 **K** 。
4.  现在，将新获得的号码加上 **1** ，因为它将保持数字的总和小于或等于 **K** 。
5.  现在，要获得超过 **N** 且位数小于或等于 **K** 的新数字，将该数字乘以 10 <sup>P + 1</sup> ，其中 **P** 是总计未超过 **K** 的位数。
6.  现在从新数字中减去 **N** 得到结果 **X** 。
7.  完成以上步骤后，打印 **X** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// needed to be added so that the sum
// of the digits does not exceed K
int minDigits(int N, int K)
{
    // Find the number of digits
    int digits_num
        = floor(log10(N) + 1);

    int temp_sum = 0;
    int temp = digits_num;
    int result;

    int X, var;

    int sum = 0;
    int num2 = N;

    // Calculate sum of the digits
    while (num2 != 0) {

        // Add the digits of num2
        sum += num2 % 10;
        num2 /= 10;
    }

    // If the sum of the digits of N
    // is less than or equal to K
    if (sum <= K) {

        // No number needs to
        // be added
        X = 0;
    }

    // Otherwise
    else {

        while (temp > 0) {

            // Calculate the sum of digits
            // from least significant digit
            var = (N / (pow(10, temp - 1)));
            temp_sum += var % 10;

            // If sum exceeds K
            if (temp_sum >= K) {

                // Increase previous
                // digit by 1
                var /= 10;
                var++;

                // Add zeros to the end
                result
                    = var * pow(10, temp);

                break;
            }

            temp--;
        }

        // Calculate difference
        // between the result and N
        X = result - N;

        // Return the result
        return X;
    }
}

// Driver Code
int main()
{
    int N = 11, K = 1;
    cout << minDigits(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find the minimum number
// needed to be added so that the sum
// of the digits does not exceed K
static int minDigits(int N, int K)
{

    // Find the number of digits
    int digits_num = (int)Math.floor(
                          Math.log(N) + 1);

    int temp_sum = 0;
    int temp = digits_num;
    int result = 0;
    int X, var;
    int sum = 0;
    int num2 = N;

    // Calculate sum of the digits
    while (num2 != 0)
    {

        // Add the digits of num2
        sum += num2 % 10;
        num2 /= 10;
    }

    // If the sum of the digits of N
    // is less than or equal to K
    if (sum <= K)
    {

        // No number needs to
        // be added
        X = 0;
    }

    // Otherwise
    else
    {
        while (temp > 0)
        {

            // Calculate the sum of digits
            // from least significant digit
            var = (N / ((int)Math.pow(
                   10, temp - 1)));
            temp_sum += var % 10;

            // If sum exceeds K
            if (temp_sum >= K)
            {

                // Increase previous
                // digit by 1
                var /= 10;
                var++;

                // Add zeros to the end
                result = var * (int)Math.pow(
                         10, temp);
                break;
            }
            temp--;
        }

        // Calculate difference
        // between the result and N
        X = result - N;

        // Return the result
        return X;
    }
    return -1;
}

// Driver Code
public static void main(String args[])
{
    int N = 11;
    int K = 1;

    System.out.println(minDigits(N, K));
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python program for
# the above approach
import math;

# Function to find the minimum number
# needed to be added so that the sum
# of the digits does not exceed K
def minDigits(N, K):

    # Find the number of digits
    digits_num = int(math.floor(math.log(N) + 1));

    temp_sum = 0;
    temp = digits_num;
    result = 0;
    X = 0; var = 0;
    sum1 = 0;
    num2 = N;

    # Calculate sum of the digits
    while (num2 != 0):

        # Add the digits of num2
        sum1 += num2 % 10;
        num2 /= 10;   

    # If the sum of the digits of N
    # is less than or equal to K
    if (sum1 <= K):

        # No number needs to
        # be added
        X = 0;   

    # Otherwise
    else:
        while (temp > 0):

            # Calculate the sum of digits
            # from least significant digit
            var = int(N // (pow(10, temp - 1)));
            temp_sum += var % 10;

            # If sum exceeds K
            if (temp_sum >= K):

                # Increase previous
                # digit by 1
                var = var // 10;
                var += 1;

                # Add zeros to the end
                result = var * int(pow(10, temp));
                break;

            temp -= 1;       

        # Calculate difference
        # between the result and N
        X = result - N;

        # Return the result
        return X;

    return -1;

# Driver Code
if __name__ == '__main__':
    N = 11;
    K = 1;
    print(minDigits(N, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// needed to be added so that the sum
// of the digits does not exceed K
static int minDigits(int N, int K)
{

    // Find the number of digits
    int digits_num = (int)Math.Floor(
                          Math.Log(N) + 1);

    int temp_sum = 0;
    int temp = digits_num;
    int result = 0;
    int X, var;
    int sum = 0;
    int num2 = N;

    // Calculate sum of the digits
    while (num2 != 0)
    {

        // Add the digits of num2
        sum += num2 % 10;
        num2 /= 10;
    }

    // If the sum of the digits of N
    // is less than or equal to K
    if (sum <= K)
    {

        // No number needs to
        // be added
        X = 0;
    }

    // Otherwise
    else
    {
        while (temp > 0)
        {

            // Calculate the sum of digits
            // from least significant digit
            var = (N / ((int)Math.Pow(
                   10, temp - 1)));

            temp_sum += var % 10;

            // If sum exceeds K
            if (temp_sum >= K)
            {

                // Increase previous
                // digit by 1
                var /= 10;
                var++;

                // Add zeros to the end
                result = var * (int)Math.Pow(
                         10, temp);
                break;
            }
            temp--;
        }

        // Calculate difference
        // between the result and N
        X = result - N;

        // Return the result
        return X;
    }
    return -1;
}

// Driver Code
public static void Main(String []args)
{
    int N = 11;
    int K = 1;

    Console.WriteLine(minDigits(N, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// needed to be added so that the sum
// of the digits does not exceed K
function minDigits(N, K)
{

    // Find the number of digits
    let digits_num
        = Math.floor(Math.log(N) / Math.log(10) + 1);

    let temp_sum = 0;
    let temp = digits_num;
    let result;

    let X, var1;

    let sum = 0;
    let num2 = N;

    // Calculate sum of the digits
    while (num2 != 0) {

        // Add the digits of num2
        sum += num2 % 10;
        num2 = parseInt(num2 / 10);
    }

    // If the sum of the digits of N
    // is less than or equal to K
    if (sum <= K) {

        // No number needs to
        // be added
        X = 0;
    }

    // Otherwise
    else {

        while (temp > 0) {

            // Calculate the sum of digits
            // from least significant digit
            var1 = parseInt(N / (Math.pow(10, temp - 1)));
            temp_sum += var1 % 10;

            // If sum exceeds K
            if (temp_sum >= K) {

                // Increase previous
                // digit by 1
                var1 = parseInt(var1 / 10);
                var1++;

                // Add zeros to the end
                result
                    = var1 * Math.pow(10, temp);
                break;
            }
            temp--;
        }

        // Calculate difference
        // between the result and N
        X = result - N;

        // Return the result
        return X;
    }
}

// Driver Code
    let N = 11, K = 1;
    document.write(minDigits(N, K));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
89
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(1)*