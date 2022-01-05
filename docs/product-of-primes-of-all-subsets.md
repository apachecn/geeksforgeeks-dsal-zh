# 所有子集素数的乘积

> 原文:[https://www . geeksforgeeks . org/所有子集的素数乘积/](https://www.geeksforgeeks.org/product-of-primes-of-all-subsets/)

给定一个大小为 **N** 的数组**[]**。子集的值是该子集中[素数](https://www.geeksforgeeks.org/print-all-prime-numbers-less-than-or-equal-to-n/)的乘积。在寻找价值副产品时，非质数被认为是 1。任务是找到所有可能子集的值的**乘积**。
**举例:**

> **输入:** a[] = {3，7}
> **输出:** 20
> 子集为:{3} {7} {3，7}
> {3，7 } = 3 * 7 = 21
> { 3 } = 3
> { 7 } = 7
> 21 * 3 * 7 = 441
> **输入:** a[] = {10，2，14，3}
> **输出**

**天真法**:天真法是利用幂集找到所有子集，然后将子集的所有值相乘得到乘积。可以使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)检查灌注。
**时间复杂度** : O(2 <sup>N</sup> )
**高效方法**:一个高效的方法就是用观察来解决问题。如果我们写所有的子序列，一个共同的观察点是每个数字在一个子集中出现**2<sup>(N–1)</sup>**次，因此将导致 **2 <sup>(N-1)</sup>** 作为对产品的贡献。遍历数组，检查数组中的元素是否为[素数](https://www.geeksforgeeks.org/prime-numbers/)。如果它质数，那么它对答案的贡献是**arr【I】<sup>2(N-1)</sup>**次。
以下是上述方法的实施:

## C++

```
// C++ program to find the product of
// the multiplication of
// prime numbers in all possible subsets.
#include <bits/stdc++.h>
using namespace std;

// Sieve method to check prime or not
void sieve(int n, vector<bool>& prime)
{
    // Initially mark all primes
    for (int i = 2; i <= n; i++)
        prime[i] = true;
    prime[0] = prime[1] = false;

    // Iterate and mark all the
    // non primes as false
    for (int i = 2; i <= n; i++) {
        if (prime[i]) {
            // Multiples of prime marked as false
            for (int j = i * i; j <= n; j += i) {
                prime[j] = false;
            }
        }
    }
}

// Function to find the sum
// of sum of all the subset
int sumOfSubset(int a[], int n)
{

    // Get the maximum element
    int maxi = *max_element(a, a + n);

    // Declare a sieve array
    vector<bool> prime(maxi + 1);

    // Sieve function called
    sieve(maxi, prime);

    // Number of times an element
    // contributes to the answer
    int times = pow(2, n - 1);

    int sum = 1;

    // Iterate and check
    for (int i = 0; i < n; i++) {
        // If prime
        if (prime[a[i]])
        sum = sum * (pow(a[i], times)); // Contribution
    }

    return sum;
}

// Driver Code
int main()
{
    int a[] = { 3, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << sumOfSubset(a, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of
// the multiplication of
// prime numbers in all possible subsets.
import java.util.*;

class GFG
{

// Sieve method to check prime or not
static void sieve(int n, boolean []prime)
{
    // Initially mark all primes
    for (int i = 2; i <= n; i++)
        prime[i] = true;
    prime[0] = prime[1] = false;

    // Iterate and mark all the
    // non primes as false
    for (int i = 2; i <= n; i++)
    {
        if (prime[i])
        {
            // Multiples of prime marked as false
            for (int j = i * i; j <= n; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function to find the sum
// of sum of all the subset
static int sumOfSubset(int a[], int n)
{

    // Get the maximum element
    int maxi = Arrays.stream(a).max().getAsInt();

    // Declare a sieve array
    boolean []prime = new boolean[maxi + 1];

    // Sieve function called
    sieve(maxi, prime);

    // Number of times an element
    // contributes to the answer
    int times = (int) Math.pow(2, n - 1);

    int sum = 1;

    // Iterate and check
    for (int i = 0; i < n; i++)
    {
        // If prime
        if (prime[a[i]])
        sum = (int) (sum * (Math.pow(a[i], times)));
    }

    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 3, 7 };
    int n = a.length;
    System.out.println(sumOfSubset(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the product of
# the multiplication of
# prime numbers in all possible subsets.
prime = [True for i in range(100)]

# Sieve method to check prime or not
def sieve(n, prime):

    # Initially mark all primes
    for i in range(1, n + 1):
        prime[i] = True
    prime[0] = prime[1] = False

    # Iterate and mark all the
    # non primes as false
    for i in range(2, n + 1):
        if (prime[i]):

            # Multiples of prime marked as false
            for j in range(2 * i, n + 1, i):
                prime[j] = False

# Function to find the Sum
# of Sum of all the subset
def SumOfSubset(a, n):

    # Get the maximum element
    maxi = max(a)

    # Declare a sieve array

    # Sieve function called
    sieve(maxi, prime)

    # Number of times an element
    # contributes to the answer
    times = pow(2, n - 1)

    Sum = 1

    # Iterate and check
    for i in range(n):

        # If prime
        if (prime[a[i]]):
            Sum = Sum * (pow(a[i], times)) # Contribution

    return Sum

# Driver Code
a = [3, 7]
n = len(a)
print(SumOfSubset(a, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find the product of
// the multiplication of
// prime numbers in all possible subsets.
using System;
using System.Linq;

class GFG
{

// Sieve method to check prime or not
static void sieve(int n, Boolean []prime)
{
    // Initially mark all primes
    for (int i = 2; i <= n; i++)
        prime[i] = true;
    prime[0] = prime[1] = false;

    // Iterate and mark all the
    // non primes as false
    for (int i = 2; i <= n; i++)
    {
        if (prime[i])
        {
            // Multiples of prime marked as false
            for (int j = i * i; j <= n; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function to find the sum
// of sum of all the subset
static int sumOfSubset(int []a, int n)
{

    // Get the maximum element
    int maxi = a.Max();

    // Declare a sieve array
    Boolean []prime = new Boolean[maxi + 1];

    // Sieve function called
    sieve(maxi, prime);

    // Number of times an element
    // contributes to the answer
    int times = (int) Math.Pow(2, n - 1);

    int sum = 1;

    // Iterate and check
    for (int i = 0; i < n; i++)
    {
        // If prime
        if (prime[a[i]])
        sum = (int) (sum * (Math.Pow(a[i], times)));
    }
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 3, 7 };
    int n = a.Length;
    Console.WriteLine(sumOfSubset(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to find the product of
// the multiplication of
// prime numbers in all possible subsets.

    // Sieve method to check prime or not
    function sieve(n,  prime)
    {

        // Initially mark all primes
        for (var i = 2; i <= n; i++)
            prime[i] = true;
        prime[0] = prime[1] = false;

        // Iterate and mark all the
        // non primes as false
        for (i = 2; i <= n; i++)
        {
            if (prime[i])
            {

                // Multiples of prime marked as false
                for (j = i * i; j <= n; j += i) {
                    prime[j] = false;
                }
            }
        }
    }

    // Function to find the sum
    // of sum of all the subset
    function sumOfSubset(a , n) {

        // Get the maximum element
        var maxi = Math.max.apply(Math,a);

        // Declare a sieve array
        var prime =Array(maxi + 1).fill(0);

        // Sieve function called
        sieve(maxi, prime);

        // Number of times an element
        // contributes to the answer
        var times = parseInt( Math.pow(2, n - 1));

        var sum = 1;

        // Iterate and check
        for (i = 0; i < n; i++) {
            // If prime
            if (prime[a[i]])
                sum = parseInt( (sum * (Math.pow(a[i], times))));
        }

        return sum;
    }

    // Driver Code
        var a = [ 3, 7 ];
        var n = a.length;
        document.write(sumOfSubset(a, n));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
441
```

**时间复杂度** : O(M log M)为预先计算，其中 M 为最大元素，O(N)为迭代。
**空间复杂度** : O(M)
**注**:由于**arr【I】<sup>2(N-1)</sup>**可能真的很大，答案可能会溢出，其可取的是使用更大的数据类型和 mod 操作来保存答案。