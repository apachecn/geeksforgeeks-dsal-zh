# 阵列 B 的最小可能和，使得所有 1 ≤ i < j ≤ N

的艾比= AjBj

> 原文:[https://www . geeksforgeeks . org/最小可能数组和-b-这样-艾比-ajbj-for-all-1-i-j-n/](https://www.geeksforgeeks.org/minimum-possible-sum-of-array-b-such-that-aibi-ajbj-for-all-1-i-j-n/)

给定一个大小为 **N** 的数组**[]**。任务是找到数组 **b[]** 元素的最小可能和，使得所有 **1 ≤ i < j ≤ N** 的 **a[i] * b[i] = a[j] * b[j]** 。答案可能很大。所以，打印答案 modoulo**10<sup>9</sup>+7**。

**示例:**

> **输入:** a[] = {2，3，4 }
> T3】输出: 13
> b[] = {6，4，3}
> 
> **输入:** a[] = {5，5，5 }
> T3】输出: 3
> b = {1，1，1}

**方法:**假设确定满足给定条件的**B<sub>I</sub>T5。然后让**K = A<sub>1</sub>* B<sub>1</sub>**，然后约束**K = A<sub>1</sub>* B<sub>1</sub>= A<sub>j</sub>* B<sub>j</sub>T21】全部保持 **j > 1** 。因此 **K** 是 **A <sub>1</sub> ，…，A <sub>N</sub>** 的公倍数。
反过来，让 **lcm** 为 **A <sub>1</sub> ，…，A<sub>N</sub>T40】的最小公倍数，让**B<sub>I</sub>= LCM/A<sub>I</sub>**则这样的 **B** 满足条件。
所以，想要的答案是 **∑lcm/A <sub>i</sub>** 。但是 **lcm** 可以是一个很大的数字，所以不能直接计算。现在，让我们考虑计算，将 **lcm** 保持在因子分解的形式。设 **p <sub>i</sub>** 为素数，假设因式分解由**X =∏p<sub>I</sub><sup>g<sub>I</sub></sup>**、**Y =∏p<sub>I</sub><sup>f<sub>I</sub></sup>T77 那么 **X** 和 **Y** 的最小公倍数由**∏p<sub>I</sub>T93】max(g<sub>I</sub>，f<sub>I</sub>)T99】给出。通过使用这个，可以以因子化的形式获得 **A <sub>1</sub> ，…，A <sub>N</sub>** 的最小公倍数。所以这个问题总共可以在 **O(N*sqrt(A))** 时间内解决，其中**A = max(A<sub>I</sub>)**。同样，通过适当的预计算加速素分解，也可以在总共 **O(A + N*logA)** 的时间内得到答案。**********

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define mod (int)(1e9 + 7)
#define N 1000005

// To store least prime factors
// of all the numbers
int lpf[N];

// Function to find the least prime
// factor of all the numbers
void least_prime_factor()
{
    for (int i = 1; i < N; i++)
        lpf[i] = i;

    for (int i = 2; i < N; i++)
        if (lpf[i] == i)
            for (int j = i * 2; j < N; j += i)
                if (lpf[j] == j)
                    lpf[j] = i;
}

// Function to return the ((a^m1) % mod)
int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1LL * a * a) % mod;
    else if (m1 & 1)
        return (1LL * a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to return the sum of
// elements of array B
long long sum_of_elements(int a[], int n)
{
    // Find the prime factors of
    // all the numbers
    least_prime_factor();

    // To store each prime count in lcm
    map<int, int> prime_factor;

    for (int i = 0; i < n; i++) {

        // Current number
        int temp = a[i];

        // Map to store the prime count
        // of a single number
        map<int, int> single_number;

        // Basic way to calculate all prime factors
        while (temp > 1) {
            int x = lpf[temp];
            single_number[x]++;
            temp /= x;
        }

        // If it is the first number in the array
        if (i == 0)
            prime_factor = single_number;

        // Take the maximum count of 
        // prime in a number
        else {
            for (auto x : single_number)
                prime_factor[x.first] = max(x.second, 
                                prime_factor[x.first]);
        }
    }

    long long ans = 0, lcm = 1;

    // Calculate lcm of given array
    for (auto x : prime_factor)
        lcm = (lcm * power(x.first, x.second)) % mod;

    // Calculate sum of elements of array B
    for (int i = 0; i < n; i++)
        ans = (ans + (lcm * power(a[i], 
                      mod - 2)) % mod) % mod;

    return ans;
}

// Driver code
int main()
{
    int a[] = { 2, 3, 4 };
    int n = sizeof(a) / sizeof(int);

    cout << sum_of_elements(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int mod = 1000000007;
static int N = 1000005;

// To store least prime factors
// of all the numbers
static int lpf[] = new int[N];

// Function to find the least prime
// factor of all the numbers
static void least_prime_factor()
{
    for (int i = 1; i < N; i++)
        lpf[i] = i;

    for (int i = 2; i < N; i++)
        if (lpf[i] == i)
            for (int j = i * 2; j < N; j += i)
                if (lpf[j] == j)
                    lpf[j] = i;
}

// Function to return the ((a^m1) % mod)
static long power(long a, long m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1l * a * a) % mod;
    else if ((m1 & 1) != 0)
        return (1l * a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to return the sum of
// elements of array B
static long sum_of_elements(long a[], int n)
{
    // Find the prime factors of
    // all the numbers
    least_prime_factor();

    // To store each prime count in lcm
    HashMap<Long, Long> prime_factor 
            = new HashMap<>();

    for (int i = 0; i < n; i++) 
    {

        // Current number
        long temp = a[i];

        // Map to store the prime count
        // of a single number
        HashMap<Long, Long> single_number
            = new HashMap<>();

        // Basic way to calculate all prime factors
        while (temp > 1) 
        {
            long x = lpf[(int)temp];
            single_number.put(x,(single_number.get(x) == 
                        null ? 1:single_number.get(x) + 1));
            temp /= x;
        }

        // If it is the first number in the array
        if (i == 0)
            prime_factor = single_number;

        // Take the maximum count of 
        // prime in a number
        else {
            for (Map.Entry<Long,Long> x : single_number.entrySet() )
                prime_factor.put(x.getKey(), Math.max(x.getValue(), 
                                (prime_factor.get(x.getKey()) == 
                                null ? 0:prime_factor.get(x.getKey()))));
        }
    }

    long ans = 0, lcm = 1;

    // Calculate lcm of given array
    for (Map.Entry<Long,Long> x : prime_factor.entrySet())
        lcm = (lcm * power(x.getKey(), x.getValue())) % mod;

    // Calculate sum of elements of array B
    for (int i = 0; i < n; i++)
        ans = (ans + (lcm * power(a[i], 
                    mod - 2)) % mod) % mod;

    return ans;
}

// Driver code
public static void main(String args[])
{
    long a[] = { 2, 3, 4 };
    int n = a.length;

    System.out.println(sum_of_elements(a, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 10 ** 9 + 7
N = 1000005

# To store least prime factors
# of all the numbers
lpf = [0 for i in range(N)]

# Function to find the least prime
# factor of all the numbers
def least_prime_factor():
    for i in range(1, N):
        lpf[i] = i

    for i in range(2,N):
        if (lpf[i] == i):
            for j in range(i * 2, N, i):
                if (lpf[j] == j):
                    lpf[j] = i

# Function to return the sum of
# elements of array B
def sum_of_elements(a, n):

    # Find the prime factors of
    # all the numbers
    least_prime_factor()

    # To store each prime count in lcm
    prime_factor=dict()

    for i in range(n):

        # Current number
        temp = a[i]

        # Map to store the prime count
        # of a single number
        single_number = dict()

        # Basic way to calculate all prime factors
        while (temp > 1):
            x = lpf[temp]
            single_number[x] = single_number.get(x, 0) + 1
            temp //= x

        # If it is the first number in the array
        if (i == 0):
            prime_factor = single_number

        # Take the maximum count of
        # prime in a number
        else:
            for x in single_number:
                if x in prime_factor:
                    prime_factor[x] = max(prime_factor[x], 
                                           single_number[x])
                else:
                    prime_factor[x] = single_number[x]

    ans, lcm = 0, 1

    # Calculate lcm of given array
    for x in prime_factor:
        lcm = (lcm * pow(x, prime_factor[x],mod)) % mod

    # Calculate sum of elements of array B
    for i in range(n):
        ans = (ans + (lcm * pow(a[i], 
                mod - 2,mod)) % mod) % mod

    return ans

# Driver code
if __name__ == '__main__':
    a = [2, 3, 4]
    n = len(a)
    print(sum_of_elements(a, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System; 
using System.Collections.Generic; 

class GFG{         

static int mod = 1000000007;
static int N = 1000005;

// To store least prime factors
// of all the numbers
static int []lpf = new int[N];

// Function to find the least prime
// factor of all the numbers
static void least_prime_factor()
{
    for(int i = 1; i < N; i++)
        lpf[i] = i;

    for(int i = 2; i < N; i++)
        if (lpf[i] == i)
            for(int j = i * 2; 
                    j < N; j += i)
                if (lpf[j] == j)
                    lpf[j] = i;
}

// Function to return the ((a^m1) % mod)
static long power(long a, long m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (a * a) % mod;

    else if ((m1 & 1) != 0)
        return (a * power(power(a, m1 / 2),
                                  2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to return the sum of
// elements of array B
static long sum_of_elements(long []a, int n)
{

    // Find the prime factors of
    // all the numbers
    least_prime_factor();

    // To store each prime count in lcm
    Dictionary<long,
               long> prime_factor = new Dictionary<long,
                                                   long>();

    for(int i = 0; i < n; i++) 
    {

        // Current number
        long temp = a[i];

        // Map to store the prime count
        // of a single number
        Dictionary<long,
                   long> single_number = new Dictionary<long,
                                                        long>();

        // Basic way to calculate all prime factors
        while (temp > 1) 
        {
            long x = lpf[(int)temp];
            if (single_number.ContainsKey(x))
            {
                single_number[x]++;
            }
            else
            {
                single_number[x] = 1;
            }
            temp /= x;
        }

        // If it is the first number in the array
        if (i == 0)
            prime_factor = single_number;

        // Take the maximum count of 
        // prime in a number
        else
        {
            foreach(KeyValuePair<long, 
                                 long> ele in single_number)
            {
                if (prime_factor.ContainsKey(ele.Key))
                {
                    prime_factor[ele.Key] = Math.Max(
                        ele.Value, prime_factor[ele.Key]);
                }
                else
                {
                    prime_factor[ele.Key] = Math.Max(
                        ele.Value, 0);
                }
            }
        }
    }

    long ans = 0, lcm = 1;

    // Calculate lcm of given array
    foreach(KeyValuePair<long, long> x in prime_factor)
    {
        lcm = (lcm * power(x.Key, x.Value)) % mod;
    }

    // Calculate sum of elements of array B
    for(int i = 0; i < n; i++)
        ans = (ans + (lcm * power(a[i],
               mod - 2)) % mod) % mod;

    return ans;
}     

// Driver Code         
public static void Main (string[] args)
{         
    long []a = { 2, 3, 4 };
    int n = a.Length;

    Console.Write(sum_of_elements(a, n));
}         
}

// This code is contributed by rutvik_56
```

**Output:**

```
13

```