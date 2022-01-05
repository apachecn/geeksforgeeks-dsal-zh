# 找出所有元素在索引处的乘积，这些索引是长度为 M 的所有可能排序子序列的 M 的因子

> 原文:[https://www . geeksforgeeks . org/find-product-of-all-elements-at-indexes-is-of-m-factors-for-all-sequed-length-m/](https://www.geeksforgeeks.org/find-product-of-all-elements-at-indexes-which-are-factors-of-m-for-all-possible-sorted-subsequences-of-length-m/)

给定一个由 **N** 个不同整数和一个正整数 **M** 组成的数组 **arr[]** ，任务是从给定的数组 **arr[]** 中找到所有元素的乘积，这些元素是长度为 **M** 的所有可能排序子序列的 **M** 的因子。
**注:**产品可能很大，取模至 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** arr[] = {4，7，5，9，3}，M = 4
> **输出:** 808556639
> **说明:**
> 有五种可能的集合。它们是:
> {4，7，5，9}。按照排序顺序，这个集合变成{4，5，7，9}。在这个集合中，索引 1、2 和 4 完全除了 M。因此，arr[1] * arr[2] * arr[4] = 4 * 5 * 9 = 180。
> 同样，其余四套及其产品为:
> {4，7，9，3} - > 108
> {4，5，9，3} - > 108
> {4，7，5，3} - > 84
> {7，5，9，3} - > 135
> 合计值=((180 * 108 * 108 * 84 * 133
> 
> **输入:** arr[] = {7，8，9}，M = 2
> T3】输出: 254016

**方法:**由于不可能找到所有集合，所以想法是统计每个元素在所需位置出现的总次数。如果找到计数，则:

> 乘积=(arr[1]<sup>arr[1]</sup>计数)*(arr[2]<sup>arr[2]</sup>计数)* …..*(逮捕人数<sup>逮捕人数</sup>

*   为了找到 arr[i]的计数，我们必须找到不同集合的总数，这些集合可以通过将 arr[i]放在每个可能的索引处(将 M 完全除)来形成。
*   因此，将**arr【I】放置在 j <sup>第</sup>T3【j 整除 m】索引处形成的集合数将为:** 

> <sup>(小于 arr[i]的元素数量)</sup> C <sub>j-1</sub> * <sup>(大于 arr[i]的元素数量)</sup> C <sub>M-j</sub>

*   由于任何元素的计数都可能很大，所以求**(arr[I]<sup>arr[I]</sup>的计数)% (10 <sup>9</sup> + 7)** ，[使用费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)。

以下是上述方法的实现:

## C++

```
// C++ program to find the product of
// all the combinations of M elements
// from an array whose index in the
// sorted order divides M completely

#include <bits/stdc++.h>
using namespace std;

typedef long long int lli;
const int m = 4;

// Iterative Function to calculate
// (x^y)%p in O(log y)
long long int power(lli x, lli y, lli p)
{
    lli res = 1;
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Iterative Function to calculate
// (nCr)%p and save in f[n][r]
// C(n, r)%p = [ C(n-1, r-1)%p + C(n-1, r)%p ] % p
// and C(n, 0) = C(n, n) = 1
void nCr(lli n, lli p, lli f[][m + 1])
{
    for (lli i = 0; i <= n; i++) {
        for (lli j = 0; j <= m; j++) {

            // If j>i then C(i, j) = 0
            if (j > i)
                f[i][j] = 0;

            // If i is equal to j then C(i, j) = 1
            else if (j == 0 || j == i)
                f[i][j] = 1;

            // C(i, j) = ( C(i-1, j) + C(i-1, j-1))%p
            else
                f[i][j] = (f[i - 1][j]
                           + f[i - 1][j - 1])
                          % p;
        }
    }
}

void operations(lli arr[], lli n, lli f[][m + 1])
{
    lli p = 1000000007;
    nCr(n, p - 1, f);

    sort(arr, arr + n);

    // Initialize the answer
    lli ans = 1;

    for (lli i = 0; i < n; i++) {

        // For every element arr[i],
        // x is count of occurrence
        // of arr[i] in different set
        // such that index of arr[i]
        // in those sets divides m completely.
        long long int x = 0;

        for (lli j = 1; j <= m; j++) {

            // Finding the count of arr[i]
            // by placing it at the index
            // which divides m completely
            if (m % j == 0)

                // Using fermat's little theorem
                x = (x
                     + (f[n - i - 1][m - j]
                        * f[i][j - 1])
                           % (p - 1))
                    % (p - 1);
        }

        // Multiplying with the count
        ans = ((ans * power(arr[i],
                            x, p))
               % p);
    }

    cout << ans << endl;
}

// Driver code
int main()
{

    lli arr[] = { 4, 5, 7, 9, 3 };

    lli n = sizeof(arr) / sizeof(arr[0]);

    lli f[n + 1][m + 1];

    operations(arr, n, f);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product of
// all the combinations of M elements
// from an array whose index in the
// sorted order divides M completely
import java.util.*;

class GFG{

static int m = 4;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static long power(long x, long y, long p)
{
    long res = 1;
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Iterative Function to calculate
// (nCr)%p and save in f[n][r]
// C(n, r)%p = [ C(n-1, r-1)%p + C(n-1, r)%p ] % p
// and C(n, 0) = C(n, n) = 1
static void nCr(int n, long p, int f[][])
{
    for(int i = 0; i <= n; i++)
    {
       for(int j = 0; j <= m; j++)
       {

          // If j>i then C(i, j) = 0
          if (j > i)
              f[i][j] = 0;

          // If i is equal to j
          // then C(i, j) = 1
          else if (j == 0 || j == i)
              f[i][j] = 1;

          // C(i, j) = ( C(i-1, j) + C(i-1, j-1))%p
          else
              f[i][j] = (f[i - 1][j] +
                         f[i - 1][j - 1]) % (int)p;
       }
    }
}

static void operations(int arr[], int n, int f[][])
{
    long p = 1000000007;
    nCr(n, p - 1, f);

    Arrays.sort(arr);

    // Initialize the answer
    long ans = 1;

    for(int i = 0; i < n; i++)
    {

       // For every element arr[i],
       // x is count of occurrence
       // of arr[i] in different set
       // such that index of arr[i]
       // in those sets divides m
       // completely.
       long x = 0;

       for(int j = 1; j <= m; j++)
       {

          // Finding the count of arr[i]
          // by placing it at the index
          // which divides m completely
          if (m % j == 0)

              // Using fermat's little theorem
              x = (x + (f[n - i - 1][m - j] *
                               f[i][j - 1]) %
                                   (p - 1)) %
                                   (p - 1);
       }

       // Multiplying with the count
       ans = ((ans * power(arr[i], x, p)) % p);
    }
    System.out.print(ans + "\n");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 7, 9, 3 };
    int n = arr.length;
    int [][]f = new int[n + 1][m + 1];

    operations(arr, n, f);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to find the product of
# all the combinations of M elements
# from an array whose index in the
# sorted order divides M completely
m = 4

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):

    res = 1
    x = x % p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1
        x = (x * x) % p
    return res

# Iterative Function to calculate
# (nCr)%p and save in f[n][r]
# C(n, r)%p = [ C(n-1, r-1)%p +
# C(n-1, r)%p ] % p
# and C(n, 0) = C(n, n) = 1
def nCr(n, p, f):

    for i in range (n):
        for j in range (m + 1):

            # If j>i then C(i, j) = 0
            if (j > i):
                f[i][j] = 0

            # If i is equal to j then
            # C(i, j) = 1
            elif (j == 0 or j == i):
                f[i][j] = 1

            # C(i, j) = ( C(i-1, j) +
            # C(i-1, j-1))%p
            else:
                f[i][j] = ((f[i - 1][j] +
                            f[i - 1][j - 1]) % p)

def operations(arr, n, f):

    p = 1000000007
    nCr(n, p - 1, f)

    arr.sort()

    # Initialize the answer
    ans = 1

    for i in range (n):

        # For every element arr[i],
        # x is count of occurrence
        # of arr[i] in different set
        # such that index of arr[i]
        # in those sets divides m completely.
        x = 0

        for j in range (1, m + 1):

            # Finding the count of arr[i]
            # by placing it at the index
            # which divides m completely
            if (m % j == 0):

                # Using fermat's little theorem
                x = ((x + (f[n - i - 1][m - j] *
                           f[i][j - 1]) % (p - 1)) %
                                          (p - 1))

        # Multiplying with the count
        ans = ((ans * power(arr[i],
                            x, p)) % p)

    print (ans)

# Driver code
if __name__ == "__main__":
    arr = [4, 5, 7, 9, 3]
    n = len(arr)
    f = [[0 for x in range (m + 1)]
            for y in range (n + 1)]
    operations(arr, n, f)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the product of
// all the combinations of M elements
// from an array whose index in the
// sorted order divides M completely
using System;

class GFG{

static int m = 4;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static long power(long x, long y, long p)
{
    long res = 1;
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Iterative Function to calculate
// (nCr)%p and save in f[n,r]
// C(n, r)%p = [ C(n-1, r-1)%p + C(n-1, r)%p ] % p
// and C(n, 0) = C(n, n) = 1
static void nCr(int n, long p, int [,]f)
{
    for(int i = 0; i <= n; i++)
    {
       for(int j = 0; j <= m; j++)
       {

          // If j>i then C(i, j) = 0
          if (j > i)
              f[i, j] = 0;

          // If i is equal to j
          // then C(i, j) = 1
          else if (j == 0 || j == i)
              f[i, j] = 1;

          // C(i, j) = ( C(i-1, j) + C(i-1, j-1))%p
          else
              f[i, j] = (f[i - 1, j] +
                         f[i - 1, j - 1]) % (int)p;
       }
    }
}

static void operations(int []arr, int n, int [,]f)
{
    long p = 1000000007;
    nCr(n, p - 1, f);

    Array.Sort(arr);

    // Initialize the answer
    long ans = 1;

    for(int i = 0; i < n; i++)
    {

       // For every element arr[i],
       // x is count of occurrence
       // of arr[i] in different set
       // such that index of arr[i]
       // in those sets divides m
       // completely.
       long x = 0;
       for(int j = 1; j <= m; j++)
       {

          // Finding the count of arr[i]
          // by placing it at the index
          // which divides m completely
          if (m % j == 0)

              // Using fermat's little theorem
              x = (x + (f[n - i - 1, m - j] *
                               f[i, j - 1]) %
                                   (p - 1)) %
                                   (p - 1);
       }

       // Multiplying with the count
       ans = ((ans * power(arr[i], x, p)) % p);
    }
    Console.Write(ans + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 5, 7, 9, 3 };
    int n = arr.Length;
    int [,]f = new int[n + 1, m + 1];

    operations(arr, n, f);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to find the product of
// all the combinations of M elements
// from an array whose index in the
// sorted order divides M completely
let m = 4;

// Iterative Function to calculate
// (x^y)%p in O(log y)
function power(x, y, p)
{
    let res = 1;
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if (y % 2 == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Iterative Function to calculate
// (nCr)%p and save in f[n][r]
// C(n, r)%p = [ C(n-1, r-1)%p + C(n-1, r)%p ] % p
// and C(n, 0) = C(n, n) = 1
function nCr(n, p, f)
{
    for(let i = 0; i <= n; i++)
    {
       for(let j = 0; j <= m; j++)
       {

          // If j>i then C(i, j) = 0
          if (j > i)
              f[i][j] = 0;

          // If i is equal to j
          // then C(i, j) = 1
          else if (j == 0 || j == i)
              f[i][j] = 1;

          // C(i, j) = ( C(i-1, j) + C(i-1, j-1))%p
          else
              f[i][j] = (f[i - 1][j] +
                         f[i - 1][j - 1]) % p;
       }
    }
}

function operations(arr, n, f)
{
    let p = 1000000007;
    nCr(n, p - 1, f);

    arr.sort();

    // Initialize the answer
    let ans = 1;

    for(let i = 0; i < n; i++)
    {

       // For every element arr[i],
       // x is count of occurrence
       // of arr[i] in different set
       // such that index of arr[i]
       // in those sets divides m
       // completely.
       let x = 0;

       for(let j = 1; j <= m; j++)
       {

          // Finding the count of arr[i]
          // by placing it at the index
          // which divides m completely
          if (m % j == 0)

              // Using fermat's little theorem
              x = (x + (f[n - i - 1][m - j] *
                                f[i][j - 1]) %
                                    (p - 1)) %
                                    (p - 1);
       }

       // Multiplying with the count
       ans = ((ans * power(arr[i], x, p)) % p);
    }
    document.write(ans + "\n");
}

// Driver Code
let arr = [ 4, 5, 7, 9, 3 ];
let n = arr.length;
let f = new Array(n + 1);

for(var i = 0; i < f.length; i++)
{
    f[i] = new Array(2);
}

operations(arr, n, f);

// This code is contributed by target_2

</script>
```

**Output:** 

```
808556639
```

**时间复杂度:** *O(N * M)* 其中 N 为数组长度，M 由用户给出。

**辅助空间:**T2【O(N * M)