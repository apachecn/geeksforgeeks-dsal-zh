# 在数组元素质因数倍数的索引处翻转位后，找到最终字符串

> 原文:[https://www . geeksforgeeks . org/在数组元素质因数的倍数索引处翻转位后找到最终字符串/](https://www.geeksforgeeks.org/find-the-final-string-after-flipping-bits-at-the-indices-that-are-multiple-of-prime-factors-of-array-elements/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个由 **M** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在所有数组元素的素因子的倍数索引处翻转字符后找到最终字符串。请注意，此问题使用基于 1 的索引。

**示例:**

> **输入:**S =“000000”，arr[] = {2，4，6}
> **输出:** 011100
> **解释:**
> 
> 1.  2 的质因数是{2}。因此，翻转所有 2 的倍数的索引值后的字符串是 S =“010101”。
> 2.  4 的质因数是{2}。因此，翻转所有 2 的倍数的索引值后的字符串是 S =“000000”。
> 3.  6 的质因数是{2，3}。因此翻转所有 2 的倍数的索引的值后的字符串是 S =“010101”，翻转所有 3 的倍数的索引的值后的字符串是 S =“011100”。
> 
> **输入:**S =“001100”，arr[] = {2，3，5 }
> T3】输出: 010010

**方法:**通过存储所有数组元素的素数因子的频率，借助厄拉多塞的[筛可以解决给定的问题。可以观察到，具有偶数频率的质因数不会有助于翻转。因此，可以通过以奇数频率翻转多个](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的索引位来获得结果串。按照以下步骤解决给定的问题:

*   创建一个函数**Get 因式分解()**，返回任意数字的所有[质因数。](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)
*   初始化一个数组， **frequency[]** ，该数组存储数组所有元素的所有不同素因子的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)**arr[]**。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[i]** ，使用**get 因式分解(arr[i] )** 找到它的素因子，并增加素因子在 **frequency[]** 数组中的频率。
*   对于数组中**频率【I】**的所有奇数值，遍历 **i** 的所有因子，翻转给定字符串 s 中各个索引的位
*   存储在 **S** 中的字符串是需要的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

#define MAXN 100001

// Stores smallest prime factor
int spf[MAXN];

// Function to find the smallest prime
// factor for every number till MAXN
void sieve()
{
    spf[1] = 1;

    // Marking smallest prime factor for
    // every number to be itself
    for (int i = 2; i < MAXN; i++)
        spf[i] = i;

    // Separately marking spf for every
    // even number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    for (int i = 3; i * i < MAXN; i++) {

        // Checking if i is prime
        if (spf[i] == i) {

            // Marking SPF for all numbers
            // divisible by i
            for (int j = i * i;
                 j < MAXN; j += i) {
                if (spf[j] == j)
                    spf[j] = i;
            }
        }
    }
}

// Function to find all the distinct prime
// factors of the given number x
vector<int> getFactorization(int x)
{
    vector<int> ret;

    // Find the prime factors for X
    while (x != 1) {

        ret.push_back(spf[x]);

        // Find the spf[] of x
        int value = spf[x];

        while (x % value == 0)
            x = x / value;
    }

    // Return the prime factors for x
    return ret;
}

// Function to find string after flipping
// the characters at indices of prime
// factors of array elements arr[]
string flipString(string S, int arr[],
                  int M)
{
    // Precalculating Smallest Prime Factor
    sieve();

    // Stores the frequency of each
    // prime factor
    int frequency[MAXN] = { 0 };

    // Iterate over all elements of
    // the array arr[]
    for (int i = 0; i < M; i++) {

        // Stores prime factors of arr[i]
        vector<int> primeFactors
            = getFactorization(arr[i]);

        // Increment the frequency of all
        // prime factors of arr[i]
        for (auto& factors : primeFactors) {
            frequency[factors]++;
            frequency[factors] %= 2;
        }
    }

    int N = S.length();

    // Iterate over all elements of
    // the array frequency[]
    for (int i = 0; i < MAXN; i++) {

        // If frequency[i] is odd
        if (frequency[i] & 1) {

            // Flip bits of all indices
            // that are multiple of i
            for (int j = i; j <= N; j += i) {
                S[j - 1] = (S[j - 1]
                                    == '1'
                                ? '0'
                                : '1');
            }
        }
    }

    // Return Answer
    return S;
}

