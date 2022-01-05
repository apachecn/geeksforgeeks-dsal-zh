# 小于等于 N 的数与质因数的最大乘积

> 原文:[https://www . geesforgeks . org/number-小于等于 n-带最大质因数乘积/](https://www.geeksforgeeks.org/number-less-than-equals-to-n-with-maximum-product-of-prime-factors/)

给定一个数 **N** ，任务是找出小于或等于 **N** 的数，其质因数的[乘积最大。
**注意:**如果有多个数的最大乘积相等，则打印其中最小的数。
**举例:**](https://www.geeksforgeeks.org/product-unique-prime-factors-number/) 

> **输入:** N = 12
> **输出:** 11
> **解释:**
> N 之前所有数字的质因数乘积:
> 2 = 2
> 3 = 3
> 4 = 2
> 5 = 5
> 6 = 2 * 3 = 6
> 7 = 7
> 8 = 2
> 9 = 3
> 10 = 2 * 5 = 10
> 11
> **输入:** N = 20
> **输出:** 19

**方法:**思路是利用厄拉多塞的[筛的概念，找出 **N 个**数的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的乘积，然后找出素因子的[乘积最大的最小数。以下是步骤:](https://www.geeksforgeeks.org/product-unique-prime-factors-number/) 

1.  创建一个从 **1 到 N** 的数字列表，并用 1 初始化每个值。
2.  设 **p = 2** 这是第一个素数。从 **p** 开始迭代，以 **p** 为增量进行计数，并在列表的每个索引处乘以 **p** 。这些指标将是 p(p+1)、p(p+2)、p(p+3)等。
    **例如:**

```
If p is a prime number, then multiply with p
at every index which is multiple of p.
For p = 2,
Multiply with 2 at index 2, 4, 6, 8, 10,..., till N.
```

1.  对所有[质数](https://www.geeksforgeeks.org/prime-numbers/)重复上述步骤，直到 **N** 。
2.  找到所有质因数的乘积直到 **N** 后，遍历数字列表，找到乘积最大的最小数。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest number
// having a maximum product of prime factors
int maxPrimefactorNum(int N)
{

    // Declare the array arr[]
    int arr[N + 1];

    // Initialise array with 1
    for (int i = 0; i < N + 1; i++)
        arr[i] = 1;

    // Iterate from [2, N]
    for (int i = 2; i <= N; i++) {

        // If value at index i is 1,
        // then i is prime and make
        // update array at index for
        // all multiples of i
        if (arr[i] == 1) {
            for (int j = i; j <= N; j += i) {
                arr[j] *= i;
            }
        }
    }

    // Initialise maxValue
    int maxValue = 1;

    // Find number having maximum product
    // of prime factor <= N
    for (int i = 2; i <= N; i++) {
        if (arr[i] > maxValue) {
            maxValue = i;
        }
    }

    // Find the maximum value
    return maxValue;
}

// Driven Code
int main()
{
    // Given Number
    int N = 20;

    // Function call
    cout << maxPrimefactorNum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the smallest number
// having a maximum product of prime factors
static int maxPrimefactorNum(int N)
{

    // Declare the array arr[]
    int []arr = new int[N + 1];

    // Initialise array with 1
    for(int i = 0; i < N + 1; i++)
        arr[i] = 1;

    // Iterate from [2, N]
    for(int i = 2; i <= N; i++)
    {

        // If value at index i is 1,
        // then i is prime and make
        // update array at index for
        // all multiples of i
        if (arr[i] == 1)
        {
            for(int j = i; j <= N; j += i)
            {
                arr[j] *= i;
            }
        }
    }

    // Initialise maxValue
    int maxValue = 1;

    // Find number having maximum product
    // of prime factor <= N
    for(int i = 2; i<= N; i++)
    {
        if (arr[i] > maxValue)
        {
            maxValue = i;
        }
    }

    // Find the maximum value
    return maxValue;
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    int N = 20;

    // Function call
    System.out.print(maxPrimefactorNum(N));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest number
# having a maximum product of prime factors
def maxPrimefactorNum(N):

    # Declare the list arr
    arr = []

    # Initialise list with 1
    for i in range(N + 1):
        arr.append(1)

    # Iterate from [2, N]
    for i in range(2, N + 1):

        # If value at index i is 1,
        # then i is prime and make
        # update list at index for
        # all multiples of i
        if (arr[i] == 1) :
            for j in range(i, N + 1, i):
                arr[j] *= i

    # Initialise maxValue
    maxValue = 1

    # Find number having maximum product
    # of prime factor <= N
    for i in range(2, N + 1):
        if (arr[i] > maxValue):
            maxValue = i

    # Find the maximum value
    return maxValue

# Driver Code

# Given number
N = 20;

# Function call
print(maxPrimefactorNum(N))

# This code is contributed by yatinagg
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the smallest number
// having a maximum product of prime factors
static int maxPrimefactorNum(int N)
{

    // Declare the array []arr
    int []arr = new int[N + 1];

    // Initialise array with 1
    for(int i = 0; i < N + 1; i++)
        arr[i] = 1;

    // Iterate from [2, N]
    for(int i = 2; i <= N; i++)
    {

        // If value at index i is 1,
        // then i is prime and make
        // update array at index for
        // all multiples of i
        if (arr[i] == 1)
        {
            for(int j = i; j <= N; j += i)
            {
                arr[j] *= i;
            }
        }
    }

    // Initialise maxValue
    int maxValue = 1;

    // Find number having maximum product
    // of prime factor <= N
    for(int i = 2; i<= N; i++)
    {
        if (arr[i] > maxValue)
        {
            maxValue = i;
        }
    }

    // Find the maximum value
    return maxValue;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number
    int N = 20;

    // Function call
    Console.Write(maxPrimefactorNum(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the smallest number
// having a maximum product of prime factors
function maxPrimefactorNum( N)
{

    // Declare the array arr[]
    let arr=Array(N + 1).fill(1);

    // Initialise array with 1
    //for (int i = 0; i < N + 1; i++)
      //  arr[i] = 1;

    // Iterate from [2, N]
    for (let i = 2; i <= N; i++) {

        // If value at index i is 1,
        // then i is prime and make
        // update array at index for
        // all multiples of i
        if (arr[i] == 1) {
            for (let j = i; j <= N; j += i) {
                arr[j] *= i;
            }
        }
    }

    // Initialise maxValue
    let maxValue = 1;

    // Find number having maximum product
    // of prime factor <= N
    for (let i = 2; i <= N; i++) {
        if (arr[i] > maxValue) {
            maxValue = i;
        }
    }

    // Find the maximum value
    return maxValue;
}

// Driven Code

    // Given Number
    let N = 20;

    // Function call
        document.write(maxPrimefactorNum(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
19
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(N)*