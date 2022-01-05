# 生成具有两个给定阵列卷积的阵列的程序

> 原文:[https://www . geeksforgeeks . org/生成具有两个给定数组卷积的数组的程序/](https://www.geeksforgeeks.org/program-to-generate-an-array-having-convolution-of-two-given-arrays/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是构造一个大小为**(N+M–1)**的卷积数组 **C[]** 。

> **2** 数组的卷积定义为每一个 **i** 和 **j** 的 **C[i + j] = ∑(a[i] * b[j])** 。

***注:**如果任一指标的值变得很大，则打印至* [***取模 998244353***](https://www.geeksforgeeks.org/find-the-value-of-p-and-modular-inverse-of-q-modulo-998244353/) *。*

**示例:**

> **输入:** A[] = {1，2，3，4}，B[] = {5，6，7，8，9}
> **输出:** {5，16，34，60，70，70，59，36}
> **说明:**
> 阵的大小，C[]= N+M–1 = 8。
> C[0]= A[0]* B[0]= 1 * 5 = 5
> C[1]= A[0]* B[1]+A[1]* B[0]= 1 * 6+2 * 5 = 16
> C[2]= A[0]* B[2]+A[1]* B[1]+A[2]* B[0]= 1 * 7+2 * 6+3 * 5 = 34
> 同样，C[3]
> 
> **输入:** A[] = {10000000}，B[] = {10000000}
> **输出:** {871938225}
> **说明:**
> 数组大小，C[]= N+M–1 = 1。
> C[0]= A[0]* B[0]=(10000000 * 1000000)% 998244353 = 871938225

**天真方法:**在卷积数组中，每个项**C[I+j]=(a[I]* b[j])% 998244353**。因此，最简单的方法是[使用](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[两个嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)对数组 **A[]** 和 **B[]** 进行迭代，以找到最终的卷积数组 **C[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
constexpr int MOD = 998244353;

// Function to generate a convolution
// array of two given arrays
void findConvolution(const vector<int>& a,
                     const vector<int>& b)
{
    // Stores the size of arrays
    int n = a.size(), m = b.size();

    // Stores the final array
    vector<long long> c(n + m - 1);

    // Traverse the two given arrays
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {

              // Update the convolution array
            c[i + j] += 1LL*(a[i] * b[j]) % MOD;
        }
    }

    // Print the convolution array c[]
    for (int k = 0; k < c.size(); ++k) {
        c[k] %= MOD;
        cout << c[k] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> A = { 1, 2, 3, 4 };
    vector<int> B = { 5, 6, 7, 8, 9 };

    findConvolution(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int MOD = 998244353;

// Function to generate a convolution
// array of two given arrays
static void findConvolution(int[] a,
                            int[] b)
{

    // Stores the size of arrays
    int n = a.length, m = b.length;

    // Stores the final array
    int[] c = new int[(n + m - 1)];

    // Traverse the two given arrays
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {

            // Update the convolution array
            c[i + j] += (a[i] * b[j]) % MOD;
        }
    }

    // Print the convolution array c[]
    for(int k = 0; k < c.length; ++k)
    {
        c[k] %= MOD;
        System.out.print(c[k] + " ");
    }
}

// Driver Code
public static void main(String args[])
{
    int[] A = { 1, 2, 3, 4 };
    int[] B = { 5, 6, 7, 8, 9 };

    findConvolution(A, B);}
}

// This code is contributed by souravghosh0416
```

## 蟒蛇 3

```
# Python3 program for the above approach
MOD = 998244353

# Function to generate a convolution
# array of two given arrays
def findConvolution(a, b):

    global MOD

    # Stores the size of arrays
    n, m = len(a), len(b)

    # Stores the final array
    c = [0] * (n + m - 1)

    # Traverse the two given arrays
    for i in range(n):
        for j in range(m):

            # Update the convolution array
            c[i + j] += (a[i] * b[j]) % MOD

    # Print the convolution array c[]
    for k in range(len(c)):
        c[k] %= MOD
        print(c[k], end = " ")

# Driver Code
if __name__ == '__main__':

    A = [1, 2, 3, 4]
    B = [5, 6, 7, 8, 9]

    findConvolution(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{
 static int MOD = 998244353;

// Function to generate a convolution
// array of two given arrays
static void findConvolution(int[] a,
                    int[] b)
{

    // Stores the size of arrays
    int n = a.Length, m = b.Length;

    // Stores the final array
    int[] c = new int[(n + m - 1)];

    // Traverse the two given arrays
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {

              // Update the convolution array
            c[i + j] += (a[i] * b[j]) % MOD;
        }
    }

    // Print the convolution array c[]
    for (int k = 0; k < c.Length; ++k) {
        c[k] %= MOD;
        Console.Write(c[k] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int[] A = { 1, 2, 3, 4 };
    int[] B = { 5, 6, 7, 8, 9 };

    findConvolution(A, B);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let MOD = 998244353;

// Function to generate a convolution
// array of two given arrays
function findConvolution(a, b)
{

    // Stores the size of arrays
    let n = a.length, m = b.length;

    // Stores the final array
    let c = [];
    for(let i = 0; i < n + m - 1; ++i)
    {
        c[i] = 0;
    }

    // Traverse the two given arrays
    for(let i = 0; i < n; ++i)
    {
        for(let j = 0; j < m; ++j)
        {

            // Update the convolution array
            c[i + j] += (a[i] * b[j]) % MOD;
        }
    }

    // Print the convolution array c[]
    for(let k = 0; k < c.length; ++k)
    {
        c[k] %= MOD;
        document.write(c[k] + " ");
    }
}

// Driver Code

    let A = [ 1, 2, 3, 4 ];
    let B = [ 5, 6, 7, 8, 9 ];

    findConvolution(A, B);

</script>
```

**Output:** 

```
5 16 34 60 70 70 59 36
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N+M)*

**高效方法:**优化上述方法，思路是使用[数论变换](https://www.geeksforgeeks.org/python-number-theoretic-transformation/) ( **NTT** )类似于[快速傅里叶变换(FFT)进行多项式乘法](https://www.geeksforgeeks.org/iterative-fast-fourier-transformation-polynomial-multiplication/)，可以在模运算下工作。这个问题可以通过使用相同的概念**迭代快速傅立叶变换**在给定的数组上执行 **NTT** 来解决，因为相同的属性适用于[模运算](https://www.geeksforgeeks.org/modular-arithmetic/)中的第 **N <sup>个</sup>单位根**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long

const ll mod = 998244353, maxn = 3e6;
ll a[maxn], b[maxn];

// Iterative FFT function to compute
// the DFT of given coefficient vector
void fft(ll w0, ll n, ll* a)
{
    // Do bit reversal of the given array
    for (ll i = 0, j = 0; i < n; i++) {

        // Swap a[i] and a[j]
        if (i < j)
            swap(a[i], a[j]);

        // Right Shift N by 1
        ll bit = n >> 1;

        for (; j & bit; bit >>= 1)
            j ^= bit;
        j ^= bit;
    }

    // Perform the iterative FFT
    for (ll len = 2; len <= n; len <<= 1) {

        ll wlen = w0;
        for (ll aux = n; aux > len; aux >>= 1) {
            wlen = wlen * wlen % mod;
        }

        for (ll bat = 0; bat + len <= n; bat += len) {

            for (ll i = bat, w = 1; i < bat + len / 2;
                 i++, w = w * wlen % mod) {

                ll u = a[i], v = w * a[i + len / 2] % mod;

                // Update the value of a[i]
                a[i] = (u + v) % mod,

                // Update the value
                // of a[i + len/2]
                    a[i + len / 2]
                    = ((u - v) % mod + mod) % mod;
            }
        }
    }
}

// Function to find (a ^ x) % mod
ll binpow(ll a, ll x)
{
    // Stores the result of a ^ x
    ll ans = 1;

    // Iterate over the value of x
    for (; x; x /= 2, a = a * a % mod) {

        // If x is odd
        if (x & 1)
            ans = ans * a % mod;
    }

    // Return the resultant value
    return ans;
}

// Function to find the
// inverse of a % mod
ll inv(ll a) { return binpow(a, mod - 2); }

// Function to find the
// convolution of two arrays
void findConvolution(ll a[], ll b[], ll n, ll m)
{
    // Stores the first power of 2
    // greater than or equal to n + m
    ll _n = 1ll << 64 - __builtin_clzll(n + m);

    // Stores the primitive root
    ll w = 15311432;
    for (ll aux = 1 << 23; aux > _n; aux >>= 1)
        w = w * w % mod;

    // Convert arrays a[] and
    // b[] to point value form
    fft(w, _n, a);
    fft(w, _n, b);

    // Perform multiplication
    for (ll i = 0; i < _n; i++)
        a[i] = a[i] * b[i] % mod;

    // Perform inverse fft to
    // recover final array
    fft(inv(w), _n, a);
    for (ll i = 0; i < _n; i++)
        a[i] = a[i] * inv(_n) % mod;

    // Print the convolution
    for (ll i = 0; i < n + m - 1; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{
    // Given size of the arrays
    ll N = 4, M = 5;

    // Fill the arrays
    for (ll i = 0; i < N; i++)
        a[i] = i + 1;

    for (ll i = 0; i < M; i++)
        b[i] = 5 + i;

    findConvolution(a, b, N, M);

    return 0;
}
```

**Output:** 

```
5 16 34 60 70 70 59 36
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N + M)*