# 使用其索引完全划分 K 的元素的大小为 K 的所有排序子集的乘积

> 原文:[https://www . geeksforgeeks . org/product-of-all-sorted-size-子集-k-use-elements-what-index-divide-k-complete/](https://www.geeksforgeeks.org/product-of-all-sorted-subsets-of-size-k-using-elements-whose-index-divide-k-completely/)

给定一个由 **N** 个不同元素组成的整数数组 **arr[]** ，以及一个正整数 **K** ( K < = N)。任务是从给定的数组中计算大小为 K 的所有排序子集的乘积，使用索引完全除以 K 的元素。

**注意:**由于答案可能非常大，以 10^9+7.为模打印

**示例:**

> **输入:** arr[] = {4，7，5，9，3}，K = 4
> **输出:** 808556639
> **解释:**
> 在这种情况下有 5 个可能的集合:
> {4，7，5，9} - > 180(排序顺序{4，5，7，9}:索引 1，2，4 除 M，所以集合的值为 4 * 5 * 9 = 180) **3} - > 108
> {4，7，5，3} - > 84
> {7，5，9，3} - > 135
> 合计值=(180 * 108 * 108 * 84 * 135)%(10<sup>9</sup>+7)= 808556639**
> 
> **输入:** arr[] = {7，8，9}，K = 2
> **输出:** 254016

**天真方法:**

