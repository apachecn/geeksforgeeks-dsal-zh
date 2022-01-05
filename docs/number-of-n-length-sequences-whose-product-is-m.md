# 乘积为 M 的 N 个长度序列的数目

> 原文:[https://www . geeksforgeeks . org/number-of-n-length-sequence-who-product-is-m/](https://www.geeksforgeeks.org/number-of-n-length-sequences-whose-product-is-m/)

给定两个整数 **N** 和 **M** ，任务是找出长度为 **N** 的可能序列 a <sub>1</sub> ，a <sub>2</sub> ，使得序列的所有元素的乘积为 **M** 。
**示例:**

> **输入:** N = 2，M = 6
> **输出:** 4
> 可能的序列有{1，6}、{2，3}、{3，2}和{6，1}
> **输入:** N = 3，M = 24
> **输出:** 30

**进场:**

*   将 **M** 的主因子分解为**p<sub>1</sub>T5】k<sub>T8】1T10】p<sub>2</sub>T13】kT15<sup>2</sup>T18】…p<sub>z</sub>T21】kT23<sup>z</sup>T26</sub>**。
*   对于每个质因数，其指数必须分布在不同的组中，因为在乘以那些 T2 项时，质因数的指数将相加。这可以使用这里[解释的公式](https://www.geeksforgeeks.org/number-of-ways-of-distributing-n-identical-objects-in-r-distinct-groups/)来完成。
*   对于每个质因数，其指数在 **N** 序列中的分布方式的数量将等于每 **1 ≤ i ≤ z** 的
    **<sup>N+K</sup><sub><sup>I</sup></sub><sup>-1</sup>C<sub>N-1</sub>**。
*   利用乘法的基本原理，将所有质因数的结果相乘得到答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// value of ncr effectively
int ncr(int n, int r)
{

    // Initializing the result
    int res = 1;

    for (int i = 1; i <= r; i += 1) {

        // Multiply and divide simultaneously
        // to avoid overflow
        res *= (n - r + i);
        res /= i;
    }

    // Return the answer
    return res;
}

// Function to return the number of sequences
// of length N such that their product is M
int NoofSequences(int N, int M)
{

    // Hashmap to store the prime factors of M
    unordered_map<int, int> prime;

    // Calculate the prime factors of M
    for (int i = 2; i <= sqrt(M); i += 1) {

        // If i divides M it means it is a factor
        // Divide M by i till it could be
        // divided to store the exponent
        while (M % i == 0) {

            // Increase the exponent count
            prime[i] += 1;
            M /= i;
        }
    }

    // If the number is a prime number
    // greater than sqrt(M)
    if (M > 1) {
        prime[M] += 1;
    }

    // Initializing the ans
    int ans = 1;

    // Multiply the answer for every prime factor
    for (auto it : prime) {

        // it.second represents the
        // exponent of every prime factor
        ans *= (ncr(N + it.second - 1, N - 1));
    }

    // Return the result
    return ans;
}

// Driver code
int main()
{
    int N = 2, M = 6;

    cout << NoofSequences(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.HashMap;

class geeks
{

    // Function to calculate the
    // value of ncr effectively
    public static int nCr(int n, int r)
    {

        // Initializing the result
        int res = 1;
        for (int i = 1; i <= r; i++)
        {

            // Multiply and divide simultaneously
            // to avoid overflow
            res *= (n - r + i);
            res /= i;
        }

        // Return the answer
        return res;
    }

    // Function to return the number of sequences
    // of length N such that their product is M
    public static int NoofSequences(int N, int M)
    {

        // Hashmap to store the prime factors of M
        HashMap<Integer, Integer> prime = new HashMap<>();

        // Calculate the prime factors of M
        for (int i = 2; i <= Math.sqrt(M); i++)
        {

            // If i divides M it means it is a factor
            // Divide M by i till it could be
            // divided to store the exponent
            while (M % i == 0)
            {

                // Increase the exponent count
                if (prime.get(i) == null)
                    prime.put(i, 1);
                else
                {
                    int x = prime.get(i);
                    prime.put(i, ++x);
                }
                M /= i;
            }
        }

        // If the number is a prime number
        // greater than sqrt(M)
        if (M > 1)
        {
            if (prime.get(M) != null)
            {
                int x = prime.get(M);
                prime.put(M, ++x);
            }
            else
                prime.put(M, 1);
        }

        // Initializing the ans
        int ans = 1;

        // Multiply the answer for every prime factor
        for (HashMap.Entry<Integer, Integer> entry : prime.entrySet())
        {

            // entry.getValue() represents the
            // exponent of every prime factor
            ans *= (nCr(N + entry.getValue() - 1, N - 1));
        }

        // Return the result
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 2, M = 6;
        System.out.println(NoofSequences(N, M));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to calculate the
# value of ncr effectively
def ncr(n, r):

    # Initializing the result
    res = 1

    for i in range(1,r+1):

        # Multiply and divide simultaneously
        # to avoid overflow
        res *= (n - r + i)
        res //= i

    # Return the answer
    return res

# Function to return the number of sequences
# of length N such that their product is M
def NoofSequences(N, M):

    # Hashmap to store the prime factors of M
    prime={}

    # Calculate the prime factors of M
    for i in range(2,int(M**(.5))+1):

        # If i divides M it means it is a factor
        # Divide M by i till it could be
        # divided to store the exponent
        while (M % i == 0):

            # Increase the exponent count
            prime[i]= prime.get(i,0)+1
            M //= i

    # If the number is a prime number
    # greater than sqrt(M)
    if (M > 1):
        prime[M] =prime.get(M,0) + 1

    # Initializing the ans
    ans = 1

    # Multiply the answer for every prime factor
    for it in prime:

        # it.second represents the
        # exponent of every prime factor
        ans *= (ncr(N + prime[it] - 1, N - 1))

    # Return the result
    return ans

# Driver code

N = 2
M = 6

print(NoofSequences(N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

public class geeks
{

    // Function to calculate the
    // value of ncr effectively
    public static int nCr(int n, int r)
    {

        // Initializing the result
        int res = 1;
        for (int i = 1; i <= r; i++)
        {

            // Multiply and divide simultaneously
            // to avoid overflow
            res *= (n - r + i);
            res /= i;
        }

        // Return the answer
        return res;
    }

    // Function to return the number of sequences
    // of length N such that their product is M
    public static int NoofSequences(int N, int M)
    {

        // Hashmap to store the prime factors of M
        Dictionary<int,int>prime = new Dictionary<int,int>();

        // Calculate the prime factors of M
        for (int i = 2; i <= Math.Sqrt(M); i++)
        {

            // If i divides M it means it is a factor
            // Divide M by i till it could be
            // divided to store the exponent
            while (M % i == 0)
            {

                // Increase the exponent count
                if (!prime.ContainsKey(i))
                    prime.Add(i, 1);
                else
                {
                    int x = prime[i];
                    prime.Remove(i);
                    prime.Add(i, ++x);
                }
                M /= i;
            }
        }

        // If the number is a prime number
        // greater than sqrt(M)
        if (M > 1)
        {
            if (prime.ContainsKey(M))
            {
                int x = prime[M];
                prime.Remove(M);
                prime.Add(M, ++x);
            }
            else
                prime.Add(M, 1);
        }

        // Initializing the ans
        int ans = 1;

        // Multiply the answer for every prime factor
        foreach(KeyValuePair<int, int> entry in prime)
        {

            // entry.getValue() represents the
            // exponent of every prime factor
            ans *= (nCr(N + entry.Value - 1, N - 1));
        }

        // Return the result
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 2, M = 6;
        Console.WriteLine(NoofSequences(N, M));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to calculate the
    // value of ncr effectively
    function nCr(n,r)
    {
        // Initializing the result
        let res = 1;
        for (let i = 1; i <= r; i++)
        {

            // Multiply and divide simultaneously
            // to avoid overflow
            res *= (n - r + i);
            res =Math.floor(res/ i);
        }

        // Return the answer
        return res;
    }

    // Function to return the number of sequences
    // of length N such that their product is M
    function NoofSequences(N,M)
    {
        // Hashmap to store the prime factors of M
        let prime = new Map();

        // Calculate the prime factors of M
        for (let i = 2; i <= Math.sqrt(M); i++)
        {

            // If i divides M it means it is a factor
            // Divide M by i till it could be
            // divided to store the exponent
            while (M % i == 0)
            {

                // Increase the exponent count
                if (prime.get(i) == null)
                    prime.set(i, 1);
                else
                {
                    let x = prime.get(i);
                    prime.set(i, ++x);
                }
                M = Math.floor(M/i);
            }
        }

        // If the number is a prime number
        // greater than sqrt(M)
        if (M > 1)
        {
            if (prime.get(M) != null)
            {
                let x = prime.get(M);
                prime.set(M, ++x);
            }
            else
                prime.set(M, 1);
        }

        // Initializing the ans
        let ans = 1;

        // Multiply the answer for every prime factor
        for (let [key, value] of prime.entries())
        {

            // entry.getValue() represents the
            // exponent of every prime factor
            ans *= (nCr(N + value - 1, N - 1));
        }

        // Return the result
        return ans;
    }

    // Driver code
    let N = 2, M = 6;
    document.write(NoofSequences(N, M));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
4
```