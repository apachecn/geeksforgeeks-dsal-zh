# 给定约束条件下排列 N 个项目的方式数

> 原文:[https://www . geeksforgeeks . org/给定约束下排列 n 个项目的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-arrange-n-items-under-given-constraints/)

我们得到了总共 K 种不同颜色的 N 件商品。相同颜色的项目无法区分，颜色可以从 1 到 K 编号，每种颜色的项目计数也给出为 k1、k2 等。现在，我们需要在所有可能的颜色的最后一项颜色 I 在最后一项颜色(i + 1)之前的约束下，一个接一个地排列这些项目。我们的目标是找出有多少种方法可以实现这一点。
**例:**

```
Input : N = 3        
        k1 = 1    k2 = 2
Output : 2
Explanation :
Possible ways to arrange are,
k1, k2, k2
k2, k1, k2 

Input : N = 4        
        k1 = 2    k2 = 2
Output : 3
Explanation :
Possible ways to arrange are,
k1, k2, k1, k2
k1, k1, k2, k2
k2, k1, k1, k2 
```

我们可以用动态规划来解决这个问题。让 dp[i]存储排列第一个 I 色项目的方法数量。对于一个彩色项目，答案将是一，因为只有一种方法。现在让我们假设所有项目都在一个序列中。现在，要从 dp[i]转到 dp[i + 1]，我们需要在最末端放置至少一个颜色项(i + 1)，但是其他颜色项(i + 1)可以在序列中的任何位置。排列颜色项(i + 1)的方法的数量是(k1 + k2)的组合..可以表示为(k1 + k2)的(k(I+1)–1)上的+ki+k(I+1)–1..+ki+k(I+1)–1)C(k(I+1)–1)。在这个表达式中，我们减去了一，因为我们需要在最后放一项。
在下面的代码中，首先我们已经计算了组合值，您可以从[这里](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)了解更多信息。之后，我们循环所有不同的颜色，并使用上述关系计算最终值。

## C++

