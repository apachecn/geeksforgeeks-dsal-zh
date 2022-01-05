# 除了最小和最大元素之外，大小为 K 的所有子序列的乘积

> 原文:[https://www . geeksforgeeks . org/除最小和最大元素之外的所有 k 大小子序列的乘积/](https://www.geeksforgeeks.org/product-of-all-subsequences-of-size-k-except-the-minimum-and-maximum-elements/)

给定一个包含 **N** 元素和一个整数 **K** 的数组**[]**。任务是计算大小为 K 的子序列的所有元素的乘积，除了每个子序列的最小和最大元素。
**注**:由于答案可能会很大，所以将最终答案打印为 *10 <sup>9</sup> + 7* 的 mod。

**示例:**

```
Input : arr[] = {1, 2, 3 4}, K = 3
Output : 36
*Subsequences of length 3 are*:
{1, 2, 3}, {1, 2, 4}, {1, 3, 4}, {2, 3, 4}
Excluding minimum and maximum elements from 
each of the above subsequences, product will be:
*(2 * 2 * 3 * 3) = 36*.

Input : arr[] = {10, 5, 16, 6}, k=3
Output : 3600 
```

**天真方法:**一个简单的方法是逐个生成所有可能的子序列，然后将除最大值和最小值之外的所有元素相乘，并进一步将所有元素相乘。因为总共会有**<sup>【n】</sup>C<sub>【K】</sub>**个子序列，所有子序列都有 K-2 个元素需要相乘，这是一项繁琐的工作。

**高效方法:**想法是首先对数组进行排序，因为我们是否考虑子序列或子集并不重要。
现在逐一统计每个元素的出现次数。
总的来说，一个数可以出现在**<sup>(n-1)</sup>C<sub>(K-1)</sub>**子序列中，其中**<sup>(I)</sup>C<sub>(K-1)</sub>**次作为最大元素出现，而**<sup>(n-I-1)</sup>C<sub>(K-1)【T20 T21】次作为最小元素出现
因此，总共会出现![i^{th} ](img/7ae0fdec52f16e041d8a940d62ebd69a.png "Rendered by QuickLaTeX.com")元素:</sub>** 

```
<sup>(n-1)C</sup><sub><sup>(K-1)</sup></sub>  - <sup>(i)C</sup><sub><sup>(K-1)</sup></sub> - <sup>(n-i-1)C</sup><sub><sup>(K-1)</sup></sub> times. (let's say it x)
```

所以，首先我们要计算每个元素 a[i]的 x，然后乘以 a[i] x 倍。即(![a[i]^x mod(10^9 + 7)  ](img/3cc95b527e37686cc48bfea022a813b8.png "Rendered by QuickLaTeX.com"))。
既然，对于大型阵列来说计算这个太难了，那么我们就用[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)。

下面是上述方法的实现:

## C++

```
// C++ program to find product of all
// Subsequences of size K except the
// minimum and maximum Elements

#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

#define ll long long

#define max 101

// 2D array to store value of
// combinations nCr
ll C[max - 1][max - 1];

ll power(ll x, unsigned ll y)
{
    unsigned ll res = 1;
    x = x % MOD;
    while (y > 0) {
        if (y & 1) {
            res = (res * x) % MOD;
        }

        y = y >> 1;
        x = (x * x) % MOD;
    }
    return res % MOD;
}

// Function to pre-calculate value of all
// combinations nCr
void combi(int n, int k)
{
    int i, j;

    for (i = 0; i <= n; i++) {
        for (j = 0; j <= min(i, k); j++) {
            if (j == 0 || j == i)
                C[i][j] = 1;
            else
                C[i][j] = (C[i - 1][j - 1] % MOD
                            + C[i - 1][j] % MOD) % MOD;
        }
    }
}

// Function to calculate product of all subsequences
// except the minimum and maximum elements
unsigned ll product(ll a[], int n, int k)
{
    unsigned ll ans = 1;

    // Sorting array so that it becomes easy
    // to calculate the number of times an
    // element will come in first or last place
    sort(a, a + n);

    // An element will occur 'powa' times in total
    // of which 'powla' times it will be last element
    // and 'powfa' times it will be first element
    ll powa = C[n - 1][k - 1];

    for (int i = 0; i < n; i++) {
        ll powla = C[i][k - 1];
        ll powfa = C[n - i - 1][k - 1];

        // In total it will come
        // powe = powa-powla-powfa times
        ll powe = ((powa % MOD) - (powla + powfa) % MOD + MOD) % MOD;

        // Multiplying a[i] powe times using
        // Fermat Little Theorem under MODulo
        // MOD for fast exponentiation
        unsigned ll mul = power(a[i], powe) % MOD;
        ans = ((ans % MOD) * (mul % MOD)) % MOD;
    }

    return ans % MOD;
}

// Driver Code
int main()
{
    // pre-calculation of all combinations
    combi(100, 100);

    ll arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof arr[0];
    int k = 3;

    unsigned ll ans = product(arr, n, k);

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of all
// Subsequences of size K except the
// minimum and maximum Elements
import java.util.Arrays;

class GFG
{

static int MOD= 1000000007;
static int max =101;

// 2D array to store value of
// combinations nCr
static long C[][] = new long[max ][max];

static long power(long x, long y)
{
    long res = 1;
    x = x % MOD;
    while (y > 0)
    {
        if (y % 2== 1)
        {
            res = (res * x) % MOD;
        }

        y = y >> 1;
        x = (x * x) % MOD;
    }
    return res % MOD;
}

// Function to pre-calculate value of all
// combinations nCr
static void combi(int n, int k)
{
    int i, j;

    for (i = 0; i <= n; i++)
    {
        for (j = 0; j <= Math.min(i, k); j++)
        {
            if (j == 0 || j == i)
                C[i][j] = 1;
            else
                C[i][j] = (C[i - 1][j - 1] % MOD
                            + C[i - 1][j] % MOD) % MOD;
        }
    }
}

// Function to calculate product of all subsequences
// except the minimum and maximum elements
static long product(long a[], int n, int k)
{
    long ans = 1;

    // Sorting array so that it becomes easy
    // to calculate the number of times an
    // element will come in first or last place
    Arrays.sort(a);

    // An element will occur 'powa' times in total
    // of which 'powla' times it will be last element
    // and 'powfa' times it will be first element
    long powa = C[n - 1][k - 1];

    for (int i = 0; i < n; i++)
    {
        long powla = C[i][k - 1];
        long powfa = C[n - i - 1][k - 1];

        // In total it will come
        // powe = powa-powla-powfa times
        long powe = ((powa % MOD) - (powla + powfa) % MOD + MOD) % MOD;

        // Multiplying a[i] powe times using
        // Fermat Little Theorem under MODulo
        // MOD for fast exponentiation
        long mul = power(a[i], powe) % MOD;
        ans = ((ans % MOD) * (mul % MOD)) % MOD;
    }

    return ans % MOD;
}

// Driver Code
public static void main(String[] args)
{
    // pre-calculation of all combinations
    combi(100, 100);

    long arr[] = { 1, 2, 3, 4 };
    int n = arr.length;
    int k = 3;

    long ans = product(arr, n, k);

    System.out.println(ans);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 program to find product of all
# Subsequences of size K except the
# minimum and maximum Elements

MOD = 1000000007

max = 101

# 2D array to store value of
# combinations nCr
C = [[0 for i in range(max)] for j in range(max)]

def power(x,y):
    res = 1
    x = x % MOD
    while (y > 0):
        if (y & 1):
            res = (res * x) % MOD

        y = y >> 1
        x = (x * x) % MOD

    return res % MOD

# Function to pre-calculate value of all
# combinations nCr
def combi(n, k):
    for i in range(n + 1):
        for j in range(min(i, k) + 1):
            if (j == 0 or j == i):
                C[i][j] = 1
            else:
                C[i][j] = (C[i - 1][j - 1] % MOD +
                            C[i - 1][j] % MOD) % MOD

# Function to calculate product of all subsequences
# except the minimum and maximum elements
def product(a, n, k):
    ans = 1

    # Sorting array so that it becomes easy
    # to calculate the number of times an
    # element will come in first or last place
    a.sort(reverse = False)

    # An element will occur 'powa' times in total
    # of which 'powla' times it will be last element
    # and 'powfa' times it will be first element
    powa = C[n - 1][k - 1]

    for i in range(n):
        powla = C[i][k - 1]
        powfa = C[n - i - 1][k - 1]

        # In total it will come
        # powe = powa-powla-powfa times
        powe = ((powa % MOD) - (powla + powfa) % MOD + MOD) % MOD

        # Multiplying a[i] powe times using
        # Fermat Little Theorem under MODulo
        # MOD for fast exponentiation
        mul = power(a[i], powe) % MOD
        ans = ((ans % MOD) * (mul % MOD)) % MOD

    return ans % MOD

# Driver Code
if __name__ == '__main__':
    # pre-calculation of all combinations
    combi(100, 100)

    arr = [1, 2, 3, 4]
    n = len(arr)
    k = 3

    ans = product(arr, n, k)
    print(ans)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find product of all
// Subsequences of size K except the
// minimum and maximum Elements
using System;

class GFG
{
static int MOD = 1000000007;
static int max = 101;

// 2D array to store value of
// combinations nCr
static long [,]C = new long[max, max];

static long power(long x, long y)
{
    long res = 1;
    x = x % MOD;
    while (y > 0)
    {
        if (y % 2 == 1)
        {
            res = (res * x) % MOD;
        }

        y = y >> 1;
        x = (x * x) % MOD;
    }
    return res % MOD;
}

// Function to pre-calculate value
// of all combinations nCr
static void combi(int n, int k)
{
    int i, j;

    for (i = 0; i <= n; i++)
    {
        for (j = 0;
             j <= Math.Min(i, k); j++)
        {
            if (j == 0 || j == i)
                C[i, j] = 1;
            else
                C[i, j] = (C[i - 1, j - 1] % MOD +
                           C[i - 1, j] % MOD) % MOD;
        }
    }
}

// Function to calculate product of
// all subsequences except
// the minimum and maximum elements
static long product(long []a, int n, int k)
{
    long ans = 1;

    // Sorting array so that it becomes easy
    // to calculate the number of times an
    // element will come in first or last place
    Array.Sort(a);

    // An element will occur 'powa' times
    // in total of which 'powla' times it
    // will be last element and 'powfa' times
    // it will be first element
    long powa = C[n - 1, k - 1];

    for (int i = 0; i < n; i++)
    {
        long powla = C[i, k - 1];
        long powfa = C[n - i - 1, k - 1];

        // In total it will come
        // powe = powa-powla-powfa times
        long powe = ((powa % MOD) -    
                     (powla + powfa) %
                      MOD + MOD) % MOD;

        // Multiplying a[i] powe times using
        // Fermat Little Theorem under MODulo
        // MOD for fast exponentiation
        long mul = power(a[i], powe) % MOD;
        ans = ((ans % MOD) *
               (mul % MOD)) % MOD;
    }

    return ans % MOD;
}

// Driver Code
static public void Main ()
{
    // pre-calculation of all combinations
    combi(100, 100);

    long []arr = { 1, 2, 3, 4 };
    int n = arr.Length;
    int k = 3;

    long ans = product(arr, n, k);

    Console.WriteLine(ans);
}
}

// This code contributed by ajit
```

## java 描述语言

```
<script>
    // Javascript program to find product of all
    // Subsequences of size K except the
    // minimum and maximum Elements

    let MOD= 1000000007;
    let max =101;

    // 2D array to store value of
    // combinations nCr
    let C = new Array(max);

    for(let i = 0; i < max; i++)
    {
        C[i] = new Array(max);
        for(let j = 0; j < max; j++)
        {
            C[i][j] = 0;
        }
    }

    function power(x, y)
    {
        let res = 1;
        x = x % MOD;
        while (y > 0)
        {
            if (y % 2== 1)
            {
                res = (res * x) % MOD;
            }

            y = y >> 1;
            x = (x * x) % MOD;
        }
        return res % MOD;
    }

    // Function to pre-calculate value of all
    // combinations nCr
    function combi(n, k)
    {
        let i, j;

        for (i = 0; i <= n; i++)
        {
            for (j = 0; j <= Math.min(i, k); j++)
            {
                if (j == 0 || j == i)
                    C[i][j] = 1;
                else
                    C[i][j] = (C[i - 1][j - 1] % MOD
                                + C[i - 1][j] % MOD) % MOD;
            }
        }
    }

    // Function to calculate product of all subsequences
    // except the minimum and maximum elements
    function product(a, n, k)
    {
        let ans = 1;

        // Sorting array so that it becomes easy
        // to calculate the number of times an
        // element will come in first or last place
        a.sort(function(a, b){return a - b});

        // An element will occur 'powa' times in total
        // of which 'powla' times it will be last element
        // and 'powfa' times it will be first element
        let powa = C[n - 1][k - 1];

        for (let i = 0; i < n; i++)
        {
            let powla = C[i][k - 1];
            let powfa = C[n - i - 1][k - 1];

            // In total it will come
            // powe = powa-powla-powfa times
            let powe = ((powa % MOD) - (powla + powfa) % MOD + MOD) % MOD;

            // Multiplying a[i] powe times using
            // Fermat Little Theorem under MODulo
            // MOD for fast exponentiation
            let mul = power(a[i], powe) % MOD;
            ans = ((ans % MOD) * (mul % MOD)) % MOD;
        }

        return ans % MOD;
    }

    // pre-calculation of all combinations
    combi(100, 100);

    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;
    let k = 3;

    let ans = product(arr, n, k);

    document.write(ans);

</script>
```

**Output:** 

```
36
```