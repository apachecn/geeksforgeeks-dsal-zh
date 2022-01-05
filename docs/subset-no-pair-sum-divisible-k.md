# 没有可被 K 整除的对和的子集

> 原文:[https://www . geesforgeks . org/subset-no-pair-sum-除尽-k/](https://www.geeksforgeeks.org/subset-no-pair-sum-divisible-k/)

给定一个整数数组，我们需要找到一个子集的最大大小，使得这个子集的每对之和不能被 k 整除。
**示例:**

```
Input :  arr[] = [3, 7, 2, 9, 1]        
         K = 3
Output : 3
Maximum size subset whose each pair sum 
is not divisible by K is [3, 7, 1] because,
3+7 = 10,    
3+1 = 4,    
7+1 = 8        all are not divisible by 3.
It is not possible to get a subset of size 
bigger than 3 with the above-mentioned property.

Input : arr[] = [3, 17, 12, 9, 11, 15]
        K = 5
Output : 4  
```

我们可以通过用 K 计算数组数的模来解决这个问题，如果两个数的和可以被 K 整除，那么如果其中一个给出余数 I，另一个给出余数(K–I)。首先，我们将给出特定余数的数的频率存储在大小为 K 的频率数组中。然后，我们对所有余数 I 进行循环，并包括 max(f[i]，f[K–I])。为什么呢？没有可被 K 整除的对和的子集必须包含余数为 f[i]或余数为 f[K–I]的元素。因为我们想要最大化子集的大小，所以我们选择两个大小中的最大值。
在下面的代码中，余数为 0 和余数为 K/2 的数组编号是分开处理的。如果我们包含 2 个以上的余数为 0 的数，那么它们的和可以被 K 整除，所以我们考虑的是最大值为 1 的数，数组数给出余数为 K/2 的情况也是如此。

## C++

```
// C++ program to get size of subset whose
// each pair sum is not divisible by K
#include <bits/stdc++.h>
using namespace std;

// Returns maximum size of subset with no pair
// sum divisible by K
int subsetPairNotDivisibleByK(int arr[], int N,
                                         int K)
{
    // Array for storing frequency of modulo
    // values
    int f[K];
    memset(f, 0, sizeof(f));

    // Fill frequency array with values modulo K
    for (int i = 0; i < N; i++)
        f[arr[i] % K]++;

    //  if K is even, then update f[K/2]
    if (K % 2 == 0)
        f[K/2] = min(f[K/2], 1);

    // Initialize result by minimum of 1 or
    // count of numbers giving remainder 0
    int res = min(f[0], 1);

    // Choose maximum of count of numbers
    // giving remainder i or K-i
    for (int i = 1; i <= K/2; i++)
        res += max(f[i], f[K-i]);

    return res;
}

//  Driver code to test above methods
int main()
{
    int arr[] = {3, 7, 2, 9, 1};
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    cout << subsetPairNotDivisibleByK(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get size of subset whose
// each pair sum is not divisible by K
import java.util.Arrays;

class Test {

    // Returns maximum size of subset with no pair
    // sum divisible by K
    static int subsetPairNotDivisibleByK(int arr[],
                                      int N, int K)
    {

        // Array for storing frequency of modulo
        // values
        int f[] = new int[K];
        Arrays.fill(f, 0);

        // Fill frequency array with values modulo K
        for (int i = 0; i < N; i++)
            f[arr[i] % K]++;

        // if K is even, then update f[K/2]
        if (K % 2 == 0)
            f[K/2] = Math.min(f[K/2], 1);

        // Initialize result by minimum of 1 or
        // count of numbers giving remainder 0
        int res = Math.min(f[0], 1);

        // Choose maximum of count of numbers
        // giving remainder i or K-i
        for (int i = 1; i <= K/2; i++)
            res += Math.max(f[i], f[K-i]);

        return res;
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {3, 7, 2, 9, 1};
        int N = arr.length;
        int K = 3;

        System.out.print(subsetPairNotDivisibleByK(
                                         arr, N, K));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to get size of
# subset whose each pair sum is
# not divisible by K

# Returns maximum size of subset
# with no pair sum divisible by K
def subsetPairNotDivisibleByK(arr, N, K):

    # Array for storing frequency
    # of modulo values
    f = [0 for i in range(K)]

    # Fill frequency array with
    # values modulo K
    for i in range(N):
        f[arr[i] % K] += 1

    # if K is even, then update f[K/2]
    if (K % 2 == 0):
        f[K//2] = min(f[K//2], 1)

    # Initialize result by minimum of 1 or
    # count of numbers giving remainder 0
    res = min(f[0], 1)

    # Choose maximum of count of numbers
    # giving remainder i or K-i
    for i in range(1,(K // 2) + 1):
        res += max(f[i], f[K - i])

    return res

# Driver Code
arr = [3, 7, 2, 9, 1]
N = len(arr)
K = 3
print(subsetPairNotDivisibleByK(arr, N, K))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to get size of subset whose
// each pair sum is not divisible by K
using System;

class Test {

    // Returns maximum size of subset
    // with no pair sum divisible by K
    static int subsetPairNotDivisibleByK(int []arr,
                                         int N, int K)
    {
        // Array for storing
        // frequency of modulo values
        int []f = new int[K];
        for(int i = 0; i < K; i++)
        f[i] = 0;

        // Fill frequency array with values modulo K
        for (int i = 0; i < N; i++)
            f[arr[i] % K]++;

        // if K is even, then update f[K/2]
        if (K % 2 == 0)
            f[K/2] = Math.Min(f[K/2], 1);

        // Initialize result by minimum of 1 or
        // count of numbers giving remainder 0
        int res = Math.Min(f[0], 1);

        // Choose maximum of count of numbers
        // giving remainder i or K-i
        for (int i = 1; i <= K/2; i++)
            res += Math.Max(f[i], f[K-i]);

        return res;
    }

    // Driver method
    public static void Main()
    {
        int []arr = {3, 7, 2, 9, 1};
        int N = arr.Length;
        int K = 3;

        // Function calling
        Console.Write(subsetPairNotDivisibleByK(arr, N, K));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get size of subset whose
// each pair sum is not divisible by K

// Returns maximum size of subset with
// no pair sum divisible by K
function subsetPairNotDivisibleByK(&$arr, $N, $K)
{
    // Array for storing frequency of
    // modulo values
    $f = array_fill(0, $K, NULL);

    // Fill frequency array with
    // values modulo K
    for ($i = 0; $i < $N; $i++)
        $f[$arr[$i] % $K]++;

    // if K is even, then update f[K/2]
    if ($K % 2 == 0)
        $f[$K / 2] = min($f[$K / 2], 1);

    // Initialize result by minimum of 1 or
    // count of numbers giving remainder 0
    $res = min($f[0], 1);

    // Choose maximum of count of numbers
    // giving remainder i or K-i
    for ($i = 1; $i <= $K / 2; $i++)
        $res += max($f[$i], $f[$K - $i]);

    return $res;
}

// Driver Code
$arr = array(3, 7, 2, 9, 1);
$N = sizeof($arr);
$K = 3;
echo subsetPairNotDivisibleByK($arr, $N, $K);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to get size of subset whose
// each pair sum is not divisible by K

    // Returns maximum size of subset with no pair
    // sum divisible by K
    function subsetPairNotDivisibleByK(arr,N,K)
    {
        // Array for storing frequency of modulo
        // values
        let f = new Array(K);
        for(let i=0;i<K;i++)
        {
            f[i]=0;
        }

        // Fill frequency array with values modulo K
        for (let i = 0; i < N; i++)
            f[arr[i] % K]++;

        // if K is even, then update f[K/2]
        if (K % 2 == 0)
            f[K/2] = Math.min(f[K/2], 1);

        // Initialize result by minimum of 1 or
        // count of numbers giving remainder 0
        let res = Math.min(f[0], 1);

        // Choose maximum of count of numbers
        // giving remainder i or K-i
        for (let i = 1; i <= K/2; i++)
            res += Math.max(f[i], f[K-i]);

        return res;
    }

    let arr=[3, 7, 2, 9, 1];
    let N = arr.length;
    let K = 3;
    document.write(subsetPairNotDivisibleByK(
                                         arr, N, K));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(N+K)
T3】辅助空间: O(K)
本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。