我们可以[找到大小为 K](https://www.geeksforgeeks.org/python-program-to-get-all-subsets-of-given-size-of-a-set/) 的所有子集，然后对子集进行排序，找到每个子集的值并相乘，得到最终的答案。
由于可以有 2 个 <sup>N</sup> 子集，这种方法对于大的 N 值来说效率不是很高

**有效方法:**

*   其思想不是创建所有子集来寻找答案，而是计算所有子集内每个元素的计数。如果我们找到所有子集中每个元素的计数，那么答案将是

> ![\text{Final answer} = ((arr[1]^{(\text{count of arr[1]})}) * ((arr[2]^{(\text{count of arr[2]})})* ..... *((arr[N]^{(\text{count of arr[N]})})       ](img/d96da58e59947169b29389555a6d951b.png "Rendered by QuickLaTeX.com")

*   为了找到 arr[i]的计数，我们必须找到不同子集的总数，这些子集可以通过将 arr[i]放置在将 K 完全除的每个可能的索引处而形成。

*   通过将 arr[i]放置在第 j <sup>个</sup>索引处(j 完全除 K)形成的集合数将为:

> **<sup>(小于 arr[i]的元素总数)</sup> C <sub>j-1</sub> * <sup>(大于 arr[i]的元素总数)</sup>C<sub>k-j</sub>**T10】

*   由于任何元素的计数都可能很大，所以要求(arr[I]<sup>(arr[I])</sup>)%(10<sup>9</sup>+7)我们就要用到 [**费马小定理**](https://www.geeksforgeeks.org/fermats-little-theorem/) 也就是

> { a<sup>(p-1)</sup>mod p = 1 } =>{(a<sup>x</sup>)% p =(a<sup>(x % p-1)</sup>)% p。

所以，利用费马小定理

> (arr[I]<sup>(arr[I])</sup>)%(10<sup>9</sup>+7)=>(arr[I]<sup>(arr[I]% 109+6)</sup>)%(10<sup>9</sup>+7)。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;
int p = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
long long int power(long long int x,
                    long long int y,
                    long long int p)
{
    long long int res = 1;
    x = x % p;
    while (y > 0) {

        // If y is odd, multiply
        // x with result
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
void nCr(long long int n, long long int p,
         int f[][100], int m)
{

    for (long long int i = 0; i <= n; i++) {
        for (long long int j = 0; j <= m; j++) {

            // If j>i then C(i, j) = 0
            if (j > i) {
                f[i][j] = 0;
            }

            // If iis equal to j then
            // C(i, j) = 1
            else if (j == 0 || j == i) {
                f[i][j] = 1;
            }

            else {
                f[i][j] = (f[i - 1][j]
                           + f[i - 1][j - 1])
                          % p;
            }
        }
    }
}

// Function calculate the Final answer
void ProductOfSubsets(int arr[], int n,
                      int m)
{
    int f[n + 1][100];

    nCr(n, p - 1, f, m);

    sort(arr, arr + n);

    // Initialize ans
    long long int ans = 1;

    for (long long int i = 0; i < n; i++) {

        // x is count of occurence of arr[i]
        // in different set such that index
        // of arr[i] in those sets divides
        // K completely.
        long long int x = 0;

        for (long long int j = 1; j <= m; j++) {

            // Finding the count of arr[i] by
            // placing it at index which
            // divides K completely
            if (m % j == 0) {

                // By Fermat's theorem
                x = (x
                     + (f[n - i - 1][m - j]
                        * f[i][j - 1])
                           % (p - 1))
                    % (p - 1);
            }
        }

        ans
            = ((ans * power(arr[i], x, p)) % p);
    }

    cout << ans << endl;
}

// Driver code
int main()
{

    int arr[] = { 4, 5, 7, 9, 3 };
    int K = 4;

    int N = sizeof(arr) / sizeof(arr[0]);

    ProductOfSubsets(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{
static int p = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(int x, int y, int p)
{
    int res = 1;
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
static void nCr(int n, int p,
                int f[][], int m)
{
    for(int i = 0; i <= n; i++)
    {
       for(int j = 0; j <= m; j++)
       {

          // If j>i then C(i, j) = 0
          if (j > i)
          {
              f[i][j] = 0;
          }

          // If iis equal to j then
          // C(i, j) = 1
          else if (j == 0 || j == i)
          {
              f[i][j] = 1;
          }
          else
          {
              f[i][j] = (f[i - 1][j] +
                         f[i - 1][j - 1]) % p;
          }
       }
    }
}

// Function calculate the Final answer
static void ProductOfSubsets(int arr[], int n,
                                        int m)
{
    int [][]f = new int[n + 1][100];

    nCr(n, p - 1, f, m);
    Arrays.sort(arr);

    // Initialize ans
    long ans = 1;

    for(int i = 0; i < n; i++)
    {

       // x is count of occurence of arr[i]
       // in different set such that index
       // of arr[i] in those sets divides
       // K completely.
       int x = 0;

       for(int j = 1; j <= m; j++)
       {

          // Finding the count of arr[i] by
          // placing it at index which
          // divides K completely
          if (m % j == 0)
          {

              // By Fermat's theorem
              x = (x + (f[n - i - 1][m - j] *
                        f[i][j - 1]) %
                        (p - 1)) %
                        (p - 1);
          }
       }
       ans = ((ans * power(arr[i], x, p)) % p);
    }
    System.out.print(ans + "\n");
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 4, 5, 7, 9, 3 };
    int K = 4;
    int N = arr.length;

    ProductOfSubsets(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
p = 1000000007

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p):
    res = 1
    x = x % p

    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1
        x = (x * x) % p

    return res

# Iterative Function to calculate
# (nCr)%p and save in f[n][r]
def nCr(n, p, f, m):

    for i in range(n + 1):
        for j in range(m + 1):

            # If j>i then C(i, j) = 0
            if (j > i):
                f[i][j] = 0

            # If i is equal to j then
            # C(i, j) = 1
            elif(j == 0 or j == i):
                f[i][j] = 1

            else:
                f[i][j] = (f[i - 1][j] +
                           f[i - 1][j - 1]) % p

# Function calculate the Final answer
def ProductOfSubsets(arr, n, m):

    f = [[0 for i in range(100)]
            for j in range(n + 1)]

    nCr(n, p - 1, f, m)
    arr.sort(reverse = False)

    # Initialize ans
    ans = 1

    for i in range(n):

        # x is count of occurence of arr[i]
        # in different set such that index
        # of arr[i] in those sets divides
        # K completely.
        x = 0

        for j in range(1, m + 1, 1):

            # Finding the count of arr[i] by
            # placing it at index which
            # divides K completely
            if (m % j == 0):

                # By Fermat's theorem
                x = ((x + (f[n - i - 1][m - j] *
                           f[i][j - 1]) %
                               (p - 1)) %
                               (p - 1))

        ans = ((ans * power(arr[i], x, p)) % p)

    print(ans)

# Driver code
if __name__ == '__main__':

    arr = [ 4, 5, 7, 9, 3 ]
    K = 4
    N = len(arr);

    ProductOfSubsets(arr, N, K)

# This code is contributed by samarth
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

static int p = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(int x, int y, int p)
{
    int res = 1;
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
static void nCr(int n, int p,
                int [,]f, int m)
{
    for(int i = 0; i <= n; i++)
    {
        for(int j = 0; j <= m; j++)
        {

            // If j>i then C(i, j) = 0
            if (j > i)
            {
                f[i, j] = 0;
            }

            // If iis equal to j then
            // C(i, j) = 1
            else if (j == 0 || j == i)
            {
                f[i, j] = 1;
            }
            else
            {
                f[i, j] = (f[i - 1, j] +
                           f[i - 1, j - 1]) % p;
            }
        }
    }
}

// Function calculate the Final answer
static void ProductOfSubsets(int []arr, int n,
                                        int m)
{
    int [,]f = new int[n + 1, 100];

    nCr(n, p - 1, f, m);
    Array.Sort(arr);

    // Initialize ans
    long ans = 1;

    for(int i = 0; i < n; i++)
    {

        // x is count of occurence of arr[i]
        // in different set such that index
        // of arr[i] in those sets divides
        // K completely.
        int x = 0;

        for(int j = 1; j <= m; j++)
        {

            // Finding the count of arr[i] by
            // placing it at index which
            // divides K completely
            if (m % j == 0)
            {

                // By Fermat's theorem
                x = (x + (f[n - i - 1, m - j] *
                          f[i, j - 1]) %
                              (p - 1)) %
                              (p - 1);
            }
        }
        ans = ((ans * power(arr[i], x, p)) % p);
    }
    Console.Write(ans + "\n");
}

// Driver code
public static void Main(String[] args)
{

    int []arr = { 4, 5, 7, 9, 3 };
    int K = 4;
    int N = arr.Length;

    ProductOfSubsets(arr, N, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation
// for the above approach

let p = 1000000007;

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
function nCr(n, p, f, m)
{
    for(let i = 0; i <= n; i++)
    {
       for(let j = 0; j <= m; j++)
       {

          // If j>i then C(i, j) = 0
          if (j > i)
          {
              f[i][j] = 0;
          }

          // If iis equal to j then
          // C(i, j) = 1
          else if (j == 0 || j == i)
          {
              f[i][j] = 1;
          }
          else
          {
              f[i][j] = (f[i - 1][j] +
                         f[i - 1][j - 1]) % p;
          }
       }
    }
}

// Function calculate the Final answer
function ProductOfSubsets(arr, n, m)
{
    let f = new Array(n+1);
    for (var i = 0; i < f.length; i++) {
    f[i] = new Array(2);
    }

    nCr(n, p - 1, f, m);
    arr.sort();

    // Initialize ans
    let ans = 1;

    for(let i = 0; i < n; i++)
    {

       // x is count of occurence of arr[i]
       // in different set such that index
       // of arr[i] in those sets divides
       // K completely.
       let x = 0;

       for(let j = 1; j <= m; j++)
       {

          // Finding the count of arr[i] by
          // placing it at index which
          // divides K completely
          if (m % j == 0)
          {

              // By Fermat's theorem
              x = (x + (f[n - i - 1][m - j] *
                        f[i][j - 1]) %
                        (p - 1)) %
                        (p - 1);
          }
       }
       ans = ((ans * power(arr[i], x, p)) % p);
    }
    document.write(ans + "<br/>");
}

// Driver Code

    let arr = [ 4, 5, 7, 9, 3 ];
    let K = 4;
    let N = arr.length;

    ProductOfSubsets(arr, N, K);

</script>
```

**Output:** 

```
808556639
```

***时间复杂度:** (N * K)*

***辅助空间:**O(N * 100)*T4】