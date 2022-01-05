# 数组所有子集的(最大元素–最小元素)之和。

> 原文:[https://www . geesforgeks . org/数组所有子集的最大元素-最小元素之和/](https://www.geeksforgeeks.org/sum-of-maximum-element-minimum-element-for-all-the-subsets-of-an-array/)

给定一个数组 **arr[]** ，任务是计算数组 arr[]的每个非空子集 A 的**和(最大{A}–最小{ A })。
**例:**** 

> **输入:** arr[] = { 4，7 }
> T3】输出: 3
> 有三个非空子集:{ 4 }、{ 7 }和{ 4，7 }。
> 最大值({4 })–最小值({4}) = 0
> 最大值({ 7 })–最小值({7}) = 0
> 最大值({4，7 })–最小值({ 4，7 })= 7–4 = 3。
> 总和= 0 + 0 + 3 = 3
> **输入:** arr[] = { 4，3，1 }
> **输出:** 9

一个**天真的解决方案**是生成所有子集，遍历每个子集，找到最大和最小元素，并将它们的差加到当前和上。这个解决方案的时间复杂度是 **O(n * 2 <sup>n</sup> )** 。
一个**有效的解决方案**是基于下面陈述的简单观察。

> 例如，A = { 4，3，1 }
> 让每个子集的总和中要添加的值为 V。
> 具有最大值、最小值和 V 值的子集:
> { 4 }，最大值= 4，最小值= 4(V = 4–4)
> { 3 }，最大值= 3，最小值= 3(V = 3–3)
> { 1 }，最大值= 1，最小值= 1(V = 1–1)
> { 4，3 }， max = 4，min = 3(V = 4–3)
> { 4，1 }，max = 4，min = 1(V = 4–1)
> { 3，1 }，max = 3，min = 1(V = 3–1)
> { 4，3，1 }，max = 4， min = 1(V = 4–1)
> 所有 V 值之和
> =(4–4)+(3–3)+(1–1)+(4–3)+(4–1)+(3–1)+(4–1)+(4–1)
> = 0+0+0+(4–3)+(4–1)+(3–1)+(4–1)
> =(4–3)+(4–1)+(3–1) +(4–1)
> 前 3 个“V”值可以忽略，因为它们的计算结果为 0
> (因为它们来自 1 大小的子集)。
> 重新排列总和，我们得到:
> =(4–3)+(4–1)+(3–1)+(4–1)
> =(1 * 0–1 * 3)+(3 * 1–3 * 1)+(4 * 3–4 * 0)
> =(1 * A–1 * B)+(3 * C–3 * D)+(4 * E–4 * F)
> 其中 A = 0，B = 3， C = 1，D = 1，E = 3 和 F = 0
> 如果我们仔细观察表达式，而不是分析每个子集，这里我们分析每个元素作为最小或最大元素出现的次数。
> A = 0 意味着 1 在任何子集内都不是最大元素。
> B = 3 意味着 1 作为最小元素出现在 3 个子集中。
> C = 1 意味着 3 作为 1 个子集的最大元素出现。
> D = 1 意味着 3 作为最小元素出现在 1 个子集中。
> E = 3 意味着 4 作为最大元素出现在 3 个子集中。
> F = 0 意味着 4 在任何子集中都不是最小元素。

如果我们知道作为最大元素和最小元素出现的每个元素的子集数，那么我们可以在**线性**时间内解决这个问题，因为上面的计算本质上是线性的。
让 A = { 6，3，89，21，4，2，7，9 }
排序(A) = { 2，3，4， **6** ，7，9，21，89 }
例如，我们分析值为 6(用粗体标出)的*元素。3 个元素小于 6，4 个元素大于 6。因此，如果我们考虑所有子集，其中 6 与 3 个较小的元素一起出现，那么在所有这些子集中，6 将是最大的元素。这些子集的数量将为 2 <sup>3</sup> 。当 4 个元素大于 6 时，6 是最小元素，类似的论点也成立。* 

> 因此，
> 元素在所有子集中出现次数最大= **2 <sup>位置</sup>–1**T5】元素在所有子集中出现次数最小=**2<sup>n–1–位置</sup>–1**T10】其中**位置**是排序数组中元素的索引。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define ll long long

using namespace std;

const int mod = 1000000007;

// Function to return a^n % mod
ll power(ll a, ll n)
{
    if (n == 0)
        return 1;

    ll p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if (n & 1) {
        p = (p * a) % mod;
    }
    return p;
}

// Compute sum of max(A) - min(A) for all subsets
ll computeSum(int* arr, int n)
{

    // Sort the array.
    sort(arr, arr + n);

    ll sum = 0;
    for (int i = 0; i < n; i++) {

        // Maxs = 2^i - 1
        ll maxs = (power(2, i) - 1 + mod) % mod;
        maxs = (maxs * arr[i]) % mod;

        // Mins = 2^(n-1-i) - 1
        ll mins = (power(2, n - 1 - i) - 1 + mod) % mod;
        mins = (mins * arr[i]) % mod;

        ll V = (maxs - mins + mod) % mod;
        sum = (sum + V) % mod;
    }
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << computeSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

static int mod = 1000000007;

    // Function to return a^n % mod
    static long power(long a, long n)
    {
        if (n == 0)
        {
            return 1;
        }

        long p = power(a, n / 2) % mod;
        p = (p * p) % mod;
        if (n == 1)
        {
            p = (p * a) % mod;
        }
        return p;
    }

    // Compute sum of max(A) - min(A) for all subsets
    static long computeSum(int[] arr, int n)
    {

        // Sort the array.
        Arrays.sort(arr);

        long sum = 0;
        for (int i = 0; i < n; i++)
        {

            // Maxs = 2^i - 1
            long maxs = (power(2, i) - 1 + mod) % mod;
            maxs = (maxs * arr[i]) % mod;

            // Mins = 2^(n-1-i) - 1
            long mins = (power(2, n - 1 - i) - 1 + mod) % mod;
            mins = (mins * arr[i]) % mod;

            long V = (maxs - mins + mod) % mod;
            sum = (sum + V) % mod;
        }
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 3, 1};
        int n = arr.length;
        System.out.println(computeSum(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to return a^n % mod
def power(a, n):

    if n == 0:
        return 1

    p = power(a, n // 2) % mod
    p = (p * p) % mod
    if n & 1 == 1:
        p = (p * a) % mod

    return p

# Compute sum of max(A) - min(A)
# for all subsets
def computeSum(arr, n):

    # Sort the array.
    arr.sort()

    Sum = 0
    for i in range(0, n):

        # Maxs = 2^i - 1
        maxs = (power(2, i) - 1 + mod) % mod
        maxs = (maxs * arr[i]) % mod

        # Mins = 2^(n-1-i) - 1
        mins = (power(2, n - 1 - i) -
                      1 + mod) % mod
        mins = (mins * arr[i]) % mod

        V = (maxs - mins + mod) % mod
        Sum = (Sum + V) % mod

    return Sum

# Driver code
if __name__ =="__main__":

    mod = 1000000007
    arr = [4, 3, 1]
    n = len(arr)

    print(computeSum(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG
{

static int mod = 1000000007;

    // Function to return a^n % mod
    static long power(long a, long n)
    {
        if (n == 0)
        {
            return 1;
        }

        long p = power(a, n / 2) % mod;
        p = (p * p) % mod;
        if (n == 1)
        {
            p = (p * a) % mod;
        }
        return p;
    }

    // Compute sum of max(A) - min(A) for all subsets
    static long computeSum(int []arr, int n)
    {

        // Sort the array.
        Array.Sort(arr);

        long sum = 0;
        for (int i = 0; i < n; i++)
        {

            // Maxs = 2^i - 1
            long maxs = (power(2, i) - 1 + mod) % mod;
            maxs = (maxs * arr[i]) % mod;

            // Mins = 2^(n-1-i) - 1
            long mins = (power(2, n - 1 - i) - 1 + mod) % mod;
            mins = (mins * arr[i]) % mod;

            long V = (maxs - mins + mod) % mod;
            sum = (sum + V) % mod;
        }
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {4, 3, 1};
        int n = arr.Length;
        Console.WriteLine(computeSum(arr, n));
    }
}

// This code has been contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$mod = 1000000007;

// Function to return a^n % mod
function power($a, $n)
{
    global $mod;
    if ($n == 0)
        return 1;

    $p = power($a, $n / 2) % $mod;
    $p = ($p * $p) % $mod;
    if ($n & 1)
    {
        $p = ($p * $a) % $mod;
    }
    return $p;
}

// Compute sum of max(A) - min(A)
// for all subsets
function computeSum(&$arr, $n)
{
    global $mod;

    // Sort the array.
    sort($arr);

    $sum = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Maxs = 2^i - 1
        $maxs = (power(2, $i) - 1 + $mod) % $mod;
        $maxs = ($maxs * $arr[$i]) % $mod;

        // Mins = 2^(n-1-i) - 1
        $mins = (power(2, $n - 1 - $i) - 1 + $mod) % $mod;
        $mins = ($mins * $arr[$i]) % $mod;

        $V = ($maxs - $mins + $mod) % $mod;
        $sum = ($sum + $V) % $mod;
    }
    return $sum;
}

// Driver code
$arr = array( 4, 3, 1 );
$n = sizeof($arr);

echo computeSum($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    let mod = 1000000007;

// Function to return a^n % mod
    function power(a,n)
    {
        if (n == 0)
        {
            return 1;
        }

        let p = power(a, n / 2) % mod;
        p = (p * p) % mod;
        if (n == 1)
        {
            p = (p * a) % mod;
        }
        return p;
    }

    // Compute sum of max(A) - min(A) for all subsets
    function computeSum(arr,n)
    {
        // Sort the array.
        arr.sort(function(a,b){return a-b;});

        let sum = 0;
        for (let i = 0; i < n; i++)
        {

            // Maxs = 2^i - 1
            let maxs = (power(2, i) - 1 + mod) % mod;
            maxs = (maxs * arr[i]) % mod;

            // Mins = 2^(n-1-i) - 1
            let mins = (power(2, n - 1 - i) - 1 + mod) % mod;
            mins = (mins * arr[i]) % mod;

            let V = (maxs - mins + mod) % mod;
            sum = (sum + V) % mod;
        }
        return sum;
    }

     // Driver code
    let arr=[4, 3, 1];
    let n = arr.length;
    document.write(computeSum(arr, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
9
```

**时间复杂度** : O(N * log(N))
**辅助空间:** O(1)