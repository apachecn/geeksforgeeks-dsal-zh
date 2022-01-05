# 计算所有有乘积的子序列<= K–递归方法

> 原文:[https://www . geesforgeks . org/count-all-sub-sequence-having-product/](https://www.geeksforgeeks.org/count-all-sub-sequences-having-product/)

给定一个整数 **K** 和一个非负数组 **arr[]** ，任务是找出具有乘积 **≤ K** 的子序列的数目。
这个问题已经有了[动态编程解决方案](https://www.geeksforgeeks.org/?p=160170)。该解决方案旨在为该问题提供一种*优化递归策略*。

**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 10
> **输出:** 11
> 子序列为{1}、{2}、{3}、{4}、{1，2}、{1，3}、{1，4}、{2，3}、{2，4}、{ 1，2，3}、{ 1，2，4 }
> 
> **输入:** arr[] = { 4，8，7，2 }，K = 50
> T3】输出: 9

**方法:**通过执行转换 **arr[i] = log(arr[i])** 和 **K = log(K)** ，将**产品**问题转换为**求和**问题。生成所有子集，并存储在子序列中已经*获取的元素的总和。如果在任何一点上，和变得大于 K，那么我们知道，如果我们在子序列中加入另一个元素，它的和也会**大于 K** 。因此，我们丢弃所有这些总和大于 **K** 的子序列，而不对它们进行递归调用。此外，如果我们当前的**和小于 K** ，那么我们检查是否有机会进一步丢弃任何子序列。如果任何进一步的子序列不能被丢弃，则不进行递归调用。
以下是上述方法的实施:*

## C++

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>

#define ll long long

using namespace std;

// This variable counts discarded subsequences
ll discard_count = 0;

// Function to return a^n
ll power(ll a, ll n)
{
    if (n == 0)
        return 1;
    ll p = power(a, n / 2);
    p = p * p;
    if (n & 1)
        p = p * a;
    return p;
}

// Recursive function that counts discarded
// subsequences
void solve(int i, int n, float sum, float k,
                   float* a, float* prefix)
{

    // If at any stage, sum > k
    // discard further subsequences
    if (sum > k) {
        discard_count += power(2, n - i);

        // Recursive call terminated
        // No further calls
        return;
    }

    if (i == n)
        return;

    // rem = Sum of array[i+1...n-1]
    float rem = prefix[n - 1] - prefix[i];

    // If there are chances of discarding
    // further subsequences then make a
    // recursive call, otherwise not
    // Including a[i]
    if (sum + a[i] + rem > k)
        solve(i + 1, n, sum + a[i], k,
                          a, prefix);

    // Excluding a[i]
    if (sum + rem > k)
        solve(i + 1, n, sum, k, a, prefix);
}

// Function to return count of non-empty
// subsequences whose product doesn't
// exceed k
int countSubsequences(const int* arr,
                         int n, ll K)
{
    float sum = 0.0;

    // Converting k to log(k)
    float k = log2(K);

    // Prefix sum array and array to
    // store log values.
    float prefix[n], a[n];

    // a[] is the array obtained
    // after converting numbers to
    // logarithms
    for (int i = 0; i < n; i++) {
        a[i] = log2(arr[i]);
        sum += a[i];
    }

    // Computing prefix sums
    prefix[0] = a[0];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Calculate non-empty subsequences
    // hence 1 is subtracted
    ll total = power(2, n) - 1;

    // If total sum is <= k, then
    // answer = 2^n - 1
    if (sum <= k) {
        return total;
    }

    solve(0, n, 0.0, k, a, prefix);
    return total - discard_count;
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 7, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    ll k = 50;
    cout << countSubsequences(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

// This variable counts discarded subsequences
static long discard_count = 0;

// Function to return a^n
static long power(long a, long n)
{
    if (n == 0)
        return 1;
    long p = power(a, n / 2);
    p = p * p;
    if (n % 2 == 1)
        p = p * a;
    return p;
}

// Recursive function that counts discarded
// subsequences
static void solve(int i, int n, float sum, float k,
                float []a, float []prefix)
{

    // If at any stage, sum > k
    // discard further subsequences
    if (sum > k)
    {
        discard_count += power(2, n - i);

        // Recursive calong terminated
        // No further calongs
        return;
    }

    if (i == n)
        return;

    // rem = Sum of array[i+1...n-1]
    float rem = prefix[n - 1] - prefix[i];

    // If there are chances of discarding
    // further subsequences then make a
    // recursive calong, otherwise not
    // Including a[i]
    if (sum + a[i] + rem > k)
        solve(i + 1, n, sum + a[i], k,
                        a, prefix);

    // Excluding a[i]
    if (sum + rem > k)
        solve(i + 1, n, sum, k, a, prefix);
}

// Function to return count of non-empty
// subsequences whose product doesn't
// exceed k
static int countSubsequences(int []arr,
                        int n, long K)
{
    float sum = 0.0f;

    // Converting k to log(k)
    float k = (float) Math.log(K);

    // Prefix sum array and array to
    // store log values.
    float []prefix = new float[n];
    float []a = new float[n];

    // a[] is the array obtained
    // after converting numbers to
    // logarithms
    for (int i = 0; i < n; i++)
    {
        a[i] = (float) Math.log(arr[i]);
        sum += a[i];
    }

    // Computing prefix sums
    prefix[0] = a[0];
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Calculate non-empty subsequences
    // hence 1 is subtracted
    long total = power(2, n) - 1;

    // If total sum is <= k, then
    // answer = 2^n - 1
    if (sum <= k)
    {
        return (int) total;
    }

    solve(0, n, 0.0f, k, a, prefix);
    return (int) (total - discard_count);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 8, 7, 2 };
    int n = arr.length;
    long k = 50;
    System.out.print(countSubsequences(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach.

# From math lib import log2
from math import log2

# This variable counts discarded
# subsequences
discard_count = 0

# Function to return a^n
def power(a, n) :

    if (n == 0) :
        return 1

    p = power(a, n // 2)
    p = p * p
    if (n & 1) :
        p = p * a
    return p

# Recursive function that counts
# discarded subsequences
def solve(i, n, sum, k, a, prefix) :
    global discard_count

    # If at any stage, sum > k
    # discard further subsequences
    if (sum > k) :
        discard_count += power(2, n - i)

        # Recursive call terminated
        # No further calls
        return;

    if (i == n) :
        return

    # rem = Sum of array[i+1...n-1]
    rem = prefix[n - 1] - prefix[i]

    # If there are chances of discarding
    # further subsequences then make a
    # recursive call, otherwise not
    # Including a[i]
    if (sum + a[i] + rem > k) :
        solve(i + 1, n, sum + a[i], k, a, prefix)

    # Excluding a[i]
    if (sum + rem > k) :
        solve(i + 1, n, sum, k, a, prefix)

# Function to return count of non-empty
# subsequences whose product doesn't
# exceed k
def countSubsequences(arr, n, K) :

    sum = 0.0

    # Converting k to log(k)
    k = log2(K)

    # Prefix sum array and array to
    # store log values.
    prefix = [0] * n
    a = [0] * n

    # a[] is the array obtained after
    # converting numbers to logarithms
    for i in range(n) :
        a[i] = log2(arr[i])
        sum += a[i]

    # Computing prefix sums
    prefix[0] = a[0]

    for i in range(1, n) :
        prefix[i] = prefix[i - 1] + a[i]

    # Calculate non-empty subsequences
    # hence 1 is subtracted
    total = power(2, n) - 1

    # If total sum is <= k, then
    # answer = 2^n - 1
    if (sum <= k) :
        return total

    solve(0, n, 0.0, k, a, prefix)
    return total - discard_count

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 8, 7, 2 ]
    n = len(arr)
    k = 50;
    print(countSubsequences(arr, n, k))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

// This variable counts discarded subsequences
static long discard_count = 0;

// Function to return a^n
static long power(long a, long n)
{
    if (n == 0)
        return 1;
    long p = power(a, n / 2);
    p = p * p;
    if (n % 2 == 1)
        p = p * a;
    return p;
}

// Recursive function that counts discarded
// subsequences
static void solve(int i, int n, float sum, float k,
                     float []a, float []prefix)
{

    // If at any stage, sum > k
    // discard further subsequences
    if (sum > k)
    {
        discard_count += power(2, n - i);

        // Recursive calong terminated
        // No further calongs
        return;
    }

    if (i == n)
        return;

    // rem = Sum of array[i+1...n-1]
    float rem = prefix[n - 1] - prefix[i];

    // If there are chances of discarding
    // further subsequences then make a
    // recursive calong, otherwise not
    // Including a[i]
    if (sum + a[i] + rem > k)
        solve(i + 1, n, sum + a[i], k,
                           a, prefix);

    // Excluding a[i]
    if (sum + rem > k)
        solve(i + 1, n, sum, k, a, prefix);
}

// Function to return count of non-empty
// subsequences whose product doesn't
// exceed k
static int countSubsequences(int []arr,
                             int n, long K)
{
    float sum = 0.0f;

    // Converting k to log(k)
    float k = (float) Math.Log(K);

    // Prefix sum array and array to
    // store log values.
    float []prefix = new float[n];
    float []a = new float[n];

    // []a is the array obtained
    // after converting numbers to
    // logarithms
    for (int i = 0; i < n; i++)
    {
        a[i] = (float) Math.Log(arr[i]);
        sum += a[i];
    }

    // Computing prefix sums
    prefix[0] = a[0];
    for (int i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Calculate non-empty subsequences
    // hence 1 is subtracted
    long total = power(2, n) - 1;

    // If total sum is <= k, then
    // answer = 2^n - 1
    if (sum <= k)
    {
        return (int) total;
    }

    solve(0, n, 0.0f, k, a, prefix);
    return (int) (total - discard_count);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 8, 7, 2 };
    int n = arr.Length;
    long k = 50;
    Console.Write(countSubsequences(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach.

// This variable counts discarded subsequences
$discard_count = 0;

// Function to return a^n
function power($a, $n)
{
    if ($n == 0)
        return 1;
    $p = power($a, $n / 2);
    $p = $p * $p;
    if ($n & 1)
        $p = $p * $a;
    return $p;
}

// Recursive function that counts discarded
// subsequences
function solve($i, $n, $sum, $k, &$a, &$prefix)
{
    global $discard_count;

    // If at any stage, sum > k
    // discard further subsequences
    if ($sum > $k)
    {
        $discard_count += power(2, $n - $i);

        // Recursive call terminated
        // No further calls
        return;
    }

    if ($i == $n)
        return;

    // rem = Sum of array[i+1...n-1]
    $rem = $prefix[$n - 1] - $prefix[$i];

    // If there are chances of discarding
    // further subsequences then make a
    // recursive call, otherwise not
    // Including a[i]
    if ($sum + $a[$i] + $rem > $k)
        solve($i + 1, $n, $sum + $a[$i], $k,
                               $a, $prefix);

    // Excluding a[i]
    if ($sum + $rem > $k)
        solve($i + 1, $n, $sum, $k, $a, $prefix);
}

// Function to return count of non-empty
// subsequences whose product doesn't
// exceed k
function countSubsequences(&$arr, $n, $K)
{
    global $discard_count;
    $sum = 0.0;

    // Converting k to log(k)
    $k = log($K, 2);

    // Prefix sum array and array to
    // store log values.
    $prefix = array_fill(0, $n, NULL);
    $a = array_fill(0, $n, NULL);

    // a[] is the array obtained after
    // converting numbers to logarithms
    for ($i = 0; $i < $n; $i++)
    {
        $a[$i] = log($arr[$i], 2);
        $sum += $a[$i];
    }

    // Computing prefix sums
    $prefix[0] = $a[0];
    for ($i = 1; $i < $n; $i++)
    {
        $prefix[$i] = $prefix[$i - 1] + $a[$i];
    }

    // Calculate non-empty subsequences
    // hence 1 is subtracted
    $total = power(2, $n) - 1;

    // If total sum is <= k, then
    // answer = 2^n - 1
    if ($sum <= $k)
    {
        return $total;
    }

    solve(0, $n, 0.0, $k, $a, $prefix);
    return $total - $discard_count;
}

// Driver code
$arr = array(4, 8, 7, 2 );
$n = sizeof($arr);
$k = 50;
echo countSubsequences($arr, $n, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach.

// This variable counts discarded subsequences
let discard_count = 0;

// Function to return a^n
function power(a,n)
{
       if (n == 0)
        return 1;
    let p = power(a, Math.floor(n / 2));
    p = p * p;
    if (n % 2 == 1)
        p = p * a;
    return p;
}

// Recursive function that counts discarded
// subsequences
function solve(i,n,sum,k,a,prefix)
{
    // If at any stage, sum > k
    // discard further subsequences
    if (sum > k)
    {
        discard_count += power(2, n - i);

        // Recursive calong terminated
        // No further calongs
        return;
    }

    if (i == n)
        return;

    // rem = Sum of array[i+1...n-1]
    let rem = prefix[n - 1] - prefix[i];

    // If there are chances of discarding
    // further subsequences then make a
    // recursive calong, otherwise not
    // Including a[i]
    if (sum + a[i] + rem > k)
        solve(i + 1, n, sum + a[i], k,
                        a, prefix);

    // Excluding a[i]
    if (sum + rem > k)
        solve(i + 1, n, sum, k, a, prefix);
}

// Function to return count of non-empty
// subsequences whose product doesn't
// exceed k
function countSubsequences(arr,n,K)
{
    let sum = 0.0;

    // Converting k to log(k)
    let k =  Math.log(K);

    // Prefix sum array and array to
    // store log values.
    let prefix = new Array(n);
    let a = new Array(n);

    // a[] is the array obtained
    // after converting numbers to
    // logarithms
    for (let i = 0; i < n; i++)
    {
        a[i] =  Math.log(arr[i]);
        sum += a[i];
    }

    // Computing prefix sums
    prefix[0] = a[0];
    for (let i = 1; i < n; i++)
    {
        prefix[i] = prefix[i - 1] + a[i];
    }

    // Calculate non-empty subsequences
    // hence 1 is subtracted
    let total = power(2, n) - 1;

    // If total sum is <= k, then
    // answer = 2^n - 1
    if (sum <= k)
    {
        return total;
    }

    solve(0, n, 0.0, k, a, prefix);
    return (total - discard_count);
}

// Driver code
let arr=[4, 8, 7, 2];
let n = arr.length;
let k = 50;
document.write(countSubsequences(arr, n, k));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
9
```