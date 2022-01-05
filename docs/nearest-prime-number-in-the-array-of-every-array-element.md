# 每个数组元素数组中最接近的素数

> 原文:[https://www . geesforgeks . org/每数组元素数组中最近的素数/](https://www.geeksforgeeks.org/nearest-prime-number-in-the-array-of-every-array-element/)

给定一个由 **N** 个整数组成的整数数组 **arr[]** ，任务是为数组中的每个元素找到数组中最近的[素数](https://www.geeksforgeeks.org/prime-numbers/)。如果数组不包含任何质数，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，2，3，1，6}
> **输出:**2 2 3 3
> **解释:**
> 对于子阵{1， **2** }，最近的素数是 2。
> 对于子阵列{ **3** ，1，6}，最近的素数是 3。
> 
> **输入:** arr[] = {8，7，12，15，3，11}
> **输出:**7 7 3 3 11
> **解释:**
> 对于子阵{8， **7** ，12}，最接近的素数是 7。
> 对于子阵{15， **3** }，最接近的素数是 3。
> 对于子阵{ **11** }，最接近的素数就是 11 本身。

**方法:**
按照以下步骤解决问题:

*   求数组中最大元素 **maxm** 。
*   使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)计算并存储所有质数直到 **maxm**
*   遍历数组并存储素数的索引。
*   如果数组中没有质数，则打印所有索引的-1。
*   将**指向第一个由素数组成的索引。**
*   对于到 **curr** 的每个索引，打印 **arr【素数【curr】】**作为最近的素数。
*   对于超过 **curr** 的指数，将距离与质数【curr】和质数【curr + 1】进行比较。如果素数[curr]更近，打印**arr[素数[curr]]【T3]。否则，增加**货币**并打印 **arr【质数【货币】】**。**
*   如果 **curr** 是数组中的最后一个质数，则打印 **arr【质数【curr】】**用于所有索引。

下面是上述方法的实现:

## C++

