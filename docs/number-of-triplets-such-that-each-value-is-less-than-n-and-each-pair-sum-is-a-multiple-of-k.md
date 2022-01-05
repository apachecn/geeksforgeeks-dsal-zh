# 三元组的数量，使得每个值小于 N，并且每个对和是 K 的倍数

> 原文:[https://www . geeksforgeeks . org/三胞胎数量-这样每个值都小于 n，并且每个对和都是 k 的倍数/](https://www.geeksforgeeks.org/number-of-triplets-such-that-each-value-is-less-than-n-and-each-pair-sum-is-a-multiple-of-k/)

给定两个整数 **N** 和 **K** 。求三元组 **(a，b，c)** 的个数，使 **0 ≤ a，b，c ≤ N** 、 **(a + b)** 、 **(b + c)** 、 **(c + a)** 为 **K** 的倍数。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 9
> 可能的三元组有:
> {(1，1，1)，(1，1，3)，(1，3，1)
> (1，3，3)，(2，2，2)，(3，1，1)
> (3，1，1)，(3，1，3)，(3，3，3，3，3)}
> 
> **输入:** N = 5，K = 3
> **输出:** 1
> 唯一可能的三元组是(3，3，3)

**进场:**鉴于 **(a + b)** 、 **(b + c)** 和 **(c + a)** 是 **K** 的倍数。因此，我们可以说 **(a + b) % K = 0** 、 **(b + c) % K = 0** 、 **(c + a) % K = 0** 。
如果 **a** 属于 **K** 的 **x** 模类，那么 **b** 应该在使用第一个条件的**(K–x)第**模类中。
从第二个条件可以看出 **c** 属于 **K** 的 **x** 模类。现在由于 **a** 和 **c** 属于同一个模类，它们必须满足第三个关系，即 **(a + c) % K = 0** 。只有 **x = 0** 或 **x = K / 2** 才有可能。
当 **K** 为奇数时， **x = K / 2** 无效。

因此要解决这个问题，在 **0 <sup>第</sup>个**模类和 **K** 的 **(K / 2) <sup>个</sup>个**模类中，计算从 **0** 到 **N** 的元素个数。

*   如果 **K** 为**奇数**则结果为**CNT【0】<sup>3</sup>**
*   如果 **K** 是**偶数**，那么结果就是**CNT【0】<sup>3</sup>+CNT【K/2】<sup>3</sup>**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of triplets
int NoofTriplets(int N, int K)
{
    int cnt[K];

    // Initializing the count array
    memset(cnt, 0, sizeof(cnt));

    // Storing the frequency of each modulo class
    for (int i = 1; i <= N; i += 1) {
        cnt[i % K] += 1;
    }

    // If K is odd
    if (K & 1)
        return cnt[0] * cnt[0] * cnt[0];

    // If K is even
    else {
        return (cnt[0] * cnt[0] * cnt[0]
                + cnt[K / 2] * cnt[K / 2] * cnt[K / 2]);
    }
}

// Driver Code
int main()
{
    int N = 3, K = 2;

    // Function Call
    cout << NoofTriplets(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    // Function to return the number of triplets
    static int NoofTriplets(int N, int K)
    {
        int[] cnt = new int[K];

        // Initializing the count array
        Arrays.fill(cnt, 0, cnt.length, 0);

        // Storing the frequency of each modulo class
        for (int i = 1; i <= N; i += 1)
        {
            cnt[i % K] += 1;
        }

        // If K is odd
        if ((K & 1) != 0)
        {
            return cnt[0] * cnt[0] * cnt[0];
        }
        // If K is even
        else
        {
            return (cnt[0] * cnt[0] * cnt[0]
                    + cnt[K / 2] * cnt[K / 2] * cnt[K / 2]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 3, K = 2;

        // Function Call
        System.out.println(NoofTriplets(N, K));
    }
}

// This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the number of triplets
    static int NoofTriplets(int N, int K)
    {
        int[] cnt = new int[K];

        // Initializing the count array
        Array.Fill(cnt, 0, cnt.Length, 0);

        // Storing the frequency of each modulo class
        for (int i = 1; i <= N; i += 1)
        {
            cnt[i % K] += 1;
        }

        // If K is odd
        if ((K & 1) != 0)
        {
            return cnt[0] * cnt[0] * cnt[0];
        }
        // If K is even
        else
        {
            return (cnt[0] * cnt[0] * cnt[0]
                    + cnt[K / 2] * cnt[K / 2] * cnt[K / 2]);
        }
    }

    // Driver Code
    static public void Main ()
    {
            int N = 3, K = 2;

        // Function Call
        Console.Write(NoofTriplets(N, K));
    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the number of triplets
def NoofTriplets(N, K) :

    # Initializing the count array
    cnt = [0]*K;

    # Storing the frequency of each modulo class
    for i in range(1, N + 1) :
        cnt[i % K] += 1;

    # If K is odd
    if (K & 1) :
        rslt = cnt[0] * cnt[0] * cnt[0];
        return rslt

    # If K is even
    else :
        rslt = (cnt[0] * cnt[0] * cnt[0] +
                cnt[K // 2] * cnt[K // 2] * cnt[K // 2]);
        return rslt

# Driver Code
if __name__ == "__main__" :

    N = 3; K = 2;

    # Function Call
    print(NoofTriplets(N, K));

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the number of triplets
function NoofTriplets(N, K)
{
    let cnt = Array(K);

    for(let i = 0; i < K; i++) 
        cnt[i] = 0;

    // Storing the frequency of
    // each modulo class
    for(let i = 1; i <= N; i += 1)
    {
        cnt[i % K] += 1;
    }

    // If K is odd
    if (K & 1)
        return cnt[0] * cnt[0] * cnt[0];

    // If K is even
    else
    {
        return (cnt[0] * cnt[0] * cnt[0] +
                 cnt[K / 2] * cnt[K / 2] *
                 cnt[K / 2]);
    }
}

// Driver Code
let N = 3;
let K = 2;

// Function Call
document.write(NoofTriplets(N, K));

// This code is contributed by mohit kumar 29

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(N)