```
// C++ program to find number of ways to arrange
// items under given constraint
#include <bits/stdc++.h>
using namespace std;

// method returns number of ways with which items
// can be arranged
int waysToArrange(int N, int K, int k[])
{
    int C[N + 1][N + 1];
    int i, j;

    // Calculate value of Binomial Coefficient in
    // bottom up manner
    for (i = 0; i <= N; i++) {
        for (j = 0; j <= i; j++) {

            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously
            // stored values
            else
                C[i][j] = (C[i - 1][j - 1] + C[i - 1][j]);
        }
    }

    // declare dp array to store result up to ith
    // colored item
    int dp[K];

    // variable to keep track of count of items
    // considered till now
    int count = 0;

    dp[0] = 1;

    // loop over all different colors
    for (int i = 0; i < K; i++) {

        // populate next value using current value
        // and stated relation
        dp[i + 1] = (dp[i] * C[count + k[i] - 1][k[i] - 1]);
        count += k[i];
    }

    // return value stored at last index
    return dp[K];
}

// Driver code to test above methods
int main()
{
    int N = 4;
    int k[] = { 2, 2 };

    int K = sizeof(k) / sizeof(int);
    cout << waysToArrange(N, K, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to arrange
// items under given constraint
class GFG
{

    // method returns number of ways with which items
    // can be arranged
    static int waysToArrange(int N, int K, int[] k)
    {
        int[][] C = new int[N + 1][N + 1];
        int i, j;

        // Calculate value of Binomial Coefficient in
        // bottom up manner
        for (i = 0; i <= N; i++)
        {
            for (j = 0; j <= i; j++)
            {

                // Base Cases
                if (j == 0 || j == i)
                {
                    C[i][j] = 1;
                }

                // Calculate value using previously
                // stored values
                else
                {
                    C[i][j] = (C[i - 1][j - 1] + C[i - 1][j]);
                }
            }
        }

        // declare dp array to store result up to ith
        // colored item
        int[] dp = new int[K + 1];

        // variable to keep track of count of items
        // considered till now
        int count = 0;

        dp[0] = 1;

        // loop over all different colors
        for (i = 0; i < K; i++)
        {

            // populate next value using current value
            // and stated relation
            dp[i + 1] = (dp[i] * C[count + k[i] - 1][k[i] - 1]);
            count += k[i];
        }

        // return value stored at last index
        return dp[K];
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 4;
        int[] k = new int[]{2, 2};
        int K = k.length;
        System.out.println(waysToArrange(N, K, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find number of ways
# to arrange items under given constraint
import numpy as np

# method returns number of ways with
# which items can be arranged
def waysToArrange(N, K, k) :

    C = np.zeros((N + 1, N + 1))

    # Calculate value of Binomial
    # Coefficient in bottom up manner
    for i in range(N + 1) :
        for j in range(i + 1) :

            # Base Cases
            if (j == 0 or j == i) :
                C[i][j] = 1

            # Calculate value using previously
            # stored values
            else :
                C[i][j] = (C[i - 1][j - 1] +
                           C[i - 1][j])

    # declare dp array to store result
    # up to ith colored item
    dp = np.zeros((K + 1))

    # variable to keep track of count
    # of items considered till now
    count = 0

    dp[0] = 1

    # loop over all different colors
    for i in range(K) :

        # populate next value using current
        # value and stated relation
        dp[i + 1] = (dp[i] * C[count + k[i] - 1][k[i] - 1])
        count += k[i]

    # return value stored at last index
    return dp[K]

# Driver code
if __name__ == "__main__" :

    N = 4
    k = [ 2, 2 ]

    K = len(k)
    print(int(waysToArrange(N, K, k)))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find number of ways to arrange
// items under given constraint
using System;

class GFG
{
    // method returns number of ways with which items
    // can be arranged
    static int waysToArrange(int N, int K, int[] k)
    {
        int[,] C = new int[N + 1, N + 1];
        int i, j;

        // Calculate value of Binomial Coefficient in
        // bottom up manner
        for (i = 0; i <= N; i++) 
        {
            for (j = 0; j <= i; j++)
            {

                // Base Cases
                if (j == 0 || j == i)
                    C[i, j] = 1;

                // Calculate value using previously
                // stored values
                else
                    C[i, j] = (C[i - 1, j - 1] + C[i - 1,  j]);
            }
        }

        // declare dp array to store result up to ith
        // colored item
        int[] dp = new int[K + 1];

        // variable to keep track of count of items
        // considered till now
        int count = 0;

        dp[0] = 1;

        // loop over all different colors
        for (i = 0; i < K; i++) {

            // populate next value using current value
            // and stated relation
            dp[i + 1] = (dp[i] * C[count + k[i] - 1, k[i] - 1]);
            count += k[i];
        }

        // return value stored at last index
        return dp[K];
    }

    // Driver code 
    static void Main()
    {
        int N = 4;
        int[] k = new int[]{ 2, 2 };
        int K = k.Length;
        Console.Write(waysToArrange(N, K, k));
    }
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// ways to arrange items under
// given constraint

// method returns number of ways
// with which items can be arranged
function waysToArrange($N, $K, $k)
{
    $C[$N + 1][$N + 1] = array(array());

    // Calculate value of Binomial 
    // Coefficient in bottom up manner
    for ($i = 0; $i <= $N; $i++)
    {
        for ($j = 0; $j <= $i; $j++)
        {

            // Base Cases
            if ($j == 0 || $j == $i)
                $C[$i][$j] = 1;

            // Calculate value using
            // previously stored values
            else
                $C[$i][$j] = ($C[$i - 1][$j - 1] +
                              $C[$i - 1][$j]);
        }
    }

    // declare dp array to store
    // result up to ith colored item
    $dp[$K] = array();

    // variable to keep track of count
    // of items considered till now
    $count = 0;

    $dp[0] = 1;

    // loop over all different colors
    for ($i = 0; $i < $K; $i++)
    {

        // populate next value using
        // current value and stated relation
        $dp[$i + 1] = ($dp[$i] * $C[$count +
                        $k[$i] - 1][$k[$i] - 1]);
        $count += $k[$i];
    }

    // return value stored at
    // last index
    return $dp[$K];
}

// Driver code
$N = 4;
$k = array( 2, 2 );

$K = sizeof($k);
echo waysToArrange($N, $K, $k),"\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
// Javascript program to find number of ways to arrange
// items under given constraint.

    // method returns number of ways with which items
    // can be arranged
    function waysToArrange(N, K, k)
    {
        let C = new Array(N + 1);
        // Loop to create 2D array using 1D array
        for (let i = 0; i < C.length; i++) {
            C[i] = new Array(2);
        }

        let i, j;

        // Calculate value of Binomial Coefficient in
        // bottom up manner
        for (i = 0; i <= N; i++)
        {
            for (j = 0; j <= i; j++)
            {

                // Base Cases
                if (j == 0 || j == i)
                {
                    C[i][j] = 1;
                }

                // Calculate value using previously
                // stored values
                else
                {
                    C[i][j] = (C[i - 1][j - 1] + C[i - 1][j]);
                }
            }
        }

        // declare dp array to store result up to ith
        // colored item
        let dp = Array.from({length: K+1}, (_, i) => 0);

        // variable to keep track of count of items
        // considered till now
        let count = 0;

        dp[0] = 1;

        // loop over all different colors
        for (i = 0; i < K; i++)
        {

            // populate next value using current value
            // and stated relation
            dp[i + 1] = (dp[i] * C[count + k[i] - 1][k[i] - 1]);
            count += k[i];
        }

        // return value stored at last index
        return dp[K];
    }

// driver function

        let N = 4;
        let k = [2, 2];
        let K = k.length;
        document.write(waysToArrange(N, K, k));

</script>   
```

**输出:**

```
3
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。