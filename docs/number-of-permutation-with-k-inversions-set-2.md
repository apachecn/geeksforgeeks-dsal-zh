# K 次逆序排列数|集合 2

> 原文:[https://www . geeksforgeeks . org/带-k-逆的置换数-set-2/](https://www.geeksforgeeks.org/number-of-permutation-with-k-inversions-set-2/)

给定两个整数 **N** 和 **K** ，任务是计算恰好具有 **K** 逆的第一个 **N** 自然数的排列数。由于计数可能很大，所以以 **10 <sup>9</sup> + 7** 为模打印。

> 一个[反转](https://www.geeksforgeeks.org/counting-inversions/)被定义为一对 a[i]，a[j]，使得 **a[i] > a[j]** 和 **i < j** 。

**示例:**

> **输入:** N = 3，K = 2
> **输出:** 2
> **说明:**
> N = 3 的所有排列都是 321，231，213，312，132，123。
> 其中只有 231 和 312 有 2 个倒位为:
> 
> *   **231:** 2 > 1 & 3 > 1
> *   **312:** 3 > 1 & 3 > 2。
> 
> 因此，两者都满足恰好有 K 个反转的条件。
> 
> **输入:** N = 5，K = 5
> T3】输出: 22

**天真的做法:**参考[之前的帖子](https://www.geeksforgeeks.org/number-of-permutation-with-k-inversions/)了解最简单的解决问题的方法。
***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

[**【动态规划】**](https://www.geeksforgeeks.org/dynamic-programming/) **采用自上而下的方法:**自上而下的方法参见本文[上一篇文章](https://www.geeksforgeeks.org/number-of-permutation-with-k-inversions/)。
***时间复杂度:**O(N * K<sup>2</sup>)*
***辅助空间:** O(N*K)*

[](https://www.geeksforgeeks.org/dynamic-programming/)****使用自下而上的方法进行动态编程:****

**插图:**

> ****例如:N = 4，K = 2****
> 
> **N–1 = 3，K<sub>0</sub>= 0…123 =>1423
> N–1 = 3，K <sub>1</sub> = 1 … 213，132 = > 2143，1342
> N–1 = 3，K <sub>2</sub> = 2 … 231，312 = > 2314，3124
> 所以答案是 **5 【T10****
> 
> **最大值取在**(K–N+1)**和 **0** 之间，因为如果**(N–1)**数的排列中的逆序数小于**K –( N–1)**的话，就不能得到 K 个逆序，因为在开头加上 **N <sup>th</sup>** 数最多可以得到(N–1)个新的逆序。**

**按照以下步骤解决问题:**

*   **创建一个辅助数组 **dp[2][K + 1]** ，其中 **dp[N][K]** 存储所有带有**K =(max(K –( N-1)，0)到 K)** 倒序的**(N–1)**号码的排列，只需将 **N <sup>th</sup>** 号码与它们相加一次。**
*   **使用 **dp[i % 2][K]** 将在两行之间交换迭代，取**j = Max(K –( N–1)，0)** 。所以**DP[N[K]= DP[N-1][j]+DP[N-1][j+1]+…。+DP[N–1][K]**。**
*   **为了计算**DP【N】【K】**不需要额外进行这个 **K** 迭代，因为它可以在 O(1)中从**DP【N】【K–1】**获得。所以递推关系由下式给出:

    *   **DP[n][k]= DP[n][k-1]+DP[n-1][k]-DP[n-1][最大(k)-(n-1，0)-1]**** 
*   **分别使用变量 **i** 和 **j** 在 **N** 和 **K** 上迭代两个嵌套循环，并按照上述递归关系更新每个 dp 状态。**
*   **将上述步骤后 **dp[N%2][K]** 的值打印为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count permutations with
// K inversions
int numberOfPermWithKInversion(
    int N, int K)
{
    // Store number of permutations
    // with K inversions
    int dp[2][K + 1];

    int mod = 1000000007;

    for (int i = 1; i <= N; i++) {
        for (int j = 0; j <= K; j++) {

            // If N = 1 only 1 permutation
            // with no inversion
            if (i == 1)
                dp[i % 2][j] = (j == 0);

            // For K = 0 only 1 permutation
            // with no inversion
            else if (j == 0)
                dp[i % 2][j] = 1;

            // Otherwise Update each dp
            // state as per the reccurrance
            // relation formed
            else
                dp[i % 2][j]
                    = (dp[i % 2][j - 1] % mod
                       + (dp[1 - i % 2][j]
                          - ((max(j - (i - 1), 0) == 0)
                                 ? 0
                                 : dp[1 - i % 2]
                                     [max(j - (i - 1), 0)
                                      - 1])
                          + mod)
                             % mod)
                      % mod;
            ;
        }
    }

    // Print final count
    cout << dp[N % 2][K];
}

// Driver Code
int main()
{
    // Given N and K
    int N = 3, K = 2;

    // Function Call
    numberOfPermWithKInversion(N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count permutations with
// K inversions
static void numberOfPermWithKInversion(int N, int K)
{

    // Store number of permutations
    // with K inversions
    int[][] dp = new int[2][K + 1];

    int mod = 1000000007;

    for(int i = 1; i <= N; i++) 
    {
        for(int j = 0; j <= K; j++) 
        {

            // If N = 1 only 1 permutation
            // with no inversion
            if (i == 1)
            {
                dp[i % 2][j] = (j == 0) ? 1 : 0;
            }

            // For K = 0 only 1 permutation
            // with no inversion
            else if (j == 0)
                dp[i % 2][j] = 1;

            // Otherwise Update each dp
            // state as per the reccurrance
            // relation formed
            else
                {
                 int maxm = Math.max(j - (i - 1));
             dp[i % 2][j] = (dp[i % 2][j - 1] % mod +
                               (dp[1 - i % 2][j] - 
                               ((Math.max(j - (i - 1), 0) == 0) ?
                                   0 : dp[1 - i % 2][maxm, 0) - 1]) +
                                         mod) % mod) % mod;
}
        }
    }

    // Print final count
    System.out.println (dp[N % 2][K]);
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 3, K = 2;

    // Function Call
    numberOfPermWithKInversion(N, K);
}
}

// This code is contributed by akhilsaini
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count permutations with
# K inversions
def numberOfPermWithKInversion(N, K):

    # Store number of permutations
    # with K inversions
    dp = [[0] * (K + 1)] * 2

    mod = 1000000007

    for i in range(1, N + 1):
        for j in range(0, K + 1):

            # If N = 1 only 1 permutation
            # with no inversion
            if (i == 1):
                dp[i % 2][j] = 1 if (j == 0) else 0

            # For K = 0 only 1 permutation
            # with no inversion
            elif (j == 0):
                dp[i % 2][j] = 1

            # Otherwise Update each dp
            # state as per the reccurrance
            # relation formed
            else:
                var = (0 if (max(j - (i - 1), 0) == 0)
                         else dp[1 - i % 2][max(j - (i - 1), 0) - 1])
                dp[i % 2][j] = ((dp[i % 2][j - 1] % mod +
                                (dp[1 - i % 2][j] -
                                (var) + mod) % mod) % mod)

    # Print final count
    print(dp[N % 2][K])

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N = 3
    K = 2

    # Function Call
    numberOfPermWithKInversion(N, K)

# This code is contributed by akhilsaini
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to count permutations with
// K inversions
static void numberOfPermWithKInversion(int N, int K)
{

    // Store number of permutations
    // with K inversions
    int[,] dp = new int[2, K + 1];

    int mod = 1000000007;

    for(int i = 1; i <= N; i++)
    {
        for(int j = 0; j <= K; j++) 
        {

            // If N = 1 only 1 permutation
            // with no inversion
            if (i == 1)
            {
                dp[i % 2, j] = (j == 0) ? 1 : 0;
            }

            // For K = 0 only 1 permutation
            // with no inversion
            else if (j == 0)
                dp[i % 2, j] = 1;

            // Otherwise Update each dp
            // state as per the reccurrance
            // relation formed
            else
                dp[i % 2, j] = (dp[i % 2, j - 1] % mod + 
                               (dp[1 - i % 2, j] - 
                               ((Math.Max(j - (i - 1), 0) == 0) ?
                                   0 : dp[1 - i % 2, Math.Max(
                                          j - (i - 1), 0) - 1]) +
                                              mod) % mod) % mod;
        }
    }

    // Print final count
    Console.WriteLine(dp[N % 2, K]);
}

// Driver Code
public static void Main()
{

    // Given N and K
    int N = 3, K = 2;

    // Function Call
    numberOfPermWithKInversion(N, K);
}
}

// This code is contributed by akhilsaini
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

// Function to count permutations with
// K inversions
function numberOfPermWithKInversion(N, K)
{

    // Store number of permutations
    // with K inversions
    let dp = new Array(2);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) 
    {
    dp[i] = new Array(2);
    }

    let mod = 1000000007;

    for(let i = 1; i <= N; i++) 
    {
        for(let j = 0; j <= K; j++) 
        {

            // If N = 1 only 1 permutation
            // with no inversion
            if (i == 1)
            {
                dp[i % 2][j] = (j == 0) ? 1 : 0;
            }

            // For K = 0 only 1 permutation
            // with no inversion
            else if (j == 0)
                dp[i % 2][j] = 1;

            // Otherwise Update each dp
            // state as per the reccurrance
            // relation formed
            else
                dp[i % 2][j] = (dp[i % 2][j - 1] % mod +
                 (dp[1 - i % 2][j] - 
                 ((Math.max(j - (i - 1), 0) == 0) ?
                   0 : dp[1 - i % 2][Math.max(j - 
                          (i - 1), 0) - 1]) +
                             mod) % mod) % mod;
        }
    }

    // Print final count
    document.write(dp[N % 2][K]);
}

    // Driver Code

           // Given N and K
    let N = 3, K = 2;

    // Function Call
    numberOfPermWithKInversion(N, K);

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N * K)*
***辅助空间:** O(K)***