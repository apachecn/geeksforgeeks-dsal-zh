# 给定数目的素因子的数组元素之和

> 原文:[https://www . geesforgeks . org/给定数字的素因子数组元素之和/](https://www.geeksforgeeks.org/sum-of-array-elements-which-are-prime-factors-of-a-given-number/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是找到所有数组元素的[和，它们是 **K** 的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

**示例:**

> **输入:** arr[] = {1，2，3，5，6，7，15}，K = 35
> **输出:** 12
> **解释:**从给定数组来看，5 和 7 是 35 的素因子。因此，所需总和= 5 + 7 = 12。
> 
> **输入:** arr[] = {1，3，5，7}，K = 42
> **输出:** 10
> **解释:**从给定数组来看，3 和 7 是 42 的素因子。因此，要求总和= 3 + 7 = 10。

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，检查是否是 **K** 的[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。将条件满足的那些元素加到总和中。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储需要的和。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，执行以下操作:
    *   检查[数组元素是否是**K**T3 的质因数。](https://www.geeksforgeeks.org/prime-factor/)
    *   如果发现为真，则将当前元素添加到**和**中。
*   完成数组遍历后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Above condition allows to check only
    // for every 6th number, starting from 5
    for (int i = 5; i * i <= n; i = i + 6)

        // If n is a multiple of i and i + 2
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to find the sum of array
// elements which are prime factors of K
void primeFactorSum(int arr[], int n, int k)
{

    // Stores the required sum
    int sum = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If current element is a prime
        // factor of k, add it to the sum
        if (k % arr[i] == 0 && isPrime(arr[i])) {
            sum = sum + arr[i];
        }
    }

    // Print the result
    cout << sum;
}

// Driver Code
int main()
{

    // Given arr[]
    int arr[] = { 1, 2, 3, 5, 6, 7, 15 };

    // Store the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 35;

    primeFactorSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

    // Function to check if a
    // number is prime or not
    static boolean isPrime(int n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check if n is a
        // multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Above condition allows to check only
        // for every 6th number, starting from 5
        for (int i = 5; i * i <= n; i = i + 6)

            // If n is a multiple of i and i + 2
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to find the sum of array
    // elements which are prime factors of K
    static void primeFactorSum(int arr[], int n, int k)
    {

        // Stores the required sum
        int sum = 0;

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If current element is a prime
            // factor of k, add it to the sum
            if (k % arr[i] == 0 && isPrime(arr[i]))
            {
                sum = sum + arr[i];
            }
        }

        // Print the result
        System.out.println(sum);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given arr[]
        int arr[] = { 1, 2, 3, 5, 6, 7, 15 };

        // Store the size of the array
        int N = arr.length;
        int K = 35;
        primeFactorSum(arr, N, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a
# number is prime or not
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check if n is a
    # multiple of 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Above condition allows to check only
    # for every 6th number, starting from 5
    i = 5

    while (i * i <= n ):

        # If n is a multiple of i and i + 2
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i = i + 6

    return True

# Function to find the sum of array
# elements which are prime factors of K
def primeFactorSum(arr, n, k):

    # Stores the required sum
    sum = 0

    # Traverse the given array
    for i in range(n):

        # If current element is a prime
        # factor of k, add it to the sum
        if (k % arr[i] == 0 and isPrime(arr[i])):
            sum = sum + arr[i]

    # Print the result
    print(sum)

# Driver Code

# Given arr[]
arr = [ 1, 2, 3, 5, 6, 7, 15 ]

# Store the size of the array
N = len(arr)

K = 35

primeFactorSum(arr, N, K)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to check if a
    // number is prime or not
    static bool isPrime(int n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check if n is a
        // multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        // Above condition allows to check only
        // for every 6th number, starting from 5
        for (int i = 5; i * i <= n; i = i + 6)

            // If n is a multiple of i and i + 2
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to find the sum of array
    // elements which are prime factors of K
    static void primeFactorSum(int []arr, int n, int k)
    {

        // Stores the required sum
        int sum = 0;

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If current element is a prime
            // factor of k, add it to the sum
            if (k % arr[i] == 0 && isPrime(arr[i]))
            {
                sum = sum + arr[i];
            }
        }

        // Print the result
        Console.Write(sum);
    }

    // Driver code
    public static void Main(string[] args)
    {

        // Given arr[]
        int []arr = { 1, 2, 3, 5, 6, 7, 15 };

        // Store the size of the array
        int N = arr.Length;
        int K = 35;
        primeFactorSum(arr, N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if a
// number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if n is a
    // multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    var i;
    // Above condition allows to check only
    // for every 6th number, starting from 5
    for (i = 5; i * i <= n; i = i + 6)

        // If n is a multiple of i and i + 2
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to find the sum of array
// elements which are prime factors of K
function primeFactorSum(arr, n, k)
{

    // Stores the required sum
    var sum = 0;
    var i;
    // Traverse the given array
    for (i = 0; i < n; i++) {

        // If current element is a prime
        // factor of k, add it to the sum
        if (k % arr[i] == 0 && isPrime(arr[i])) {
            sum = sum + arr[i];
        }
    }

    // Print the result
    document.write(sum);
}

// Driver Code
    // Given arr[]
    var arr = [1, 2, 3, 5, 6, 7, 15]

    // Store the size of the array
    var N = arr.length;

    var K = 35;

    primeFactorSum(arr, N, K);

</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N*√X)，其中 X 是数组中最大的* [*元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
***辅助空间:** O(1)*