// Driver Code
int main()
{
    string S = "000000";
    int arr[] = { 2, 4, 6 };
    int M = sizeof(arr) / sizeof(arr[0]);

    cout << flipString(S, arr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Arrays;

class GFG {

    public static int MAXN = 100001;

    // Stores smallest prime factor
    public static int[] spf = new int[MAXN];

    // Function to find the smallest prime
    // factor for every number till MAXN
    public static void sieve() {
        spf[1] = 1;

        // Marking smallest prime factor for
        // every number to be itself
        for (int i = 2; i < MAXN; i++)
            spf[i] = i;

        // Separately marking spf for every
        // even number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++) {

            // Checking if i is prime
            if (spf[i] == i) {

                // Marking SPF for all numbers
                // divisible by i
                for (int j = i * i; j < MAXN; j += i) {
                    if (spf[j] == j)
                        spf[j] = i;
                }
            }
        }
    }

    // Function to find all the distinct prime
    // factors of the given number x
    public static ArrayList<Integer> getFactorization(int x) {
        ArrayList<Integer> ret = new ArrayList<Integer>();

        // Find the prime factors for X
        while (x != 1) {

            ret.add(spf[x]);

            // Find the spf[] of x
            int value = spf[x];

            while (x % value == 0)
                x = x / value;
        }

        // Return the prime factors for x
        return ret;
    }

    // Function to find string after flipping
    // the characters at indices of prime
    // factors of array elements arr[]
    public static String flipString(String S, int arr[], int M) {
        // Precalculating Smallest Prime Factor
        sieve();

        // Stores the frequency of each
        // prime factor
        int[] frequency = new int[MAXN];

        Arrays.fill(frequency, 0);

        // Iterate over all elements of
        // the array arr[]
        for (int i = 0; i < M; i++) {

            // Stores prime factors of arr[i]
            ArrayList<Integer> primeFactors = getFactorization(arr[i]);

            // Increment the frequency of all
            // prime factors of arr[i]
            for (int factors : primeFactors) {
                frequency[factors]++;
                frequency[factors] %= 2;
            }
        }

        int N = S.length();

        // Iterate over all elements of
        // the array frequency[]
        for (int i = 0; i < MAXN; i++) {

            // If frequency[i] is odd
            if ((frequency[i] & 1) > 0) {

                // Flip bits of all indices
                // that are multiple of i
                for (int j = i; j <= N; j += i)
                {

                    // S.replace(S.charAt(j - 1), (S.charAt(j - 1) == '1' ? '0' : '1'));
                    S = S.substring(0, j - 1) + (S.charAt(j - 1) == '1' ? '0' : '1') + S.substring(j);
                }
            }
        }

        // Return Answer
        return S;
    }

    // Driver Code
    public static void main(String args[]) {
        String S = "000000";
        int arr[] = { 2, 4, 6 };
        int M = arr.length;

        System.out.println(flipString(S, arr, M));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python program for the above approach
MAXN = 100001

# Stores smallest prime factor
spf = [0] * MAXN

# Function to find the smallest prime
# factor for every number till MAXN
def sieve():
    spf[1] = 1

    # Marking smallest prime factor for
    # every number to be itself
    for i in range(2, MAXN):
        spf[i] = i

    # Separately marking spf for every
    # even number as 2
    for i in range(4, MAXN, 2):
        spf[i] = 2

    i = 3
    while(i * 8 < MAXN):
        i += 1

        # Checking if i is prime
        if (spf[i] == i):

            # Marking SPF for all numbers
            # divisible by i
            for j in range(i * i, MAXN, i):
                if (spf[j] == j):
                    spf[j] = i

# Function to find all the distinct prime
# factors of the given number x
def getFactorization (x):
    ret = []

    # Find the prime factors for X
    while (x != 1):

        ret.append(spf[x])

        # Find the spf[] of x
        value = spf[x]

        while (x % value == 0):
            x = x // value

    # Return the prime factors for x
    return ret

# Function to find string after flipping
# the characters at indices of prime
# factors of array elements arr[]
def flipString (S, arr, M):

    # Precalculating Smallest Prime Factor
    sieve();

    # Stores the frequency of each
    # prime factor
    frequency = [0] * MAXN

    # Iterate over all elements of
    # the array arr[]
    for i in range(0, M):

        # Stores prime factors of arr[i]
        primeFactors = getFactorization(arr[i])

        # Increment the frequency of all
        # prime factors of arr[i]
        for factors in primeFactors :
            frequency[factors] += 1
            frequency[factors] %= 2

    N = len(S)

    # Iterate over all elements of
    # the array frequency[]
    for i in range(0, MAXN):

        # If frequency[i] is odd
        if (frequency[i] & 1):

            # Flip bits of all indices
            # that are multiple of i
            for j in range(i, N + 1, i):
                S[j - 1] = ('0' if S[j - 1] == '1' else '1')

    # Return Answer
    return S

# Driver Code
S = "000000"
S = list(S)
arr = [2, 4, 6]
M = len(arr)

print("".join(flipString(S, arr, M)))

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG
{

    public static int MAXN = 100001;

    // Stores smallest prime factor
    public static int[] spf = new int[MAXN];

    // Function to find the smallest prime
    // factor for every number till MAXN
    public static void sieve()
    {
        spf[1] = 1;

        // Marking smallest prime factor for
        // every number to be itself
        for (int i = 2; i < MAXN; i++)
            spf[i] = i;

        // Separately marking spf for every
        // even number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++)
        {

            // Checking if i is prime
            if (spf[i] == i)
            {

                // Marking SPF for all numbers
                // divisible by i
                for (int j = i * i; j < MAXN; j += i)
                {
                    if (spf[j] == j)
                        spf[j] = i;
                }
            }
        }
    }

    // Function to find all the distinct prime
    // factors of the given number x
    public static List<int> getFactorization(int x)
    {
        List<int> ret = new List<int>();

        // Find the prime factors for X
        while (x != 1)
        {

            ret.Add(spf[x]);

            // Find the spf[] of x
            int value = spf[x];

            while (x % value == 0)
                x = x / value;
        }

        // Return the prime factors for x
        return ret;
    }

    // Function to find string after flipping
    // the characters at indices of prime
    // factors of array elements arr[]
    public static String flipString(String S, int[] arr, int M)
    {
        // Precalculating Smallest Prime Factor
        sieve();

        // Stores the frequency of each
        // prime factor
        int[] frequency = new int[MAXN];

        Array.Fill(frequency, 0);

        // Iterate over all elements of
        // the array arr[]
        for (int i = 0; i < M; i++)
        {

            // Stores prime factors of arr[i]
            List<int> primeFactors = getFactorization(arr[i]);

            // Increment the frequency of all
            // prime factors of arr[i]
            foreach (int factors in primeFactors)
            {
                frequency[factors]++;
                frequency[factors] %= 2;
            }
        }

        int N = S.Length;

        // Iterate over all elements of
        // the array frequency[]
        for (int i = 0; i < MAXN; i++)
        {

            // If frequency[i] is odd
            if ((frequency[i] & 1) > 0)
            {

                // Flip bits of all indices
                // that are multiple of i
                for (int j = i; j <= N; j += i)
                {

                    // S.replace(S.charAt(j - 1), (S.charAt(j - 1) == '1' ? '0' : '1'));
                    S = S.Substring(0, j - 1) + (S[j - 1] == '1' ? '0' : '1') + S.Substring(j);
                }
            }
        }

        // Return Answer
        return S;
    }

    // Driver Code
    public static void Main()
    {
        String S = "000000";
        int[] arr = { 2, 4, 6 };
        int M = arr.Length;

        Console.Write(flipString(S, arr, M));
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    const MAXN = 100001;

    // Stores smallest prime factor
    let spf = new Array(MAXN).fill(0);

    // Function to find the smallest prime
    // factor for every number till MAXN
    const sieve = () => {
        spf[1] = 1;

        // Marking smallest prime factor for
        // every number to be itself
        for (let i = 2; i < MAXN; i++)
            spf[i] = i;

        // Separately marking spf for every
        // even number as 2
        for (let i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (let i = 3; i * i < MAXN; i++) {

            // Checking if i is prime
            if (spf[i] == i) {

                // Marking SPF for all numbers
                // divisible by i
                for (let j = i * i;
                    j < MAXN; j += i) {
                    if (spf[j] == j)
                        spf[j] = i;
                }
            }
        }
    }

    // Function to find all the distinct prime
    // factors of the given number x
    const getFactorization = (x) => {
        let ret = [];

        // Find the prime factors for X
        while (x != 1) {

            ret.push(spf[x]);

            // Find the spf[] of x
            let value = spf[x];

            while (x % value == 0)
                x = parseInt(x / value);
        }

        // Return the prime factors for x
        return ret;
    }

    // Function to find string after flipping
    // the characters at indices of prime
    // factors of array elements arr[]
    const flipString = (S, arr, M) => {

        // Precalculating Smallest Prime Factor
        sieve();

        // Stores the frequency of each
        // prime factor
        let frequency = new Array(MAXN).fill(0);

        // Iterate over all elements of
        // the array arr[]
        for (let i = 0; i < M; i++) {

            // Stores prime factors of arr[i]
            let primeFactors = getFactorization(arr[i]);

            // Increment the frequency of all
            // prime factors of arr[i]
            for (let factors in primeFactors) {
                frequency[primeFactors[factors]]++;
                frequency[factors] %= 2;
            }
        }

        let N = S.length;

        // Iterate over all elements of
        // the array frequency[]
        for (let i = 0; i < MAXN; i++) {

            // If frequency[i] is odd
            if (frequency[i] & 1) {

                // Flip bits of all indices
                // that are multiple of i
                for (let j = i; j <= N; j += i) {
                    S[j - 1] = (S[j - 1] == '1' ? '0' : '1');
                }
            }
        }
        // Return Answer
        return S;
    }

    // Driver Code

    let S = "000000";
    S = S.split("");
    let arr = [2, 4, 6];
    let M = arr.length;

    document.write(flipString(S, arr, M).join(''));

    // This code is contributed by rakeshsahni
</script>
```

**Output:** 

```
011100
```

***时间复杂度:** O(N*log N + K*log K)，其中 K 是数组中* [*最大整数*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *arr[]。*
***辅助空间:** O(K)*