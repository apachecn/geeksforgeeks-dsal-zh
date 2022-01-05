# 具有 K 个逆的置换数

> 原文:[https://www . geeksforgeeks . org/带-k-逆的置换数/](https://www.geeksforgeeks.org/number-of-permutation-with-k-inversions/)

给定一个数组，求逆定义为 a[i]，a[j]这样的一对，a[i] > a[j]和 i < j .给我们两个数字 N 和 K，我们需要知道前 N 个数字中有多少排列恰好有 K 个求逆。

**示例:**

```
Input  : N = 3, K = 1
Output : 2
Explanation :  
Total Permutation of first N number,
123, 132, 213, 231, 312, 321
Permutation with 1 inversion : 132 and 213

Input  : N = 4, K = 2
Output : 5
```

解决这个问题的一个简单方法是记下[所有的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，然后检查它们中的逆序计数，但是遍历排列本身将花费 O(N！)时间，太大了。

我们可以用动态规划的方法来解决这个问题。下面是递归公式。

```
If N is 0, Count(0, K) = 0

If K is 0, Count(N, 0) = 1 (Only sorted array)

In general case, 
If we have N number and require K inversion, 
Count(N, K) = Count(N - 1, K) + 
              Count(N – 1, K - 1) + 
              Count(N – 1, K – 2) + 
              .... + 
              Count(N – 1, 0)
```

**以上递归公式是如何工作的？**
如果我们有 N 个数，想有 K 个排列，假设(N–1)数的所有排列都写在某个地方，那么新的数(第 N 个数，最大)需要放在(N–1)数的所有排列中，那些加完这个数后逆序数变成 K 的应该加到我们的答案中。现在拿那些已经让(K–3)求逆的(N–1)数的置换集来说，现在我们可以把这个新的最大的数放在从最后开始的位置 3，那么求逆计数将是 K，所以计数(N–1，K–3)应该加到我们的答案中，同样的参数也可以给其他求逆，我们将得到上面的递归作为最终的答案。

下面的代码是按照上面的递归以记忆的方式编写的。

## C++

```
// C++ program to find number of permutation
// with K inversion using Memoization
#include <bits/stdc++.h>
using namespace std;

// Limit on N and K
const int M = 100;

// 2D array memo for stopping
// solving same problem again
int memo[M][M];

// method recursively calculates
// permutation with K inversion
int numberOfPermWithKInversion(int N, int K)
{

    // base cases
    if (N == 0)
        return 0;
    if (K == 0)
        return 1;

    // if already solved then
    // return result directly
    if (memo[N][K] != 0)
        return memo[N][K];

    // calling recursively all subproblem
    // of permutation size N - 1
    int sum = 0;
    for (int i = 0; i <= K; i++)
    {

        // Call recursively only
        // if total inversion
        // to be made are less
        // than size
        if (i <= N - 1)
            sum += numberOfPermWithKInversion(N - 1,
                                              K - i);
    }

    // store result into memo
    memo[N][K] = sum;

    return sum;
}

// Driver code
int main()
{
    int N = 4;
    int K = 2;
    cout << numberOfPermWithKInversion(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of permutation with
// K inversion using Memoization

import java.io.*;

class GFG {

    // Limit on N and K
    static int M = 100;

    // 2D array memo for stopping solving same problem
    // again
    static int memo[][] = new int[M][M];

    // method recursively calculates permutation with
    // K inversion
    static int numberOfPermWithKInversion(int N, int K)
    {

        // base cases
        if (N == 0)
            return 0;
        if (K == 0)
            return 1;

        // if already solved then return result directly
        if (memo[N][K] != 0)
            return memo[N][K];

        // calling recursively all subproblem of
        // permutation size N - 1
        int sum = 0;
        for (int i = 0; i <= K; i++) {

            // Call recursively only if total inversion
            // to be made are less than size
            if (i <= N - 1)
                sum += numberOfPermWithKInversion(N - 1,
                                                  K - i);
        }

        // store result into memo
        memo[N][K] = sum;

        return sum;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        int N = 4;
        int K = 2;
        System.out.println(numberOfPermWithKInversion(N, K));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find number of permutation
# with K inversion using Memoization

# Limit on N and K
M = 100

# 2D array memo for stopping 
# solving same problem again
memo = [[0 for i in range(M)] for j in range(M)]

# method recursively calculates
# permutation with K inversion
def numberOfPermWithKInversion(N, K):

    # Base cases
    if (N == 0): return 0
    if (K == 0): return 1

    # If already solved then
    # return result directly
    if (memo[N][K] != 0):
        return memo[N][K]

    # Calling recursively all subproblem
    # of permutation size N - 1
    sum = 0
    for i in range(K + 1):

        # Call recursively only if
        # total inversion to be made
        # are less than size
        if (i <= N - 1):
            sum += numberOfPermWithKInversion(N - 1, K - i)

    # store result into memo
    memo[N][K] = sum

    return sum

# Driver code
N = 4; K = 2
print(numberOfPermWithKInversion(N, K))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find number of
// permutation with K inversion
// using Memoization
using System;

class GFG
{

// Limit on N and K
static int M = 100;

// 2D array memo for stopping
// solving same problem again
static int [,]memo = new int[M, M];

// method recursively calculates
// permutation with K inversion
static int numberOfPermWithKInversion(int N,
                                      int K)
{

    // base cases
    if (N == 0)
        return 0;
    if (K == 0)
        return 1;

    // if already solved then
    // return result directly
    if (memo[N, K] != 0)
        return memo[N, K];

    // calling recursively all
    // subproblem of permutation
    // size N - 1
    int sum = 0;
    for (int i = 0; i <= K; i++)
    {

        // Call recursively only if
        // total inversion to be
        // made are less than size
        if (i <= N - 1)
            sum += numberOfPermWithKInversion(N - 1,
                                              K - i);
    }

    // store result into memo
    memo[N, K] = sum;

    return sum;
}

// Driver Code
static public void Main ()
{
    int N = 4;
    int K = 2;
    Console.WriteLine(numberOfPermWithKInversion(N, K));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of permutation
// with K inversion using Memoization

// method recursively calculates
// permutation with K inversion
function numberOfPermWithKInversion($N, $K)
{

    $memo = array();

    // base cases
    if ($N == 0)
        return 0;
    if ($K == 0)
        return 1;

    // if already solved then
    // return result directly
    if ($memo[$N][$K] != 0)
        return $memo[$N][$K];

    // calling recursively all subproblem
    // of permutation size N - 1
    $sum = 0;
    for ($i = 0; $i <= $K; $i++)
    {

        // Call recursively only
        // if total inversion
        // to be made are less
        // than size
        if ($i <= $N - 1)
            $sum += numberOfPermWithKInversion($N - 1,
                                               $K - $i);
    }

    // store result into memo
    $memo[$N][$K] = $sum;

    return $sum;
}

// Driver code
$N = 4;
$K = 2;
echo numberOfPermWithKInversion($N, $K);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to find number of
// permutation with K inversion using
// Memoization

// Limit on N and K
let M = 100;

// 2D array memo for stopping solving
// same problem again
let memo = new Array(M);
for(let i = 0; i < M; i++)
{
    memo[i] = new Array(M);
    for(let j = 0; j < M; j++)
    {
        memo[i][j] = 0;
    }
}

// Method recursively calculates permutation
// with K inversion
function numberOfPermWithKInversion(N, K)
{

    // base cases
    if (N == 0)
        return 0;
    if (K == 0)
        return 1;

    // If already solved then return
    // result directly
    if (memo[N][K] != 0)
        return memo[N][K];

    // Calling recursively all subproblem of
    // permutation size N - 1
    let sum = 0;
    for(let i = 0; i <= K; i++)
    {

        // Call recursively only if total inversion
        // to be made are less than size
        if (i <= N - 1)
            sum += numberOfPermWithKInversion(
                N - 1, K - i);
    }

    // Store result into memo
    memo[N][K] = sum;

    return sum;
}

// Driver code
let N = 4;
let K = 2;

document.write(numberOfPermWithKInversion(N, K));

// This code is contributed by divyesh072019 

</script>
```

**Output**

```
5
```

**时间复杂度:** O(N*N*K)

**优化方法:**使用列表和累积和

## C++

```
// C++ program to find number of permutation
// with K inversions

#include <bits/stdc++.h>
using namespace std;

int numberOfPermWithKInversions(int N, int K) {
    vector<vector<int>> dp(N+1,vector<int>(K+1));

    // As for k=0, number of permutations is 1 for every N
      for(int i = 1; i <= N; i++)
        dp[i][0] = 1;

      // Using Dynamic Programming with cumulative sum
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= K; j++)
        {
              // This is same as val = dp[i-1][j] - dp[i-1][j-i]
              // i.e. dp[i-1][j........j-i], just taking care of
              // boundaries
            int val = dp[i-1][j];
            if(j >= i)
                val -= dp[i-1][j-i];

            dp[i][j] = dp[i][j-1] + val;
        }
    }

      // And, in the end calculate the dp[n][k]
      // which is dp[n][k]-dp[n][k-1]
    int ans = dp[N][K];
    if(K >= 1)
        ans -= dp[N][K-1];

    return ans;
}

int main() {
    int N = 4;
    int K = 2;

      cout << numberOfPermWithKInversions(N,K) << "\n";
    return 0;
}
```

**Output**

```
5

```

**时间复杂度:** O(N*K)

本文由 [**【乌卡什·特里维迪】**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)[**安基特·库马尔·夏尔马**](https://www.linkedin.com/in/cgankitsharma/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。