# n 位步进数个数|空间优化解

> 原文:[https://www . geesforgeks . org/number-of-n-digital-steping-numbers-space-optimized-solution/](https://www.geeksforgeeks.org/number-of-n-digit-stepping-numbers-space-optimized-solution/)

给定 n，求 n 位数步进数的个数。如果所有相邻数字的绝对差值为 1，则该数字称为步进数。321 是步进数，而 421 不是。
**例:**

```
Input : 2
Output : 17
The numbers are 10, 12, 21, 
23, 32, 34, 43, 45, 54, 56, 65, 67, 76, 
78, 87, 89, 98.

Input : 1
Output : 10
The numbers are 0, 1, 2, 3, 
4, 5, 6, 7, 8, 9.
```

在[之前的帖子](https://www.geeksforgeeks.org/number-n-digit-stepping-numbers/)中，讨论了一个需要 O(n)个辅助空间的解决方案。可以优化解决问题所需的辅助空间。二维 dp 数组 dp[i][j]表示长度为 I 和最后一个数字 j 的步进数的计数。对于数字 j，计数从数字 j–1 和 j + 1 获得。递推关系为**DP[I][j]= DP[I-1][j-1]+DP[I-1][j+1]**。注意，当前长度 I 的答案仅取决于 I–1。因此，可以使用一维 dp 数组，其中对于给定的 I，dp[j]存储以数字 j 结束的长度 I 的步进数的计数。在更新给定长度 I 的 dp 数组之前，将长度 I–1 的结果存储在另一个数组中 *prev* ，然后使用 *prev* 数组更新 dp 数组。
以下是上述方法的实施:

## C++

```
// CPP program to calculate the number of
// n digit stepping numbers.
#include <bits/stdc++.h>
using namespace std;

// function that calculates the answer
long long answer(int n)
{
    // dp[j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    int dp[10];

    // To store result of length i - 1
    // before updating dp[j] for length i.
    int prev[10];

    // if n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for (int j = 0; j <= 9; j++)
        dp[j] = 1;

    // Compute values for count of digits
    // more than 1.
    for (int i = 2; i <= n; i++) {
        for (int j = 0; j <= 9; j++) {
            prev[j] = dp[j];
        }

        for (int j = 0; j <= 9; j++) {

            // If ending digit is 0
            if (j == 0)
                dp[j] = prev[j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[j] = prev[j - 1];

            // For other digits.
            else
                dp[j] = prev[j - 1] + prev[j + 1];
        }
    }

    // stores the final answer
    long long sum = 0;
    for (int j = 1; j <= 9; j++)
        sum += dp[j];
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
class GFG
{

// function that calculates the answer
static long answer(int n)
{
    // dp[j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    int[] dp = new int[10];

    // To store result of length i - 1
    // before updating dp[j] for length i.
    int[] prev = new int[10];

    // if n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for (int j = 0; j <= 9; j++)
        dp[j] = 1;

    // Compute values for count of digits
    // more than 1.
    for (int i = 2; i <= n; i++)
    {
        for (int j = 0; j <= 9; j++)
        {
            prev[j] = dp[j];
        }

        for (int j = 0; j <= 9; j++)
        {

            // If ending digit is 0
            if (j == 0)
                dp[j] = prev[j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[j] = prev[j - 1];

            // For other digits.
            else
                dp[j] = prev[j - 1] + prev[j + 1];
        }
    }

    // stores the final answer
    long sum = 0;
    for (int j = 1; j <= 9; j++)
        sum += dp[j];
    return sum;
}

// Driver code
public static void main (String[] args)
{
    int n = 2;
    System.out.println(answer(n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to calculate the number of
# n digit stepping numbers.

# function that calculates the answer
def answer(n) :

    # dp[j] stores count of i digit
    # stepping numbers ending with digit j.
    dp = [0] * 10

    # To store resu1lt of length i - 1
    # before updating dp[j] for length i.
    prev = [0] * 10

    # if n is 1 then answer will be 10.
    if (n == 1):
        return 10

    # Initialize values for count of
    # digits equal to 1.
    for j in range(0, 10) :
        dp[j] = 1

    # Compute values for count of digits
    # more than 1.
    for i in range(2, n + 1):
        for j in range (0, 10):
            prev[j] = dp[j]

        for j in range (0, 10):

            # If ending digit is 0
            if (j == 0):
                dp[j] = prev[j + 1]

            # If ending digit is 9
            elif (j == 9) :
                dp[j] = prev[j - 1]

            # For other digits.
            else :
                dp[j] = prev[j - 1] + prev[j + 1]

    # stores the final answer
    sum = 0
    for j in range (1, 10):
        sum = sum + dp[j]
    return sum

# Driver Code
n = 2
print(answer(n))

# This code is contributed by ihritik
```

## C#

```
// C# program to calculate the number of
// n digit stepping numbers.
using System;

class GFG
{

// function that calculates the answer
static long answer(int n)
{
    // dp[j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    int[] dp = new int[10];

    // To store result of length i - 1
    // before updating dp[j] for length i.
    int[] prev = new int[10];

    // if n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for (int j = 0; j <= 9; j++)
        dp[j] = 1;

    // Compute values for count of digits
    // more than 1.
    for (int i = 2; i <= n; i++)
    {
        for (int j = 0; j <= 9; j++)
        {
            prev[j] = dp[j];
        }

        for (int j = 0; j <= 9; j++)
        {

            // If ending digit is 0
            if (j == 0)
                dp[j] = prev[j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[j] = prev[j - 1];

            // For other digits.
            else
                dp[j] = prev[j - 1] + prev[j + 1];
        }
    }

    // stores the final answer
    long sum = 0;
    for (int j = 1; j <= 9; j++)
        sum += dp[j];
    return sum;
}

// Driver code
static void Main()
{
    int n = 2;
    Console.WriteLine(answer(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate the number of
// n digit stepping numbers.

// function that calculates the answer
function answer($n)
{
    // dp[j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    $dp = array_fill(0, 10, 0);

    // To store result of length i - 1
    // before updating dp[j] for length i.
    $prev = array_fill(0, 10, 0);;

    // if n is 1 then answer will be 10.
    if ($n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for ($j = 0; $j <= 9; $j++)
        $dp[$j] = 1;

    // Compute values for count of digits
    // more than 1.
    for ($i = 2; $i <= $n; $i++)
    {
        for ($j = 0; $j <= 9; $j++)
        {
            $prev[$j] = $dp[$j];
        }

        for ($j = 0; $j <= 9; $j++)
        {

            // If ending digit is 0
            if ($j == 0)
                $dp[$j] = $prev[$j + 1];

            // If ending digit is 9
            else if ($j == 9)
                $dp[$j] = $prev[$j - 1];

            // For other digits.
            else
                $dp[$j] = $prev[$j - 1] + $prev[$j + 1];
        }
    }

    // stores the final answer
    $sum = 0;
    for ($j = 1; $j <= 9; $j++)
        $sum += $dp[$j];
    return $sum;
}

    // Driver program to test the above function
    $n = 2;
    echo answer($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate the number of
// n digit stepping numbers.

// function that calculates the answer
function answer(n)
{
    // dp[j] stores count of i digit
    // stepping numbers ending with digit
    // j.
    var dp = Array(10);

    // To store result of length i - 1
    // before updating dp[j] for length i.
    var prev = Array(10);

    // if n is 1 then answer will be 10.
    if (n == 1)
        return 10;

    // Initialize values for count of
    // digits equal to 1.
    for (var j = 0; j <= 9; j++)
        dp[j] = 1;

    // Compute values for count of digits
    // more than 1.
    for (var i = 2; i <= n; i++) {
        for (var j = 0; j <= 9; j++) {
            prev[j] = dp[j];
        }

        for (var j = 0; j <= 9; j++) {

            // If ending digit is 0
            if (j == 0)
                dp[j] = prev[j + 1];

            // If ending digit is 9
            else if (j == 9)
                dp[j] = prev[j - 1];

            // For other digits.
            else
                dp[j] = prev[j - 1] + prev[j + 1];
        }
    }

    // stores the final answer
    var sum = 0;
    for (var j = 1; j <= 9; j++)
        sum += dp[j];
    return sum;
}

// driver program to test the above function
var n = 2;
document.write( answer(n));

</script>
```

**Output:** 

```
17
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)