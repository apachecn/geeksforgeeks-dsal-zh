# 计算位数总和等于素数的 N 位数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-具有等于素数的位数总和/](https://www.geeksforgeeks.org/count-n-digit-numbers-having-sum-of-digits-equal-to-a-prime-number/)

给定一个正整数 **N** ，任务是统计 **N** 位数，其[位数之和](https://www.geeksforgeeks.org/how-can-we-sum-the-digits-of-a-given-number-in-single-statement/)是一个 [**素数**](https://www.geeksforgeeks.org/tag/prime-number/) 。

**示例:**

> **输入:** N = 1
> **输出:** 4
> **说明:**【2，3，5，7】为一位数，位数之和等于一个素数。
> 
> **输入:**N = 2
> T3】输出: 33

**天真方法:**解决给定问题的最简单方法是**生成所有可能的 N 位数**并计算那些数字的**和为质数**的数字。检查所有数字后，打印**计数的值**作为数字的总计数。

***时间复杂度:** O(N *10 <sup>N</sup> )*

**高效方法:**上述方法也可以通过使用 [**递归动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 进行优化，因为上述问题有 [**重叠子问题**](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/) **和一个** [**最优子结构**](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/) 。按照以下步骤解决问题:

*   初始化一个全局 **2D** 数组 **dp[N+1][N*10]** ，所有值为 **-1** ，存储每个[递归调用](https://www.geeksforgeeks.org/recursion/)的结果。
*   使用厄拉多塞的[筛计算素数至 **(N * 10)** 数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   定义一个递归函数，通过执行以下步骤，说出 **countOfNumbers(index，sum，N)** 。
    *   如果指数值为 **N+1** ，
        *   如果总和是一个**质数**，返回 **1** 作为一个已经形成的有效 **N** 位数。
        *   否则返回 **0** 。
    *   如果已经计算出状态**DP[指数][总和]** 的结果，则返回该值**DP[指数][总和]。**
    *   如果当前索引为 **1** ，则可以放置**【1-9】**中的任意一个数字，否则可以放置**【0-9】**。
    *   对数字进行有效放置后，[**递归地**](https://www.geeksforgeeks.org/recursion/) 调用 **countOfNumbers** 函数进行**下一个索引，**并将所有递归的待定结果汇总到变量 **val** 中。
    *   将**值**的值存储到 **dp【指数】【总和】**表的当前状态。
    *   将这个状态的结果值返回给它的父递归调用。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Stores the dp states
int dp[100][1000];

// Check if a number is
// a prime or not
bool prime[1005];

// Function to generate all prime numbers
// that are less than or equal to n
void SieveOfEratosthenes(int n)
{
    // Base cases.
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples
            // of as non-prime
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the count of N-digit numbers
// such that the sum of digits is a prime number
int countOfNumbers(int index, int sum, int N)
{

    // If end of array is reached
    if (index == N + 1) {

        // If the sum is equal to a prime number
        if (prime[sum] == true) {
            return 1;
        }

        // Otherwise
        return 0;
    }

    int& val = dp[index][sum];

    // If the dp-states are already computed
    if (val != -1) {

        return val;
    }

    val = 0;

    // If index = 1, any digit from [1 - 9] can be placed.
    // If N = 1, 0 also can be placed.
    if (index == 1) {

        for (int digit = (N == 1 ? 0 : 1); digit <= 9;
             ++digit) {
            val += countOfNumbers(index + 1, sum + digit,
                                  N);
        }
    }

    // Otherwise, any digit from [0 - 9] can be placed.
    else {
        for (int digit = 0; digit <= 9; ++digit) {
            val += countOfNumbers(index + 1, sum + digit,
                                  N);
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
int main()
{
    // Initializing dp array with -1
    memset(dp, -1, sizeof dp);

    // Initializing prime array to true
    memset(prime, true, sizeof(prime));

    // Find all primes less than or equal to 1000,
    // which is sufficient for N upto 100
    SieveOfEratosthenes(1000);

    // Given Input
    int N = 6;

    // Function call
    cout << countOfNumbers(1, 0, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

class GFG{

// Stores the dp states
public static int[][] dp = new int[100][1000];

// Check if a number is
// a prime or not
public static boolean[] prime = new boolean[1005];

// Function to generate all prime numbers
// that are less than or equal to n
public static void SieveOfEratosthenes(int n)
{

    // Base cases.
    prime[0] = prime[1] = false;
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples
            // of as non-prime
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the count of N-digit numbers
// such that the sum of digits is a prime number
public static int countOfNumbers(int index, int sum,
                                 int N)
{

    // If end of array is reached
    if (index == N + 1)
    {

        // If the sum is equal to a prime number
        if (prime[sum] == true)
        {
            return 1;
        }

        // Otherwise
        return 0;
    }

    int val = dp[index][sum];

    // If the dp-states are already computed
    if (val != -1)
    {
        return val;
    }

    val = 0;

    // If index = 1, any digit from [1 - 9] can be placed.
    // If N = 1, 0 also can be placed.
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Otherwise, any digit from [0 - 9] can be placed.
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
public static void main(String args[])
{

    // Initializing dp array with -1
    for(int[] row : dp)
        Arrays.fill(row, -1);

    // Initializing prime array to true
    Arrays.fill(prime, true);

    // Find all primes less than or equal to 1000,
    // which is sufficient for N upto 100
    SieveOfEratosthenes(1000);

    // Given Input
    int N = 6;

    // Function call
    System.out.println(countOfNumbers(1, 0, N));
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the dp states
dp = [[-1]*100]*1000

# Check if a number is
# a prime or not
prime = [True] * 1005

# Function to generate all prime numbers
# that are less than or equal to n
def SieveOfEratosthenes(n) :

    # Base cases.
    prime[0] = prime[1] = False
    p = 2
    while(p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples
            # of as non-prime
            for i in range(p * p, n+1, p) :
                prime[i] = False

        p += 1

# Function to find the count of N-digit numbers
# such that the sum of digits is a prime number
def countOfNumbers(index, sum, N) :

    # If end of array is reached
    if (index == N + 1) :

        # If the sum is equal to a prime number
        if (prime[sum] == True) :
            return 1

        # Otherwise
        return 0

    val = dp[index][sum]

    # If the dp-states are already computed
    if (val != -1) :

        return val

    val = 0

    # If index = 1, any digit from [1 - 9] can be placed.
    # If N = 1, 0 also can be placed.
    if (index == 1) :

        for digit in range(((0, 1) [N == 1])+1, 10, 1) :
            val += countOfNumbers(index + 1, sum + digit, N)

    # Otherwise, any digit from [0 - 9] can be placed.
    else :
        for digit in range(0, 10, 1) :
            val += countOfNumbers(index + 1, sum + digit, N)

    # Return the answer.
    return val

# Driver Code

# Find all primes less than or equal to 1000,
# which is sufficient for N upto 100
SieveOfEratosthenes(1000)

# Given Input
N = 6

# Function call
print(countOfNumbers(1, 0, N))

# This code is contributed by avijitmondal1998.
```

## C#

```
using System;

public class GFG{

// Stores the dp states
public static int[,] dp = new int[100,1000];

// Check if a number is
// a prime or not
public static bool[] prime = new bool[1005];

// Function to generate all prime numbers
// that are less than or equal to n
public static void SieveOfEratosthenes(int n)
{

    // Base cases.
    prime[0] = prime[1] = false;
    for(int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples
            // of as non-prime
            for(int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the count of N-digit numbers
// such that the sum of digits is a prime number
public static int countOfNumbers(int index, int sum,
                                 int N)
{

    // If end of array is reached
    if (index == N + 1)
    {

        // If the sum is equal to a prime number
        if (prime[sum] == true)
        {
            return 1;
        }

        // Otherwise
        return 0;
    }

    int val = dp[index,sum];

    // If the dp-states are already computed
    if (val != -1)
    {
        return val;
    }

    val = 0;

    // If index = 1, any digit from [1 - 9] can be placed.
    // If N = 1, 0 also can be placed.
    if (index == 1)
    {
        for(int digit = (N == 1 ? 0 : 1);
                digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Otherwise, any digit from [0 - 9] can be placed.
    else
    {
        for(int digit = 0; digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Return the answer.
    return val;
}

// Driver Code
public static void Main(String []args)
{

    // Initializing dp array with -1
    for(int i = 0; i < 100; i++)
    {
        for (int j = 0; j < 1000; j++) {
            dp[i,j] = -1;
        }
    }

    // Initializing prime array to true
    for (int i = 0; i < prime.Length; i++)
        prime[i] = true;

    // Find all primes less than or equal to 1000,
    // which is sufficient for N upto 100
    SieveOfEratosthenes(1000);

    // Given Input
    int N = 6;

    // Function call
    Console.WriteLine(countOfNumbers(1, 0, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Stores the dp states
let dp = new Array(100).fill(0).map(() =>
         new Array(1000).fill(-1));

// Check if a number is
// a prime or not
let prime = new Array(1005).fill(true);

// Function to generate all prime numbers
// that are less than or equal to n
function SieveOfEratosthenes(n)
{

    // Base cases.
    prime[0] = prime[1] = false;

    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples
            // of as non-prime
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the count of N-digit numbers
// such that the sum of digits is a prime number
function countOfNumbers(index, sum, N)
{

    // If end of array is reached
    if (index == N + 1)
    {

        // If the sum is equal to a prime number
        if (prime[sum] == true)
        {
            return 1;
        }

        // Otherwise
        return 0;
    }

    let val = dp[index][sum];

    // If the dp-states are already computed
    if (val != -1)
    {
        return val;
    }

    val = 0;

    // If index = 1, any digit from [1 - 9] can
    // be placed. If N = 1, 0 also can be placed.
    if (index == 1)
    {
        for(let digit = N == 1 ? 0 : 1;
                digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Otherwise, any digit from [0 - 9]
    // can be placed.
    else
    {
        for(let digit = 0; digit <= 9; ++digit)
        {
            val += countOfNumbers(index + 1,
                                    sum + digit, N);
        }
    }

    // Return the answer.
    return val;
}

// Driver Code

// Find all primes less than or equal to 1000,
// which is sufficient for N upto 100
SieveOfEratosthenes(1000);

// Given Input
let N = 6;

// Function call
document.write(countOfNumbers(1, 0, N));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
222638
```

***时间复杂度:**O(N<sup>2</sup>* 10)*
***辅助空间:** O(N <sup>2</sup> )*