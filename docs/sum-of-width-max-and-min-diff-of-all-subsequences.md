# 所有子序列的宽度之和(最大和最小差值)

> 原文:[https://www . geesforgeks . org/所有子序列的最大宽度和最小宽度之和/](https://www.geeksforgeeks.org/sum-of-width-max-and-min-diff-of-all-subsequences/)

给定一个整数数组**【A】**。任务是返回 **A** 所有子序列的宽度之和。对于任何序列 **S** ，s 的宽度是 s 的最大和最小元素之差。
**注**:由于答案可能很大，所以打印答案时取模 10^9 + 7。

**示例:**

> 输入:A[] = {1，3，2}
> 输出:6
> 子序列为{1}、{2}、{3}、{1，3}、{1，2} {3，2}和{1，3，2}。宽度分别为 0、0、0、2、1、1 和 2。宽度之和是 6。
> 输入:A[] = [5，6，4，3，8]
> 输出:87
> 输入:A[] = [1，2，3，4，5，6，7]
> 输出:522

思路是先，**排序**数组作为排序数组不会影响最终答案。排序后，这让我们知道**最小 A[I]****最大 A[j]** 的子序列数将为 **2 <sup>j-i-1</sup>** 。
因此，我们的答案归结为发现:

下面是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

#define MOD 1000000007

// Function to return sum of width of all subsets
int SubseqWidths(int A[], int n)
{
    // Sort the array
    sort(A, A + n);

    int pow2[n];
    pow2[0] = 1;

    for (int i = 1; i < n; ++i)
        pow2[i] = (pow2[i - 1] * 2) % MOD;

    int ans = 0;

    for (int i = 0; i < n; ++i)
        ans = (ans + (pow2[i] - pow2[n - 1 - i]) * A[i]) % MOD;

    return ans;
}

// Driver program
int main()
{
    int A[] = { 5, 6, 4, 3, 8 };

    int n = sizeof(A) / sizeof(A[0]);

    cout << SubseqWidths(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.Arrays;

class GFG{
static int MOD=1000000007;

// Function to return sum of width of all subsets
static int SubseqWidths(int[] A, int n)
{
    // Sort the array
    Arrays.sort(A);

    int[] pow2=new int[n];
    pow2[0] = 1;

    for (int i = 1; i < n; ++i)
        pow2[i] = (pow2[i - 1] * 2) % MOD;

    int ans = 0;

    for (int i = 0; i < n; ++i)
        ans = (ans + (pow2[i] -
                pow2[n - 1 - i]) * A[i]) % MOD;

    return ans;
}

// Driver program
public static void main(String[] args)
{
    int[] A = new int[]{ 5, 6, 4, 3, 8 };

    int n = A.length;

    System.out.println(SubseqWidths(A, n));
}
}
// This code is contributed by mits
```

## 计算机编程语言

```
# Python3 implementation of above approach

# Function to return sum of width of all subsets
def SubseqWidths(A):
    MOD = 10**9 + 7
    N = len(A)
    A.sort()

    pow2 = [1]
    for i in range(1, N):
        pow2.append(pow2[-1] * 2 % MOD)

    ans = 0
    for i, x in enumerate(A):
        ans = (ans + (pow2[i] - pow2[N - 1 - i]) * x) % MOD
    return ans

# Driver program
A = [5, 6, 4, 3, 8]

print(SubseqWidths(A))
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
static int MOD = 1000000007;

// Function to return sum of
// width of all subsets
static int SubseqWidths(int[] A, int n)
{
    // Sort the array
    Array.Sort(A);

    int[] pow2 = new int[n];
    pow2[0] = 1;

    for (int i = 1; i < n; ++i)
        pow2[i] = (pow2[i - 1] * 2) % MOD;

    int ans = 0;

    for (int i = 0; i < n; ++i)
        ans = (ans + (pow2[i] -
                       pow2[n - 1 - i]) *
                       A[i]) % MOD;

    return ans;
}

// Driver Code
static void Main()
{
    int[] A = new int[]{ 5, 6, 4, 3, 8 };

    int n = A.Length;

    Console.WriteLine(SubseqWidths(A, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
$MOD = 1000000007;

// Function to return sum
// of width of all subsets
function SubseqWidths(&$A, $n)
{
    global $MOD;

    // Sort the array
    sort($A);

    $pow2 = array_fill(0, $n, NULL);
    $pow2[0] = 1;

    for ($i = 1; $i < $n; ++$i)
        $pow2[$i] = ($pow2[$i - 1] * 2) % $MOD;

    $ans = 0;

    for ($i = 0; $i < $n; ++$i)
        $ans = ($ans + ($pow2[$i] -
                        $pow2[$n - 1 - $i]) *
                              $A[$i]) % $MOD;

    return $ans;
}

// Driver Code
$A = array(5, 6, 4, 3, 8 );

$n = sizeof($A);

echo SubseqWidths($A, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

var MOD = 1000000007

// Function to return sum of width of all subsets
function SubseqWidths(A, n)
{
    // Sort the array
    A.sort((a,b) => a-b)

    var pow2 = Array(n).fill(0);
    pow2[0] = 1;

    for (var i = 1; i < n; ++i)
        pow2[i] = (pow2[i - 1] * 2) % MOD;

    var ans = 0;

    for (var i = 0; i < n; ++i)
        ans = (ans + (pow2[i] - pow2[n - 1 - i]) * A[i]) % MOD;

    return ans;
}

// Driver program
var A = [ 5, 6, 4, 3, 8 ];
var n = A.length;
document.write( SubseqWidths(A, n));

</script>
```

**Output:** 

```
87
```

**时间复杂度:** O(N*log(N))，其中 N 为 a 的长度