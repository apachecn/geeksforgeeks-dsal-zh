# n 位步进数数量

> 原文:[https://www . geesforgeks . org/number-n-digit-steping-numbers/](https://www.geeksforgeeks.org/number-n-digit-stepping-numbers/)

给定 n，求 n 位数[步数](https://www.geeksforgeeks.org/stepping-numbers/)的个数。如果所有相邻数字的绝对差值都为 1，则该数字称为步进数。321 是步进数，而 421 不是。

**示例:**

```
Input : 2 
Output : 17
Explanation: The numbers are 10, 12, 21, 
23, 32, 34, 43, 45, 54, 56, 65, 67, 76, 
78, 87, 89, 98.

Input : 1
Output : 10
Explanation: the numbers are 0, 1, 2, 3, 
4, 5, 6, 7, 8, 9.
```

一种**天真的方法**是对所有 n 位数运行一个循环，并检查每个数字是否为步进。

一种有效的方法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。

```
In dp[i][j], i denotes number of
digits and j denotes last digit.

// If there is only one digit
if (i == 1)
   dp(i, j) = 1;

// If last digit is 0.
if (j == 0) 
   dp(i, j) = dp(i-1, j+1)

// If last digit is 9
else if (j == 9) 
   dp(i, j) = dp(i-1, j-1)

// If last digit is neither 0
// nor 9.
else 
   dp(i, j) = dp(i-1, j-1) + 
              dp(i-1, j+1)

Result is ∑dp(n, j) where j varies
from 1 to 9\. 
```

## C++

```
// CPP program to calculate the number of
// n digit stepping numbers.
#include <bits/stdc++.h>
using namespace std;

// function that calculates the answer
long long answer(int n)
{
    // dp[i][j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    int dp[n + 1][10];

    // if n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for (int j = 0; j <= 9; j++)
        dp[1][j] = 1;

    // Compute values for count of digits
    // more than 1.
    for (int i = 2; i <= n; i++) {
        for (int j = 0; j <= 9; j++) {

            // If ending digit is 0
            if (j == 0)
                dp[i][j] = dp[i - 1][j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[i][j] = dp[i - 1][j - 1];

            // For other digits.
            else
                dp[i][j] = dp[i - 1][j - 1] +
                           dp[i - 1][j + 1];
        }
    }

    // stores the final answer
    long long sum = 0;
    for (int j = 1; j <= 9; j++)
        sum += dp[n][j];
    return sum;
}

// driver program to test the above function
int main()
{
    int n = 2;
    cout << answer(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the number of
// n digit stepping numbers.

class GFG {

    // function that calculates the answer
    static long answer(int n)
    {
        // dp[i][j] stores count of i
        // digit stepping numbers ending
        // with digit j.
        int dp[][] = new int[n+1][10];

        // if n is 1 then answer will be 10.
        if (n == 1)
            return 10;

        // Initialize values for count of
        // digits equal to 1.
        for (int j = 0; j <= 9; j++)
            dp[1][j] = 1;

        // Compute values for count of
        // digits more than 1.
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {

                // If ending digit is 0
                if (j == 0)
                    dp[i][j] = dp[i - 1][j + 1];

                // If ending digit is 9
                else if (j == 9)
                    dp[i][j] = dp[i - 1][j - 1];

                // For other digits.
                else
                    dp[i][j] = dp[i - 1][j - 1] +
                               dp[i - 1][j + 1];
            }
        }

        // stores the final answer
        long sum = 0;
        for (int j = 1; j <= 9; j++)
            sum += dp[n][j];
        return sum;
    }

    // driver program to test the above function
    public static void main(String args[])
    {
        int n = 2;
        System.out.println(answer(n));
    }
}

/*This code is contributed by Nikita tiwari.*/
```

## 蟒蛇 3

```
# Python3 program to calculate
# the number of n digit
# stepping numbers.

# function that calculates
# the answer
def answer(n):

    # dp[i][j] stores count of
    # i digit stepping numbers
    # ending with digit j.
    dp = [[0 for x in range(10)]
             for y in range(n + 1)];

    # if n is 1 then answer
    # will be 10.
    if (n == 1):
        return 10;
    for j in range(10):
        dp[1][j] = 1;

    # Compute values for count
    # of digits more than 1.
    for i in range(2, n + 1):
        for j in range(10):

            # If ending digit is 0
            if (j == 0):
                dp[i][j] = dp[i - 1][j + 1];

            # If ending digit is 9
            elif (j == 9):
                dp[i][j] = dp[i - 1][j - 1];

            # For other digits.
            else:
                dp[i][j] = (dp[i - 1][j - 1] +
                            dp[i - 1][j + 1]);

    # stores the final answer
    sum = 0;
    for j in range(1, 10):
        sum = sum + dp[n][j];
    return sum;

# Driver Code
n = 2;
print(answer(n));

# This code is contributed
# by mits
```

## C#

```
// C# program to calculate the number of
// n digit stepping numbers.
using System;

class GFG {

    // function that calculates the answer
    static long answer(int n)
    {

        // dp[i][j] stores count of i
        // digit stepping numbers ending
        // with digit j.
        int [,]dp = new int[n+1,10];

        // if n is 1 then answer will be 10.
        if (n == 1)
            return 10;

        // Initialize values for count of
        // digits equal to 1.
        for (int j = 0; j <= 9; j++)
            dp[1,j] = 1;

        // Compute values for count of
        // digits more than 1.
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= 9; j++) {

                // If ending digit is 0
                if (j == 0)
                    dp[i,j] = dp[i - 1,j + 1];

                // If ending digit is 9
                else if (j == 9)
                    dp[i,j] = dp[i - 1,j - 1];

                // For other digits.
                else
                    dp[i,j] = dp[i - 1,j - 1] +
                               dp[i - 1,j + 1];
            }
        }

        // stores the final answer
        long sum = 0;
        for (int j = 1; j <= 9; j++)
            sum += dp[n,j];

        return sum;
    }

    // driver program to test the above function
    public static void Main()
    {
        int n = 2;

        Console.WriteLine(answer(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the number of n digit
// stepping numbers.

// function that calculates
// the answer
function answer($n)
{
    // dp[i][j] stores count of
    // i digit stepping numbers
    // ending with digit j.

    // if n is 1 then answer
    // will be 10.
    if ($n == 1)
        return 10;
    for ( $j = 0; $j <= 9; $j++)
        $dp[1][$j] = 1;

    // Compute values for count
    // of digits more than 1.
    for ($i = 2; $i <= $n; $i++)
    {
        for ($j = 0; $j <= 9; $j++)
        {

            // If ending digit is 0
            if ($j == 0)
                $dp[$i][$j] = $dp[$i - 1][$j + 1];

            // If ending digit is 9
            else if ($j == 9)
                $dp[$i][$j] = $dp[$i - 1][$j - 1];

            // For other digits.
            else
                $dp[$i][$j] = $dp[$i - 1][$j - 1] +
                               $dp[$i - 1][$j + 1];
        }
    }

    // stores the final answer
    $sum = 0;
    for ($j = 1; $j <= 9; $j++)
        $sum += $dp[$n][$j];
    return $sum;
}

// Driver Code
$n = 2;
echo answer($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to calculate the number of
// n digit stepping numbers.

// Function that calculates the answer
function answer(n)
{

    // dp[i][j] stores count of i
    // digit stepping numbers ending
    // with digit j.
    let dp = new Array(n + 1);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    // If n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for(let j = 0; j <= 9; j++)
        dp[1][j] = 1;

    // Compute values for count of
    // digits more than 1.
    for(let i = 2; i <= n; i++)
    {
        for(let j = 0; j <= 9; j++)
        {

            // If ending digit is 0
            if (j == 0)
                dp[i][j] = dp[i - 1][j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[i][j] = dp[i - 1][j - 1];

            // For other digits.
            else
                dp[i][j] = dp[i - 1][j - 1] +
                           dp[i - 1][j + 1];
        }
    }

    // Stores the final answer
    let sum = 0;
    for(let j = 1; j <= 9; j++)
        sum += dp[n][j];

    return sum;
}

// Driver Code
let n = 2;

document.write(answer(n));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
17
```

**时间复杂度:**O(n)
T3】辅助空间:O(n)[n 位步进数个数|空间优化解](https://www.geeksforgeeks.org/number-of-n-digit-stepping-numbers-space-optimized-solution/)