```
// C++ program to find nearest
// prime number in the array
// for all array elements
#include <bits/stdc++.h>
using namespace std;

#define max 10000000

// Create a boolean array and set all
// entries it as false. A value in
// prime[i] will be true if i is not a
// prime, else false
bool prime[max] = { false };

// Sieve of Eratosthenes function
void SieveOfEratosthenes(int maxm)
{
    prime[0] = prime[1] = true;
    for (int i = 2; i * i <= maxm; i++) {
        // Update all multiples of i greater
        // than or equal to the square of it
        // numbers which are multiple of i and are
        // less than i^2 are already been marked.
        if (!prime[i]) {
            for (int j = i * i; j <= maxm; j += i) {
                prime[j] = true;
            }
        }
    }
}
// Function to find nearest
// prime number for all elements
void print_nearest_prime(int arr[], int N)
{
    int maxm = *max_element(arr, arr + N);
    // Compute and store all prime
    // numbers up to maxm
    SieveOfEratosthenes(maxm);

    vector<int> primes;
    for (int i = 0; i < N; i++) {
        // Store the indices of
        // all primes
        if (!prime[arr[i]])
            primes.push_back(i);
    }

    // If no primes are present
    // in the array
    if (primes.size() == 0) {
        for (int i = 0; i < N; i++) {
            cout << -1 << " ";
        }

        return;
    }

    // Store the current prime
    int curr = 0;
    for (int i = 0; i < N; i++) {
        // If the no further
        // primes exist in the array
        if (curr == primes.size() - 1
            // For all indices less than
            // that of the current prime
            || i <= primes[curr]) {
            cout << arr[primes[curr]] << " ";
            continue;
        }

        // If the current prime is
        // nearer
        if (abs(primes[curr] - i)
            < abs(primes[curr + 1] - i)) {
            cout << arr[primes[curr]] << " ";
        }
        // If the next prime is nearer
        else {
            // Make the next prime
            // as the current
            curr++;
            cout << arr[primes[curr]] << " ";
        }
    }
}
// Driver Program
int main()
{
    int N = 6;
    int arr[] = { 8, 7, 12, 15, 3, 11 };
    print_nearest_prime(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nearest
// prime number in the array
// for all array elements
import java.util.*;

class GFG{

static final int max = 10000000;

// Create a boolean array and set all
// entries it as false. A value in
// prime[i] will be true if i is not a
// prime, else false
static boolean []prime = new boolean[max];

// Sieve of Eratosthenes function
static void SieveOfEratosthenes(int maxm)
{
    prime[0] = prime[1] = true;

    for(int i = 2; i * i <= maxm; i++)
    {

       // Update all multiples of i greater
       // than or equal to the square of it
       // numbers which are multiple of i
       // and are less than i^2 are already
       // been marked.
       if (!prime[i])
       {
           for(int j = i * i;
                   j <= maxm; j += i)
           {
              prime[j] = true;
           }
       }
    }
}

// Function to find nearest
// prime number for all elements
static void print_nearest_prime(int arr[], int N)
{
    int maxm = Arrays.stream(arr).max().getAsInt();

    // Compute and store all prime
    // numbers up to maxm
    SieveOfEratosthenes(maxm);

    Vector<Integer> primes = new Vector<Integer>();

    for(int i = 0; i < N; i++)
    {

       // Store the indices of
       // all primes
       if (!prime[arr[i]])
           primes.add(i);
    }

    // If no primes are present
    // in the array
    if (primes.size() == 0)
    {
        for(int i = 0; i < N; i++)
        {
           System.out.print(-1 + " ");
        }
        return;
    }

    // Store the current prime
    int curr = 0;
    for(int i = 0; i < N; i++)
    {

       // If the no further
       // primes exist in the array
       if (curr == primes.size() - 1 ||

           // For all indices less than
           // that of the current prime
           i <= primes.get(curr))
       {
           System.out.print(
               arr[primes.get(curr)] + " ");
           continue;
       }

       // If the current prime is
       // nearer
       if (Math.abs(primes.get(curr) - i) <
           Math.abs(primes.get(curr + 1) - i))
       {
           System.out.print(
               arr[primes.get(curr)] + " ");
       }

       // If the next prime is nearer
       else
       {

           // Make the next prime
           // as the current
           curr++;
           System.out.print(
               arr[primes.get(curr)] + " ");
       }
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 6;
    int arr[] = { 8, 7, 12, 15, 3, 11 };

    print_nearest_prime(arr, N);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find nearest
# prime number in the array
# for all array elements
maxi = 10000000

# Create a boolean array and set all
# entries it as false. A value in
# prime[i] will be true if i is not a
# prime, else false
prime = [False] * (maxi)

# Sieve of Eratosthenes function
def SieveOfEratosthenes(maxm):

    prime[0] = prime[1] = True
    for i in range(2, maxm + 1):
        if i * i > maxm:
            break

        # Update all multiples of i greater
        # than or equal to the square of it
        # numbers which are multiple of i and are
        # less than i^2 are already been marked.
        if (not prime[i]):
            for j in range(i * i, maxm + 1, i):
                prime[j] = True

# Function to find nearest
# prime number for all elements
def print_nearest_prime(arr, N):

    maxm = max(arr)

    # Compute and store all prime
    # numbers up to maxm
    SieveOfEratosthenes(maxm)

    primes = []
    for i in range(N):

        # Store the indices of
        # all primes
        if (not prime[arr[i]]):
            primes.append(i)

    # If no primes are present
    # in the array
    if len(primes) == 0:
        for i in range(N):
            print(-1, end = " ")
        return

    # Store the current prime
    curr = 0
    for i in range(N):

        # If the no further primes
        # exist in the array
        if (curr == len(primes) - 1 or

            # For all indices less than
            # that of the current prime
            i <= primes[curr]):
            print(arr[primes[curr]], end = " ")
            continue

        # If the current prime is
        # nearer
        if (abs(primes[curr] - i) <
            abs(primes[curr + 1] - i)):
            print(arr[primes[curr]], end = " ")

        # If the next prime is nearer
        else:

            # Make the next prime
            # as the current
            curr += 1
            print(arr[primes[curr]], end = " ")

# Driver code
if __name__ == '__main__':

    N = 6
    arr = [ 8, 7, 12, 15, 3, 11 ]

    print_nearest_prime(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find nearest
// prime number in the array
// for all array elements
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

static readonly int max = 10000000;

// Create a bool array and set all
// entries it as false. A value in
// prime[i] will be true if i is not a
// prime, else false
static bool []prime = new bool[max];

// Sieve of Eratosthenes function
static void SieveOfEratosthenes(int maxm)
{
    prime[0] = prime[1] = true;

    for(int i = 2; i * i <= maxm; i++)
    {

        // Update all multiples of i greater
        // than or equal to the square of it
        // numbers which are multiple of i
        // and are less than i^2 are already
        // been marked.
        if (!prime[i])
        {
            for(int j = i * i;
                    j <= maxm; j += i)
            {
                prime[j] = true;
            }
        }
    }
}

// Function to find nearest
// prime number for all elements
static void print_nearest_prime(int []arr,
                                int N)
{
    int maxm = arr.Max();

    // Compute and store all prime
    // numbers up to maxm
    SieveOfEratosthenes(maxm);

    List<int> primes = new List<int>();

    for(int i = 0; i < N; i++)
    {

        // Store the indices of
        // all primes
        if (!prime[arr[i]])
            primes.Add(i);
    }

    // If no primes are present
    // in the array
    if (primes.Count == 0)
    {
        for(int i = 0; i < N; i++)
        {
            Console.Write(-1 + " ");
        }
        return;
    }

    // Store the current prime
    int curr = 0;
    for(int i = 0; i < N; i++)
    {

        // If the no further
        // primes exist in the array
        if (curr == primes.Count - 1 ||

            // For all indices less than
            // that of the current prime
            i <= primes[curr])
        {
            Console.Write(
                arr[primes[curr]] + " ");
            continue;
        }

        // If the current prime is
        // nearer
        if (Math.Abs(primes[curr] - i) <
            Math.Abs(primes[curr + 1] - i))
        {
            Console.Write(
                arr[primes[curr]] + " ");
        }

        // If the next prime is nearer
        else
        {

            // Make the next prime
            // as the current
            curr++;
            Console.Write(
                arr[primes[curr]] + " ");
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 6;
    int []arr = { 8, 7, 12, 15, 3, 11 };

    print_nearest_prime(arr, N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find nearest
// prime number in the array
// for all array elements
let max = 10000000;

// Create a boolean array and set all
// entries it as false. A value in
// prime[i] will be true if i is not a
// prime, else false
let prime = new Array(max);

// Sieve of Eratosthenes function
function SieveOfEratosthenes(maxm)
{
    prime[0] = prime[1] = true;

    for(let i = 2; i * i <= maxm; i++)
    {

        // Update all multiples of i greater
        // than or equal to the square of it
        // numbers which are multiple of i
        // and are less than i^2 are already
        // been marked.
        if (!prime[i])
        {
            for(let j = i * i; j <= maxm; j += i)
            {
                prime[j] = true;
            }
        }
    }
}

// Function to find nearest
// prime number for all elements
function print_nearest_prime(arr, N)
{
    let maxm = Math.max(...arr);

    // Compute and store all prime
    // numbers up to maxm
    SieveOfEratosthenes(maxm);

    let primes = [];

    for(let i = 0; i < N; i++)
    {

        // Store the indices of
        // all primes
        if (!prime[arr[i]])
            primes.push(i);
    }

    // If no primes are present
    // in the array
    if (primes.length == 0)
    {
        for(let i = 0; i < N; i++)
        {
            document.write(-1 + " ");
        }
        return;
    }

    // Store the current prime
    let curr = 0;
    for(let i = 0; i < N; i++)
    {

        // If the no further
        // primes exist in the array
        if (curr == primes.length - 1 ||

            // For all indices less than
            // that of the current prime
            i <= primes[curr])
        {
            document.write(arr[primes[curr]] + " ");
            continue;
        }

        // If the current prime is
        // nearer
        if (Math.abs(primes[curr] - i) <
            Math.abs(primes[curr + 1] - i))
        {
            document.write(
            arr[primes[curr]] + " ");
        }

        // If the next prime is nearer
        else
        {

            // Make the next prime
            // as the current
            curr++;
            document.write(arr[primes[curr]] + " ");
        }
    }
}

// Driver code
let N = 6;
let arr = [ 8, 7, 12, 15, 3, 11 ];

print_nearest_prime(arr, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
7 7 7 3 3 11
```

***时间复杂度:**O(maxm *(log(log(maxm)))+N)*
***辅助空间:** O(N)*