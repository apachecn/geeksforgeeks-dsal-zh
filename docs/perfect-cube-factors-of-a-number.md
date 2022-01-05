# 一个数的完美立方因子

> 原文:[https://www . geeksforgeeks . org/perfect-cube-factors-of-a-number/](https://www.geeksforgeeks.org/perfect-cube-factors-of-a-number/)

给定一个整数 **N，**的任务是找到 **N** 的因子数，它们是一个完美的立方体。

**示例:**

> **输入:** N = 27
> **输出:** 2
> **说明:**
> 27(1，27)有 2 个因子是完美立方体
> 
> **输入:** N = 216
> **输出:** 4
> **说明:**
> 216(1，8，27，216)有 4 个因子是完美立方体

**天真的方法:**天真的想法是[找到给定数**N**T5】的所有可能因子，并计算每个](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)[因子是否为完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。如果是，那么计算这个因素，并检查下一个因素。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**思路是利用数学观察找到一个公式，计算出一个完美立方体的因子个数。一个数的因子数由下式给出:

> N =(1+a<sub>1</sub>)*(1+a<sub>2</sub>)*(1+a<sub>3</sub>)因素*..*(1 + a <sub>n</sub> )
> 其中 a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ，..，a <sub>n</sub> 是 n
> 的不同素因子的计数

在一个完美的立方体中，不同质因数的计数必须能被 3 整除。因此，完美立方体的因子数由下式给出:

> 正方体的 N 的因子=(1+a<sub>1</sub>/3)*(1+a<sub>2</sub>/3)*……*(1+a<sub>N</sub>/3)
> 其中 a <sub>1</sub> ，a <sub>2</sub> ，a <sub>3</sub> ，..，a <sub>n</sub> 是 n
> 的不同素因子的计数

插图:

> N = 216 的因子是 2，2，2，3，3，3。
> 因此，完美立方的因子数为(1 + 3/3) * (1 + 3/3) = 4。因子是 1、8、27 和 216。

因此，找到质因数的计数，并应用上述公式找到完美立方体的因数计数。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the count
// of factors that are perfect cube
int noOfFactors(int N)
{
    if (N == 1)
        return 1;

    // To store the count of number
    // of times a prime number
    // divides N.
    int count = 0;

    // To store the number of factors
    // that are perfect cube
    int ans = 1;

    // Count number of 2's that divides N
    while (N % 2 == 0) {
        count++;
        N = N / 2;
    }

    // Calculate ans according
    // to above formula
    ans *= (count / 3 + 1);

    // Check for all the possible
    // numbers that can divide it
    for (int i = 3; i * i <= N; i = i + 2) {
        count = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (N % i == 0) {
            count++;
            N = N / i;
        }

        // Calculate ans according
        // to above formula
        ans *= (count / 3 + 1);
    }

    // Return final count
    return ans;
}

// Driver Code
int main()
{
    // Given number
    int N = 216;

    // Function Call
    cout << noOfFactors(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that returns the count
// of factors that are perfect cube
static int noOfFactors(int N)
{
    if (N == 1)
        return 1;

    // To store the count of number
    // of times a prime number
    // divides N.
    int count = 0;

    // To store the number of factors
    // that are perfect cube
    int ans = 1;

    // Count number of 2's that divides N
    while (N % 2 == 0)
    {
        count++;
        N = N / 2;
    }

    // Calculate ans according
    // to above formula
    ans *= (count / 3 + 1);

    // Check for all the possible
    // numbers that can divide it
    for(int i = 3; i * i <= N; i = i + 2)
    {
        count = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (N % i == 0)
        {
            count++;
            N = N / i;
        }

        // Calculate ans according
        // to above formula
        ans *= (count / 3 + 1);
    }

    // Return final count
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    int N = 216;

    // Function call
    System.out.print(noOfFactors(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that returns the count
# of factors that are perfect cube
def noofFactors(N):

    if N == 1:
        return 1

    # To store the count of number
    # of times a prime number
    # divides N
    count = 0

    # To store the count of factors that
    # are perfect cube
    ans = 1

    # Count number of 2's that divides N
    while(N % 2 == 0):
        count += 1
        N //= 2

    # Calculate ans according
    # to above formula
    ans *= ((count // 3) + 1)

    # Check for all possible
    # numbers that can divide it
    i = 3
    while((i * i) <= N):
        count = 0

        # Loop to check the number
        # of times prime number
        # i divides it
        while(N % i == 0):
            count += 1
            N //= i

        # Calculate ans according
        # to above formula
        ans *= ((count // 3) + 1)
        i += 2

    return ans

# Driver Code

# Given number
N = 216

# Function call
print(noofFactors(N))

# This code is contributed by VirusBuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that returns the count
// of factors that are perfect cube
static int noOfFactors(int N)
{
    if (N == 1)
        return 1;

    // To store the count of number
    // of times a prime number
    // divides N.
    int count = 0;

    // To store the number of factors
    // that are perfect cube
    int ans = 1;

    // Count number of 2's that divides N
    while (N % 2 == 0)
    {
        count++;
        N = N / 2;
    }

    // Calculate ans according
    // to above formula
    ans *= (count / 3 + 1);

    // Check for all the possible
    // numbers that can divide it
    for(int i = 3; i * i <= N; i = i + 2)
    {
        count = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (N % i == 0)
        {
            count++;
            N = N / i;
        }

        // Calculate ans according
        // to above formula
        ans *= (count / 3 + 1);
    }

    // Return final count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    int N = 216;

    // Function call
    Console.Write(noOfFactors(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that returns the count
// of factors that are perfect cube
function noOfFactors(N)
{
    if (N == 1)
        return 1;

    // To store the count of number
    // of times a prime number
    // divides N.
    let count = 0;

    // To store the number of factors
    // that are perfect cube
    let ans = 1;

    // Count number of 2's that divides N
    while (N % 2 == 0) {
        count++;
        N = parseInt(N / 2);
    }

    // Calculate ans according
    // to above formula
    ans *= (parseInt(count / 3) + 1);

    // Check for all the possible
    // numbers that can divide it
    for (let i = 3; i * i <= N; i = i + 2) {
        count = 0;

        // Loop to check the number
        // of times prime number
        // i divides it
        while (N % i == 0) {
            count++;
            N = parseInt(N / i);
        }

        // Calculate ans according
        // to above formula
        ans *= (parseInt(count / 3) + 1);
    }

    // Return final count
    return ans;
}

// Driver Code
// Given number
let N = 216;

// Function Call
document.write(noOfFactors(N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*