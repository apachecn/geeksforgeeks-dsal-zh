# 前半部分用两个零计数二进制字符串

> 原文:[https://www . geesforgeks . org/count-binary-strings-two-zero-first-half/](https://www.geeksforgeeks.org/count-binary-strings-twice-zeros-first-half/)

给我们一个整数 N，我们需要计算这种长度为 N 的二进制字符串的总数，使得长度为 N/2 的第一个字符串中的“0”的数量是长度为 N/2 的第二个字符串中“0”的数量的两倍。
注意:N 始终为偶数正整数。
**例:**

> 输入:N = 4
> 输出:2
> 说明:0010 和 0001 是两个二进制字符串，使得前半部分的零的个数是后半部分的零的个数的两倍。
> 
> 输入:N = 6
> 输出:9

**天真方法:**我们可以生成所有长度为 N 的二进制字符串，然后逐一检查所选字符串是否符合给定的场景。但是这种方法的时间复杂度是指数的，并且是 0(N * 2<sup>N</sup>)。
**高效方法:**这种方法是基于对问题的一些数学分析。
这种方法的先决条件:阶乘和模函数组合。
注:设 n = N/2。
如果我们一步步进行一些分析:

1.  前半串包含两个“0”，后半串包含一个“0”的串数等于**T1】nC<sub>2</sub>*<sup>n</sup>C<sub>1</sub>T9】。**
2.  前半弦包含四个“0”后半弦包含两个“0”的弦的数量等于**T1】nC<sub>4</sub>*<sup>n</sup>C<sub>2</sub>T9】。**
3.  前半串包含 6 个“0”，后半串包含 3 个“0”的串数等于**T1】nC<sub>6</sub>*<sup>n</sup>C<sub>3</sub>T9】。**

我们重复上面的过程，直到前半部分的“0”变成 n，如果 n 是偶数，或者(n-1)如果 n 是奇数。
那么，我们最终的答案是**σ(<sup>n</sup>C<sub>(2 * I)</sub>*<sup>n</sup>C<sub>I</sub>)**，对于 2 < = 2*i < = n.
现在，我们只需要使用排列组合就可以计算出所需的字符串数。
**算法:**

```
int n = N/2;
for(int i=2;i<=n;i=i+2)
             ans += ( nCr(n, i) * nCr(n, i/2);
```

**注意:**可以使用动态规划技术来预先计算系数(N，I)，即 <sup>n</sup> C <sub>i</sub> 。
如果我们预先计算 O(N*N)中的系数(N，I)，时间复杂度为 O(N)。

## C++

```
// CPP for finding number of binary strings
// number of '0' in first half is double the
// number of '0' in second half of string
#include <bits/stdc++.h>

// pre define some constant
#define mod 1000000007
#define max 1001
using namespace std;

// global values for pre computation
long long int nCr[1003][1003];

void preComputeCoeff()
{
    for (int i = 0; i < max; i++) {
        for (int j = 0; j <= i; j++) {
            if (j == 0 || j == i)
                nCr[i][j] = 1;
            else
                nCr[i][j] = (nCr[i - 1][j - 1] +
                             nCr[i - 1][j]) % mod;
        }
    }
}

// function to print number of required string
long long int computeStringCount(int N)
{
    int n = N / 2;
    long long int ans = 0;

    // calculate answer using proposed algorithm
    for (int i = 2; i <= n; i += 2)
        ans = (ans + ((nCr[n][i] * nCr[n][i / 2])
                      % mod)) % mod;
    return ans;
}

// Driver code
int main()
{
    preComputeCoeff();
    int N = 3;
    cout << computeStringCount(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding number of binary strings
// number of '0' in first half is double the
// number of '0' in second half of string
class GFG {

    // pre define some constant
    static final long mod = 1000000007;
    static final long max = 1001;

    // global values for pre computation
    static long nCr[][] = new long[1003][1003];

    static void preComputeCoeff()
    {
        for (int i = 0; i < max; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 0 || j == i)
                    nCr[i][j] = 1;
                else
                    nCr[i][j] = (nCr[i - 1][j - 1] +
                                nCr[i - 1][j]) % mod;
            }
        }
    }

    // function to print number of required string
    static long computeStringCount(int N)
    {
        int n = N / 2;
        long ans = 0;

        // calculate answer using proposed algorithm
        for (int i = 2; i <= n; i += 2)
            ans = (ans + ((nCr[n][i] * nCr[n][i / 2])
                        % mod)) % mod;
        return ans;
    }

    // main function
    public static void main(String[] args)
    {
        preComputeCoeff();
        int N = 3;
        System.out.println( computeStringCount(N) );

    }
}

// This code is contributed by Arnab Kundu.
```

## 蟒蛇 3

```
# Python3 for finding number of binary strings
# number of '0' in first half is double the
# number of '0' in second half of string

# pre define some constant
mod = 1000000007
Max = 1001

# global values for pre computation
nCr = [[0 for _ in range(1003)]
          for i in range(1003)]

def preComputeCoeff():

    for i in range(Max):
        for j in range(i + 1):
            if (j == 0 or j == i):
                nCr[i][j] = 1
            else:
                nCr[i][j] = (nCr[i - 1][j - 1] +
                             nCr[i - 1][j]) % mod

# function to print number of required string
def computeStringCount(N):
    n = N // 2
    ans = 0

    # calculate answer using proposed algorithm
    for i in range(2, n + 1, 2):
        ans = (ans + ((nCr[n][i] *
                       nCr[n][i // 2]) % mod)) % mod
    return ans

# Driver code
preComputeCoeff()
N = 3
print(computeStringCount(N))

# This code is contributed by mohit kumar
```

## C#

```
// C# program for finding number of binary
// strings number of '0' in first half is
// double the number of '0' in second half
// of string
using System;

class GFG {

    // pre define some constant
    static long mod = 1000000007;
    static long max = 1001;

    // global values for pre computation
    static long [,]nCr = new long[1003,1003];

    static void preComputeCoeff()
    {
        for (int i = 0; i < max; i++)
        {
            for (int j = 0; j <= i; j++)
            {
                if (j == 0 || j == i)
                    nCr[i,j] = 1;
                else
                    nCr[i,j] = (nCr[i - 1,j - 1]
                          + nCr[i - 1,j]) % mod;
            }
        }
    }

    // function to print number of required
    // string
    static long computeStringCount(int N)
    {
        int n = N / 2;
        long ans = 0;

        // calculate answer using proposed
        // algorithm
        for (int i = 2; i <= n; i += 2)
            ans = (ans + ((nCr[n,i]
                * nCr[n,i / 2]) % mod)) % mod;

        return ans;
    }

    // main function
    public static void Main()
    {
        preComputeCoeff();
        int N = 3;
        Console.Write( computeStringCount(N) );

    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// Javascript for finding number of binary strings
// number of '0' in first half is double the
// number of '0' in second half of string

// pre define some constant
var mod = 1000000007
var max = 1001

// global values for pre computation
var nCr = Array.from(Array(1003), ()=> Array(1003));

function preComputeCoeff()
{
    for (var i = 0; i < max; i++) {
        for (var j = 0; j <= i; j++) {
            if (j == 0 || j == i)
                nCr[i][j] = 1;
            else
                nCr[i][j] = (nCr[i - 1][j - 1] +
                             nCr[i - 1][j]) % mod;
        }
    }
}

// function to print number of required string
function computeStringCount(N)
{
    var n = N / 2;
    var ans = 0;

    // calculate answer using proposed algorithm
    for (var i = 2; i <= n; i += 2)
        ans = (ans + ((nCr[n][i] * nCr[n][i / 2])
                      % mod)) % mod;
    return ans;
}

// Driver code
preComputeCoeff();
var N = 3;
document.write( computeStringCount(N));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
0
```