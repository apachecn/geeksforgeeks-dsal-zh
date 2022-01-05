# 计数由 X 或 Y 组成的 N 位数，其位数之和也由 X 或 Y 组成

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-composed-of-x-or-y-其数字总和也是-x-or-y/](https://www.geeksforgeeks.org/count-n-digit-numbers-made-up-of-x-or-y-whose-sum-of-digits-is-also-made-up-of-x-or-y/)

给定三个正整数 **N** 、 **X** 和 **Y** ，任务是将包含 **X** 或 **Y** 的 **N** 位数字仅作为数字计数，数字之和还包含 **X** 或 **Y** 。由于计数可能很大，打印计数[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 2，X = 1，Y = 2
> **输出:** 1
> **说明:**所有可以用 X 和 Y 组成的 2 位数都是 11，12，21，22。其中，只有 11 是有效数字，因为它的位数总和是 2 (= Y)。
> 
> **输入:** N = 3，X = 1，Y = 5
> **输出:** 4
> **说明:**所有可以用 X 和 Y 组成的 3 位数都是 111，115，151，155。但是只有 155、515、551 和 555 满足给定的条件。因此，计数为 4。

**天真方法:**使用[递归](https://www.geeksforgeeks.org/recursion/)解决这个问题最简单的方法。每一步都有 **2 个选择，**将数字 **X** 或 **Y** 放置在当前位置，当形成的数字长度等于 **N** 时，计算数字之和。如果总和也仅由 **X** 或 **Y** 组成，则计算该数字。检查所有数字后，打印计数模 **10 <sup>9</sup> + 7** 。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**由于该问题同时具有 [**【最优子结构】**](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/) 和 [**重叠子问题**](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/) 的性质，因此可以使用 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 对上述方法进行优化。当剩余位数为 **N** 且填充位数之和为**和**时，使用辅助数组 **dp[N][sum]** 存储数值，可以避免相同子问题的计算。以下是步骤:

*   初始化一个辅助数组 **dp[][]** 来存储中间计算。
*   每一步都有 **2 个选择**在当前位置放置数字 **X** 或 **Y** 。
*   当剩余位数为 **0** 时，检查是否可以使用 **X** 或 **Y** 进行位数求和。如果是，则将当前状态值增加 **1** 。
*   否则将当前状态更新为 **0** 。
*   如果遇到相同的子问题，以 **10 <sup>9</sup> + 7** 为模返回已经计算的值。
*   将数字 **X** 和数字 **Y** 放在**当前位置**和**重复**剩余位置，并传递每一步的数字总和。
*   对于值 x 和 y 的每次递归调用，将当前状态更新为这些状态返回的值的总和。
*   完成上述步骤后，打印 **dp[N][0]** 的值作为结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the value of overlapping
// states
int dp[1000 + 5][9000 + 5];
int mod = 1000000007;

// Function to check whether a number
// have only digits X or Y or not
int check(int sum, int x, int y)
{
    // Until sum is positive
    while (sum > 0) {

        int ln = sum % 10;

        // If any digit is not
        // X or Y then return 0
        if (ln != x && ln != y) {
            return 0;
        }
        sum /= 10;
    }

    // Return 1
    return 1;
}

// Function to find the count of
// numbers that are formed by digits
// X and Y and whose sum of digit
// also have digit X or Y
int countNumbers(int n, int x, int y, int sum)
{
    // Initialize dp array
    memset(dp, -1, sizeof(dp));

    // Base Case
    if (n == 0) {

        // Check if sum of digits
        // formed by only X or Y
        return check(sum, x, y);
    }

    // Return the already computed
    if (dp[n][sum] != -1) {
        return dp[n][sum] % mod;
    }

    // Place the digit X at the
    // current position
    int option1 = countNumbers(n - 1, x,
                               y, sum + x) % mod;

    // Place the digit Y at the
    // current position
    int option2 = countNumbers(n - 1, x,
                               y, sum + y) % mod;

    // Update current state result
    return dp[n][sum] = (option1 + option2) % mod;
}

// Driver Code
int main()
{
    int N = 3, X = 1, Y = 5;

    // Function Call
    cout << countNumbers(N, X, Y, 0) % mod;
    // This code is contributed by bolliranadheer
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    // Stores the value of overlapping
    // states
    static int dp[][] = new int[1000 + 5][9000 + 5];
    static int mod = 1000000007;

    // Function to find the count of
    // numbers that are formed by digits
    // X and Y and whose sum of digit
    // also have digit X or Y
    public static int countNumbers(int n, int x, int y,
                                   int sum)
    {
        // Initialize dp array
        for (int i[] : dp)
            Arrays.fill(i, -1);

        // Base Case
        if (n == 0) {

            // Check if sum of digits
            // formed by only X or Y
            return check(sum, x, y);
        }

        // Return the already computed
        if (dp[n][sum] != -1) {
            return dp[n][sum] % mod;
        }

        // Place the digit X at the
        // current position
        int option1
            = countNumbers(n - 1, x, y, sum + x) % mod;

        // Place the digit Y at the
        // current position
        int option2
            = countNumbers(n - 1, x, y, sum + y) % mod;

        // Update current state result
        return dp[n][sum] = (option1 + option2) % mod;
    }

    // Function to check whether a number
    // have only digits X or Y or not
    public static int check(int sum, int x, int y)
    {
        // Until sum is positive
        while (sum > 0) {

            int ln = sum % 10;

            // If any digit is not
            // X or Y then return 0
            if (ln != x && ln != y) {
                return 0;
            }
            sum /= 10;
        }

        // Return 1
        return 1;
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 3, X = 1, Y = 5;

        // Function Call
        System.out.println(countNumbers(N, X, Y, 0) % mod);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the value of overlapping
# states
dp = [[-1 for x in range(9000 + 5)]
          for y in range(1000 + 5)]
mod = 1000000007

# Function to check whether a number
# have only digits X or Y or not
def check(sum, x, y):

    # Until sum is positive
    while (sum > 0):
        ln = sum % 10

        # If any digit is not
        # X or Y then return 0
        if (ln != x and ln != y):
            return 0

        sum //= 10

    # Return 1
    return 1

# Function to find the count of
# numbers that are formed by digits
# X and Y and whose sum of digit
# also have digit X or Y
def countNumbers(n, x, y, sum):

    # Initialize dp array
    global dp

    # Base Case
    if (n == 0):

        # Check if sum of digits
        # formed by only X or Y
        return check(sum, x, y)

    # Return the already computed
    if (dp[n][sum] != -1):
        return dp[n][sum] % mod

    # Place the digit X at the
    # current position
    option1 = countNumbers(n - 1, x,
                      y, sum + x) % mod

    # Place the digit Y at the
    # current position
    option2 = countNumbers(n - 1, x,
                      y, sum + y) % mod

    # Update current state result
    dp[n][sum] = (option1 + option2) % mod

    return dp[n][sum]

# Driver Code
if __name__ == "__main__":

    N = 3
    X = 1
    Y = 5

    # Function Call
    print(countNumbers(N, X, Y, 0) % mod)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the value of overlapping
// states
static int [,]dp = new int[100 + 5, 900 + 5];
static int mod = 10000007;

// Function to find the count of
// numbers that are formed by digits
// X and Y and whose sum of digit
// also have digit X or Y
public static int countNumbers(int n, int x,
                               int y, int sum)
{

    // Initialize dp array
    for(int i = 0; i < dp.GetLength(0); i++)
    {
        for(int j = 0; j < dp.GetLength(1); j++)
        {
            dp[i, j] = -1;
        }
    }

    // Base Case
    if (n == 0)
    {

        // Check if sum of digits
        // formed by only X or Y
        return check(sum, x, y);
    }

    // Return the already computed
    if (dp[n, sum] != -1)
    {
        return dp[n, sum] % mod;
    }

    // Place the digit X at the
    // current position
    int option1 = countNumbers(n - 1, x, y,
                             sum + x) % mod;

    // Place the digit Y at the
    // current position
    int option2 = countNumbers(n - 1, x, y,
                             sum + y) % mod;

    // Update current state result
    return dp[n,sum] = (option1 + option2) % mod;
}

// Function to check whether a number
// have only digits X or Y or not
public static int check(int sum, int x, int y)
{

    // Until sum is positive
    while (sum > 0)
    {
        int ln = sum % 10;

        // If any digit is not
        // X or Y then return 0
        if (ln != x && ln != y)
        {
            return 0;
        }
        sum /= 10;
    }

    // Return 1
    return 1;
}

// Driver Code
public static void Main(String []args)
{
    int N = 3, X = 1, Y = 5;

    // Function Call
    Console.WriteLine(countNumbers(
        N, X, Y, 0) % mod);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the value of overlapping
// states
let dp = [];
for(let i = 0;i<1005;i++){
   dp[i] = [];
   for(let j = 0;j<9005;j++){
        dp[i][j] = 0;
   }
}
let mod = 1000000007;

// Function to check whether a number
// have only digits X or Y or not
function check( sum,  x, y)
{
    // Until sum is positive
    while (sum > 0) {

        let ln = sum % 10;

        // If any digit is not
        // X or Y then return 0
        if (ln != x && ln != y) {
            return 0;
        }
        sum = Math.floor(sum/10);
    }

    // Return 1
    return 1;
}

// Function to find the count of
// numbers that are formed by digits
// X and Y and whose sum of digit
// also have digit X or Y
function countNumbers(n, x, y, sum)
{
    // Initialize dp array
    for(let i = 0;i<1005;i++){
   for(let j = 0;j<9005;j++){
        dp[i][j] = -1;
   }
}
    // Base Case
    if (n == 0) {

        // Check if sum of digits
        // formed by only X or Y
        return check(sum, x, y);
    }

    // Return the already computed
    if (dp[n][sum] != -1) {
        return dp[n][sum] % mod;
    }

    // Place the digit X at the
    // current position
    let option1 = countNumbers(n - 1, x,
                               y, sum + x) % mod;

    // Place the digit Y at the
    // current position
    let option2 = countNumbers(n - 1, x,
                               y, sum + y) % mod;

    // Update current state result
    return dp[n][sum] = (option1 + option2) % mod;
}

// Driver Code
let N = 3, X = 1, Y = 5;

    // Function Call
    document.write(countNumbers(N, X, Y, 0) % mod);

</script>
```

**Output**

```
4
```

**时间复杂度:**(N *和)
**辅助空间:**O(N *和)