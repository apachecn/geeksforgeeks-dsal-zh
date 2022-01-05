# 计数数字乘积为复合数的数组元素

> 原文:[https://www . geesforgeks . org/count-array-elements-其数字乘积是一个复合数/](https://www.geeksforgeeks.org/count-array-elements-whose-product-of-digits-is-a-composite-number/)

给定一个由 **N** 个非负整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算数组元素的数量，这些元素的[个数字的乘积](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)是一个[复合数](https://www.geeksforgeeks.org/composite-number/)。

**示例:**

> **输入:** arr[] = {13，55，7，13，11，71，233，144，89}
> **输出:** 4
> **说明:**位数乘积等于复合数的数组元素为 55 (5 * 5 = 25)、233 (2 * 3 * 3 = 18)、144 (1 * 4 * 4 = 16)、89 ( = 8 * 9 = 72)
> 
> **输入:** arr[] = {34，13，55，11，8，3，55，23}
> **输出:** 3
> **说明:**位数乘积等于一个复合数的数组元素是 34 ( = 3 * 4 = 12)、55 ( 5 * 5 = 25)、23 ( = 2 * 3 = 6)

**方法:**按照以下步骤解决问题:

*   使用厄拉多塞的[筛预计算并存储所有质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   创建一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储[所有不同的数组元素](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)，它们的[数字乘积](https://www.geeksforgeeks.org/program-to-calculate-product-of-digits-of-a-number/)是一个[复合数字](https://www.geeksforgeeks.org/composite-number/)。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，[检查其所有数字的乘积是否为素数。](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)如果发现为真，将当前元素添加到[设置](https://www.geeksforgeeks.org/hashset-in-java/)中。
*   否则，继续下一个数组元素。
*   遍历完毕后，打印设置的[尺寸作为所需答案。](https://www.geeksforgeeks.org/setsize-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <set>
using namespace std;

#define N 100005

// Function to generate prime numbers
// using Sieve of Eratosthenes
void SieveOfEratosthenes(bool prime[],
                         int p_size)
{
    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {
        // If p is a prime
        if (prime[p]) {

            // Set all multiples of p as non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to calculate the product
// of digits of the given number
long long int digitProduct(int number)
{
    // Stores the product of digits
    long long int res = 1;
    while (number > 0) {

        // Extract digits and
        // add to the sum
        res *= (number % 10);
        number /= 10;
    }

    // Return the product
    // of its digits
    return res;
}

// Function to print number of distinct
// values with digit product as composite
void DistinctCompositeDigitProduct(int arr[],
                                   int n)
{
    // Initialize set
    set<int> output;

    // Initialize boolean array
    bool prime[N + 1];
    memset(prime, true, sizeof(prime));

    // Pre-compute primes
    SieveOfEratosthenes(prime, N);

    // Traverse array
    for (int i = 0; i < n; i++) {

        // Stores the product of digits
        // of the current array element
        long long int ans
            = digitProduct(arr[i]);

        // If Product of digits is
        // less than or equal to 1
        if (ans <= 1) {
            continue;
        }

        // If Product of digits is
        // not a prime
        if (!prime[ans]) {
            output.insert(ans);
        }
    }

    // Print the answer
    cout << output.size() << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[]
        = { 13, 55, 7, 13, 11,
            71, 233, 233, 144, 89 };

    // Given size
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    DistinctCompositeDigitProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

static int N = 100005;

// Function to generate prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(boolean prime[],
                                int p_size)
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If p is a prime
        if (prime[p])
        {

            // Set all multiples of p as non-prime
            for(int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to calculate the product
// of digits of the given number
static int digitProduct(int number)
{

    // Stores the product of digits
    int res = 1;
    while (number > 0)
    {

        // Extract digits and
        // add to the sum
        res *= (number % 10);
        number /= 10;
    }

    // Return the product
    // of its digits
    return res;
}

// Function to print number of distinct
// values with digit product as composite
static void DistinctCompositeDigitProduct(int arr[],
                                          int n)
{

    // Initialize set
    TreeSet<Integer> output = new TreeSet<Integer>();

    // Initialize boolean array
    boolean prime[] = new boolean[N + 1];
    Arrays.fill(prime, true);

    // Pre-compute primes
    SieveOfEratosthenes(prime, N);

    // Traverse array
    for(int i = 0; i < n; i++)
    {

        // Stores the product of digits
        // of the current array element
        int ans = digitProduct(arr[i]);

        // If Product of digits is
        // less than or equal to 1
        if (ans <= 1)
        {
            continue;
        }

        // If Product of digits is
        // not a prime
        if (!prime[ans])
        {
            output.add(ans);
        }
    }

    // Print the answer
    System.out.print(output.size());
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 13, 55, 7, 13, 11,
                  71, 233, 233, 144, 89 };

    // Given size
    int n = arr.length;

    // Function call
    DistinctCompositeDigitProduct(arr, n);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach
N = 100005
from math import sqrt

# Function to generate prime numbers
# using Sieve of Eratosthenes
def SieveOfEratosthenes(prime, p_size):

    # Set 0 and 1 as non-prime
    prime[0] = False
    prime[1] = False
    for p in range(2, int(sqrt(p_size)), 1):

        # If p is a prime
        if (prime[p]):

            # Set all multiples of p as non-prime
            for i in range(p * 2, p_size + 1, p):
                prime[i] = False

# Function to calculate the product
# of digits of the given number
def digitProduct(number):

    # Stores the product of digits
    res = 1
    while(number > 0):

        # Extract digits and
        # add to the sum
        res *= (number % 10)
        number //= 10

    # Return the product
    # of its digits
    return res

# Function to print number of distinct
# values with digit product as composite
def DistinctCompositeDigitProduct(arr, n):

    # Initialize set
    output = set()

    # Initialize boolean array
    prime = [True for i in range(N + 1)]

    # Pre-compute primes
    SieveOfEratosthenes(prime, N)

    # Traverse array
    for i in range(n):

        # of the current array element
        ans = digitProduct(arr[i])

        # If Product of digits is
        # less than or equal to 1
        if (ans <= 1):
            continue

        # If Product of digits is
        # not a prime
        if (prime[ans] == False):
            output.add(ans)

    # Print the answer
    print(len(output))

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [13, 55, 7, 13, 11, 71, 233, 233, 144, 89]

    # Given size
    n = len(arr)

    # Function call
    DistinctCompositeDigitProduct(arr, n)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int N = 100005;

// Function to generate prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(bool[] prime,
                                int p_size)
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If p is a prime
        if (prime[p])
        {

            // Set all multiples of p as non-prime
            for(int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to calculate the product
// of digits of the given number
static int digitProduct(int number)
{

    // Stores the product of digits
    int res = 1;
    while (number > 0)
    {

        // Extract digits and
        // add to the sum
        res *= (number % 10);
        number /= 10;
    }

    // Return the product
    // of its digits
    return res;
}

// Function to print number of distinct
// values with digit product as composite
static void DistinctCompositeDigitProduct(int[] arr,
                                          int n)
{

    // Initialize set
    SortedSet<int> output = new SortedSet<int>();

    // Initialize boolean array
    bool[] prime = new bool[N + 1];
    for(int i = 0; i < N + 1; i++)
    {
        prime[i] = true;
    }

    // Pre-compute primes
    SieveOfEratosthenes(prime, N);

    // Traverse array
    for(int i = 0; i < n; i++)
    {

        // Stores the product of digits
        // of the current array element
        int ans = digitProduct(arr[i]);

        // If Product of digits is
        // less than or equal to 1
        if (ans <= 1)
        {
            continue;
        }

        // If Product of digits is
        // not a prime
        if (!prime[ans])
        {
            output.Add(ans);
        }
    }

    // Print the answer
    Console.WriteLine(output.Count);
}

// Driver Code
public static void Main()
{
    // Given array
    int[] arr = { 13, 55, 7, 13, 11,
                  71, 233, 233, 144, 89 };

    // Given size
    int n = arr.Length;

    // Function call
    DistinctCompositeDigitProduct(arr, n);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// javascript program for the above approach

var N = 100005;

// Function to generate prime numbers
// using Sieve of Eratosthenes
function SieveOfEratosthenes(prime, p_size)
{
    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    var p,i;
    for (p = 2; p * p <= p_size; p++) {
        // If p is a prime
        if (prime[p]) {

            // Set all multiples of p as non-prime
            for (i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to calculate the product
// of digits of the given number
function digitProduct(number)
{
    // Stores the product of digits
    var res = 1;
    while (number > 0) {

        // Extract digits and
        // add to the sum
        res *= (number % 10);
        number = parseInt(number/10);
    }

    // Return the product
    // of its digits
    return res;
}

// Function to print number of distinct
// values with digit product as composite
function DistinctCompositeDigitProduct(arr, n)
{
    // Initialize set
    var output = new Set();

    // Initialize boolean array
    var prime = Array(N + 1).fill(true);

    // Pre-compute primes
    SieveOfEratosthenes(prime, N);

    var i;
    // Traverse array
    for (i = 0; i < n; i++) {

        // Stores the product of digits
        // of the current array element
        var ans = digitProduct(arr[i]);

        // If Product of digits is
        // less than or equal to 1
        if (ans <= 1) {
            continue;
        }

        // If Product of digits is
        // not a prime
        if (prime[ans]==false) {
            output.add(ans);
        }
    }

    // Print the answer
    document.write(output.size);
}

// Driver Code
    // Given array
    var arr = [13, 55, 7, 13, 11,
            71, 233, 233, 144, 89];

    // Given size
    var n = arr.length;

    // Function call
    DistinctCompositeDigitProduct(arr, n);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N + MlogM)，其中 **N** 为给定数组的大小， **M** 为* [*最大数组元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*