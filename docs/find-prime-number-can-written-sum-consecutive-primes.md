# 找出可以写成最连续素数之和的素数

> 原文:[https://www . geesforgeks . org/find-质数-可写-和-连续-质数/](https://www.geeksforgeeks.org/find-prime-number-can-written-sum-consecutive-primes/)

给定一系列限制。对于每一个极限，求可以写成小于或等于极限的最连续素数之和的素数。
极限的最大可能值是 10^4.

**示例:**

```
Input  : arr[] = {10, 30}
Output : 5, 17
Explanation : There are two limit values 10 and 30.
Below limit 10, 5 is sum of two consecutive primes,
2 and 3\. 5 is the prime number which is sum of largest 
chain of consecutive below limit 10.

Below limit 30, 17 is sum of four consecutive primes.
2 + 3 + 5 + 7 = 17
```

以下是步骤。

1.  使用巽他拉姆的[筛找出所有低于最大极限(10^6)的质数，并将它们存储在质数[]中。](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)
2.  为质数[]
    中的所有质数构造前缀和数组**质数和[]**=质数和[i] +质数[i]。
    素数和[i]和素数和[j]中的两个值之差表示从索引 I 到索引 j 的连续素数之和
3.  遍历两个循环，外环从 i (0 到极限)和内环从 j (0 到 I)
4.  对于每个 I，内部循环遍历(0 到 I)，我们检查连续素数的当前和(**consSum**= prime _ sum[I]–prime _ sum[j])是否为素数(我们使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在 prime[]中搜索 consSum)。
5.  如果 consSum 是素数，那么如果当前长度大于当前结果的长度，我们就更新结果。

下面是上述步骤的实现。

## C++

```
\
// C++ program to find Longest Sum of consecutive
// primes
#include<bits/stdc++.h>
using namespace std;
const int MAX  = 10000;

// utility function for sieve of sundaram
void sieveSundaram(vector <int> &primes)
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool marked[MAX/2 + 1] = {0};

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i=1; i<=(sqrt(MAX)-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=MAX/2; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// function find the prime number which can be written
// as the sum of the most consecutive primes
int LSCPUtil(int limit, vector<int> &prime, long long int sum_prime[])
{
    // To store maximum length of consecutive primes that can
    // sum to a limit
    int max_length = -1;

    // The prime number (or result) that can be represented as
    // sum of maximum number of primes.
    int prime_number = -1;

    // Consider all lengths of consecutive primes below limit.
    for (int i=0; prime[i]<=limit; i++)
    {
        for (int j=0; j<i; j++)
        {
            // if we cross the limit, then break the loop
            if (sum_prime[i] - sum_prime[j] > limit)
                break;

            // sum_prime[i]-sum_prime[j] is prime number or not
            long long int consSum  = sum_prime[i] - sum_prime[j];

            // Check if sum of current length of consecutives is
            // prime or not.
            if (binary_search(prime.begin(), prime.end(), consSum))
            {
                // update the length and prime number
                if (max_length < i-j+1)
                {
                    max_length = i-j+1;
                    prime_number = consSum;
                }
            }
        }
    }

    return prime_number;
}

// Returns the prime number that can written as sum
// of longest chain of consecutive primes.
void LSCP(int arr[], int n)
{
    // Store prime number in vector
    vector<int> primes;
    sieveSundaram(primes);

    long long int sum_prime[primes.size() + 1];

    // Calculate sum of prime numbers and store them
    // in sum_prime array. sum_prime[i] stores sum of
    // prime numbers from primes[0] to primes[i-1]
    sum_prime[0] = 0;
    for (int i = 1 ; i <= primes.size(); i++)
        sum_prime[i] = primes[i-1] + sum_prime[i-1];

    // Process all queries one by one
    for (int i=0; i<n; i++)
      cout << LSCPUtil(arr[i], primes, sum_prime) << " ";
}

// Driver program
int main()
{
    int arr[] = {10, 30, 40, 50, 1000};
    int n = sizeof(arr)/sizeof(arr[0]);
    LSCP(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest sum
// of consecutive primes
import java.util.*;

class GFG{

static int MAX = 10000;

// Store prime number in vector
static ArrayList<Object> primes = new ArrayList<Object>();

// Utility function for sieve of sundaram
static void sieveSundaram()
{

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than MAX, we reduce MAX
    // to half. This array is used to
    // separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    boolean []marked = new boolean[MAX / 2 + 1];
    Arrays.fill(marked, false);

    // Main logic of Sundaram. Mark
    // all numbers which do not
    // generate prime number by
    // doing 2*i+1
    for(int i = 1;
            i <= (Math.sqrt(MAX) - 1) / 2; i++)
        for(int j = (i * (i + 1)) << 1;
                j <= MAX / 2;
                j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes. Remaining
    // primes are of the form 2*i + 1
    // such that marked[i] is false.
    for(int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function find the prime number
// which can be written as the
// sum of the most consecutive primes
static int LSCPUtil(int limit, long []sum_prime)
{

    // To store maximum length of
    // consecutive primes that can
    // sum to a limit
    int max_length = -1;

    // The prime number (or result)
    // that can be represented as
    // sum of maximum number of primes.
    int prime_number = -1;

    // Consider all lengths of
    // consecutive primes below limit.
    for(int i = 0; (int)primes.get(i) <= limit; i++)
    {
        for(int j = 0; j < i; j++)
        {

            // If we cross the limit, then
            // break the loop
            if (sum_prime[i] - sum_prime[j] >
                limit)
                break;

            // sum_prime[i]-sum_prime[j] is
            // prime number or not
            long consSum  = sum_prime[i] -
                            sum_prime[j];

            Object[] prime = primes.toArray();

            // Check if sum of current length
            // of consecutives is prime or not.
            if (Arrays.binarySearch(
                prime, (int)consSum) >= 0)
            {

                // Update the length and prime number
                if (max_length < i - j + 1)
                {
                    max_length = i - j + 1;
                    prime_number = (int)consSum;
                }
            }
        }
    }
    return prime_number;
}

// Returns the prime number that
// can written as sum of longest
// chain of consecutive primes.
static void LSCP(int []arr, int n)
{
    sieveSundaram();

    long []sum_prime = new long[primes.size() + 1];

    // Calculate sum of prime numbers
    // and store them in sum_prime
    // array. sum_prime[i] stores sum
    // of prime numbers from
    // primes[0] to primes[i-1]
    sum_prime[0] = 0;
    for(int i = 1; i <= primes.size(); i++)
        sum_prime[i] = (int)primes.get(i - 1) +
                             sum_prime[i - 1];

    // Process all queries one by one
    for(int i = 0; i < n; i++)
      System.out.print(LSCPUtil(
          arr[i], sum_prime) + " ");
}

// Driver code
public static void main(String []arg)
{
    int []arr = { 10, 30, 40, 50, 1000 };
    int n = arr.length;

    LSCP(arr, n);
}
}

// This code is contributed by pratham76
```

## C#

```
// C# program to find longest sum
// of consecutive primes
using System;
using System.Collections;

class GFG{

static int MAX = 10000;

// Store prime number in vector
static ArrayList primes = new ArrayList();

// Utility function for sieve of sundaram
static void sieveSundaram()
{

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than MAX, we reduce MAX
    // to half. This array is used to
    // separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool []marked = new bool[MAX / 2 + 1];
    Array.Fill(marked, false);

    // Main logic of Sundaram. Mark
    // all numbers which do not
    // generate prime number by
    // doing 2*i+1
    for(int i = 1;
            i <= (Math.Sqrt(MAX) - 1) / 2; i++)
        for(int j = (i * (i + 1)) << 1;
                j <= MAX / 2;
                j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes. Remaining
    // primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for(int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function find the prime number
// which can be written as the
// sum of the most consecutive primes
static int LSCPUtil(int limit, long []sum_prime)
{

    // To store maximum length of
    // consecutive primes that can
    // sum to a limit
    int max_length = -1;

    // The prime number (or result)
    // that can be represented as
    // sum of maximum number of primes.
    int prime_number = -1;

    // Consider all lengths of
    // consecutive primes below limit.
    for(int i = 0; (int)primes[i] <= limit; i++)
    {
        for(int j = 0; j < i; j++)
        {

            // If we cross the limit, then
            // break the loop
            if (sum_prime[i] - sum_prime[j] >
                limit)
                break;

            // sum_prime[i]-sum_prime[j] is
            // prime number or not
            long consSum  = sum_prime[i] -
                            sum_prime[j];

            int[] prime = (int[])primes.ToArray(typeof(int));

            // Check if sum of current length
            // of consecutives is prime or not.
            if (Array.BinarySearch(prime,
                (int)consSum) >= 0)
            {

                // Update the length and prime number
                if (max_length < i - j + 1)
                {
                    max_length = i - j + 1;
                    prime_number = (int)consSum;
                }
            }
        }
    }
    return prime_number;
}

// Returns the prime number that
// can written as sum of longest
// chain of consecutive primes.
static void LSCP(int []arr, int n)
{
    sieveSundaram();

    long []sum_prime = new long[primes.Count + 1];

    // Calculate sum of prime numbers
    // and store them in sum_prime
    // array. sum_prime[i] stores sum
    // of prime numbers from
    // primes[0] to primes[i-1]
    sum_prime[0] = 0;
    for(int i = 1; i <= primes.Count; i++)
        sum_prime[i] = (int)primes[i - 1] +
                         sum_prime[i - 1];

    // Process all queries one by one
    for(int i = 0; i < n; i++)
      Console.Write(LSCPUtil(
          arr[i], sum_prime) + " ");
}

// Driver code
public static void Main(string []arg)
{
    int []arr = { 10, 30, 40, 50, 1000 };
    int n = arr.Length;

    LSCP(arr, n);
}
}

// This code is contributed by rutvik_56
```

**输出:**

```
5 17 17 41 953
```

本文由[**Nishant _ Singh(pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。