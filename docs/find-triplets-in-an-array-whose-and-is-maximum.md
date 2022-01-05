# 在 AND 最大的数组中寻找三元组

> 原文:[https://www . geesforgeks . org/find-数组中的三元组-谁的和最大值/](https://www.geeksforgeeks.org/find-triplets-in-an-array-whose-and-is-maximum/)

给定一个大小为 n 的正整数数组，求其 AND 为最大值的三元组的计数，并求该最大值，假设数字不大于 10^9。
**示例:**

> 输入:a[] = {1，2，3，4，5，6}
> 输出:1 4
> 说明:能形成的最大个数为 4 ( 4 & 5 & 6)，只能有 1 个三联体。
> 输入:a[] = {4，11，10，15，26}
> 输出:4 10
> 说明:最多可形成 10 个。可能有 4 个三元组–{11，10，15}、{11，10，26}、{ 11，15，26}、{10，15，26}

一种**天真的方法**是使用 3 个循环，生成所有的三元组，并计算出可以形成的最大数量和这种三元组的数量。
*时间复杂度:* O(N^3)
A **更好的方法**是首先用二进制表示来表示数字，并将其存储在 2d 数组中。由于该数字不能大于 2^32(由于问题中给出的限制)，因此每个数字最多需要 32 次迭代。我们还将采用布尔标志数组，它将表示哪些数字可以用来构成最大三元组。最初，我们将数组设置为 true，因为每个数字都可以使用。
让最大“与”数 X 最初为零。
现在我们想要最大化 X，所以我们开始从索引遍历 2D 表，它代表数字的第 32 位，我们将计算出现在数字的第 32 位的 1 的数量，这些 1 可用于标志为真的三元组。如果 1 的计数大于或等于 3，这意味着有/有三元组可以设置 X 的第 I 位，那么我们将设置所有第 I 位未设置的数字的标志，并将基数 2 的幂 I 加到 X。否则，如果计数小于 3，那么 X 的第 I 位将被取消设置，并且我们不需要更改数字的标志，因为该位可以有 1 和 0 的组合。
我们将按照从 32 到 0 的相反顺序对每个位重复上述过程。
在，我们将计算标志被设置为 r 的数字的数量，然后对于三元组的数量，我们只需要计算 rC3 { r*(r-1)*(r-2)/6 }。

## C++

```
// CPP program to find triplet with maximum
// bitwise AND.
#include "cmath"
#include "cstring"
#include "iostream"
using namespace std;

int maxTriplet(int a[], int n)
{
    // Flag Array initially set to true
    // for all numbers
    bool f[n];
    memset(f, true, sizeof(f));

    // 2D array for bit representation
    // of all the numbers.
    // Initially all bits are set to 0.
    int bits[n][33];
    memset(bits, 0, sizeof(bits));

    for (int i = 0; i < n; ++i) {
        int num = a[i];
        int j = 32;

        // Finding bit representation
        // of every number and
        // storing it in bits array.
        while (num) {

            // Checking last bit of the number
            if (num & 1) {
                bits[i][j] = 1;
            }

            j--;

            // Dividing number by 2.
            num >>= 1;
        }
    }

    // maximum And number initially 0.
    long long ans = 0;

    // Traversing the 2d binary representation.
    // 0th index represents 32th bits
    // while 32th index represents 0th bit.
    for (long long i = 0; i <= 32; ++i) {
        int cnt = 0;

        for (int j = 0; j < n; ++j) {
            if (bits[j][i] and f[j]) {
                cnt++;
            }
        }

        // If cnt greater than 3 then (32-i)th bits
        // of the number will be set.
        if (cnt >= 3) {

            ans += pow(2LL, 32 - i);

            // Setting flags of the numbers
            // whose ith bit is not set.
            for (int j = 0; j < n; ++j) {
                if (!bits[j][i]) {
                    f[j] = false;
                }
            }
        }
    }

    // Counting the numbers whose flag are true.
    int cnt = 0;
    for (int i = 0; i < n; ++i) {
        if (f[i]) {
            cnt++;
        }
    }

    long long NumberOfTriplets =
          (cnt * (cnt - 1) * (cnt - 2)) / 6;

    cout << NumberOfTriplets << " " << ans;
}

int main(int argc, char const* argv[])
{
    int a[] = { 4, 11, 10, 15, 26 };
    int n = sizeof(a) / sizeof(a[0]);
    maxTriplet(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find triplet with maximum
// bitwise AND.
import java.util.Arrays;

class GFG {

static void maxTriplet(int a[], int n)
{
    // Flag Array initially set to true
    // for all numbers
    boolean []f = new boolean[n];
    Arrays.fill(f, true);

    // 2D array for bit representation
    // of all the numbers.
    // Initially all bits are set to 0.
    int bits[][] = new int[n][33];

    for (int i = 0; i < n; ++i)
    {
        int num = a[i];
        int j = 32;

        // Finding bit representation
        // of every number and
        // storing it in bits array.
        while (num > 0)
        {
            // Checking last bit of the number
            if (num % 2 == 1)
            {
                bits[i][j] = 1;
            }

            j--;

            // Dividing number by 2.
            num >>= 1;
        }
    }

    // maximum And number initially 0.
    long ans = 0;

    // Traversing the 2d binary representation.
    // 0th index represents 32th bits
    // while 32th index represents 0th bit.
    for (int i = 0; i <= 32; ++i)
    {
        int cnt = 0;

        for (int j = 0; j < n; ++j)
        {
            if (bits[j][i] == 1 & f[j])
            {
                cnt++;
            }
        }

        // If cnt greater than 3 then (32-i)th bits
        // of the number will be set.
        if (cnt >= 3) {

            ans += Math.pow(2, 32 - i);

            // Setting flags of the numbers
            // whose ith bit is not set.
            for (int j = 0; j < n; ++j) {
                if (bits[j][i] != 1) {
                    f[j] = false;
                }
            }
        }
    }

    // Counting the numbers whose flag are true.
    int cnt = 0;
    for (int i = 0; i < n; ++i) {
        if (f[i]) {
            cnt++;
        }
    }

    long NumberOfTriplets = (cnt * (cnt - 1) * (cnt - 2)) / 6;

    System.out.print(NumberOfTriplets + " " + ans);
}

// Driver code
public static void main(String[] args) {
int a[] = { 4, 11, 10, 15, 26 };
    int n = a.length;
    maxTriplet(a, n);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find triplet with
# maximum bitwise AND.
def maxTriplet(a, n):

    # Flag Array initially set to true
    # for all numbers
    f = [True for i in range(n)]

    # 2D array for bit representation
    # of all the numbers.
    # Initially all bits are set to 0.
    bits = [[0 for i in range(33)]
               for i in range(n)]

    for i in range(n):
        num = a[i]
        j = 32

        # Finding bit representation
        # of every number and
        # storing it in bits array.
        while (num):

            # Checking last bit of the number
            if (num & 1) :
                bits[i][j] = 1

            j -= 1

            # Dividing number by 2.
            num >>= 1

    # maximum And number initially 0.
    ans = 0

    # Traversing the 2d binary representation.
    # 0th index represents 32th bits
    # while 32th index represents 0th bit.
    for i in range(33):
        cnt = 0

        for j in range(n):
            if (bits[j][i] and f[j]):
                cnt += 1

        # If cnt greater than 3 then (32-i)th
        # bits of the number will be set.
        if (cnt >= 3):

            ans += pow(2, 32 - i)

            # Setting flags of the numbers
            # whose ith bit is not set.
            for j in range(n):
                if (bits[j][i] == False) :
                    f[j] = False

    # Counting the numbers whose
    # flag are true.
    cnt = 0
    for i in range(n):
        if (f[i]):
            cnt += 1

    NumberOfTriplets = (cnt * (cnt - 1) * (cnt - 2)) // 6
    print(NumberOfTriplets, ans)

# Driver Code
a = [ 4, 11, 10, 15, 26]
n = len(a)
maxTriplet(a, n)

# This code is contributed by Mohit Kumar29
```

## C#

```
// C# program to find triplet with maximum
// bitwise AND.
using System;
class GFG
{
static void maxTriplet(int []a, int n)
{
    // Flag Array initially set to true
    // for all numbers
    Boolean []f = new Boolean[n];
    for (int i = 0; i < n; ++i)
        f[i] = true;

    // 2D array for bit representation
    // of all the numbers.
    // Initially all bits are set to 0.
    int [,]bits = new int[n, 33];

    for (int i = 0; i < n; ++i)
    {
        int num = a[i];
        int j = 32;

        // Finding bit representation
        // of every number and
        // storing it in bits array.
        while (num > 0)
        {
            // Checking last bit of the number
            if (num % 2 == 1)
            {
                bits[i, j] = 1;
            }

            j--;

            // Dividing number by 2.
            num >>= 1;
        }
    }

    // maximum And number initially 0.
    long ans = 0;
    int cnt;

    // Traversing the 2d binary representation.
    // 0th index represents 32th bits
    // while 32th index represents 0th bit.
    for (int i = 0; i <= 32; ++i)
    {
        cnt = 0;

        for (int j = 0; j < n; ++j)
        {
            if (bits[j, i] == 1 & f[j])
            {
                cnt++;
            }
        }

        // If cnt greater than 3 then (32-i)th bits
        // of the number will be set.
        if (cnt >= 3)
        {
            ans += (long)Math.Pow(2, 32 - i);

            // Setting flags of the numbers
            // whose ith bit is not set.
            for (int j = 0; j < n; ++j)
            {
                if (bits[j, i] != 1)
                {
                    f[j] = false;
                }
            }
        }
    }

    // Counting the numbers whose flag are true.
    cnt = 0;
    for (int i = 0; i < n; ++i)
    {
        if (f[i])
        {
            cnt++;
        }
    }

    long NumberOfTriplets = (cnt * (cnt - 1) *
                            (cnt - 2)) / 6;

    Console.Write(NumberOfTriplets + " " + ans);
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 4, 11, 10, 15, 26 };
    int n = a.Length;
    maxTriplet(a, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find triplet with maximum
// bitwise AND.

function maxTriplet(a,n)
{
    // Flag Array initially set to true
    // for all numbers
    let f = new Array(n);
    for(let i=0;i<n;i++)
    {
        f[i]=true;
    }

    // 2D array for bit representation
    // of all the numbers.
    // Initially all bits are set to 0.
    let bits = new Array(n);
    for(let i=0;i<n;i++)
    {
        bits[i]=new Array(33);
        for(let j=0;j<33;j++)
        {
            bits[i][j]=0;
        }
    }

    for (let i = 0; i < n; ++i)
    {
        let num = a[i];
        let j = 32;

        // Finding bit representation
        // of every number and
        // storing it in bits array.
        while (num > 0)
        {
            // Checking last bit of the number
            if (num % 2 == 1)
            {
                bits[i][j] = 1;
            }

            j--;

            // Dividing number by 2.
            num >>= 1;
        }
    }

    // maximum And number initially 0.
    let ans = 0;

    // Traversing the 2d binary representation.
    // 0th index represents 32th bits
    // while 32th index represents 0th bit.
    for (let i = 0; i <= 32; ++i)
    {
        let cnt = 0;

        for (let j = 0; j < n; ++j)
        {
            if (bits[j][i] == 1 & f[j])
            {
                cnt++;
            }
        }

        // If cnt greater than 3 then (32-i)th bits
        // of the number will be set.
        if (cnt >= 3) {

            ans += Math.pow(2, 32 - i);

            // Setting flags of the numbers
            // whose ith bit is not set.
            for (let j = 0; j < n; ++j) {
                if (bits[j][i] != 1) {
                    f[j] = false;
                }
            }
        }
    }

    // Counting the numbers whose flag are true.
    let cnt = 0;
    for (let i = 0; i < n; ++i) {
        if (f[i]) {
            cnt++;
        }
    }

    let NumberOfTriplets = (cnt * (cnt - 1) * (cnt - 2)) / 6;

    document.write(NumberOfTriplets + " " + ans);
}

// Driver code
let a=[4, 11, 10, 15, 26];
let n = a.length;
maxTriplet(a, n);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
4 10
```

**时间复杂度:** O(NlogN)
因为每个数字都是可以转换成它的二进制的 logN。