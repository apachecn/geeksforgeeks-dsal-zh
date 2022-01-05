# 两个不同素数乘积的前 N 个自然数的逐位异或

> 原文:[https://www . geeksforgeeks . org/两个不同素数乘积的第一个 n 个自然数的按位异或/](https://www.geeksforgeeks.org/bitwise-xor-of-first-n-natural-numbers-that-are-product-of-two-distinct-prime-numbers/)

给定一个正整数 **N** ，任务是计算第一个 **N** 数的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，这是两个截然不同的质数的[乘积。](https://www.geeksforgeeks.org/numbers-less-than-n-which-are-product-of-exactly-two-distinct-prime-numbers/)

**示例:**

> ***输入:** N = 20*
> ***输出:** 7*
> ***解释:*** 范围[1，20]中正好是两个不同素数乘积的数是{6，10，12，14，15，18，20}。
> *这些数字的按位异或= 6 ^ 10 ^ 12 ^ 14 ^ 15 ^ 18 ^ 20 = 7*
> 
> ***输入:*** *N = 50*
> ***输出:*** *26*

**天真法:**最简单的方法是[迭代每个数直到**N**T5](https://www.geeksforgeeks.org/range-based-loop-c/)[使用质因数分解法](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)找到每个数的质因数。发现不同质因数的计数为 2 的数字，然后计算它们与答案的异或。核对所有数字后，打印得到的答案。

***时间复杂度:** O(N*√N)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是稍加修改使用厄拉多塞的[筛。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   将变量**和**初始化为 **0** ，以存储所需的结果。
*   创建一个大小为 **N+1** 的整数[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，并用全零初始化，其中 **arr[i]** 表示 **i** 的不同素数的个数。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**中迭代，如果 **arr[i]** 的值为 **0** ，则使用变量 **j** 遍历 **i** 的所有倍数，并将 **arr[j]** 的值增加 **1** ，因为 **i** 是【T29】的质因数
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**内迭代，如果**arr【I】**等于 **2** ，则取 **i** 与 **ans** 的**异或**。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count prime factors
// using Sieve of Eratosthenes
void sieve(int arr[], int n)
{
    // Iterate in the [2, N]
    for (int i = 2; i <= n; i++) {

        // If the current number is prime
        if (arr[i] == 0)

            // Iterate over all multiples of i
            for (int j = 2 * i; j <= n; j += i) {

                // Increment arr[j] by 1 since
                // i is a prime factor of j
                arr[j]++;
            }
    }
}

// Function to find Bitwise XOR
// of first N natural numbers
// satisfying the given condition
void findXOR(int n)
{
    // arr[i]: Stores the number of
    // distinct prime factors of i
    int arr[n + 1] = { 0 };

    // Initialize the base cases
    arr[0] = arr[1] = 1;

    // Function Call to fill
    // the array, arr[]
    sieve(arr, n);

    // Store the required result
    int ans = 0;

    // Iterate over the range [2, N]
    for (int i = 2; i <= n; i++) {

        // Check if the i-th number has
        // exactly two distinct prime factor
        if (arr[i] == 2) {

            // If true, update the answer
            ans = (ans ^ i);
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given Input
    int n = 20;

    // Function Call
    findXOR(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to count prime factors
    // using Sieve of Eratosthenes
    static void sieve(int arr[], int n)
    {
        // Iterate in the [2, N]
        for (int i = 2; i <= n; i++) {

            // If the current number is prime
            if (arr[i] == 0)

                // Iterate over all multiples of i
                for (int j = 2 * i; j <= n; j += i) {

                    // Increment arr[j] by 1 since
                    // i is a prime factor of j
                    arr[j]++;
                }
        }
    }

    // Function to find Bitwise XOR
    // of first N natural numbers
    // satisfying the given condition
    static void findXOR(int n)
    {

        // arr[i]: Stores the number of
        // distinct prime factors of i
        int arr[] = new int[n + 1];

        // Initialize the base cases
        arr[0] = arr[1] = 1;

        // Function Call to fill
        // the array, arr[]
        sieve(arr, n);

        // Store the required result
        int ans = 0;

        // Iterate over the range [2, N]
        for (int i = 2; i <= n; i++) {

            // Check if the i-th number has
            // exactly two distinct prime factor
            if (arr[i] == 2) {

                // If true, update the answer
                ans = (ans ^ i);
            }
        }

        // Print the result
        System.out.println(ans);
    }

    // Driver code
    public static void main(String[] args)
    {
      // Given Input
        int n = 20;

        // Function Call
        findXOR(n);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count prime factors
# using Sieve of Eratosthenes
def sieve(arr, n):

    # Iterate in the [2, N]
    for i in range(2, n + 1, 1):

        # If the current number is prime
        if (arr[i] == 0):

            # Iterate over all multiples of i
            for j in range(2 * i, n + 1, i):

                # Increment arr[j] by 1 since
                # i is a prime factor of j
                arr[j] += 1

# Function to find Bitwise XOR
# of first N natural numbers
# satisfying the given condition
def findXOR(n):

    # arr[i]: Stores the number of
    # distinct prime factors of i
    arr = [0 for i in range(n + 1)]

    # Initialize the base cases
    arr[0] = arr[1] = 1

    # Function Call to fill
    # the array, arr[]
    sieve(arr, n)

    # Store the required result
    ans = 0

    # Iterate over the range [2, N]
    for i in range(2, n + 1, 1):

        # Check if the i-th number has
        # exactly two distinct prime factor
        if (arr[i] == 2):

            # If true, update the answer
            ans = (ans ^ i)

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 20

    # Function Call
    findXOR(n)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count prime factors
// using Sieve of Eratosthenes
static void sieve(int []arr, int n)
{

    // Iterate in the [2, N]
    for(int i = 2; i <= n; i++)
    {

        // If the current number is prime
        if (arr[i] == 0)

            // Iterate over all multiples of i
            for(int j = 2 * i; j <= n; j += i)
            {

                // Increment arr[j] by 1 since
                // i is a prime factor of j
                arr[j]++;
            }
    }
}

// Function to find Bitwise XOR
// of first N natural numbers
// satisfying the given condition
static void findXOR(int n)
{

    // arr[i]: Stores the number of
    // distinct prime factors of i
    int []arr = new int[n + 1];

    // Initialize the base cases
    arr[0] = arr[1] = 1;

    // Function Call to fill
    // the array, arr[]
    sieve(arr, n);

    // Store the required result
    int ans = 0;

    // Iterate over the range [2, N]
    for(int i = 2; i <= n; i++)
    {

        // Check if the i-th number has
        // exactly two distinct prime factor
        if (arr[i] == 2)
        {

            // If true, update the answer
            ans = (ans ^ i);
        }
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver code
public static void Main(String[] args)
{

    // Given Input
    int n = 20;

    // Function Call
    findXOR(n);
}
}

// This code is contributed by ankThon
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count prime factors
// using Sieve of Eratosthenes
function  sieve( arr, n)
{
    // Iterate in the [2, N]
    for (var i = 2; i <= n; i++) {

        // If the current number is prime
        if (arr[i] == 0)

            // Iterate over all multiples of i
            for (var j = 2 * i; j <= n; j += i) {

                // Increment arr[j] by 1 since
                // i is a prime factor of j
                arr[j]++;
            }
    }
}

// Function to find Bitwise XOR
// of first N natural numbers
// satisfying the given condition
function findXOR( n)
{
    // arr[i]: Stores the number of
    // distinct prime factors of i
    var arr = new Array(n + 1);
    arr.fill(0);

    // Initialize the base cases
    arr[0] = arr[1] = 1;

    // Function Call to fill
    // the array, arr[]
    sieve(arr, n);

    // Store the required result
    var ans = 0;

    // Iterate over the range [2, N]
    for (var i = 2; i <= n; i++) {

        // Check if the i-th number has
        // exactly two distinct prime factor
        if (arr[i] == 2) {

            // If true, update the answer
            ans = (ans ^ i);
        }
    }

    // Print the result
    document.write( ans);
}

n = 20;

// Function Call
findXOR(n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N * log(logN))*
***辅助空间:** O(N)*