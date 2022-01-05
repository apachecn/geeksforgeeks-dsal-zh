# 0-1 背包问题的空间优化动态规划解

> 原文:[https://www . geesforgeks . org/space-optimized-DP-solution-0-1-背包问题/](https://www.geeksforgeeks.org/space-optimized-dp-solution-0-1-knapsack-problem/)

给定 n 个物品的重量和值，将这些物品放入容量为 W 的背包中，得到背包中的最大总值。换句话说，给定两个整型数组 val[0..n-1]和 wt[0..n-1 ),其分别表示与 n 个项目相关联的值和权重。同样给定一个代表背包容量的整数 W，找出 val[]的最大值子集，使得这个子集的权重之和小于或等于 W。我们不能分解一个项目，要么选择完整的项目，要么不选择它(0-1 属性)。
这里 W < = 2000000，n < = 500

**示例:**

```
Input : W = 10, n = 3
        val[] = {7, 8, 4}
        wt[] = {3, 8, 6}
Output: 11
We get maximum value by picking items of 3 KG and 6 KG.
```

我们已经讨论了基于动态规划的解决方案。在前面的解决方案中，我们使用了一个 n * W 矩阵。我们可以减少使用的额外空间。优化背后的思想是，为了计算 mat[i][j]，我们只需要前一行的解。在 0-1 背包问题中，如果我们当前在 mat[i][j]上，并且我们包含了第一个元素，那么我们在前一行中向后移动 j-wt[i]步，并且如果我们排除当前元素，那么我们在前一行的第十列上移动。所以在这里我们可以观察到，一次我们只处理 2 个连续的行。

在下面的解决方案中，我们创建了一个大小为 2*W 的矩阵。如果 n 是奇数，那么最终答案将在 mat[0][W]处，如果 n 是偶数，那么最终答案将在 mat[1][W]处，因为索引从 0 开始。

## C++

```
// C++ program of a space optimized DP solution for
// 0-1 knapsack problem.
#include<bits/stdc++.h>
using namespace std;

// val[] is for storing maximum profit for each weight
// wt[] is for storing weights
// n number of item
// W maximum capacity of bag
// mat[2][W+1] to store final result
int KnapSack(int val[], int wt[], int n, int W)
{
    // matrix to store final result
    int mat[2][W+1];
    memset(mat, 0, sizeof(mat));

    // iterate through all items
    int i = 0;
    while (i < n) // one by one traverse each element
    {
        int j = 0; // traverse all weights j <= W

        // if i is odd that mean till now we have odd
        // number of elements so we store result in 1th
        // indexed row
        if (i%2!=0)
        {
            while (++j <= W) // check for each value
            {
                if (wt[i] <= j) // include element
                    mat[1][j] = max(val[i] + mat[0][j-wt[i]],
                                    mat[0][j] );
                else           // exclude element
                    mat[1][j] = mat[0][j];
            }

        }

        // if i is even that mean till now we have even number
        // of elements so we store result in 0th indexed row
        else
        {
            while(++j <= W)
            {
                if (wt[i] <= j)
                    mat[0][j] = max(val[i] + mat[1][j-wt[i]],
                                     mat[1][j]);
                else
                    mat[0][j] = mat[1][j];
            }
        }
        i++;
    }

    // Return mat[0][W] if n is odd, else mat[1][W]
    return (n%2 != 0)? mat[0][W] : mat[1][W];
}

// Driver program to test the cases
int main()
{
    int val[] = {7, 8, 4}, wt[] = {3, 8, 6}, W = 10, n = 3;
    cout << KnapSack(val, wt, n, W) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of a space optimized DP solution for
// 0-1 knapsack problem.
class GFG
{

    // val[] is for storing maximum
    // profit for each weight
    // wt[] is for storing weights
    // n number of item
    // W maximum capacity of bag
    // mat[2][W+1] to store final result
    static int KnapSack(int val[], int wt[],
                            int n, int W)
    {
        // matrix to store final result
        int mat[][] = new int[2][W + 1];

        // iterate through all items
        int i = 0;
        while (i < n) // one by one traverse each element
        {
            int j = 0; // traverse all weights j <= W

            // if i is odd that mean till now we have odd
            // number of elements so we store result in 1th
            // indexed row
            if (i % 2 != 0)
            {
                while (++j <= W) // check for each value
                {
                    if (wt[i] <= j) // include element
                    {
                        mat[1][j] = Math.max(val[i] + mat[0][j - wt[i]],
                                                      mat[0][j]);
                    } else // exclude element
                    {
                        mat[1][j] = mat[0][j];
                    }
                }

            }

            // if i is even that means till now
            // we have even number of elements
            // so we store result in 0th indexed row
            else
            {
                while (++j <= W)
                {
                    if (wt[i] <= j)
                    {
                        mat[0][j] = Math.max(val[i] + mat[1][j - wt[i]],
                                                      mat[1][j]);
                    } else
                    {
                        mat[0][j] = mat[1][j];
                    }
                }
            }
            i++;
        }

        // Return mat[0][W] if n is odd, else mat[1][W]
        return (n % 2 != 0) ? mat[0][W] : mat[1][W];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int val[] = {7, 8, 4},
            wt[] = {3, 8, 6},
            W = 10, n = 3;
        System.out.println(KnapSack(val, wt, n, W));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program of a space
# optimized DP solution for
# 0-1 knapsack problem.

# val[] is for storing maximum
# profit for each weight
# wt[] is for storing weights
# n number of item
# W maximum capacity of bag
# mat[2][W+1] to store final result

def KnapSack(val, wt, n, W):

    # matrix to store final result
    mat = [[0 for i in range(W + 1)]
              for i in range(2)]
    # iterate through all items
    i = 0
    while i < n: # one by one traverse
                 # each element
        j = 0 # traverse all weights j <= W

        # if i is odd that mean till
        # now we have odd number of
        # elements so we store result 
        # in 1th indexed row
        if i % 2 == 0:
            while j < W: # check for each value
                j += 1
                if wt[i] <= j: # include element
                    mat[1][j] = max(val[i] + mat[0][j -
                                     wt[i]], mat[0][j])
                else: # exclude element
                    mat[1][j] = mat[0][j]

        # if i is even that mean till
        # now we have even number
        # of elements so we store
        # result in 0th indexed row
        else:
            while j < W:
                j += 1
                if wt[i] <= j:
                    mat[0][j] = max(val[i] + mat[1][j -
                                     wt[i]], mat[1][j])
                else:
                    mat[0][j] = mat[1][j]
        i += 1
    # Return mat[0][W] if n is
    # odd, else mat[1][W]
    if n % 2 == 0:
        return mat[0][W]
    else:
        return mat[1][W]

# Driver code
val = [7, 8, 4]
wt = [3, 8, 6]
W = 10
n = 3
print(KnapSack(val, wt, n, W))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program of a space optimized DP solution for
// 0-1 knapsack problem.
using System;

class GFG
{

    // val[] is for storing maximum
    // profit for each weight
    // wt[] is for storing weights
    // n number of item
    // W maximum capacity of bag
    // mat[2,W+1] to store final result
    static int KnapSack(int []val, int []wt,
                            int n, int W)
    {
        // matrix to store final result
        int [,]mat = new int[2, W + 1];

        // iterate through all items
        int i = 0;
        while (i < n) // one by one traverse each element
        {
            int j = 0; // traverse all weights j <= W

            // if i is odd that mean till now we have odd
            // number of elements so we store result in 1th
            // indexed row
            if (i % 2 != 0)
            {
                while (++j <= W) // check for each value
                {
                    if (wt[i] <= j) // include element
                    {
                        mat[1, j] = Math.Max(val[i] + mat[0, j - wt[i]],
                                                      mat[0, j]);
                    } else // exclude element
                    {
                        mat[1,j] = mat[0,j];
                    }
                }

            }

            // if i is even that means till now
            // we have even number of elements
            // so we store result in 0th indexed row
            else
            {
                while (++j <= W)
                {
                    if (wt[i] <= j)
                    {
                        mat[0, j] = Math.Max(val[i] + mat[1, j - wt[i]],
                                                      mat[1, j]);
                    }
                    else
                    {
                        mat[0, j] = mat[1, j];
                    }
                }
            }
            i++;
        }

        // Return mat[0,W] if n is odd, else mat[1,W]
        return (n % 2 != 0) ? mat[0, W] : mat[1, W];
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []val = {7, 8, 4};
        int []wt = {3, 8, 6};
        int W = 10, n = 3;
        Console.WriteLine(KnapSack(val, wt, n, W));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of a space optimized DP
// solution for 0-1 knapsack problem.

// val[] is for storing maximum profit
// for each weight wt[] is for storing
// weights n number of item
// W maximum capacity of bag
// mat[2][W+1] to store final result
function KnapSack(&$val, &$wt, $n, $W)
{
    // matrix to store final result
    $mat = array_fill(0, 2,
           array_fill(0, $W + 1, NULL));

    // iterate through all items
    $i = 0;
    while ($i < $n) // one by one traverse
                    // each element
    {
        $j = 0; // traverse all weights j <= W

        // if i is odd that mean till now we
        // have odd number of elements so we
        // store result in 1th indexed row
        if ($i % 2 != 0)
        {
            while (++$j <= $W) // check for each value
            {
                if ($wt[$i] <= $j) // include element
                    $mat[1][$j] = max($val[$i] + $mat[0][$j -
                                       $wt[$i]], $mat[0][$j]);
                else         // exclude element
                    $mat[1][$j] = $mat[0][$j];
            }

        }

        // if i is even that mean till now we have
        // even number of elements so we store result
        // in 0th indexed row
        else
        {
            while(++$j <= $W)
            {
                if ($wt[$i] <= $j)
                    $mat[0][$j] = max($val[$i] + $mat[1][$j -
                                       $wt[$i]], $mat[1][$j]);
                else
                    $mat[0][$j] = $mat[1][$j];
            }
        }
        $i++;
    }

    // Return mat[0][W] if n is odd,
    // else mat[1][W]
    if ($n % 2 != 0)
        return $mat[0][$W];
    else
        return $mat[1][$W];
}

// Driver Code
$val = array(7, 8, 4);
$wt = array(3, 8, 6);
$W = 10;
$n = 3;
echo KnapSack($val, $wt, $n, $W) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program of a space optimized DP solution for
// 0-1 knapsack problem.

    // val[] is for storing maximum
    // profit for each weight
    // wt[] is for storing weights
    // n number of item
    // W maximum capacity of bag
    // mat[2][W+1] to store final result
    function KnapSack(val, wt, n, W)
    {

        // matrix to store final result
        let mat = new Array(2);
        for(let i = 0; i < 2; i++)
        {
            mat[i] = new Array(W + 1);
        }
        for(let i = 0; i < 2; i++)
        {
            for(let j = 0; j < W + 1; j++)
            {
                mat[i][j] = 0;
            }
        }

        // iterate through all items
        let i = 0;
        while (i < n) // one by one traverse each element
        {
            let j = 0; // traverse all weights j <= W

            // if i is odd that mean till now we have odd
            // number of elements so we store result in 1th
            // indexed row
            if (i % 2 != 0)
            {
                while (++j <= W) // check for each value
                {
                    if (wt[i] <= j) // include element
                    {
                        mat[1][j] = Math.max(val[i] + mat[0][j - wt[i]],
                                                      mat[0][j]);
                    } else // exclude element
                    {
                        mat[1][j] = mat[0][j];
                    }
                }

            }

            // if i is even that means till now
            // we have even number of elements
            // so we store result in 0th indexed row
            else
            {
                while (++j <= W)
                {
                    if (wt[i] <= j)
                    {
                        mat[0][j] = Math.max(val[i] + mat[1][j - wt[i]],
                                                      mat[1][j]);
                    } else
                    {
                        mat[0][j] = mat[1][j];
                    }
                }
            }
            i++;
        }

        // Return mat[0][W] if n is odd, else mat[1][W]
        return (n % 2 != 0) ? mat[0][W] : mat[1][W];
    }

    let val=[7, 8, 4];
    let wt=[3, 8, 6];
    let W = 10, n = 3;
    document.write(KnapSack(val, wt, n, W));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
11
```

**时间复杂度:**O(n * W)
T3】辅助空间: O(W)

这是一个由 Gaurav Mamgain 贡献的优化代码

## C++

```
// C++ program of a space optimized DP solution for
// 0-1 knapsack problem.
#include<bits/stdc++.h>
using namespace std;

// val[] is for storing maximum profit for each weight
// wt[] is for storing weights
// n number of item
// W maximum capacity of bag
// dp[W+1] to store final result
int KnapSack(int val[], int wt[], int n, int W)
{
    // array to store final result
    //dp[i] stores the profit with KnapSack capacity "i"
    int dp[W+1];

    //initially profit with 0 to W KnapSack capacity is 0
    memset(dp, 0, sizeof(dp));

    // iterate through all items
    for(int i=0; i < n; i++)
        //traverse dp array from right to left
        for(int j=W; j>=wt[i]; j--)
            dp[j] = max(dp[j] , val[i] + dp[j-wt[i]]);
    /*above line finds out maximum of  dp[j](excluding ith element value)
      and val[i] + dp[j-wt[i]] (including ith element value and the
      profit with "KnapSack capacity - ith element weight") */   
    return dp[W];
}

// Driver program to test the cases
int main()
{
    int val[] = {7, 8, 4}, wt[] = {3, 8, 6}, W = 10, n = 3;
    cout << KnapSack(val, wt, n, W) << endl;
    return 0;
}

// This code is contributed by Gaurav Mamgain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of a space optimized DP solution for
// 0-1 knapsack problem.
import java.util.Arrays;

class GFG
{

// val[] is for storing maximum profit for each weight
// wt[] is for storing weights
// n number of item
// W maximum capacity of bag
// dp[W+1] to store final result
static int KnapSack(int val[], int wt[], int n, int W)
{
    // array to store final result
    //dp[i] stores the profit with KnapSack capacity "i"
    int []dp = new int[W+1];

    //initially profit with 0 to W KnapSack capacity is 0
    Arrays.fill(dp, 0);

    // iterate through all items
    for(int i=0; i < n; i++)

        //traverse dp array from right to left
        for(int j = W; j >= wt[i]; j--)
            dp[j] = Math.max(dp[j] , val[i] + dp[j - wt[i]]);

    /*above line finds out maximum of dp[j](excluding ith element value)
    and val[i] + dp[j-wt[i]] (including ith element value and the
    profit with "KnapSack capacity - ith element weight") */
    return dp[W];
}

// Driver code
public static void main(String[] args)
{
    int val[] = {7, 8, 4}, wt[] = {3, 8, 6}, W = 10, n = 3;
    System.out.println(KnapSack(val, wt, n, W));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python program of a space optimized DP solution for
# 0-1 knapsack problem.

# val[] is for storing maximum profit for each weight
# wt[] is for storing weights
# n number of item
# W maximum capacity of bag
# dp[W+1] to store final result
def KnapSack(val, wt, n, W):

    # array to store final result
    # dp[i] stores the profit with KnapSack capacity "i"
    dp = [0]*(W+1);

    # iterate through all items
    for i in range(n):

        #traverse dp array from right to left
        for j in range(W,wt[i],-1):
            dp[j] = max(dp[j] , val[i] + dp[j-wt[i]]);

    '''above line finds out maximum of dp[j](excluding ith element value)
    and val[i] + dp[j-wt[i]] (including ith element value and the
    profit with "KnapSack capacity - ith element weight") *'''
    return dp[W];

# Driver program to test the cases
val = [7, 8, 4];
wt = [3, 8, 6];
W = 10; n = 3;
print(KnapSack(val, wt, n, W));

# This code is contributed by Princi Singh
```

## C#

```
// C# program of a space optimized DP solution for
// 0-1 knapsack problem.
using System;

class GFG
{

// val[] is for storing maximum profit for each weight
// wt[] is for storing weights
// n number of item
// W maximum capacity of bag
// dp[W+1] to store final result
static int KnapSack(int []val, int []wt, int n, int W)
{
    // array to store final result
    //dp[i] stores the profit with KnapSack capacity "i"
    int []dp = new int[W + 1];

    //initially profit with 0 to W KnapSack capacity is 0
    for(int i = 0; i < W + 1; i++)
        dp[i] = 0;

    // iterate through all items
    for(int i = 0; i < n; i++)

        //traverse dp array from right to left
        for(int j = W; j >= wt[i]; j--)
            dp[j] = Math.Max(dp[j] , val[i] + dp[j - wt[i]]);

    /*above line finds out maximum of dp[j](excluding ith element value)
    and val[i] + dp[j-wt[i]] (including ith element value and the
    profit with "KnapSack capacity - ith element weight") */
    return dp[W];
}

// Driver code
public static void Main(String[] args)
{
    int []val = {7, 8, 4};
    int []wt = {3, 8, 6};
    int W = 10, n = 3;
    Console.WriteLine(KnapSack(val, wt, n, W));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program of a space optimized DP solution for
// 0-1 knapsack problem.

    // val[] is for storing maximum profit for each weight
    // wt[] is for storing weights
    // n number of item
    // W maximum capacity of bag
    // dp[W+1] to store final result
    function KnapSack(val,wt,n,W)
    {
        // array to store final result
        // dp[i] stores the profit with KnapSack capacity "i"
        let dp = new Array(W+1);

        // initially profit with 0 to W KnapSack capacity is 0
        for(let i=0;i<W+1;i++)
        {
            dp[i]=0;
        }

        // iterate through all items
        for(let i=0; i < n; i++)

            // traverse dp array from right to left
            for(let j = W; j >= wt[i]; j--)
                dp[j] = Math.max(dp[j] , val[i] + dp[j - wt[i]]);

        /*above line finds out maximum of dp[j]
        (excluding ith element value)and
        val[i] + dp[j-wt[i]] (including ith element value and the
        profit with "KnapSack capacity - ith element weight") */
        return dp[W];
    }

    // Driver code

    let val=[7, 8, 4];
    let wt=[3, 8, 6];
    let W = 10, n = 3;
    document.write(KnapSack(val, wt, n, W));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
11
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank Mishra) 供稿。本文由 geeksforgeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。